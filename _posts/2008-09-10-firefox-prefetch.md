---
title: FireFox Prefetch
author: Ahmet Kakıcı
layout: post
permalink: /web/firefox-prefetch/
views:
  - 575
comment_count:
  - 2
trackback_count:
  - 
categories:
  - Programlama
  - Web
tags:
  - firefox
  - prefetch
---
Geçtiğimiz günlerde Facebook&#8217;ta bir albüm gezerken bir şey dikkatimi çekti; bildiğiniz gibi albümde fotoğrafın üzerine tıklayarak (veya klavyeden sağ ok tuşuna basarak) bir sonraki fotoğrafa geçiyorsunuz. Peki bu işlem sonunda bir sonraki fotoğrafın gösterilme hızına hiç dikkat ettiniz mi ? Sanki kendi bilgisayarımda bir fotoğraf albümüne bakar gibi fotoğrafları oldukça hızlı bir şekilde gezdim. Bu bana biraz garip geldi çünkü daha önceden bu albümü ziyaret etmemiştim, yani ön bellekten gösterme imkanı yoktu. Tabi ben istemeden bu fotoğraflar bilgisayarıma gelmişse olaylar değişir.

<!--more-->

Bu konu hakkında biraz araştırma yaptım ve Mozilla&#8217;nın sayfasında <a href="http://developer.mozilla.org/en/Link_prefetching_FAQ" target="_blank">bir yazı </a>buldum. Olayın özeti şöyle ki web sitenizin kodlamasını yaparken içeriğe göre kullanıcının ziyaret edebileceği içeriğe link veriyorsunuz. Tarayıcı belirli bir süre boş kaldığında otomatik olarak o muhtemel içeriği ön belleğe çekiyor. Bu sayede sanki o sayfaya daha önce erişmiş gibi hızlı bir şekilde ulaşıyoruz.

Bu özellik sadece Firefox tarayıcısında bulunmuyor. Mozilla&#8217;nın da belirttiği gibi:

> Browsers based on Mozilla 1.2 (or later) as well as browsers based on Mozilla 1.0.2 (or later) support prefetching. This includes Firefox and Netscape 7.01+

Eğer tarayıcınızın prefetch özelliğini destekleyip desteklemediğini öğrenmek istiyorsanız <a href="http://gemal.dk/browserspy/prefetch.php" target="_blank"><strong>bu</strong></a> adrese girin ve 10-15sn civarı bekledikten sonra sayfayı yenileyin. *Prefetch is working. *yazısını gördüyseniz ne mutlu size.

Bu arada FaceBook&#8217;un bu özelliği kullanıp kullanmadığına dikkat etmedim, kaynak kodunda bulan olursa bir yorum bıraksın.