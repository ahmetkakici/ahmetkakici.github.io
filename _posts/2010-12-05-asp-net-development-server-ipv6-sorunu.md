---
title: 'ASP.NET Development Server &#8211; IPv6 sorunu'
author: Ahmet Kakıcı
layout: post
permalink: /yazilim/asp-net-development-server-ipv6-sorunu/
views:
  - 504
categories:
  - Yazılım
---
Son bir yıldır ASP.NET ile uygulama geliştiren ve günlük hayatta Firefox kullanan biri olarak üzerinde çalıştığım uygulamaların debug aşamasında bu kadar yavaş çalışmasına bir anlam veremiyordum. Nasıl oluyorsa Internet Explorer gibi bir tarayıcıda sorunsuz bir şekilde debug ettiğim sayfalar Firefox ve Chrome ile anlamsız bir şekilde yavaş açılıyordu.

Geçen hafta [stackoverflow][1]&#8216;da gezerken gözüme takılan bir [soruya][2] gelen [cevap][3] ise günü kurtardı ve sorumu da çözmüş oldu.

Sorunun sebebi Firefox&#8217;un ASP.NET development server&#8217;ın verdiği rastgele portları çözerken yaşadığı karmaşaymış. Firefox&#8217;un IPv6 desteğini pasif hale getirince sorun kalmadı.

Eğer sizler de benim gibi ASP.NET ile uygulama geliştiriyorsanız ve Firefox&#8217;un debug performansından şikayetçiyseniz Firefox&#8217;ta adres çubuğuna `<strong>about:config</strong> `yazıp dikkatli olacağınıza da söz verdikten sonra ` ``<strong>network.dns.disableIPv6</strong> `özelliğini` <strong>true</strong> `yaparsanız sizin de sorununuz çözülmüş olacaktır.

Bu sayede debug işleminde de Internet Explorer&#8217;dan uzak durabilirsiniz.

 [1]: http://stackoverflow.com/ "www.stackoverflow.com"
 [2]: http://stackoverflow.com/q/795451/93732
 [3]: http://stackoverflow.com/questions/795451/asp-net-mvc-on-cassini-how-can-i-force-the-content-directory-to-return-304s-in/795476#795476