---
title: Komut Satırından Dns Adresi Değiştirme
author: Ahmet Kakıcı
layout: post
permalink: /genel/komut-satirindan-dns-adresi-degistirme/
views:
  - 2137
categories:
  - Genel
tags:
  - dhcp
  - dns
  - netsh
---
Son günlerde yine bir site engelleme furyası başladı. Dns değiştirerek bu sorunlardan kısmen de olsa kurtulabiliyoruz. Ancak iş yerinde dns değiştirdiğimde interente giremediğimden dolayı mecburen elle girdiğim dns sunucusunu silerek internete erişiyorum.

Akşam dns yaz sabah sil diye uğraşmaktansa bu işi komut satırından yapabiliyor muyuz diye biraz araştırdım ve netsh komutunu (windows için geçerli) [buldum][1].

netsh komutuyla dns değiştirmek istiyorsa öncelikle hani ağ bağdaştırıcısıyla çalışacağımızı belirlemeliyiz. Bunun için aşağıdaki parametrelerle beraber varolan bağdaştırıcı isimlerini alacağız.

<pre class="brush: csharp; title: ; notranslate" title="">netsh interface ip show config
</pre>

Gelen sonuçlarda &#8220;Kablosuz ağ bağlantısı 1&#8243;, &#8220;Yerel ağ bağlantısı 2&#8243; gibi isimler göreceksiniz. Hangi bağlantıyı değiştireceğinizi seçtikten sonra aşağıdaki komutta &#8220;bağlantı adı&#8221; yazan yere ilgili bağlantının adını yazdıktan sonra dns adresini değiştirebilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">netsh interface ip set dns name="bağlantı adı" static xxx.xxx.xxx.xxx
</pre>

Eğer ikincil dns sunucusu eklemek istiyorsanız aşağıdaki komutu kullanbilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">netsh interface ip add dns name="bağlantı adı" static xxx.xxx.xxx.xxx
</pre>

Daha sonra bu adresleri silmek için aşağıdaki komutu kullanabilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">netsh interface ip set dns name="bağlantı adı" source=dhcp
</pre>

 [1]: http://www.petri.co.il/configure_tcp_ip_from_cmd.htm "kaynak"