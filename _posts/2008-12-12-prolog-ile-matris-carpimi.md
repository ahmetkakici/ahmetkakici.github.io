---
title: Prolog ile Matris Çarpımı
author: Ahmet Kakıcı
layout: post
permalink: /programlama/prolog-ile-matris-carpimi/
views:
  - 1560
categories:
  - Programlama
tags:
  - kod
  - prolog
---
Matris çarpımı birçok programlama dilinde öncelikli verilen ödevlerden biri olsa gerek. Aşağıdaki kodu yazarken anladım ki prolog bu dillerin arasında yok ve olmamalı. Prolog yapısından dolayı bu tip işlemleri yapmak için [bence] oldukça zor bir dil. Mantıksal programlamada veya öz-yinelemeli şekildeki problemlerin çözümünde kullanıldığı zaman az kod ile çok iş yapılabiliniyor ancak matris çarpımı için aynı şeyi diyemiyorum ve sizlere kodu takdim ediyorum :

<!--more-->

<pre class="brush: css; title: ; notranslate" title="">DOMAINS
liste=integer*
matris = liste*
int=integer

PREDICATES
listeGoster(liste)
matrisGoster(matris)
listeTopla(liste,int)
listeCarp(liste,liste,liste)
listeVeMatris(liste,matris,liste)
matrisCarp(matris,matris,matris)

CLAUSES
listeGoster([]).
listeGoster([B|K]):-write(B," "),listeGoster(K).

matrisGoster([]).
matrisGoster([B|K]):-
write("["),
listeGoster(B),
write("]"),nl,
matrisGoster(K).

listeTopla([],0).
listeTopla([X|K],T):-listeTopla(K,Y),T=Y+X.

listeCarp([],[],[]).
listeCarp([Bas1|Kuyruk1],[Bas2|Kuyruk2],[SonucBas|SonucKuyruk]):-
SonucBas=Bas1*Bas2,
listeCarp(Kuyruk1,Kuyruk2,SonucKuyruk).

listeVeMatris(_,[],[]).
listeVeMatris(Liste1,[MatrisBas|MatrisKuyruk],[CarpimBas|CarpimKuyruk]):-
listeCarp(Liste1,MatrisBas,Carpim),
listeTopla(Carpim,CarpimBas),
listeVeMatris(Liste1,MatrisKuyruk,CarpimKuyruk).

matrisCarp([],_,[]).
matrisCarp([Bas1|Kuyruk1],Matris2,[SonucBas|SonucKuyruk]):-
listeVeMatris(Bas1,Matris2,SonucBas),
matrisCarp(Kuyruk1,Matris2,SonucKuyruk).

GOAL
matrisCarp(
[[1,2,3],[3,4,5],[3,1,1]],
[[1,5,5],[2,3,3],[3,4,1],[5,5,1]], Y),
matrisGoster(Y).
</pre>

Programda kullanılan yüklemlere tek tek bakacak olursak yüklemlerin yaptığı görevler aşağıda açıklanmıştır:

  * *listeGoster* : Liste elemanlarını write iç yüklemi ile göstermek yerine bu yüklem kullanılmıştır.

  * *matrisGoster* : Matris elemanlarını write iç yüklemi ile göstermek yerine bu yüklem kullanılmıştır, aldığı matrisin her bir satırını listeGoster yüklemi sayesinde ekrana yazdırır.

  * *listeTopla*: Listenin elemanlarını toplayan bir yüklemdir. Çarpım sonucu elde edilen listeyi toplamada kullanılmıştır.

  * *listeCarp*: Uzunluğu eşit iki liste elemanlarını birebir çarpan bir yüklemdir.

  * *listeVeMatris*: Birinci matrisin ilk satırı ile ikinci matrisin tamamını çarpmak için bu yüklem kullanılmıştır.

  * *matrisCarp*: Verilen iki matrisin birincisini satır satır alıp ikinci matrisle listeVeMatris yüklemi saysinde çarpar.

Programa goal kısmındaki ikinci matris transpozesi alınmış şekilde yazılmıştır. Transpozesini hesaplayacak bir yüklem yazmayı gözüme kestiremediğim için bu şekilde yaptım, umarım işinize yarar.