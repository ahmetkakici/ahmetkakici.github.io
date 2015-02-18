---
title: Prolog ile Liste İşlemleri
author: Ahmet Kakıcı
layout: post
permalink: /programlama/prolog-ile-liste-islemleri/
views:
  - 2548
categories:
  - Programlama
tags:
  - kod
  - Programlama
  - prolog
---
Prolog&#8217;un bel kemiği olan liste veri yapısı için daha önceden kullandığım liste fonksiyonlarını aşağıda listeledim. Fonksiyonların isimlerinden ne iş yaptıkları belli oluyor yine de anlamadığınız yer olursa bir yorum bırakabilirsiniz.

<!--more-->

<pre class="brush: jscript; title: ; notranslate" title="">PREDICATES
listeGoster(liste)
uzunluk(liste,int)
uye(int,liste)
ekle(int,liste,liste)
yoksaEkle(int,liste,liste)
sil(int,liste,liste)
hepsiniSil(int,liste,liste)
elemanTopla(liste,int)
arttir(int,liste,liste)
birles(liste,liste,liste)
birlesim(liste,liste,liste)
kesisim(liste,liste,liste)
buda(liste,liste)
tersCevir(liste,liste)
tersCevirici(liste,liste,liste)
prefix(liste,liste)
suffix(liste,liste)

CLAUSES
listeGoster([]).
listeGoster([B|K]):-write(B),nl,listeGoster(K).

uzunluk([],0).
uzunluk([_|K],U):-uzunluk(K,X),U=X+1.

uye(X,[X|_]).
uye(X,[_|K]):-uye(X,K).

ekle(X,L,[X|L]).

yoksaEkle(X,L,L):-uye(X,L),!.
yoksaEkle(X,L,[X|L]).

sil(X,[X|L],L).
sil(X,[B|K1],[B|K2]):-sil(X,K1,K2).

hepsiniSil(_,[],[]).
hepsiniSil(X,[X|L],M):-sil(X,L,M),!.
hepsiniSil(X,[Y|K1],[Y|K2]):-sil(X,K1,K2).

elemanTopla([],0).
elemanTopla([X|K],T):-elemanTopla(K,Y),T=Y+X.

arttir(_,[],[]).
arttir(X,[B1|K1],[B2|K2]):-B2=B1+X,arttir(X,K1,K2).

birles([],L,L).
birles([B|K1],L2,[B|K2]):-birles(K1,L2,K2).

birlesim([],L,L).
birlesim([B|K1],L2,K2):- uye(B,L2),birlesim(K1,L2,K2),!.
birlesim([B|K1],L2,[B|K2]):- birlesim(K1,L2,K2).

kesisim([],_,[]).
kesisim(_,[],[]).
kesisim([B|K1],L2,[B|K2]):-uye(B,L2),kesisim(K1,L2,K2),!.
kesisim([_|K1],L2,K2):-kesisim(K1,L2,K2).

buda([],[]).
buda([B|K],L):- uye(B,K),buda(K,L),!.
buda([B|K1],[B|K2]):- buda(K1,K2).

tersCevir(X,Y):-tersCevirici(X,[],Y).
tersCevirici([],X,X).
tersCevirici([B|K],TMP,SONUC) :- tersCevirici(K,[B|TMP],SONUC).

prefix([],_).
prefix([B|K1],[B|K2]):-prefix(K1,K2).

suffix(X,Y):-tersCevir(X,TX),tersCevir(Y,TY),prefix(TX,TY).

</pre>