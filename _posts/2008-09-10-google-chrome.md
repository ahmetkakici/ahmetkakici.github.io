---
title: Google Chrome
author: Ahmet Kakıcı
layout: post
permalink: /web/google-chrome/
views:
  - 666
comment_count:
  - 9
trackback_count:
  - 
categories:
  - Web
  - Yazılım
tags:
  - exploit
  - google
  - safari
  - webkit
---
Google Chome piyasaya bomba gibi girdi. Binlerce (veya milyonlarca) internet kullanıcısı tarafından heyecan ile indirildi, denendi. Sonrasında yorumlar yavaş yavaş forumlara bloglara düşmeye başladı. Hızlıydı, güzeldi, çirkindi, IE daha güzel, FireFox&#8217;a benzemiş vs derken bir Chrome rüzgarı aldı gitti. Ben o tarz bir yazı yazmayacağım çünkü henüz Chrome kullanmadım. Ben size Chrome&#8217;un özünü yazacağım.

<!--more-->

Yazıma Chorme kullanan kişilerin &#8216;çoğumuzun yaptığı gibi&#8217; okumadan kabul ettiği kullanım koşullarına göz atarak başlarsam iyi olur sanırım. İşte az da olsa bazı sitelerin yazdığı o meşhur kullanım şartlarının 11. maddesinden birkaç alıntı:

  * By submitting, posting or displaying the content you give Google a perpetual, irrevocable, worldwide, royalty-free, and non-exclusive license to reproduce, adapt, modify, translate, publish, publicly perform, publicly display and distribute any content which you submit, post or display on or through, the services. This license is for the sole purpose of enabling Google to display, distribute and promote the services and may be revoked for certain services as defined in the additional terms of those services.
  * The software which you use may automatically download and install updates from time to time from Google. These updates are designed to improve, enhance and further develop the services and may take the form of bug fixes, enhanced functions, new software modules and completely new versions. You agree to receive such updates (and permit Google to deliver these to you) as part of your use of the services.
  * Some of the services are supported by advertising revenue and may display advertisements and promotions. These advertisements may be targeted to the content of information stored on the services, queries made through the services or other information.The manner, mode and extent of advertising by Google on the services are subject to change without specific notice to you.

Bir çoğumuz bu şartları okumadık keza okuyanların da bir kısmı muhtemelen deneme amaçlı kabul etmiştir. Zira arama motoru, reklamları, mail hizmeti ve diğer tüm hizmetleri sayesinde bizler hakkında **çok** fazla bilgi topluyor. Varsın Chrome ile de biraz bilgi toplasın.

Bu kullanım şartları konusu biraz göze batmaya başlamş olacak ki Google ufak bir düzenleme yapıp yeni bir anlaşma ile karşımıza çıktı.

Ama bazı durumlar var ki bilgi toplamaktan da zararlı olabiliyor(!). Chorme, Safari tarafından da kullanılan WebKit tarayıcı motorunu kullanıyor diye Safari&#8217;de bilinen açıklar hemen Chorme üzerinde de denendi. Bu açıklardan biri de *Carpet-Bomb*. Bu açık sayesinde Windows XP veya Vista üzerinde Safari kullananların bilgisayarlarına istemsiz olarak dosya aktarılıyordu. Nasıl mı ? İşte böyle:

> `#!/usr/bin/perl<br />
print "Content-type: blah/blah\n\n"`

Yukarıdaki perl kodunu içeren sayfayı gören Safari bu içerik tipini tanımadığı için direk olarak sayfayı kullanıcının masaüstüne indirmeye başlıyor. Tabii bu kodu içeren sayfayı iframe içinde sayfaya defalarca gömerek olaya adını veren *bomb* işlemini yapıyorlar.

Bu açıktan hemen sonra Apple Safari&#8217;nin bu açığını kapattı ayrıca Microsoft&#8217;ta kullanıcılarına <a href="http://www.microsoft.com/technet/security/advisory/953818.mspx" target="_blank">bir açıklama</a> yaparak bu açığı bildirdi.

Chrome&#8217;u henüz denemedim ancak bu açığın Chrome&#8217;da olacağını pek zannetmiyorum. Çünkü bu açık Nitesh Dhanjani tarafından 14 Mayıs tarihinde açıklandı, yani üzerinden epey zaman geçti. Ayrıca WebKit açık kanyak kodlu bir proje. Yani bu süre boyunca Google&#8217;ın açık kaynak kodlu bir projedeki bu kadar bilinen bir açığı kapatmamış olmayacağını düşünmüyorum (aksini ispat eden varsa bir yorum bıraksın :] )

Chrome&#8217;daki bir diğer sorun da aşağıdaki gibi girilen bağlantılarda programın hata vererek sonlanması ki Google&#8217;ın bunu da en kısa sürede çözeceğini düşünüyorum.

> <pre id="line70">&lt;<span class="start-tag">a</span><span class="attribute-name"> href</span>=<span class="attribute-value">"EVIL:%"</span>&gt;HERE&lt;/<span class="end-tag">a</span>&gt;</pre>

Chrome&#8217;u kullanmadan edindiğim bilgiler bunlar. Açıkçası bu kısa süre içerisinde denemeyi de düşünmüyorum çünkü FireFox ve eklentilerimle gayet mutluyum ve beta tester olmayacak kadar da pinpirikliyim.