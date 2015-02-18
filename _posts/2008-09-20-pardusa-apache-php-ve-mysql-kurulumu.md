---
title: 'Pardus&#8217;a Apache, PHP ve MySql Kurulumu'
author: Ahmet Kakıcı
layout: post
permalink: /yazilim/pardusa-apache-php-ve-mysql-kurulumu/
views:
  - 2861
comment_count:
  - 2
trackback_count:
  - 
categories:
  - Programlama
  - Yazılım
tags:
  - apache
  - kurulum
  - mysql
  - pardus
  - php
  - pisi
---
Apache, PHP ve MySql üçlüsüyle ilk tanıştığım zamanlarda kurulumu yapana kadar akla karayı seçmiştim. Tabii o zamanlar bilgisayar sadece oyun ve müzikten ibaretti. Kurduğum diğer programlar sadece &#8220;next&#8221; tuşuna basmaktan ibaretti. Bundan dolayı epey zorlanmıştım. Tabii daha sonraları AppServ,Xamp,Wamp gibi üçlü paketler piyasaya çıktı da kurulum işi kolaylaştı.

Bu yaşadığım tecrübeler hep Windows işletim sistemine aitti. Geçtiğimiz ay Pardus&#8217;u kurduktan sonra haliyle üç silahşörleri de kullanmak istedim. Nasıl yaparım ne ederim derken bir baktım ki kurmuşum :]

<!--more-->

Pardus&#8217;da bulunan paket yöneticisi PİSİ sayesinde herşey tek satırlık bir komut ile oldu bitti.

> sudo pisi it apache mysql-server mod_php

İşte bilgisayarınıza Apache, Mysql ve PHP kuran komut. Tabii bu komutu kullanabilmek için super user haklarına sahip olmanız lazım.

*su* komutuyla bu isteğinizi Pardus&#8217;a bildirip şifrenizi girdikten sonra bir sorununuz kalmayacaktır.

MySql sunucusunun çalışması için gerekli olan veritabanlarını da aşağıdaki komut ile oluşturabilirsiniz

> mysql\_install\_db

Eğer Apache ve Mysql&#8217;in servis olarak çalışmasını istiyorsanız [işletim sisteminin açılışyla otomatik olarak çalışmaya başlaması] aşağıdaki iki komutu çalıştırmalısınız

> service mysql_server on  
> service apache on

Üç silahşörler emrinize amade :)

Not: En güncel PİSİ paketleri için kurulumdan önce &#8220;pisi update-repo&#8221; komutu ile paket yöneticisini güncellemelisiniz.