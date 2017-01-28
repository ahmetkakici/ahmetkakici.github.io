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


**Biyolojik Sinir Ağlarının Yapısı**  
Bir insanın beyninde yaklaşık olarak 10 milyar sinir hücresi ve bu nöronların birbirleriyle yaptığı bağlantı sayısının ise 60 trilyon olduğu tahmin edilmektedir. Bu sinirler girdi bilgilerini duyu organlarından alırlar. Daha sonra alıcı (taşıyıcı) sinirler bu sinyalleri işleyip bir sonraki sinire aktararak sinyalin merkezi sinir sistemine kadar ulaşmasını sağlar. Merkezi sinir sistemi bu sinyalleri alıp yorumladıktan sonra tepki sinyallerini üretir. Bu sinyaller de tepkilerin oluşacağı organlara tepki sinirleri vasıtasıyla iletilir. Bu sayede duyu organlarından gelen bilgilere karşı tepki organlarına uygun işaretler sinir sistemi vasıtasıyla yollanır.

![Biyolojik Sinir Ağları](/assets/images/ysa/sinir sistemi.jpg)
 

**Yapay Sinir Hücresinin Yapısı**  
Yapay sinir hücreleri de biyolojik sinir hücrelerine benzer yapıdadır. Yapay nöronlar da aralarında bağ kurarak yapay sinir ağlarını oluştururlar. Aynı biyolojik nöronlarda olduğu gibi yapay nöronların da giriş sinyallerini aldıkları, bu sinyalleri toplayıp işledikleri ve çıktıları ilettikleri bölümleri bulunmaktadır.  
Bir yapay sinir hücresi beş bölümden oluşmaktadır;

  * Girdiler
  * Ağırlıklar
  * Birleştirme fonksiyonu
  * Aktivasyon fonksiyonu
  * Çıktılar

![Yapay sinir hücresi](/assets/images/ysa/yapay-sinir-hucresi.jpg)

  * **Girdiler**

Girdiler nöronlara gelen verilerdir. Girdiler yapay sinir hücresine bir diğer hücreden gelebileceği gibi direk olarak dış dünyadan da gelebilir. Bu girdilerden gelen veriler biyolojik sinir hücrelerinde olduğu gibi toplanmak üzere nöron çekirdeğine gönderilir.

  * **Ağırlıklar**

Yapay sinir hücresine gelen bilgiler girdiler üzerinden çekirdeğe ulaşmadan önce geldikleri bağlantıların ağırlığıyla çarpılarak çekirdeğe iletilir. Bu sayede girdilerin üretilecek çıktı üzerindeki etkisi ayarlanabilinmektedir. Bu ağırlıkların değerleri pozitif, negatif veya sıfır olabilir. Ağırlığı sıfır olan girdilerin çıkıl üzerinde herhangi bir etkisi olmamaktadır.

  * **Birleştirme Fonksiyonu**

Birleştirme fonksiyonu bir yapay sinir hücresine ağırlıklarla çarpılarak gelen girdileri toplayarak o hücrenin net girdisini hesaplayan bir fonksiyondur.

![Birleştirme Fonksiyonu](/assets/images/ysa/birlestirme.jpg)

  * **Aktivasyon Fonksiyonu**

Birleştirme (toplama ) fonksiyonundan çıkan NET toplam hücrenin çıktısını oluşturmak üzere aktivasyon fonksiyonuna iletilir. Aktivasyon fonksiyonu genellikle doğrusal olmayan bir fonksiyon seçilir. Yapay sinir ağlarının bir özelliği olan “doğrusal olmama” aktivasyon fonksiyonlarının doğrusal olmama özelliğinden gelmektedir.  
Aktivasyon fonksiyonu seçilirken dikkat edilmesi gereken bir diğer nokta ise fonksiyonun türevinin kolay hesaplanabilir olmasıdır. Geri beslemeli ağlarda aktivasyon fonksiyonunun türevi de kullanıldığı için hesaplamanın yavaşlamaması için türevi kolay hesaplanır bir fonksiyon seçilir.

**- Doğrusal Aktivasyon Fonksiyonu**  
Doğrusal problemler çözmek amacıyla aktivasyon fonksiyonu doğrusal bir fonksiyon da seçilebilir. Doğrusal aktivasyon fonksiyonları matematiksel olarak F(x) = A * x olarak genellenebilir. Bu formülde A sabit bir katsayıdır.  A değerinin değişimi şekilde gösterilen doğrunun çıkış ekseniyle yaptığı açıyı değiştirmektedir.  

![Doğrusal/Lineer Aktivasyon Fonksiyonu](/assets/images/ysa/Lineer.jpg)

**- Adım Aktivasyon Fonksiyonu**  
Girdilerin sıfırdan büyük olup olmamasına göre -1 veya 1 çıktısı veren fonksiyondur. Sadece iki çeşit çıktı vermektedir.

![Adım/Step Aktivasyon Fonksiyonu](/assets/images/ysa/adim.jpg)


**- Sigmoid Aktivasyon Fonksiyonu**  
Sigmoid aktivasyon fonksiyonu sürekli ve türevi alınabilir bir fonksiyondur. Doğrusal olmayışı dolayısıyla yapay sinir ağı uygulamalarında en sık kullanılan fonksiyondur. Bu fonksiyon girdi değerlerinin her biri için sıfır ile bir arasında bir değer üretir. Sigmoid fonksiyonunun matematiksel ifadesi F(x)= 1/[(1+e)^(-x)]


![Sigmod Aktivasyon Fonksiyonu](/assets/images/ysa/Sigmod.jpg) 

**- Tanjant Hiperbolik Aktivasyon Fonksiyonu**  
Tanjant hiperbolik fonksiyonu, sigmoid fonksiyonuna benzer bir fonksiyondur. Sigmoid fonksiyonunda çıkış değerleri 0 ile 1 arasında değişirken hiperbolik tanjant fonksiyonunun çıkış değerleri -1 ile 1 arasında değişmektedir. Matematiksel ifadesi:  F(X)  =  (1- e^(-2x))/(1+ e^2x )

![Tanjant Hiperbolik Aktivasyon Fonksiyonu](/assets/images/ysa/tanh.jpg) 

  * **Çıktılar**

Aktivasyon fonksiyonundan çıkan değer nöronun çıktı değeri olmaktadır. Bu değer ister yapay sinir ağının çıktısı olarak dış dünyaya verilir ister tekrardan ağın içinde kullanılabilir. Nöronun bir çıktısı olmasına rağmen bu çıktı istenilen sayıda nörona bağlı olabilir.

Yapay sinir hücresi hakkında bu kadar bilgiden sonra bir sonraki yazının konusu yapay sinir ağının yapısı olacak. Sonraki yazıda görüşmek üzere.