---
title: 'C# ile Görüntü İşleme &#8211; 1'
author: Ahmet Kakıcı
layout: post
permalink: /programlama/c-ile-goruntu-isleme-1/
views:
  - 21371
syntaxhighlighter_encoded:
  - 1
categories:
  - Programlama
tags:
  - c
  - görüntü işleme
  - image processing
---
Blogda bu kadar kod dolu yazılar yazmak konusunda kararszıdım ama yine de bir kez denemek istedim bakalım ilgi olacak mı.

Görüntü işleme ile ilgili temel bilgileri biliyorsunuz farzederek bu yazıyı yazıyorum. Zira işin hikaye kısmını yazması biraz zor oluyor diyerekten konuya geçelim.

<!--more-->

Görüntü işleme sırasında image veya bitmap nesneleri üzerinde işlem yapmak yerine dizileri kullanıyorum ondan dolayı aşağıdaki kodlarda da bütün işlemler diziler üzerinde olacak. Kullandığım birçok fonksiyon pointer kullanarak çalışıyor. C# ile nasıl pointer kullanacağınızı bilmiyorsanız** [şurada][1]** bulunan yazımı okuyabilirsiniz.

Öncelikle picturebox nesnesinden diziye dönüşüm işlemini yapan fonksiyonu verelim:

<pre class="brush: csharp; title: ; notranslate" title="">int[,] pixelArray = new int[pictureBox1.Image.Height, pictureBox1.Image.Width];
int[,] greyPixelArray = new int[pictureBox1.Image.Height, pictureBox1.Image.Width];

private void BuildPixelArray(Image myImage)
{
Rectangle rect = new Rectangle(0, 0, myImage.Width, myImage.Height);
Bitmap temp = new Bitmap(myImage);
BitmapData bmpData = temp.LockBits(rect, ImageLockMode.ReadWrite, PixelFormat.Format24bppRgb);
int remain = bmpData.Stride - bmpData.Width * 3;
unsafe
{
byte* ptr = (byte*)bmpData.Scan0;
for (int i = 0; i &lt; bmpData.Height; i++)
{
for (int j = 0; j &lt; bmpData.Width; j++)
{
pixelArray[i, j] = ptr[0] + ptr[1] * 255 + ptr[2] * 255 * 255;
greyPixelArray[i, j] = (int)((double)ptr[0] * 0.11 + (double)ptr[1] * 0.59 + (double)ptr[2] * 0.3);
ptr += 3;
}
ptr += remain;
}
}
temp.UnlockBits(bmpData);
}

</pre>

Bu fonksiyon sayesinde picturebox nesnesindeki görüntüyü pixelArray dizisine taşıyoruz. Aynı fonksiyonda greyPixelArray dizisi ile tutulan griseviye görüntü de oluşturuluyor.

Dizideki görüntüyü form üzerinde bulunan bir picturebox nesnesine aktarmak için aşağıdaki fonksiyonu kullanabilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">private void SetImage(int[,] sourceArray, ref PictureBox myPictureBox)
{
Rectangle rect = new Rectangle(0, 0, myPictureBox.Image.Width, myPictureBox.Image.Height);
Bitmap temp = new Bitmap(myPictureBox.Image);
BitmapData bmpData = temp.LockBits(rect, ImageLockMode.ReadWrite, PixelFormat.Format24bppRgb);
int remain = bmpData.Stride - bmpData.Width * 3;
unsafe
{
byte* ptr = (byte*)bmpData.Scan0;
for (int i = 0; i &lt; bmpData.Height; i++)
{
for (int j = 0; j &lt; bmpData.Width; j++)
{
ptr[0] = ptr[1] = ptr[2] = (byte)sourceArray[i, j];
ptr += 3;
}
ptr += remain;
}
}
temp.UnlockBits(bmpData);
myPictureBox.Image = temp;
}

</pre>

Üstteki fonksiyon aldığı diziyi gri seviye olarak değerlendiriyor. Eğer renkli bir görüntünüz varsa bir aşağıdaki fonksiyonu kullanabilirsiniz

<pre class="brush: csharp; title: ; notranslate" title="">public void SetColorImage(ref int[,] sourceArray)
{
Rectangle rect = new Rectangle(0, 0, sourceArray.GetLength(0), sourceArray.GetLength(1));
Bitmap temp = new Bitmap(sourceArray.GetLength(0), sourceArray.GetLength(1));
BitmapData bmpData = temp.LockBits(rect, ImageLockMode.ReadWrite, PixelFormat.Format24bppRgb);
int remain = bmpData.Stride - bmpData.Width * 3;
unsafe
{
byte* ptr = (byte*)bmpData.Scan0;
for (int i = 0; i &lt; bmpData.Width; i++)
{
for (int j = 0; j &lt; bmpData.Height; j++)
{
ptr[0] = (byte)(sourceArray[i, j]%256);
ptr[1] = (byte)((sourceArray[i, j]/256)%256);
ptr[2] = (byte)((sourceArray[i, j]/65536)%256);
ptr += 3;
}
ptr += remain;
}
}
temp.UnlockBits(bmpData);
destPictBox.Image = temp;
}

</pre>

Görüntüyü yeniden boyutlandırmak için aşağıdaki fonksiyonu kullanabilirsiniz. ConstWidth değişkenine istediğiniz değeri vererek işlem sonucundaki görüntünün enini ayarlayabilirsiniz. Ben tüm görüntüleri standart boyuta getirmek için böyle bir yol kullanmıştım. Fonksiyonun çalışmasını kolaylıkla anlayabilir ve istediğiniz en-boy değiştirme işlemini kolayca yapabilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">private void ResizeImage(ref Image myImage)
{
float nPercent = ((float)constWidth / myImage.Width);
int sourceWidth = myImage.Width;
int sourceHeight = myImage.Height;
int sourceX = 0;
int sourceY = 0;

int destX = 0;
int destY = 0;
int destWidth = (int)(sourceWidth * nPercent);
int destHeight = (int)(sourceHeight * nPercent);

Bitmap bmPhoto = new Bitmap(destWidth, destHeight, PixelFormat.Format24bppRgb);
bmPhoto.SetResolution(myImage.HorizontalResolution, myImage.VerticalResolution);

Graphics grPhoto = Graphics.FromImage(bmPhoto);
grPhoto.DrawImage(myImage,
new Rectangle(destX, destY, destWidth, destHeight),
new Rectangle(sourceX, sourceY, sourceWidth, sourceHeight),
GraphicsUnit.Pixel);
myImage = bmPhoto;
grPhoto.Dispose();
}

</pre>

Kenar algılama, gürültü yok etme ve yapısal (morfolojik) filtreleri de [bir sonraki yazımda][2] paylaşmak üzere. İyi işlemeler diliyorum :)

 [1]: http://www.ahmetkakici.com/yazilim/pointer-ve-c/
 [2]: http://www.ahmetkakici.com/programlama/c-ile-goruntu-isleme-2/