---
title: Prolog ile Determinant Hesabı
author: Ahmet Kakıcı
layout: post
permalink: /programlama/prolog-ile-determinant-hesabi/
views:
  - 2673
categories:
  - Programlama
tags:
  - kod
  - Programlama
  - prolog
---
<a href="http://en.wikipedia.org/wiki/Determinant" target="_blank">Determinant</a>; bir kare matrisi, reel bir sayıyla eşleştiren özel bir fonksiyondur. Sadece kare matrislere uygulanabilir. Determinant hesabının temel yolu minör ve kofaktörlerinin hesaplanması yöntemidir. Buna ek olarak kolay hesaplama için <a href="http://en.wikipedia.org/wiki/Rule_of_Sarrus" target="_blank">Sarrus Yöntemi</a> adında başka bir yöntem daha geliştirilmiştir.  
<!--more-->

  
Minör ve kofaktör hesabı ile daha büyük matrisleri daha sistemli bir şekilde çarpabiliriz.  
Minör tanım olarak: A = (aij) nxn kare matrisinde bir aij ( 1≤i,j≤n)  öğesinin bulunduğu i. satır ve j. sütunun çıkarılmasıyla elde edilen n-1. dereceden kare matrisinin determinantıdır. Mij ile ifade edilir.  
A = (aij) nxn matrisinde aij öğesinin minörü olan Mij ‘nin (-1)^(i+j) ile çarpılmasıyla elde edilen sayıya aij öğesinin kofakötür denir ve Aij ile gösterilir.  
Bir kare matrisin minör ve kofaktörlerinin çarpımlarının toplamı o matrisin determinantını verir.  
Prolog dilinde yazılan programda da kofaktör ve minör hesabı ile determinant hesabı yapılmıştır. Goal kısmında örnek bir matris verilerek determinantı hesaplanıştır.

<pre class="brush: jscript; title: ; notranslate" title="">DOMAINS
liste=integer*
matris = liste*
int=integer

PREDICATES
ilkEleman(liste,int)
uzunluk(liste,int)
detBul(liste,liste,int)
ilkleriSil(matris,matris)
negatif(int,int)
sonaAt(matris,matris)
tersCevirListe(matris,matris)
tersCeviriciListe(matris,matris,matris)
det(matris,int,int,int)

CLAUSES
ilkEleman([X|_],X).

uzunluk([],0).
uzunluk([_|K],U):-uzunluk(K,X),U=X+1.

ilkleriSil([],[]).
ilkleriSil([[_|BasKuyruk]|Kuyruk1],[ BasKuyruk |SonucKuyruk]):-
ilkleriSil(Kuyruk1,SonucKuyruk).

negatif(-1,1).
negatif(1,-1).

sonaAt([Bas|Kuyruk],Sonuc):-
tersCevirListe(Kuyruk,TersKuyruk),
tersCevirListe([Bas|TersKuyruk],Sonuc).

tersCevirListe(X,Y):-tersCeviriciListe(X,[],Y).
tersCeviriciListe([],X,X).
tersCeviriciListe([B|K],TMP,SONUC) :-
tersCeviriciListe(K,[B|TMP],SONUC).

detBul([Bas1,Kuyruk1|_],[Bas2,Kuyruk2|_],Sonuc):-
Sonuc = Bas1*Kuyruk2-Bas2*Kuyruk1.

det([Bas1,Bas2|_],_,Sonuc,_):-
uzunluk(Bas1,En),
En&lt;=2,
detBul(Bas1,Bas2,Sonuc),!.

det([Bas|_],Sayac,0,_):-uzunluk(Bas,En),En&lt;=Sayac,!.

det([Bas|Kuyruk],Sayac,Sonuc,_):-
YeniSayac=Sayac+1,
uzunluk(Bas,En),
En&gt;Sayac,
En&lt;=3,
sonaAt([Bas|Kuyruk],Sonda),
ilkEleman(Bas,KatSayi),
ilkleriSil(Kuyruk,KuyrukOrta),
det(KuyrukOrta,0,OrtaSonuc,_),
det(Sonda,YeniSayac,YanSonuc,_),
Sonuc=(KatSayi*OrtaSonuc)+YanSonuc,!.

det([Bas|Kuyruk],Sayac,Sonuc,X):-
YeniSayac=Sayac+1,
uzunluk(Bas,En),
En&gt;Sayac,
sonaAt([Bas|Kuyruk],Sonda),
ilkEleman(Bas,KatSayi),
ilkleriSil(Kuyruk,KuyrukOrta),
negatif(X,Y),
det(KuyrukOrta,0,OrtaSonuc,Y),
det(Sonda,YeniSayac,YanSonuc,Y),
Sonuc=(X*KatSayi*OrtaSonuc)+YanSonuc.

GOAL
write("_____"),nl,det([[1,2,4,8],[2,2,7,11],[3,6,3,12],[4,13,0,5]],0,Sonuc,1),write(Sonuc).

</pre>

Programda kullanılan yüklemlere tek tek bakacak olursak yüklemlerin yaptığı görevler aşağıda açıklanmıştır:

  * ilkEleman(liste,int):  aldığı tamsayı listesinin ilk elemanını vermektedir.
  * uzunluk(liste,int) :  aldığı tamsayı listesinin eleman sayısını vermektedir.
  * detBul(liste,liste,int) :  2&#215;2 matrisin çarpımını yapar. Aldığı iki listenin uzunluğu da birbirine eşit ve iki olmalıdır.
  * ilkleriSil(matris,matris) :  Minörleri ilk satıra göre açtığım için verilen matrisin ilk satırını silmek için bu yüklem kullanılmıştır.
  * negatif(-1,1) :  Kofaktörlerin katsayılarını hesaplamak için kullanılmıştır. Her kofaktörde bir önceki kofaktörün katsayısının negatifi hesaplanmıştır.
  * sonaAt(matris,matris) :  Minörlerin hesabında bir sonraki sütuna göre açılım yapıldığında bu yüklem sayesinde ilk sütun sona atılarak ikinci sütun ilk sütun haline getirilir. Ayrıca 3&#215;3 matrislerde determinant hesaplanırken katsayılarının sırasıyla +1 ve -1 ile çarpılmasına bu yüklem sayesinde gerek kalmamıştır.
  * tersCevirListe(matris,matris) :  Sona at yükleminde ilk sütunu sona atmak için varolan matrisin ilk sütunu alınarak kalan matris ters çevirilerek ilk sütun başa koyulduktan sonra matris tekrar ters çevrilmiştir. Bu yüklem ters çevirme işlemini yapmaktadır.
  * tersCeviriciListe(matris,matris,matris) :  tersCevirListe yükleminde kullanılan geçici matrisi bu yüklem ile tanımlayarak asıl yüklemin iki parametre ile gerekli çevirmeyi yapması sağlanmıştır.  
    det(matris,int,int,int) ) : det yüklemi bütün determinant çarpım işlemlerini gerçekleştirmektedir.

Yukarıdan aşağıya doğru yazılmış dört yüklemi sırasıyla incelersek;

  1. İlk yüklem 2&#215;2 matris kaldığı zaman bunu detBul yüklemi sayesinde hesaplar ver geri döndürür.
  2. İkinci yüklem ise ilk sütunu sona atarak hesaplanan determinantların durma koşulunu belirler. Eğer sayac değişkeni sıfır olmuşsa yani n sütun varsa ve her biri için açılım yapılmışsa sonuç değeri sıfır olarak döndürür.
  3. Üçüncü yüklem ise 3. dereceden matrislerin determinant hesabında kullanılmıştır. 3. Dereceden matrislerde daha fazla alt matris olmadığından dolayı katsayı değişimine gerek kalmamıştır.
  4. Dördüncü yüklem ise 4. derece ve üstü matrislerin determinantını hesaplarken kofaktörü değiştirmek için kullanılmıştır.