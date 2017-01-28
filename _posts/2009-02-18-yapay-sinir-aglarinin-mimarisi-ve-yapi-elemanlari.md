---
title: Yapay Sinir Ağlarının Mimarisi ve Yapı Elemanları
author: Ahmet Kakıcı
layout: post
permalink: /yapay-sinir-aglari/yapay-sinir-aglarinin-mimarisi-ve-yapi-elemanlari/
views:
  - 20779
categories:
  - Yapay Sinir Aglari
tags:
  - Programlama
  - Yapay Sinir Aglari
---
<a href="https://ahmetkakici.github.io/yazilim/yapay-sinir-aglarina-giris/">Yapay sinir ağlarına giriş</a> yazısının ardından seriye devam ediyoruz.

**Yapay Sinir Ağlarının Mimarisi ve Yapı Elemanları**  
Yapay sinir ağları biyolojik sinir ağlarının modellemesi olduğu için yapay sinir ağlarının çalışmasını anlayabilmek için öncelikle biyolojik sinir sisteminin yapısına bakmak gerekir. Biyolojik sinir sisteminin yapı taşı olan sinir hücreleri nöronlar, yapay sinir ağlarının da yapı taşıdır.

<!--more-->

**Biyolojik Sinir Hücresinin Yapısı**  
Biyolojik sinir sisteminin temel yapı taşı olan nöronların yapısı dört ana bölümden oluşmaktadır; dendrit, akson, çekirdek ve bağlantılar. Dendritlerin sinir hücresinin ucunda bulunan ve ağaç kökü görünümüne sahip bir yapıya sahiptir. Dendritlerin görevi bağlı olduğu diğer nöronlardan veya duyu organlarından gelen sinyalleri çekirdeğe iletmektir. Çekirdek dendrit tarafından gelen sinyalleri bir araya toplayarak ve aksona iletir. Toplanan bu sinyaller akson tarafından işlenerek nöronun diğer ucunda bulunan bağlantılara gönderilir. Bağlantılar ise yeni üretilen sinyalleri diğer nöronlara iletir.  

![Sinir Hücresi - Nöron](/assets/images/ysa/noron.gif)


<span></span> 

**Biyolojik Sinir Ağlarının Yapısı**  
Bir insanın beyninde yaklaşık olarak 10 milyar sinir hücresi ve bu nöronların birbirleriyle yaptığı bağlantı sayısının ise 60 trilyon olduğu tahmin edilmektedir. Bu sinirler girdi bilgilerini duyu organlarından alırlar. Daha sonra alıcı (taşıyıcı) sinirler bu sinyalleri işleyip bir sonraki sinire aktararak sinyalin merkezi sinir sistemine kadar ulaşmasını sağlar. Merkezi sinir sistemi bu sinyalleri alıp yorumladıktan sonra tepki sinyallerini üretir. Bu sinyaller de tepkilerin oluşacağı organlara tepki sinirleri vasıtasıyla iletilir. Bu sayede duyu organlarından gelen bilgilere karşı tepki organlarına uygun işaretler sinir sistemi vasıtasıyla yollanır.

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 320px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/sinir sistemi.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/sinir sistemi.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_sinir sistemi.jpg"
             data-image-id="69"
             data-title="Biyolojik Sinir Ağları"
             data-description=""
             target='_self'
             class="thickbox" rel="901a4ce7fd57986039dea345af134a66"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/sinir sistemi-nggid0269-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="Biyolojik Sinir Ağları"
             title="Biyolojik Sinir Ağları"
              width="320" /> </a>
</div>

<span></span> 

**Yapay Sinir Hücresinin Yapısı**  
Yapay sinir hücreleri de biyolojik sinir hücrelerine benzer yapıdadır. Yapay nöronlar da aralarında bağ kurarak yapay sinir ağlarını oluştururlar. Aynı biyolojik nöronlarda olduğu gibi yapay nöronların da giriş sinyallerini aldıkları, bu sinyalleri toplayıp işledikleri ve çıktıları ilettikleri bölümleri bulunmaktadır.  
Bir yapay sinir hücresi beş bölümden oluşmaktadır;

  * Girdiler
  * Ağırlıklar
  * Birleştirme fonksiyonu
  * Aktivasyon fonksiyonu
  * Çıktılar

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 320px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/yapay-sinir-hucresi.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/yapay-sinir-hucresi.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_yapay-sinir-hucresi.jpg"
             data-image-id="70"
             data-title="Yapay sinir hücresi"
             data-description=""
             target='_self'
             class="thickbox" rel="16a4483eeb1dd9c073a262edc4abda73"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/yapay-sinir-hucresi-nggid0270-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="Yapay sinir hücresi"
             title="Yapay sinir hücresi"
              width="320" /> </a>
</div>

<span></span> 

  * **Girdiler**

Girdiler nöronlara gelen verilerdir. Girdiler yapay sinir hücresine bir diğer hücreden gelebileceği gibi direk olarak dış dünyadan da gelebilir. Bu girdilerden gelen veriler biyolojik sinir hücrelerinde olduğu gibi toplanmak üzere nöron çekirdeğine gönderilir.

  * **Ağırlıklar**

Yapay sinir hücresine gelen bilgiler girdiler üzerinden çekirdeğe ulaşmadan önce geldikleri bağlantıların ağırlığıyla çarpılarak çekirdeğe iletilir. Bu sayede girdilerin üretilecek çıktı üzerindeki etkisi ayarlanabilinmektedir. Bu ağırlıkların değerleri pozitif, negatif veya sıfır olabilir. Ağırlığı sıfır olan girdilerin çıkıl üzerinde herhangi bir etkisi olmamaktadır.

  * **Birleştirme Fonksiyonu**

Birleştirme fonksiyonu bir yapay sinir hücresine ağırlıklarla çarpılarak gelen girdileri toplayarak o hücrenin net girdisini hesaplayan bir fonksiyondur.

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 148px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/birlestirme.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/birlestirme.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_birlestirme.jpg"
             data-image-id="71"
             data-title="Birleştirme Fonksiyonu"
             data-description=""
             target='_self'
             class="thickbox" rel="8945e84f02aaca831b328b094ed24e1f"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/birlestirme-nggid0271-ngg0dyn-148x67x100-00f0w010c010r110f110r010t010.jpg"
             alt="Birleştirme Fonksiyonu"
             title="Birleştirme Fonksiyonu"
              width="148" /> </a>
</div>

<span></span> 

  * **Aktivasyon Fonksiyonu**

Birleştirme (toplama ) fonksiyonundan çıkan NET toplam hücrenin çıktısını oluşturmak üzere aktivasyon fonksiyonuna iletilir. Aktivasyon fonksiyonu genellikle doğrusal olmayan bir fonksiyon seçilir. Yapay sinir ağlarının bir özelliği olan “doğrusal olmama” aktivasyon fonksiyonlarının doğrusal olmama özelliğinden gelmektedir.  
Aktivasyon fonksiyonu seçilirken dikkat edilmesi gereken bir diğer nokta ise fonksiyonun türevinin kolay hesaplanabilir olmasıdır. Geri beslemeli ağlarda aktivasyon fonksiyonunun türevi de kullanıldığı için hesaplamanın yavaşlamaması için türevi kolay hesaplanır bir fonksiyon seçilir.

**- Doğrusal Aktivasyon Fonksiyonu**  
Doğrusal problemler çözmek amacıyla aktivasyon fonksiyonu doğrusal bir fonksiyon da seçilebilir. Doğrusal aktivasyon fonksiyonları matematiksel olarak F(x) = A * x olarak genellenebilir. Bu formülde A sabit bir katsayıdır.  A değerinin değişimi şekilde gösterilen doğrunun çıkış ekseniyle yaptığı açıyı değiştirmektedir.  


<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 246px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/Lineer.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/Lineer.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_Lineer.jpg"
             data-image-id="43"
             data-title="Doğrusal/Lineer Aktivasyon Fonksiyonu"
             data-description=""
             target='_self'
             class="thickbox" rel="8b1f1821d0805a30b2cc7f38207d841e"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/Lineer-nggid0243-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="Doğrusal/Lineer Aktivasyon Fonksiyonu"
             title="Doğrusal/Lineer Aktivasyon Fonksiyonu"
              width="246" /> </a>
</div>

<span></span> 

**- Adım Aktivasyon Fonksiyonu**  
Girdilerin sıfırdan büyük olup olmamasına göre -1 veya 1 çıktısı veren fonksiyondur. Sadece iki çeşit çıktı vermektedir.

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 251px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/adim.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/adim.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_adim.jpg"
             data-image-id="45"
             data-title="Adım/Step Aktivasyon Fonksiyonu"
             data-description=""
             target='_self'
             class="thickbox" rel="1fb9d869ade8804f296f423bdf650dc8"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/adim-nggid0245-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="Adım/Step Aktivasyon Fonksiyonu"
             title="Adım/Step Aktivasyon Fonksiyonu"
              width="251" /> </a>
</div>

<span></span> 

**- Sigmoid Aktivasyon Fonksiyonu**  
Sigmoid aktivasyon fonksiyonu sürekli ve türevi alınabilir bir fonksiyondur. Doğrusal olmayışı dolayısıyla yapay sinir ağı uygulamalarında en sık kullanılan fonksiyondur. Bu fonksiyon girdi değerlerinin her biri için sıfır ile bir arasında bir değer üretir. Sigmoid fonksiyonunun matematiksel ifadesi F(x)= 1/[(1+e)^(-x)]

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 244px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/Sigmod.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/Sigmod.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_Sigmod.jpg"
             data-image-id="44"
             data-title="Sigmod Aktivasyon Fonksiyonu"
             data-description=""
             target='_self'
             class="thickbox" rel="4d268c4fa59db68718938fa8c3c058f7"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/Sigmod-nggid0244-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="Sigmod Aktivasyon Fonksiyonu"
             title="Sigmod Aktivasyon Fonksiyonu"
              width="244" /> </a>
</div>

<span></span> 

**- Tanjant Hiperbolik Aktivasyon Fonksiyonu**  
Tanjant hiperbolik fonksiyonu, sigmoid fonksiyonuna benzer bir fonksiyondur. Sigmoid fonksiyonunda çıkış değerleri 0 ile 1 arasında değişirken hiperbolik tanjant fonksiyonunun çıkış değerleri -1 ile 1 arasında değişmektedir. Matematiksel ifadesi:  F(X)  =  (1- e^(-2x))/(1+ e^2x )

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 251px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/tanh.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/tanh.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_tanh.jpg"
             data-image-id="68"
             data-title="Tanjant Hiperbolik Aktivasyon Fonksiyonu"
             data-description=""
             target='_self'
             class="thickbox" rel="97dba7064d64e2b973ad1acf9133b639"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/tanh-nggid0268-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="Tanjant Hiperbolik Aktivasyon Fonksiyonu"
             title="Tanjant Hiperbolik Aktivasyon Fonksiyonu"
              width="251" /> </a>
</div>

<span></span> 

  * **Çıktılar**

Aktivasyon fonksiyonundan çıkan değer nöronun çıktı değeri olmaktadır. Bu değer ister yapay sinir ağının çıktısı olarak dış dünyaya verilir ister tekrardan ağın içinde kullanılabilir. Nöronun bir çıktısı olmasına rağmen bu çıktı istenilen sayıda nörona bağlı olabilir.

Yapay sinir hücresi hakkında bu kadar bilgiden sonra bir sonraki yazının konusu yapay sinir ağının yapısı olacak. Sonraki yazıda görüşmek üzere ;)