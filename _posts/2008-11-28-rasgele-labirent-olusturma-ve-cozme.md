---
title: Rasgele Labirent Oluşturma ve Çözme
author: Ahmet Kakıcı
layout: post
permalink: /programlama/rasgele-labirent-olusturma-ve-cozme/
views:
  - 6763
syntaxhighlighter_encoded:
  - 1
categories:
  - Programlama
tags:
  - c
  - kod
  - pointer
---
Aşağıdaki program çalışan ve bir şeye benzeyen ilk C programım diyebilirim :) Tabii ilk programım olmasından dolayı optimum şekilde çalışmıyor olabilir. Ayrıca programı yazdığım zamanda görsel programlama namına bir şey bilmediğim için program konsoldan çalışıyor.

Sadece kod verip bırakmak istemedim ve az da olsa ne yaptığımı açıklayım dedim. Öncelikle programın üç ana özelliğini belirtmeliyim sanırım;

<!--more-->

-Her seferinde rasgele bir labirent oluşturulacak

-Labirent üzerinde kapalı yani ulaşılamayan bir bölge olmayacak

-Son olarak labirent çözülecek :)

Ana hatları söyledikten sonra programın çalışmasına gelelim.

Labirenti oluşturacak alan belirlendikten sonra (ör 10&#215;10) bu çerçeve üzerinde bulunan her noktayı bir listeye ekleniyor. Daha sonra bu noktalardan biri rasgele olarak seçiliyor. Bu nokta başlangıç alınarak daha önceden belirlenen adım sayısı kadar rasgele yönlerde ilerlenerek duvar örülüyor. Rasgele yönlerde atılan bu adımlar sonrasında oluşan yeni duvarlar çerçevenin olduğu listeye ekleniyor. Başlangıç olarak seçtiğimz ilk nokta ise listeden siliniyor.Yeni bir adım atılıp duvar örüldüğünde dikkat edilmesi gereken nokta ise kapalı alan oluşturmamaktır.

Labirenti çözmek ise oluşturmaktan çok daha kolay. Klasik **<a href="http://en.wikipedia.org/wiki/Self-avoiding_walk" target="_blank">self avoding walk</a>** algoritmasıyla çözüme gidilmiştir. Labirentin sol en üst köşesi başlangıç, sağ en alt köşesi ise bitiş noktası olarak belirlenmiş ve çözüm ona göre çalışmaktadır. Tabii değiştirmek sizin elinizde :)

<pre class="brush: cpp; title: ; notranslate" title="">///////////////////////////////////////////////////
/*             HEADER DOSYALARI                  */
///////////////////////////////////////////////////
#include "conio.h"
#include "stdlib.h"
#include "stdio.h"
#include "iostream.h"
#define STEP 5
#define YOL 0
#define YOL2 1
#define GEREKSIZ -6
#define DUVAR -2
#define pasifDUVAR -5
#define DUGUM -1
#define eskiDUGUM -3
#define pasifDUGUM -4
#include &lt;time.h&gt;

///////////////////////////////////////////////////
/*                LISTE YAPISI                   */
///////////////////////////////////////////////////
struct Item {
	struct Item *next;
	int val1,val2;    // Dizi iki boyutlu oldugu icin 2 elemanli liste olusturdum.
};

struct List {
	struct Item *list;
};


///////////////////////////////////////////////////
/*     LISTE FONKSIYONLARININ PROTOTIPLERI       */
///////////////////////////////////////////////////
	struct List *liste_yarat(struct List *pl);			//Liste Olusturuyor
	void listeye_ekle(struct List *pl,int,int);			//Listeye eleman ekliyor
	void listeden_sil(struct List *pl,int,int);			//Listeden eleman siliyor
	void liste_gez(struct List *pl,int ,int& , int&);	//Listeden n. siradaki elemani aliyor
	void liste_goster(struct List *pl);					//Lisde degerlerini yazdiriyor
	int  uzunluk(struct List *pl);						//Liste uzunlugunu veriyor
	bool arama(int,int);								//listede eleman ariyor
///////////////////////////////////////////////////
/*         DIGER FONKSIYON PROTOTIPLERI          */
///////////////////////////////////////////////////
	void degeryaz(int **);                             	//ekrana labirenti ciziyor
	void diziyap();                                    	//dinamik dizi olusturuyor
	void duzenle();                                    	//bos labirent olusturuyor
	void kontrol(int,int);                             	//kapali alan kontrolu yapiyor
	void ilerle(int ,int);                             	//duvar olusturuyor
	int rasgele(int);                                  	//random sayi uretiyor
	void devam(int, int);                              	//adim sayisini tutuyor
	void ayikla();                                     	//gereksiz dugumleri ayikliyor
	void labirent();                                   	//Genel fonksiyon
	void yonbul(int , int );                           	//cikis yolunu buluyor
	int adim_sayisi();									//cikisa kac adim var
///////////////////////////////////////////////////
/*       KULLANACAGIM DEGISKENLER, GLOBAL        */
///////////////////////////////////////////////////
	int **dizi,**dizii,x,y,val1,val2,yon,adim=0,varmi=0;
/*/////////////////////////////////////////////////////
//dizi=&gt;Labirenti tutuyor                            //
//x,y=&gt; labirent boyutlari                           //
//val1,val2=&gt;Liste degerlerini almak icin kullandim  //
//yon=&gt;gidilecek yonu tutuyor                        //
//adim=&gt;kac adim gidildigini tutuyor                 //
//varmi=&gt;labirent olup olmadigini tutuyor            //
*//////////////////////////////////////////////////////

	struct List *l1;

//###############################################//
/*               MAIN FONKSIYONU                 */
//###############################################//

main(){

	l1=liste_yarat(l1);                // Listemi yaratyiyorum
	char ch='1';                      // Kullanici arayuzu
	while(ch!='2')   {
		cout&lt;&lt;endl&lt;&lt;
		"0-Ekrani temizle"&lt;&lt;endl&lt;&lt;
		"1-Yeni labirent Olustur"&lt;&lt;endl&lt;&lt;
		"2-Programdan Cik"&lt;&lt;endl;
		if(varmi==1){
			cout&lt;&lt;"3-Labirenti Coz"&lt;&lt;endl;
		}
		ch=getch();
		if(ch=='1'){
			clrscr();labirent();yonbul(1,1);varmi=1; 
		}
		else if (ch=='2'){
			clrscr();
			cout&lt;&lt;endl&lt;&lt;
			"Veri Yaplilari Labirent Olusturma Odevi\nYazan:Ahmet KAKICI - 150165\nCikmak icin herhangi bir tusa basiniz.";
			getch();
		}
		else if(ch=='3'){
			clrscr();
			degeryaz(dizi);
			cout&lt;&lt;endl;
			degeryaz(dizii);
			cout&lt;&lt;"Labirentten "&lt;&lt;adim_sayisi()&lt;&lt;" adimda cikildi."&lt;&lt;endl;
			varmi=0;
		}
		else if(ch=='0'){
			clrscr();
		}
	}
}


//////////////////////////////////////////////////
/*  SELF AVOIDING WALK ve LABIRENTTEN CIKIS     */
//////////////////////////////////////////////////

void yonbul(int a, int b){

	int xMax=x-1,yMax=y-1;
	if(a==x-2 && b==y-2){
		for(int i=0;i&lt;x;i++)
		for(int j=0;j&lt;y;j++)
		dizii[i][j]=dizi[i][j];
		return;
	}

	if(b+2&lt;yMax && dizi[a][b+1]==pasifDUVAR && dizi[a][b+2]==YOL){
		dizi[a][b+2]=YOL2;
		yonbul(a,b+2);
		dizi[a][b+2]=YOL;
	}
	if(a-2&gt;0 && dizi[a-1][b]==pasifDUVAR && dizi[a-2][b]==YOL){
		dizi[a-2][b]=YOL2;
		yonbul(a-2,b);
		dizi[a-2][b]=YOL;
	}
	if(b-2&gt;1 && dizi[a][b-1]==pasifDUVAR && dizi[a][b-2]==YOL){
		dizi[a][b-2]=YOL2;
		yonbul(a,b-2);
		dizi[a][b-2]=YOL;
	}
	if(a+2&lt;xMax && dizi[a+1][b]==pasifDUVAR && dizi[a+2][b]==YOL){
		dizi[a+2][b]=YOL2;
		yonbul(a+2,b);
		dizi[a+2][b]=YOL;
	}
}
///////////////////////////////////////////////////
/*      LABIRENT OLUSTURMA FONKSIYONU            */
///////////////////////////////////////////////////
void labirent(){
	srand(time(NULL));
	cout&lt;&lt;endl&lt;&lt;"Labirent boyutlarini gir"&lt;&lt;endl&lt;&lt;"x=";
	cin&gt;&gt;x;
	cout&lt;&lt;endl&lt;&lt;"y=";
	cin&gt;&gt;y;
	diziyap();
	duzenle();

	while((uzunluk(l1))&gt;0){
		liste_gez(l1,rasgele(uzunluk(l1)),val1,val2);
		ilerle(val1,val2);
		ayikla();
	}
	degeryaz(dizi);
}
///////////////////////////////////////////////////
/*          DIZI OLUSTURMA FONKSIYONU            */
///////////////////////////////////////////////////
void diziyap()
{
	x=x*2+1;
	y=y*2+1;
	dizi=new int *[x];
	dizii=new int *[x];
	for(int i=0;i&lt;x;i++){
		dizi[i]=new int[y];
		dizii[i]=new int[y];
	}
}
///////////////////////////////////////////////////
/*       RASGELE SAYI URETEN FONKSIYON           */
///////////////////////////////////////////////////
int rasgele(int n)
{
	return rand()%n;
}
///////////////////////////////////////////////////
/*       ADIM SAYISINI TUTAN FONKSIYON           */
///////////////////////////////////////////////////
int adim_sayisi()
{
	int adimSayisi=0;
	for(int i=0;i&lt;x;i++){
		for(int j=0;j&lt;y;j++){
			if(dizii[i][j]==YOL2){
				adimSayisi++;
			}
		}
	}
	return adimSayisi;
}
///////////////////////////////////////////////////
/*   DIZI DEGERLERINI YAZAN FONKSIYON            */
///////////////////////////////////////////////////
void degeryaz(int **dizim){
	for(int i=0;i&lt;x;i++){
		for(int j=0;j&lt;y;j++){
			if(dizim[i][j]==DUVAR)
			cout&lt;&lt;'\xDB'&lt;&lt;'\xDB';
			else if(dizim[i][j]==YOL)
			cout&lt;&lt;" "&lt;&lt;" ";
			else if(dizim[i][j]==YOL2)
			cout&lt;&lt;"_"&lt;&lt;"_";
			else if (dizim[i][j]==pasifDUGUM)
			cout&lt;&lt;'\xDB'&lt;&lt;'\xDB';
			else if (dizim[i][j]==eskiDUGUM ||dizim[i][j]==GEREKSIZ || dizim[i][j]==-2 )
			cout&lt;&lt;'\xDB'&lt;&lt;'\xDB';
			else cout&lt;&lt;' '&lt;&lt;" ";
		}
		cout&lt;&lt;endl;
	}
}
///////////////////////////////////////////////////
/*      LABIRENTIN BOS HALINI OLUSTURUYOR        */
/*     ILK DUGUM NOKTALARINI LISTEYE ATIYOR      */
///////////////////////////////////////////////////
void duzenle(){
	int xx,yy;
	xx=x-1;
	yy=y-1;
	for(int i=0;i&lt;x;i++){
		for(int j=0;j&lt;y;j++){
			if( i==0 || j==0 || i==xx || j==yy)
				dizi[i][j]=GEREKSIZ;          			//KENARLARDAKI GEREKSIZ YERLER
			if(  (  (j==0 ||j==yy) && j%2==0)|| ( (i==0||i==xx) && i%2==0) ){
				dizi[i][j]=DUGUM;    					//LABIRENTIN KENARLARINI
				listeye_ekle(l1,i,j);     				//LISTEYE EKLE
			}
			else if (i%2!=0 && j%2!=0){     			//GIDILECEK YOLLAR
				dizi[i][j]=YOL;
			}
			else if( ((i%2!=0 && j!=0 && j!=yy) &&  j%2==0)||(i%2==0 && (i!=0 && i!=xx &&  j%2!=0)) ){
				dizi[i][j]=pasifDUVAR;            		//PASIF DUVARLAR
			}
			else if(i%2==0 && j%2==0){
				dizi[i][j]=pasifDUGUM;           		//PASIF DUGUMLER
			}
			//else dizi[i][j]=8;
		}
	}
	//LABIRENTIN KOSELERINDEKI DUGUMLERI LISTEDEN SIL
	listeden_sil(l1,0,0);dizi[0][0]=eskiDUGUM;
	listeden_sil(l1,xx,0);dizi[xx][0]=eskiDUGUM;
	listeden_sil(l1,0,yy);dizi[0][yy]=eskiDUGUM;
	listeden_sil(l1,xx,yy);dizi[xx][yy]=eskiDUGUM;
}
///////////////////////////////////////////////////
/*  LABIRENTTE DUVAR OREREK ILERLEME FONKSIYONU  */
///////////////////////////////////////////////////
void ilerle(int Xnokta,int Ynokta){
	yon=rasgele(4);
	int a=Xnokta;
	int b=Ynokta;

	if(Xnokta==0)yon=3;
	if(Ynokta==0)yon=1;
	if(Xnokta==x-1)yon=0;
	if(Ynokta==y-1)yon=2;
    //liste_goster(l1);

	// Kuzey =&gt; 0 , dogu =&gt;1 , bati=&gt;2 , guney=&gt; 3,
	if(yon==0){             //KUZEY
		if(a-2&gt;0){
			if(dizi[a-2][b]==pasifDUGUM){
				dizi[a-1][b]=DUVAR;
				kontrol(a-2,b);
				kontrol(a,b);
				devam(a-2,b);
			}             
		}
	}

	if(yon==1){         // DOGU
		if(b+2&lt;y){
			if(dizi[a][b+2]==pasifDUGUM){
				dizi[a][b+1]=DUVAR;
				kontrol(a,b+2);
				kontrol(a,b);
				devam(a,b+2);
			}
		}
	}
	if(yon==2){        // BATI
		if(b-2&lt;0){
			if(dizi[a][b-2]==pasifDUGUM){
				dizi[a][b-1]=DUVAR;
				kontrol(a,b-2);
				kontrol(a,b);
				devam(a,b-2);
			}
		}
	}
	if(yon==3){             // GUNEY
		if(a+2&lt;x){
			if(dizi[a+2][b]==pasifDUGUM){
					dizi[a+1][b]=DUVAR;
					kontrol(a+2,b);
					kontrol(a,b);
					devam(a+2,b);
			}               
		}
	}

}  //gezi func. sonu

void devam(int Xnokta,int Ynokta)
{
	if(adim&lt;STEP){
		adim++;
		ilerle(Xnokta,Ynokta);
    }
	else{
		adim = 0;
	}
}
 ///////////////////////////////////////////////////
/*                   AYIKLA  FONKSIYONU          */
//////////////////////////////////////////////////
void ayikla(){
	for (int i=0;i&lt;uzunluk(l1);i++){
		liste_gez(l1,i,val1,val2);
		kontrol(val1,val2); 
	}
}
////////////////////////////////////////////////////
/*                KONTROL  FONKSIYONU            */
//////////////////////////////////////////////////
void kontrol(int Xnokta,int Ynokta)
{
	int cevre = 0;

	if(Ynokta+2&lt;y){
		if(dizi[Xnokta][Ynokta+2]==pasifDUGUM ){
			cevre++;
		}
	}
	if(Ynokta-2&gt;0){
		if(dizi[Xnokta][Ynokta-2]==pasifDUGUM ){
			cevre++;
		}
	}
	if(Xnokta+2&lt;x){
		if(dizi[Xnokta+2][Ynokta]==pasifDUGUM ){
			cevre++;          
		}
	}
	if(Xnokta-2&gt;0){
		if( dizi[Xnokta-2][Ynokta]==pasifDUGUM){
			cevre++;
		}
	}
	if (cevre==0){
		dizi[Xnokta][Ynokta]=eskiDUGUM;
		listeden_sil(l1,Xnokta,Ynokta);
	}
	else if( cevre!=0 && (dizi[Xnokta][Ynokta]!=DUGUM)){
		if(!(arama(Xnokta,Ynokta))){
			listeye_ekle(l1,Xnokta,Ynokta);
		}
		dizi[Xnokta][Ynokta]=DUGUM;
	}
}
 ///////////////////////////////////////////////////
/*             LISTE FONKSIYONLARI                */
///////////////////////////////////////////////////

///////////////////////////////////////////////////
/*           LISTE YARATMA FONKSIYONU           */
//////////////////////////////////////////////////
struct List *liste_yarat(struct List *pl){
	pl=(struct List *)malloc(sizeof(struct List));
	pl-&gt;list=0;
	return pl;
}
///////////////////////////////////////////////////
/*      LISTE UZUNLUGUNU BULAN FONKSIYON         */
///////////////////////////////////////////////////
int uzunluk(struct List *pl){
	struct Item *tmp=pl-&gt;list;
	int uzun=0;
	while(tmp){
		uzun++;
		tmp=tmp-&gt;next;
	}
	return(uzun);
}
///////////////////////////////////////////////////
/*      LISTEDEN ELEMAN SILEN FONKSIYON          */
///////////////////////////////////////////////////
void listeden_sil(struct List *pl,int val1,int val2){
	struct Item *prv, *pt = pl-&gt;list;
	if ( (pt) && (pt-&gt;val1==val1)&&(pt-&gt;val2==val2)  ){
		pl-&gt;list= pt-&gt;next;
		free(pt);
	}
	else if (pt){
		for ( prv=pt, pt= pt-&gt;next;
			  ((pt) && ((pt-&gt;val1 != val1) || (pt-&gt;val2 != val2)));
			  prv=prv-&gt;next, pt=pt-&gt;next);
		if ( (pt)&& (pt-&gt;val1==val1) && (pt-&gt;val2==val2) ){
			prv-&gt;next=pt-&gt;next;
			free(pt);
		}
	}
}
///////////////////////////////////////////////////
/*    LISTE ELEMANLARINI YAZDIRAN FONKSIYON      */
///////////////////////////////////////////////////
void liste_goster(struct List *pl){
	struct Item *tmp=pl-&gt;list;
	while (tmp){
		printf("%d ", tmp-&gt;val1) ;
		printf("%d \n", tmp-&gt;val2) ;
		tmp=tmp-&gt;next;
	}
}
///////////////////////////////////////////////////
/*  LISTE BASINA ELEMAN EKLEYEN FONKSIYON        */
///////////////////////////////////////////////////
void listeye_ekle(struct List *pl,int val1, int val2) {
	struct Item *pt=(struct Item *)malloc(sizeof(struct Item));
	pt-&gt;val1=val1;
	pt-&gt;val2=val2;
	pt-&gt;next=pl-&gt;list;
	pl-&gt;list=pt;
}
///////////////////////////////////////////////////
/*    LISTEDEN n. ELEMANI ALMA FONKSIYONU        */
///////////////////////////////////////////////////
void liste_gez(struct List *pl,int n,int &val1, int &val2){
	struct Item *tmp=pl-&gt;list;
	while(n--&gt;0){
		tmp=tmp-&gt;next;
	}
	val1=tmp-&gt;val1;
	val2=tmp-&gt;val2;
}
bool arama(int xVal,int yVal){
	struct Item *tmp=l1-&gt;list;
	int uzun=uzunluk(l1);
	while(uzun--&gt;0){
		if(tmp-&gt;val1==xVal && tmp-&gt;val2==yVal){
			return true;
		}
		tmp=tmp-&gt;next;
	}
	return false;
}
</pre>