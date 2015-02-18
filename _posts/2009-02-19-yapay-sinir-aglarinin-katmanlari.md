---
title: Yapay Sinir Ağlarının Katmanları
author: Ahmet Kakıcı
layout: post
permalink: /yapay-sinir-aglari/yapay-sinir-aglarinin-katmanlari/
views:
  - 9812
categories:
  - Yapay Sinir Aglari
tags:
  - Programlama
  - Yapay Sinir Aglari
---
Serinin üçüncü ve diğerlerine göre nispeten kısa bir bölümüyle yapay sinir ağlarına devam ediyoruz (<a href="http://www.ahmetkakici.com/yazilim/yapay-sinir-aglarina-giris/" target="_blank">1</a> &#8211; <a href="http://www.ahmetkakici.com/yapay-sinir-aglari/yapay-sinir-aglarinin-mimarisi-ve-yapi-elemanlari/" target="_blank">2</a>) . Bu yazıyı kısa kesmemin sebebi bundan sonraki bölümde yapay sinir ağlarının sınıflandırılması konusuna değinecek olmam ve onun da biraz uzun olmasıdır. Uzun uzadıya yazıp kimseyi bunaltmak istemem :)

**Yapay Sinir Ağlarının Yapısı  
**

Yapay sinir ağları yapay sinir hücrelerinin birbirine bağlanmasıyla oluşan yapılardır. Yapay sinir ağları üç ana bölümde incelenir; giriş, ara ve çıkış katmanları. <!--more-->

<div class="ngg-gallery-singlepic-image ngg-center" style="max-width: 320px">
  <a href="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/ysa-yapi.jpg"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/ysa-yapi.jpg"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/thumbs/thumbs_ysa-yapi.jpg"
             data-image-id="74"
             data-title="ysa-yapi.jpg"
             data-description=""
             target='_self'
             class="thickbox" rel="b9dab0aa6fb5ba79085879e2876b0b15"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/uploads/2009/02/ysa/dynamic/ysa-yapi-nggid0274-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.jpg"
             alt="ysa-yapi.jpg"
             title="ysa-yapi.jpg"
              width="320" /> </a>
</div>

<span></span> 

**Giriş Katmanı**

Yapay sinir ağına dış dünyadan girdilerin geldiği katmandır. Bu katmanda dış dünyadan gelecek giriş sayısı kadar nöron bulunmasına rağmen genelde girdiler herhangi bir işleme uğramadan alt katmanlara iletilmektedir.

**Ara Katmanı**

Giriş katmanından çıkan bilgiler bu katmana gelir. Ara katman sayısı ağdan ağa değişebilir. Bazı yapay sinir ağlarında ara katman bulunmadığı gibi bazı yapay sinir ağlarında ise birden fazla ara katman bulunmaktadır.  Ara katmanlardaki nöron sayıları giriş ve çıkış sayısından bağımsızdır. Birden fazla ara katman olan ağlarda ara katmanların kendi aralarındaki nöron sayıları da farklı olabilir. Ara katmanların ve bu katmanlardaki nöronların sayısının artması hesaplama karmaşıklığını ve süresini arttırmasına rağmen yapay sinir ağının daha karmaşık problemlerin çözümünde de kullanılabilmesini sağlar.****

**Çıkış Katmanı**

Ara katmanlardan gelen bilgileri işleyerek ağın girdi katmanından gelen verilere karşılık olan çıktıları üreten katmandır. Bu katmanda üretilen çıktılar dış dünyaya gönderilir. Geri beslemeli ağlarda bu katmanda üretilen çıktı kullanılarak ağın yeni ağırlık değerleri hesaplanır.