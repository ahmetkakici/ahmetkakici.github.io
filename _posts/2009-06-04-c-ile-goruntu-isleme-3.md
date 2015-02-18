---
title: 'C# ile Görüntü İşleme - 3'
author: Ahmet Kakıcı
layout: post
permalink: /programlama/c-ile-goruntu-isleme-3/
syntaxhighlighter_encoded:
  - 1
views:
  - 5855
categories:
  - Programlama
tags:
  - görüntü işleme
  - image processing
  - kod
---
İlk iki yazının ardından ( <a title="C# ile Görüntü İşleme - 1" href="http://www.ahmetkakici.com/programlama/c-ile-goruntu-isleme-1/" target="_self">1</a> &#8211; <a title="C# ile Görüntü İşleme - 2" href="http://www.ahmetkakici.com/programlama/c-ile-goruntu-isleme-2/" target="_self">2</a> ) sonunda üçüncü yazıyı da yazabildim. Bu yazıya sadece morfolojik filtreler kaldı. Diğer yazılara gelen yorumlardan sonra açıklamadan çok koda ihtiyaç olduğu anladım, onun için aşağıda genleşme (dilation) ve aşınma (erosion) işlemini yapan fonksiyonları bulacaksınız. Benim kullandığım genleşme ve aşınma maskeleri en basit olanları. Siz kendi maskelerinizi if koşulu içine yazarak dilediğiniz gibi kullanabilirsiniz.

Eğer genleşme ve aşınma hakkında daha fazla bilgi istiyorsanız <a title="Dilation" href="http://homepages.inf.ed.ac.uk/rbf/HIPR2/dilate.htm" target="_blank">Dilation</a> &#8211; <a title="Erosion" href="http://homepages.inf.ed.ac.uk/rbf/HIPR2/erode.htm" target="_blank">Erosion</a> bağlantılarını takip edebilirsiniz.  
<!--more-->

<pre class="brush: csharp; title: ; notranslate" title="">void Dilation()
{
    if (!dilationDone)
    {
        
        dilationPixelArray = new int[imageWidth, imageHeight];
        for (int i = 1; i &lt; imageWidth - 1; i++)
        {
            for (int j = 1; j &lt; imageHeight - 1; j++)
            {
                if (binaryPixelArray[i, j] == 255)
                {
                    dilationPixelArray[i - 1, j] = 255;
                    dilationPixelArray[i, j - 1] = 255;
                    dilationPixelArray[i, j + 1] = 255;
                    dilationPixelArray[i + 1, j] = 255;
                }
            }
        }
    }
    else
    {
        int[,] tempArray = new int[imageWidth, imageHeight];
        Array.Copy(dilationPixelArray, tempArray, imageWidth * imageHeight);
        for (int i = 1; i &lt; imageWidth - 1; i++)
        {
            for (int j = 1; j &lt; imageHeight - 1; j++)
            {
                if (tempArray[i, j] == 255)
                {
                    dilationPixelArray[i - 1, j] = 255;
                    dilationPixelArray[i, j - 1] = 255;
                    dilationPixelArray[i, j + 1] = 255;
                    dilationPixelArray[i + 1, j] = 255;
                }
            }
        }
    }
    
}
void Erosion()
{
    if (!erosionDone)
    {
        erosionPixelArray = new int[imageWidth, imageHeight];
        for (int i = 1; i &lt; imageWidth - 1; i++)
        {
            for (int j = 1; j &lt; imageHeight - 1; j++)
            {
                if (binaryPixelArray[i, j] == 255)
                {
                    if (binaryPixelArray[i, j - 1] == 0 ||
                        binaryPixelArray[i - 1, j] == 0 ||
                        binaryPixelArray[i + 1, j] == 0 ||
                        binaryPixelArray[i, j + 1] == 0
                        )
                    {
                        erosionPixelArray[i - 1, j] = 0;
                        erosionPixelArray[i, j - 1] = 0;
                        erosionPixelArray[i, j + 1] = 0;
                        erosionPixelArray[i + 1, j] = 0;
                        erosionPixelArray[i, j] = 0;
                    }
                    else
                    {
                        erosionPixelArray[i, j] = binaryPixelArray[i, j];
                    }
                }
                else
                {
                    erosionPixelArray[i, j] = binaryPixelArray[i, j];
                }
            }
        }
    }
    else
    {
        int[,] tempArray = new int[imageWidth, imageHeight];
        Array.Copy(erosionPixelArray, tempArray, imageWidth * imageHeight);
        for (int i = 1; i &lt; imageWidth - 1; i++)
        {
            for (int j = 1; j &lt; imageHeight - 1; j++)
            {
                if (tempArray[i, j] == 255)
                {
                    if (tempArray[i, j - 1] == 0 ||
                        tempArray[i - 1, j] == 0 ||
                        tempArray[i + 1, j] == 0 ||
                        tempArray[i, j + 1] == 0 
                        )
                    {
                        erosionPixelArray[i - 1, j] = 0;
                        erosionPixelArray[i, j - 1] = 0;
                        erosionPixelArray[i, j + 1] = 0;
                        erosionPixelArray[i + 1, j] = 0;
                        erosionPixelArray[i, j] = 0;
                    }
                    else
                    {
                        erosionPixelArray[i, j] = tempArray[i, j];
                    }
                }
                else
                {
                    erosionPixelArray[i, j] = tempArray[i, j];
                }
            }
        }
    }
}
</pre>

Bundan önceki yazılardaki yapıyı kullandığınızı varsayarak yukarıdaki iki fonksiyonu aşağıdaki şekilde çağırmanız gerekli. Bu fonksiyonların yaptığı iş ise eğer resim ikili seviyeye indirgenmemişse (siyah-beyaz) önce bu işlemi yapmak. Tabii ikiliye çevirmek için herhangi bir eşik değeri belirlenmemişse otsu fonksiyonunu çağırarak önce bir eşik değeri hesaplatıyoruz. Binary fonksyionu ise 0-255 arasındaki parametreyi eşik değeri olarak kullanarak resmi ikili seviyeye indirgiyor, parametrenin 256 olması ise otsu ile hesaplanan eşik değerini alması içindir.

<pre class="brush: csharp; title: ; notranslate" title="">public void ShowDilation()
{
    if (!dilationDone)
    {
        if (!binaryDone)
        {
            if (otsuValue == 0)
                Otsu();
            Binary(256);
        }
        Dilation();
        dilationDone = true;
    }
    else
    {
        Dilation();
    }
    SetImage(ref dilationPixelArray);
}


public void ShowErosion()
{
    if (!erosionDone)
    {
        if (!binaryDone)
        {
            if (otsuValue == 0)
                Otsu();
            Binary(256);
        }
        Erosion();
        erosionDone = true;
    }
    else
    {
        Erosion();
    }
    SetImage(ref erosionPixelArray);
}
</pre>