---
title: PHP ile EXIF bilgisi okuma
author: Ahmet Kakıcı
layout: post
permalink: /web/php-ile-exif-bilgisi-okuma/
views:
  - 1164
comment_count:
  - 
trackback_count:
  - 
categories:
  - Programlama
  - Web
tags:
  - dll
  - exif
  - mbstring
  - php
---
Jpeg ve Tiff formatındaki fotoğrafların <a href="http://tr.pardus-wiki.org/EXIF" target="_blank">exif</a> bilgilerini okumak için php_exif.dll mevcut. Bu DLL sayesinde *exif\_read\_data* fonksiyonuna erişebiliyoruz. Tabii öntanımlı olarak gelen php.ini dosyasında bu dll aktif değil. Öncelikle php.ini dosyasından *extension=php_exif.dll* yazan satırı bulup başındaki noktalı virgülü kaldırmamız gerekli. Evet az önce ben bu şekilde yaparak exif bilgilerini mutlu mesud bir şekilde okuyacağımı zannetmiştim. <!--more-->Ama apache&#8217;yi yeninden başlattığımda verdiği hata oldukça ilginçi; php\_mbstring.dll dosyasını bulamadığına dair bir hata veriyordu. Oysa php.ini dosyasında da php\_mbstring.dll aktifti ki şimdiye kadar bu hatayı almamıştım.

Çözüm mü ? Çözüm gayet kolay :) php.ini dosyası içinde php\_mbstring.dll&#8217;in aktif edildiği satırı php\_exif.dll&#8217;yi aktif ettiğiniz satırın üstünde olmak koşuluyla herhangi bir yere koyduğunuz zaman sorun çözülüyor. Neden mi ? Çünkü tahmin edebileceğiniz gibi exif bilgilerini okumamızı sağlayan dll mbstring ile birlikte çalışıyor ;)

Bundan sonrası gayet kolay:

> var\_dump( exif\_read_data(&#8216;ahmeTT.jpg&#8217;, &#8216;IFD0&#8242;));

gibi bir kod ile exif bilgisini ekrana yazdırabilirsiniz. Bu kütüphane hakkında daha fazla bilgi için (<a href="http://tr2.php.net/manual/en/ref.exif.php" target="_blank">buradan</a>) php.net&#8217;in sayfasını ziyaret edebilirsiniz.