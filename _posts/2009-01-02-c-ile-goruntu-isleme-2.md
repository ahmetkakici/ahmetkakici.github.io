---
title: 'C# ile Görüntü İşleme &#8211; 2'
author: Ahmet Kakıcı
layout: post
permalink: /programlama/c-ile-goruntu-isleme-2/
views:
  - 22359
syntaxhighlighter_encoded:
  - 1
categories:
  - Programlama
tags:
  - c
  - görüntü işleme
  - image processing
  - kod
  - Programlama
---
Daha önce görüntü okuma, gösterme ve kaydetme gibi başlıca fonksiyonları <a href="http://www.ahmetkakici.com/yazilim/goruntu-isleme-c/" target="_blank">vermiştim</a>. Aşağıda ise asıl görüntüyü işeyecek fonksiyonlar bulunmaktadır. Tabii buradaki fonksiyonları kullanbilmek için daha önceden verdiğim şekilde görüntünün dizilere aktarılmış olması gerekiyor.

Önceki yazıda gri seviyeye çevirilmiş görüntümüz vardı eğer bu görüntüyü siyah beyaza çevirmek istiyorsanız bunun için bir eşik değeri seçerek 0-255 arasındaki gri seviye görüntüyü bu seviyeye göre siyah veya beyaz olarak ayırmak gerekiyor. Eşik değerini sabit bir değer olarak belirleyebileceğiniz gibi her görüntüye göre dinamik olarak bir eşik değeri belirleyebilen bir yöntem de mevcuttur: otsu. Otsu algoritması sayesinde üzerinde çalıştığınız görüntüye özel bir eşik değerini otomatik olarak belirleyebilirsiniz. Bunun için görüntünün histogram dizisine ihtiyacınız olacak. İlk yazıda verdiğim kodda histogram çıkartma özelliği yoktu. Bunun için aşağıdaki kodu kullanabilirsiniz:

<!--more-->

<pre class="brush: csharp; title: ; notranslate" title="">int[,] pixelArray = new int[pictureBox1.Image.Height, pictureBox1.Image.Width];
int[,] greyPixelArray = new int[pictureBox1.Image.Height, pictureBox1.Image.Width];
int[] histogram = new int[256];

void BuildPixelArray(ref Image myImage)
{
pixelArray = new int[imageWidth, imageHeight];
greyPixelArray = new int[imageWidth, imageHeight];
Rectangle rect = new Rectangle(0, 0, myImage.Width, myImage.Height);
Bitmap temp = new Bitmap(myImage);
BitmapData bmpData = temp.LockBits(rect, ImageLockMode.ReadWrite, PixelFormat.Format24bppRgb);
int remain = bmpData.Stride - bmpData.Width * 3;
unsafe
{
byte* ptr = (byte*)bmpData.Scan0;
for (int j = 0; j &lt; bmpData.Height; j++)
{
for (int i = 0; i &lt; bmpData.Width; i++)
{
pixelArray[i, j] = ptr[0] + ptr[1] * 256 + ptr[2] * 256 * 256;
greyPixelArray[i, j] = (int)((double)ptr[0] * 0.11 + (double)ptr[1] * 0.59 + (double)ptr[2] * 0.3);
histogram[greyPixelArray[i, j]]++;
ptr += 3;
}
ptr += remain;
}
}
temp.UnlockBits(bmpData);
}

</pre>

Burada histogram dizisini de oluşturduktan sonra artık otsu algoritması sayesinde dinamik olarak eşik değerini belirleyebiliriz:

<pre class="brush: csharp; title: ; notranslate" title="">int otsuValue;

void Otsu()
{
double fmax = -1.0;
double m1, m2, S, toplam1 = 0.0, toplam2 = 0.0;
int nTop = 0, n1 = 0, n2;

for (int i = 0; i &lt; 256; i++)
{
toplam1 += (double)i * (double)histogram[i];
nTop += histogram[i];
}

for (int i = 0; i &lt; 256; i++)
{
n1 += histogram[i];
if (n1 == 0)
continue;
n2 = nTop - n1;
if (n2 == 0)
break;
toplam2 += (double)i * (double)histogram[i];
m1 = toplam2 / n1;
m2 = (toplam1 - toplam2) / n2;
S = (double)n1 * (double)n2 * (m1 - m2) * (m1 - m2);
if (S &gt; fmax)
{
fmax = S;
otsuValue = i;
}
}
}

</pre>

Otsu veya sabit bir değere göre görüntüyü siyah beyaza çevirecek kod ise aşağıdadır. Bu fonksiyonun aldığı argThreshold parametresi eşik değerini belirtern 0-255 arasında bir değerdir.

<pre class="brush: csharp; title: ; notranslate" title="">void Binary(int argThreshold)
{
binaryPixelArray = new int[imageWidth, imageHeight];
for (int i = 0; i &lt; imageWidth; i++)
{
for (int j = 0; j &lt; imageHeight; j++)
{
if (greyPixelArray[i, j] &lt; threshold)
binaryPixelArray[i, j] = 0;
else
binaryPixelArray[i, j] = 255;
}
}
}

</pre>

Görüntüyü siyah beyaza çevirdikten sonra eğer kenar bulma algoritmalarını kullanmak isterseniz bir kaç seçeneğiniz mevcut. Bunlardan en popüleri sobel kenar bulma filtresidir. Aşağıdaki fonksiyonda type parametresi hangi tür kenarların bulunacağını belirtmek içindir. Dikey, yatay, köşegen şeklindeki kenarları veya tamamını ayrı ayrı bulabilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">void Sobel(int type)
{
int normalizeMax = 0;
int normalizeMin = maxIntVal;

sobelPixelArray = new int[imageWidth, imageHeight];
int[,] sobelArray1 =
new int[3, 3] {
{ 1, 0, -1 },
{ 2, 0, -2 },
{ 1, 0, -1 }
};

int[,] sobelArray2 =
new int[3, 3] {
{ 1, 2, 1 },
{ 0, 0, 0 },
{-1,-2,-1 }
};
int[,] sobelArray3 =
new int[3, 3] {
{ 2, 1, 0 },
{ 1, 0,-1 },
{ 0,-1,-2 }
};

int G1, G2, G3;
for (int i = 1; i &lt; imageWidth - 1; i++)
{
for (int j = 1; j &lt; imageHeight - 1; j++)
{
G1 = 0;
G2 = 0;
G3 = 0;
for (int k = -1; k &lt; 2; k++)
{
for (int l = -1; l &lt; 2; l++)
{
G1 += greyPixelArray[i + k, j + l] * sobelArray1[k + 1, l + 1];
G2 += greyPixelArray[i + k, j + l] * sobelArray2[k + 1, l + 1];
G3 += greyPixelArray[i + k, j + l] * sobelArray3[k + 1, l + 1];
}
}
if(type == 0)
{
sobelPixelArray[i, j] = Math.Abs(G1) + Math.Abs(G2) + Math.Abs(G3);
}
else if (type == 1)
{
sobelPixelArray[i, j] = Math.Abs(G2);
}
else if (type == 2)
{
sobelPixelArray[i, j] = Math.Abs(G1);
}
else if (type == 3)
{
sobelPixelArray[i, j] = Math.Abs(G3);
}

if (normalizeMax &lt; sobelPixelArray[i, j])
normalizeMax = sobelPixelArray[i, j];
if (normalizeMin &gt; sobelPixelArray[i, j])
normalizeMin = sobelPixelArray[i, j];
}
}

NormalizeArray(ref sobelPixelArray, normalizeMax, normalizeMin);
}
</pre>

Yukarıda bulunan kodun en altında çağırılan normalize fonksiyonu ise sonuç dizisini 0-255 değerleri arasına düşürmek içindir:

<pre class="brush: csharp; title: ; notranslate" title="">void NormalizeArray(ref int[,] sourceArray,int normalizeMax,int normalizeMin)
{

int factor = normalizeMax - normalizeMin;
for (int i = 0; i &lt; sourceArray.GetLength(0); i++)
{
for (int j = 0; j &lt; sourceArray.GetLength(1); j++)
{
sourceArray[i, j] = (sourceArray[i, j] - normalizeMin) * 255 / factor;
}
}
}

</pre>

Bir diğer kenar bulma yöntemi ise Prewitt&#8217;tir:

<pre class="brush: csharp; title: ; notranslate" title="">int[,] prewittPixelArray;

void Prewitt()
{
int normalizeMax = 0;
int normalizeMin = maxIntVal;
prewittPixelArray = new int[imageWidth, imageHeight];
int[,] PrewittArray1 =
new int[3, 3] {
{-1,-1,-1 },
{ 0, 0, 0 },
{ 1, 1, 1 }
};

int[,] PrewittArray2 =
new int[3, 3] {
{ -1, 0, 1 },
{ -1, 0, 1 },
{ -1, 0, 1 }
};
int[,] PrewittArray3 =
new int[3, 3] {
{-1,-1, 0 },
{-1, 0, 1 },
{ 0, 1, 1 }
};

int[,] PrewittArray4 =
new int[3, 3] {
{ 1, 1, 0 },
{ 1, 0,-1 },
{ 0,-1,-1 }
};

int G1, G2, G3, G4;
for (int i = 1; i &lt; imageWidth - 1; i++)
{
for (int j = 1; j &lt; imageHeight - 1; j++)
{
G1 = 0;
G2 = 0;
G3 = 0;
G4 = 0;
for (int k = -1; k &lt; 2; k++)
{
for (int l = -1; l &lt; 2; l++)
{
G1 += greyPixelArray[i + k, j + l] * PrewittArray1[k + 1, l + 1];
G2 += greyPixelArray[i + k, j + l] * PrewittArray2[k + 1, l + 1];
G3 += greyPixelArray[i + k, j + l] * PrewittArray3[k + 1, l + 1];
G4 += greyPixelArray[i + k, j + l] * PrewittArray4[k + 1, l + 1];
}
}

prewittPixelArray[i, j] = Math.Abs(G1) + Math.Abs(G2) + Math.Abs(G3) + Math.Abs(G4);
if (normalizeMax &lt; prewittPixelArray[i, j])
normalizeMax = prewittPixelArray[i, j];
if (normalizeMin &gt; prewittPixelArray[i, j])
normalizeMin = prewittPixelArray[i, j];
}
}

int factor = normalizeMax - normalizeMin;
for (int j = 1; j &lt; imageHeight - 1; j++)
{
for (int i = 1; i &lt; imageWidth - 1; i++)
{
prewittPixelArray[i, j] = (prewittPixelArray[i, j] - normalizeMin) * 255 / factor;
}
}
}
</pre>

Prewitt ve sobel&#8217;e alternatif olarak Robert kenar bulma filtresi de mevcuttur :

<pre class="brush: csharp; title: ; notranslate" title="">int[,] robertPixelArray;

void Robert()
{

robertPixelArray = new int[imageWidth, imageHeight];
for (int i = 1; i &lt; imageHeight - 1; i++)
{
for (int j = 1; j &lt; imageWidth - 1; j++)
{
robertPixelArray[j, i] = Math.Abs(greyPixelArray[j, i] - greyPixelArray[j - 1, i - 1]) + Math.Abs(greyPixelArray[j, i - 1] - greyPixelArray[j - 1, i]);
}
}
}

</pre>

Eğer kenar bulma algoritmalarını kullanmadan önce görüntüdeki gürültüleri temizlemek istiyorsanız mean, median ve gaussian filtereleri ile bu işlemi yapabilirsiniz.

Mean filtresi :

<pre class="brush: csharp; title: ; notranslate" title="">int[,] meanPixelArray;

void Mean()
{
meanPixelArray = new int[imageWidth, imageHeight];
for (int i = 1; i &lt; imageHeight - 1; i++)
{
for (int j = 1; j &lt; imageWidth - 1; j++)
{
meanPixelArray[j, i] =
(
greyPixelArray[j, i - 1]
+ greyPixelArray[j, i + 1]
+ greyPixelArray[j, i]
+ greyPixelArray[j - 1, i - 1]
+ greyPixelArray[j - 1, i + 1]
+ greyPixelArray[j - 1, i]
+ greyPixelArray[j + 1, i - 1]
+ greyPixelArray[j + 1, i + 1]
+ greyPixelArray[j + 1, i]
) / 9;
}
}
}

</pre>

Median filtresi:

<pre class="brush: csharp; title: ; notranslate" title="">int[,] medianPixelArray;

void Median()
{

medianPixelArray = new int[imageWidth, imageHeight];
int[] tempArray = new int[9];
for (int i = 1; i &lt; imageHeight - 1; i++)
{
for (int j = 1; j &lt; imageWidth - 1; j++)
{
int counter = 0;
for (int k = -1; k &lt; 2; k++)
{
for (int l = -1; l &lt; 2; l++)
{
tempArray[counter++] = greyPixelArray[j + l, i + k];
}
}
System.Array.Sort(tempArray);
medianPixelArray[j, i] = tempArray[4];
}
}
}
</pre>

Gaussian filtresi

<pre class="brush: csharp; title: ; notranslate" title="">int[,] gaussianPixelArray;

void Gaussian()
{
gaussianPixelArray = new int[imageWidth, imageHeight];

int[,] gaussianArray =
new int[5, 5] {
{1,4,7,4,1},
{4,16,26,16,4},
{7,26,41,26,7},
{4,16,26,16,4},
{1,4,7,4,1}
};
int tempSum;
for (int i = 2; i &lt; imageHeight - 2; i++)
{
for (int j = 2; j &lt; imageWidth - 2; j++)
{
tempSum = 0;
for (int k = -2; k &lt; 3; k++)
{
for (int l = -2; l &lt; 3; l++)
{
tempSum += greyPixelArray[j + l, i + k] * gaussianArray[k + 2, l + 2];
}
}
gaussianPixelArray[j, i] = tempSum / 273;
}
}
}

</pre>

Daha sonraki yazıda yapısal (morfolojik) işlemleri yapan filtreleri de açıklamalarıyla birlikte vermeyi düşünüyorum. O zamana kadar hepinize kolay gelsin.