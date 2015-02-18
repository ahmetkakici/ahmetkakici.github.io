---
title: 'Pointer ve C#'
author: Ahmet Kakıcı
layout: post
permalink: /yazilim/pointer-ve-c/
views:
  - 4221
comment_count:
  - 2
trackback_count:
  - 
categories:
  - Programlama
  - Yazılım
tags:
  - csharp
  - pointer
  - unsafe
  - visual studio
---
C programlama dilini öğrenme aşamasında en çok dikkat edilecek noktalardan biri kuşkusuz pointer kavramıdır. Web programlama dillerinden C ve türevi dillere geçenlerin de en çok zorlandığı konu sanırım yine pointer konusudur.

Derleyicilerin kendi bileşenleri (component) çıkmaya başladığında bir nevi alt seviye kodlardan bizi uzaklaştırdı. Daha sonra Java ve .NET dillerinde hazır gelen kütüphaneler ile artık pointerdan bir hayli uzaklaşmış durumdayız. [ Bu konu hakkında Faruk Enes&#8217;in çok güzel bir yazısı <a href="http://turkce.focusoncode.com/pointer-bilmeyen-programcilar-ve-gelecek/" target="_blank">var</a> ] . Ancak bazı durumlar oluyor ki pointer kullanmadan işin içinden çıkmanın maliyeti oldukça yüksek oluyor.

<!--more-->

Görüntü işleme ile uğraşmaya başladığımda C++ kullanıyordum ve pointerlar ile güzelce geçiniyordum. Ne zaman Visual Studio kullanmaya başlayıp C#&#8217;a geçiş yaptım işte o zaman pointer ile ilk sorunumu da yaşadım. .NET ile gelen GDI fonksiyonlarıyla resimlerden gerekli bilgileri alıp işimi yapabiliyordum ancak C++ ile yaptığımdan kat kat yavaş işlem yapıyordum.

Ve sonrasında bu yazıya konu olan şeyi buldum :) .NET pointer&#8217;lara güvenlikten dolayı [ belleği korumak için ] güvenmiyor ve kullanımını da kısmen yasaklıyordu. Ancak illa pointer kullanacağım diyen kişiler için de açık bir kapı bırakmış:

Visual studio&#8217;yu açtığınızda [genelde] sağda bulunan Solution Explorer&#8217;dan Properties&#8217;e çift tıklayarak açılan pencerede soldan &#8216;Build&#8217;i seçin. Açılan sayfada ise &#8216;Allow unsafe code&#8217; kutucuğuna bir tik attı mı bu iş bitiyor.

Bundan sonra aşağıdaki gibi unsafe kod bloğu içinde pointer kullanabilirsiniz.

<pre class="alt2" dir="ltr">unsafe
{
  // pointer kullanabileceğiniz bölge.
}

            
		

<div class="ngg-gallery-singlepic-image " style="max-width: 320px">
  <a href="http://www.ahmetkakici.com/wp-content/gallery/blog-post/p.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/gallery/blog-post/p.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/gallery/blog-post/thumbs/thumbs_p.jpg"
             data-image-id="1"
             data-title="p.jpg"
             data-description=""
             target='_self'
             class="thickbox" rel="11093a0faa48f78cc0a02b31c85c3f19">
              <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/gallery/blog-post/dynamic/p-nggid011-ngg0dyn-320x240x100-00f0w010c010r110f110r011t010.jpg"
             alt="p.jpg"
             title="p.jpg"
              width="320" />
      	</a>
  		      
</div>
    

<span></span>    </pre>