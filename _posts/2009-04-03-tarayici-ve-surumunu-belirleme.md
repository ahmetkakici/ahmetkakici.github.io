---
title: Tarayıcı ve Sürümünü Belirleme
author: Ahmet Kakıcı
layout: post
permalink: /programlama/tarayici-ve-surumunu-belirleme/
syntaxhighlighter_encoded:
  - 1
views:
  - 1208
categories:
  - Programlama
tags:
  - browser
  - javascript
---
Tarayıcı pazarında firmalar ve sürümler arttıkça tasarımcıların işi de günden güne zorlaşıyor. X tarayıcısında sorunsuz görünen bir tasarım Y tarayıcısı tarafından yorumlanınca istenmedik sonuçlar verebiliyor bunun içinde tarayıcıya özel tasarımlar yazmak veya kullanıcıyı uyarmak gerekiyor. Genelde sunucu taraflı kod yazdığım için beni pek ilgilendirmeyen bu sorunu son zamanlarda javascript ve az da olsa css ile uğraştığım için ben de yaşadım ve internette tarayıcı belirlemek için yazılan hazır bir kod bulmak için hemen google&#8217;a doğru yol aldım. Derdimi google&#8217;a anlatamamdan olsa gerek tam olarak aradığımı bulamadım ve aşağıdaki kod ortaya çıktı. Benim gibi google&#8217;a başvurup aradığını bulamayanlar için de paylaşayım dedim. Aşağıdaki kod kullanılan tarayıcının adını ve sürümünü bulmakta. Bana sürüm numarasının ilk hanesi gerektiği için sadece ilk haneyi aldım, düzenli ifadeyi kendinize göre ayarlayıp istediğiniz userAgent bilgisini alabilirsiniz.

<!--more-->

<pre class="brush: jscript; title: ; notranslate" title="">&lt;script&gt;
var application = navigator.appName;
var agent = navigator.userAgent;
var browser;
var version;

if (application == 'Microsoft Internet Explorer'){
	var patternIE = "MSIE ([0-9])";
	if (RegExp(patternIE).exec(agent) != null){
		browser = "Microsoft Internet Explorer";
		version = RegExp.$1;
	}
}
else if (application == 'Netscape'){
	var patternFF = "Firefox/([0-9])";
	var patternCH = "Chrome/([0-9])";
	if (RegExp(patternFF).exec(agent) != null){
		browser = "Mozilla Firefox";
		version = RegExp.$1;
	}
	else if (RegExp(patternCH).exec(agent) != null){
		browser = "Google Chrome";
		version = RegExp.$1;
	}
}
else if (application == 'Opera'){
	var patternOP = "Opera/([0-9])";
	if (RegExp(patternOP).exec(agent) != null){
		browser = "Opera";
		version = RegExp.$1;
	}
}
alert (browser+'  '+ version);
&lt;/script&gt;

</pre>