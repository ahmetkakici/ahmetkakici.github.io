---
title: WordPress All in One SEO Pack XSRF açığını kapatma
author: Ahmet Kakıcı
layout: post
permalink: /wordpress/wordpress-all-in-one-seo-pack-xsrf-acigini-kapatma/
syntaxhighlighter_encoded:
  - 1
views:
  - 1331
categories:
  - Wordpress
tags:
  - Wordpress
  - xsrf
---
Bugün friendfeed&#8217;de Onur Yılmaz&#8217;ın yazdığı <a href="http://friendfeed.com/onuryilmaz/1cdaa34e/wordpress-all-in-one-seo-pack-ten-kaynakl-bir" target="_blank">mesajı</a> görünce biraz panik yaptım. Çünkü All in One SEO Pack eklentisini ben de kullanıyorum. WordPress fonksiyonlarıyla çok fazla içli dışlı olmadığımdan dolayı hemen <a href="http://codex.wordpress.org/" target="_blank">WordPress Codex</a> sayfasına gidip kullanabileceğim bir kaç fonksiyon aradım ve sanırım aradığımı da buldum. Kendi bilgisayarımda denedim ve herhangi bir sorun ile karşılaşmadım.

Lafı fazla uzatmadan bu açığı nasıl kapatacağımıza bakalım.Sunucunuzda wordpress&#8217;in kurulu olduğu dizini açın ve aşağıdaki dosyaya kadar ilerleyin

<pre class="brush: php; title: ; notranslate" title="">wp-content/plugins/all_in_one_seo_pack/all_in_one_seo_pack.php</pre>

Dosyayı açıp aşağıdaki satırı bulun:

<pre class="brush: php; title: ; notranslate" title="">if ($_POST['action'] && $_POST['action'] == ‘aiosp_update’) { </pre>

Bu satırın hemen altına aşağıdaki satırı ekleyin:

<pre class="brush: php; title: ; notranslate" title="">if (! wp_verify_nonce($nonce, ’seo-nonce’) ) die(’Dikkat’); </pre>

Benim &#8216;Dikkat&#8217; yazdığıma bakmayın, istediğiniz hata mesajını girebilisiniz. Daha sonra da form alanına bir nonce alanı ekleyelim. Bunun için de aynı dosyada aşağıdaki satırı bulun:

<pre class="brush: php; title: ; notranslate" title="">&lt;input type=”hidden” name=”action” value=”aiosp_update” /&gt;</pre>

ve hemen altına şu satırı eklemeniz ile işlem tamamlanacaktır:

<pre class="brush: php; title: ; notranslate" title="">&lt;input type=”hidden” name=”seo-nonce-input” value=”&lt;?php echo wp_create_nonce(’seo-nonce’); ?&gt;”&gt; </pre>

Eğer amacımıza ulaşamadıysak haber verin biraz daha kurcalayalım.