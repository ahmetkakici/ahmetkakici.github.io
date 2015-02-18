---
title: NotePad++ ile FTP erişimi
author: Ahmet Kakıcı
layout: post
permalink: /web/notepad-ile-ftp-erisimi/
views:
  - 2688
comment_count:
  - 1
trackback_count:
  - 
categories:
  - Web
  - Yazılım
tags:
  - ftp
  - notepad
---
Kod yazarken en sık kullandığım editörler C# için Visual Studio, Java için NetBeans. Bu iki dilin haricinde **her türlü** kodu yazdığım ve text editörü olarak kullandığım yegane program NotePad++. Sourceforge altında açık kaynak olarak geliştirilen NotePad++&#8217;ı fazla da övmeye gerek yok sanırım zira SourceForge tarafından en iyi developer aracı **<a href="http://sourceforge.net/community/index.php/landing-pages/cca08/" target="_blank">seçilerek</a>** başarısını ispat ediyor.

<!--more-->

NotePad++&#8217;ın en güzel özelliklerinden biri de PlugIn desteği. Benim bilgisayarımda şu an 5.0 versiyonu kurulu ve 2 gün önce çok güzel bir özelliğini keşfettim. En sevdiğim editörüm ile web siteme bağlanıp istediğim dosyaları NotePad++ ile düzenleyip kaydedebilioyrmuşum! Bu özelliği keşfetmeden önce genelde WinScp&#8217;nin dandik editörü ile bu işimi hallediyordum veya dosyayı bilgisayarıma indirip NotePad++ ile düzenleyip tekrar WinScp ile sunucuya gönderiyordum. Yazması bile zor oldu&#8230;

NotePad++ ile bunu nasıl mı yapıyorum ? *Plugins *menüsünden *FTP_SynchronizeA*&#8216;yı seçip *Show FTP Folders*&#8216;ı işaretliyorum. Bu sayede editörün içinde sağ tarafta yeni bir blok beliriyor. Yeni açılan bölümde *Open Settings Dialog* butonuna basarak *Adress* &#8211; *Username* &#8211; *Password* bölümlerini doldurup *Tamam*&#8216;a basıyoruz ve ayarlarımızı yapmış oluyoruz. Bu ayarları yaptıktan sonra *Open Settings Dialog* butonunun hemen yanında *Connect* butonu aktif oluyor. Bundan sonra bize bu butona basıp NotePad++&#8217;ın sunucumuza bağlanmasını izlemek düşüyor. Kısa bir süre sonra sunucudaki klasörlerimiz huzurumuzda.. Artık istediğimiz dosyayı seçip çift tıklayarak açıyor, düzenliyor ve kaydederek işimizi bitiriyoruz.

Eğer hala NotePad++ kullanmadıysanız mutlaka <a href="http://notepad-plus.sourceforge.net/uk/download.php" target="_blank">indirip</a> kullanmanızı tavsiye ediyorum.