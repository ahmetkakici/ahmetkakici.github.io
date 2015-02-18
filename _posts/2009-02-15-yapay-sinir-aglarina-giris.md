---
title: Yapay Sinir Ağlarına Giriş
author: Ahmet Kakıcı
layout: post
permalink: /yazilim/yapay-sinir-aglarina-giris/
views:
  - 12374
categories:
  - Programlama
  - Yapay Sinir Aglari
  - Yazılım
tags:
  - Programlama
  - Yapay Sinir Aglari
---
Bitirme ödevim için uğraşmaya başladığım ve tezimde de genişçe yer ayırdığım yapay sinir ağları hakkında tezimden ufak tefek alıntılar yaparak burada paylaşmaya başlıyorum. Tezin tamamını yayınlamak yerine can alıcı noktalarını bir yazı dizisi halinde burada yayınlayacağım.

Öncelikle yapay sinir ağlarının ne olduğu ve özellikleri hakkındaki bölüm ile başlamak iyi olur diyerekten yazıma geçiyorum;

<!--more-->

**Yapay Sinir Ağlarının Tanımı**

Yapay sinir ağları canlılarda bulunan sinir sisteminin çalışmasını elektronik ortama taşımayı hedefleyen bir programlama yaklaşımıdır. Yapay sinir ağlarının da canlılarda olduğu gibi öğrenme, hatırlama ve öğrendiklerini güncelleme gibi yeteneklerinin olması hedeflenmektedir.

Sinir sisteminin davranışlarını kopyalayabilmek için yapısının da kopyalanması gerektiğini düşünen bilim adamları yapay sinir ağlarını modellerken de sinir sisteminin yapısını örnek almışlardır.

Yapay sinir hücrelerinin birbirine bağlanmasıyla oluşan bir yapay sinir ağı öğrenme algoritmalarından herhangi birini kullanarak öğrenme sürecini tamamladığında kullanıma hazır hale gelir. Yapay sinir ağı çalıştığı sürece öğrenme ve bilgilerini güncelleme yeteneğine de sahiptir.

**Yapay Sinir Ağlarının Genel Özellikleri**

Yapay sinir ağları genel olarak canlı beyninin yapısını gerçekleştirmeyi hedefler. Aşağıdaki işlemleri gerçekleştirebilir:

  * Öğrenme
  * İlişkilendirme
  * Sınıflandırma
  * Genelleme
  * Tahmin
  * Özellik belirleme
  * Optimizasyon

Bu işlemleri yapan sinir ağlarının ortak noktası ise bir müdahale yapılmaksızın, elinde bulunan bilgilere göre sonuç üretebilmesidir.  
Yapay sinir ağları öğrenme işlemi sırasında verilen bilgiler ile kendini düzenleyerek daha sonraki girdiler için doğru kararlar verebilme yeteneğine sahiptir.

**Yapay Sinir Ağlarının Üstünlükleri**  
Yapay sinir ağ modelleri biyolojik sinir ağlarının çalışmasından esinlenerek ortaya çıkarılmıştır. Canlılarda bulunan sinir sisteminin modellenmesi sayesinde yapay sinir ağları biyolojik sinir sisteminin üstünlüklerine sahip olmuştur.

  * **Doğrusal Olmama **
Yapay sinir ağları özellikle doğrusal olmayan sistemlerde tahmin yapma açısından istatistik hesaplamalarına göre daha kolay ve doğru sonuç vermesinden dolayı sık kullanılan bir yöntem haline gelmiştir. Özellikle işletmecilik ve finans alanlarında olmak üzere tahmin gerektiren birçok alanda kullanılmaktadır.  
Yapay sinir ağlarının temel elemanlarından olan yapay sinir hücrelerinin (nöron) doğrusal sonuçlar vermeyişinden dolayı bu özellik ağa da yansımıştır. Doğrusal olmama özelliğinden dolayı yapay sinir ağları karmaşık problemlerin çözümünde de sıkça kullanılmaktadır

  * **Paralellik**
Klasik problem çözme algoritmalarının aksine yapay sinir ağları paralel çalışmaya uygun bir yapıya sahiptir. Bu özelliği sayesinde çok daha hızlı problem çözebilme yeteneğine sahip olmuştur.

  * **Hata Toleransı**
Yapay sinir ağları özellikle doğrusal olmayan sistemlerde tahmin yapma açısından istatistik hesaplamalarına göre daha kolay ve doğru sonuç vermesinden dolayı sık kullanılan bir yöntem haline gelmiştir. Özellikle işletmecilik ve finans alanlarında olmak üzere tahmin gerektiren birçok alanda kullanılmaktadır.  
Yapay sinir ağlarının temel elemanlarından olan yapay sinir hücrelerinin (nöron) doğrusal sonuçlar vermeyişinden dolayı bu özellik ağa da yansımıştır. Doğrusal olmama özelliğinden dolayı yapay sinir ağları karmaşık problemlerin çözümünde de sıkça kullanılmaktadır

Bilgisayar üzerinde çalışan bir elemanın zarar görüp devre dışı kalması o elmanın içinde bulunduğu sistemin çalışmamasına neden olur. Ancak paralel çalışabilme özelliği ve yapay sinir hücrelerinin bağımsız çalışabilme yapısından dolayı yapay sinir ağında herhangi bir eleman zarar gördüğünde ağın geri kalanı sorunsuz bir şekilde çalışmaya devam eder. İlk olarak yanlış sonuçlar verebilse de daha sonra yeni yapısını öğrenerek eski performansında çalışmaya devam edebilir.

  * **Öğrenebilirlik**
Klasik algoritmaların çoğu verilen formüllerin hesaplanması ile aynı girdiler için daima aynı çıktıları üretirler. Lineer olan bu algoritmaların aksine yapay sinir ağları sayesinde programlar öğrenme yeteneği de kazanmışlardır. Klasik algoritmalarda tam olarak tanımlı bir çözüm yolu olmayan problemler çözülemezken yapay sinir ağları sayesinde problemler çözüm yöntemi hakkında herhangi bir bilgi verilmeksizin çözülebilir. Yapay sinir ağlarının bu tip problemleri çözebilmesi için gereken tek şey örnek girdiler için sonuçların verilmesidir.

  * **Genelleme **
Yapay sinir ağları üzerinde çalıştığı probleme göre eğitildikten sonra eğitim sırasında karşılaşmadığı durumlar için de yanıt verebilir. Örneğin bir satranç taşının görüntüsünün tanıtılmasından sonra bu taşın görüntüsünü içeren ancak gürültülü bir görüntü verildiğinde bile yapay sinir ağı bu taşı tanıyabilir.

  * **Uyarlanabilirlik **
Yapay sinir ağı üzerinde çalıştığı probleme gör kendini düzenleyerek ağırlıklarını belirler. Bir problemi çözmek için eğitilen yapay sinir ağı herhangi bir başka problemde de kolaylıkla kullanılabilir. Bunun için gereken tek şey yeni problemin girdi ve çıktılarıyla ağın tekrar eğitilmesidir.

  * **Hız **
Yapay sinir ağları paralel yapısı nedeniyle hızlı bir şekilde çalışıp problem çözme yeteneğine sahiptir. Aynı özelliğinden dolayı donanım üzerinde de kolaylıkla gerçeklenebilir.

  * **Analiz ve Tasarım Kolaylığı **
Yapay sinir ağlarının temel yapı taşı olan yapay sinir yapısı bütün yapay sinir ağlarında aynıdır. Bundan dolayı yapay sinir hücresinin tasarımından sonra bu temel eleman ile yapay sinir ağları kolaylıkla oluşturulabilir. Yapay sinir ağlarının temel yapısının da aynı olmasından dolayı bu ağlar her türlü problemin çözümünde kullanılabilinir.</ul> 

**Yapay Sinir Ağlarının Dezavantajları**

  * **Eğitim Süreci**
Yapay sinir ağları oluşturulduklarında hiçbir bilgi içermediğinden dolayı direk olarak kullanılamazlar. Herhangi bir problem çözümünde kullanılacak olan yapay sinir ağının problemde kullanılmadan önce eğitilmesi şarttır. Bu eğitim süresi problemin çözümünden çok daha uzun zaman alabilir.

  * **Başlangıç Koşullarına Bağlı Olması**
Yapay sinir ağları başlangıç koşullarından bağımsız olarak çok kolay dahi olsa herhangi bir problemi çözemezler. Karar verme anında sadece daha önce öğrendiği koşullara göre sonuç üretebilir. Eğitim sırasında verilen örnekler ağın sonraki problemleri çözmesinde de etkilidir.</ul> 

<a href="http://www.ahmetkakici.com/yapay-sinir-aglari/yapay-sinir-aglarinin-mimarisi-ve-yapi-elemanlari/" target="_blank">Bir sonraki yazıda</a> biyolojik sinir sisteminin yapısına kısaca değinerek yapay sinir ağlarının yapısını anlatan bir yazı ile beraber olacağız. Daha sonrasında ise yapay sinir ağlarının işleyişini ele alabiliriz.