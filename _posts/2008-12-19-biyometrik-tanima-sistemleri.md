---
title: Biyometrik Tanıma Sistemleri
author: Ahmet Kakıcı
layout: post
permalink: /genel/biyometrik-tanima-sistemleri/
views:
  - 15204
syntaxhighlighter_encoded:
  - 1
categories:
  - Genel
tags:
  - biyometri
  - görüntü işleme
  - image processing
---
Biyometri konusunun gitgide yaygınlaştığı günlerde bu konuda araştırma yapacaklara özel, hazır araştırılmışı var diyorum ve yazıma geçiyorum.

**Biyometri Nedir?**

Biyometri insanları birbirinden ayırt edebilecek fiziksel özelliklerini ve sergiledikleri davranışları inceleyen bilim dalıdır.  İnsanları birbirinden ayırt edebilme şansını bize sunduğundan dolayı biyometri bir kimlik doğrulama sistemi olarakta kullanılmaktadır. Biyometrik tanıma sistemleri bir bireyin gerçekten ‘kim’ olduğunu kanıtlamasına olanak sağlar.

<!--more-->

  
İnsanların bunu yapması için ek olarak bir kart, cihaz, kimlik taşımamaları ve şifre gibi ezbere dayalı bilgileri kafalarında tutmamaları ise bu biyometrik tanımanın önemli avantajlarındandır. Unutulması veya başkası tarafından kullanılması söz konusu olmayan bir kimlik onaylama yoludur. Bu sayede kimlik, pasaport, ehliyet gibi kartların yerini tamamen alacak bir sistem geliştirilebilir. Hem daha güvenli hemde aşılması zor sistemler gün geçtikçe orataya çıkacaktır. Örneğin üniversitemizin giriş kapısında bulunan kapılarda manyetik kartlar yerine araç sürücüsünü tanıyarak girişne izin veren bir sistemin kullanılması çok daha güvenli ve mantıklı olacaktır. Bu sayede yetki verilen kişi başka araçla da giriş yapabildiği gibi, yetkisiz bir kişi herhangi bir kartla giriş yapamayacaktır.

Biyometrik tanımada kullanılacak birden fazla yöntem vardır. Gereksinimlere göre bu yöntemlerden biri veya birkaçı kullanılabilir. Birden fazla yöntemi bir arada kullanmak sonuçları kesinleştirmek için gerekli olabilir. Bu yöntemler her zaman doğru sonuçları vermeyebilir, bundan dolayı kullanım alanına göre yüksek başarı sağlayanlar seçilmelidir. Başarı oranının yanı sıra tanıma işleminin gerçekleşmesi için gereken sürede yöntemlerin seçilmesinde dikkate alınmalıdır. Gerçek zamanlı (real-time) tespit yapmak gerektiğinde yöntem seçimine çok daha fazla dikkat edilmelidir.

Genel olarak bu sistemlerin çalışma prensibi; her yöntemin kendine ait girdi cihazıyla alınan verilerin analiz edilip daha önceden girilmiş değerlerle karşılarşıtırılıp eşleştirilmesine dayanmaktadır. Bilgisayarların birim zamanda yaptığı işlem sayısının sürekli artması  göz önüne alındığında eldeki veriler ile anlık olarak alınan örneğin karşılaştırılma hızı da gittikçe artmaktadır. Saniyeler içinde yüzbinlerce veriyi karşılaştırıp doğru sonuçları veren sistemler günümüzde çeşitli alanlarda kullanılmaktadır.

**Biyometrinin Tarihi**  
İnsanoğlu biyometrik tanımayı doğduğu andan itibaren yapmaya başlar. Yeni doğan bebekeler gerek annesini gerek çevresindeki diğer kişi ve cisimleri sıfırdan başlayarak öğrenir. Bu öğrenme işlemini veritabanına ilk bilgilerin girilmesi olarak düşünebiliriz. Yeni doğan bebekler örneğine dönersek bu bebekler daha sonradan gördüğü, duyduğu yani duyu organlarıyla algıladığı her şeyi önceki veriler ile karşılaştırıp belirli sonuçlar elde ederek tanıma işlemini yapar. Örneğin annesini sesinden ve kokusundan rahatlıkla tanıyabilir. Beynimiz bu tanıma işlemlerini otomatik olarak yapmaya başlar ve genellikle mükemmele yakın başarı sağlar.

Beynimiz tarafından otomatik olarak yaptığımız bu tanımanın yanı sıra sistematik olarak yapılan tanımanın ilk örnekleri insanoğlunun tarihi kadar eski değildir. Binlerce yıl önce yaşamış insanların birbirlerini göz rengi, ten rengi, boy gibi kolaylıkla ölçülen özelliklerle kesin olarak ayırt ettikleri konuyla ilgili kaynaklarda belirtilmektedir.

Birçok yeni teknolojinin geliştirilmesinde olduğu gibi biyometrinin de gelişiminde güvenlik unsuru öncülük etmiştir. Biyometrik tanıma birçoğumuzun filmlerden aşina olduğu parmak izinden suçluyu tespit etme gibi yöntemlerle hala kullanılmaktadır. Hızla gelişen teknoloji sayesinde parmak izinin yanı sıra günümüzde bir çok yöntem ile bu tip suçlu tespiti yapılmaktadır. Bunların en bilindik olanlarından biriyse DNA testidir. İnsanların DNA’larının birbirinden farklı olduğu dış görünüşümüne de yansıdığı gibi belirgin bir şekilde ortadadır. Tek yumurta ikizleri haricinde (tek yumurta ikizlerinin parmak izleri birbirinden farklıdır) bir insanın başka bir insanla aynı DNA’ya sahip olmadığından dolayı günümüzde bu testlerde geçerliliğini korumaktadır.

**Başlıca Biyometrik Yöntemler ve Çalışma Prensipleri**

Biyometrik yöntemlerin genel çalışma prensibi iki adımdan oluşmaktadır. Birinci adımda tanınacak kişinin ilgili yönteme ait bilgiler gerekli araçlar vasıtasıyla bilgisayar ortamına aktarılıyor. Bu bilgiler yine yönteme özel algoritmalar sayesinde analiz ediliyor ve kişiyi tanımlayacak parametreler bu bilgiler içinden seçilerek veritabanına kayıt ediliyor. İkinci adım ise kişinin kimlik doğrulama isteğidir. Bu adımda sisteme aynı araçlar vasıtasyıla girilen bilgiler genellikle kayıt sisteminde uygulanan aynı algoritmayla analiz edilip veritabanındaki bilgilerle karşılaştırılıp eşleştirmelere bakılıyor. Eğer eşleşme varsa kişinin kimliği onaylanmıştır aksi halde sistemde bir sorun yoksa kişi iddia ettiği kimliğe sahip değildir.

Yukarıda geçen birinci adımında gerekli olan algoritmalar yöntemler arasında büyük farklılıklar göstermektedir. Örneğin ses ve parmak izi tanıma arasında bilgiyi dijital ortama aktaran araçlardan bu bilginin analizinde kullanılan algoritmaya kadar çoğu araç ve yazılım farklıdır. Ancak sisteme alınan bilgilerin işlenişi çoğunda ortaktır. Hangi yöntemde olursa olsun analogdan dijitale çevirilen veri içinden belirli özellikler seçilir. Bu özellik seçimi sonucunda ortaya çıkan veriler bizim karşılaştırma ve kayıt fonksiyonlarına vereceğimiz parametrelerdir. Bu parametrelerin sayısı arttıkça tanıma işleminin doğruluğu artar. Ancak doğru orantılı bir artış söz konusu değildir. Belirli bir limitten sonra parametre sayısının arttırılması sadece sisteme ek yük getirecektir ve tanıımanın doğruluğu üzerinde bir etki etmeyecektir.    Örneğin bir kişiyi tanımak için sadece boyunu parametre olarak alırsak aynı boyda iki insanı ayırt edemeyiz. Bunun yanı sıra eğer kişilerin kilolarını da parametre alırsak başarı oranımız artar.  Kişinin vücudundaki bütün ölçüleri almanın bir anlamının olmayacağı ortadadır.

Biyometrik tanıma işlemindeki bu iki adıma dört ayrı katman olarak bakabiliriz:

  * Yönteme ait cihazlar ile analog ortamdan dijital ortama veri aktarımı

  * Dijital ortamda aktarılan verilerden gerekli parametrelerin çıkarılması

  * Bu parametrelerin önceki verilerle karşılaştırılması

  * Karşılaştırma işleminin yapılması için gerekli olan verileri tutacak veritabanı

Analog ortamdan dijital ortama veri aktarımı sırasında kayıt esnasındaki ortamın **tamamen** aynısını oluşturmak çok zordur. Bundan dolayı çıkarılacak parametrelerin çevre koşullarının değişimine karşı sabit kalması veya sonucu etkilemeyecek kadar az değişmesine dikkat edilmelidir.

Örneğin bir ses tanıma sisteminde kayıt esnasında kişi mikrofona konuştuğu zaman çevredeki seslerde kayıt altına alınacaktır. Kimlik doğrulama için aynı kişi tekrar mikrofona konuştuğunda ise çevredeki seslerin (gürültülerin) aynı olamaz. Bundan dolayı tanıma işleminde kullanılacak parametreler özenle seçilmelidir.

Bu tip yanlış algılama olasılıklarının olduğu biyometrik tanıma yöntemlerinin kıyaslanması için aşağıdaki terimler ileri sürülmüştür:

  * **False Accept Rate (FAR) **: Sistemin veritabanında bulunmayan bir kişiye ait bilgileri yanlış analiz etmesinden ve veritabanında bulunan biriyle eşleştirmesinden kaynaklanan yanlış tespitlerin oranıdır.

  * **False Reject Rate (FRR)** : Sistemin veritabanında varolan kişileri sonraki bir tarama sonucunda bulamamasının oranıdır.

Bu iki orana bakılarak tanıma yöntemleri birbirleriyle kıyaslanabilir.

**i.    Parmak İzi Tanıma**

**Tarihçe:**  
Parmak izinin oldukça eski bir tarihi vardır. Nehemiah Grew (1684), Marcello Malpighi (1686)  ve  J. E. Purkinje (1823)  adlı bilimadamları parmak izlerinin birtakım özellikler barındırdığına dikkat çekmiş olmalarına rağmen bu özelliklerin kişi tespitinde kullanacak kadar benzersiz olduğunu ortaya sürecek herhangi bir çalışma yapmamışlardır.

Günümzüde kullanılan yöntemlerin temeli olarak kullanılan parmak izi tanıma sistemlerinin temeli ise Henry Faulds ve Wiliam James Herschel adında iki İngilizin bilimadamının çalışmalarıyla başlamıştır. Bu iki bilimadamı kişilerin parmak izlerini alma yöntemleri üzerine çalışmışlar ve temel olarak mürekkep kullanımının üzerine gitmişlerdir.

Sir Francis Galton (1822-1911)  istatistik üzerine yaptığı çalışmalar soncunda iki bağımsız değişken arasındaki doğrusal ilişkinin yönünün ve kuvvetini belirten korelasyon (correlation) yöntemini ileri sürmüştür. Bu sayede iki örüntü (pattern) arasında karşılaştırma yapacak bir yöntem elde etmiştir. Çalışmalarının devamında insanların parmak izleri arasındaki farkı sınıflandırıp ayırt edecek yöntemler ortaya çıkarmıştır. Galton parmak izinin kalıtımsal olmadığını ve her insanın parmak izinin birbirinden farklı olacağını çalışmalarıyla ortaya çıkarmıştır.

Galton’un çalışmalarını takiben Dr Henry Faulds (1983-1930) parmak izinin sınıflandırılmasına tam olarak açıklık getirmiştir. Farklı sınıflandırmala olsa bile Galnton ve Henry’nin yaptığı çalışmaların ürünü olan sınıflandırma sistemi yaygın olarak kullanılmaktadır.

Günümüzdeki sistemlerde bu sınıflandırma genelde iki parmaktan alınan örnekler üzerinde gerçekleştirilmektedir. Tek parmaktan alınan bilgi ile de aynı işlem yapılabilir olmasına rağmen güvenlik ve stabil çalışma açısından en az iki parmak izi alınmaktadır. 25 Haziran 2007’de ABD’de sınır kapılarında bundan sonra iki değil on parmak izinin birden alınacağı bir sisteme geçileceğini açıklamıştır.

Ülkemizde parmak izinin incelenilmesi ve biyometrik tanıma olarak kullanılması 1910 yılında Macar asıllı Yusuf Cemil tarafından başlatılmıştır. Daha sonra ise polis teşkilatı tarafından kullanılmıştır.

** Özellikleri:**  
Galton ve Henry’nin çalışmaları sonucunda ortaya çıkan sınıflar çizgilerin şekline göre ayrılmaktadır ve bu sınıflar aşağıdaki gibidir:

  * Yay (arch)
  * Döngü (loop)
  * Helezon (whorl) 

	<p style="text-align: center;">
	![Parmak İzi Türleri](/assets/images/biyometri/turler.jpg)
	</p>
<p style="text-align: center;">
  Yay (Arch)                      Döngü (Loop)               Helezon (Whorl)
</p>

Daha detaylı işlemler için bu sınıflarda alt sınılara bölünmektedir.

Bu sınıflandırmaların yanı sıra parmak izlerine çizgi bazında bakıldığında belirli özelliklere sahip noktalar ortaya çıkmaktadır.

  * Eni boyuna neredeyse eşit olan çizgiler nokta (ridge dots) olarak alandırılır
  ![Ridge dots](/assets/images/biyometri/1.jpg)

  * Noktalardan daha uzun olan ve değişken boyutlu çizgilerde vardır ve ada (island) olarak adlandırılır
  ![Island](/assets/images/biyometri/2.jpg)

  * Bir çizginin bölünüp birden çok çizgiye ayrılıdığı noktalar çatal (bifurcation) olarak adlandırılır
  ![Bifurcation](/assets/images/biyometri/3.jpg)

Karşılıklı çatal (opposed bifurcation)  
![Opposed Bifurcation](/assets/images/biyometri/4.jpg)

İkili Çatal (double bifurcation)  
![Double Bifurcation](/assets/images/biyometri/5.jpg)
Üçlü Çatal (trifurcation)
![Trifurcation](/assets/images/biyometri/6.jpg)


  * Çizgilerin bitiş noktalarıda özel olarak ele alınır  
	![Parmak İzi](/assets/images/biyometri/7.jpg)
  
  * Birden fazla çizginin kesiştiği noktalarda özel olarak ele alınır  
	![Parmak İzi](/assets/images/biyometri/8.jpg)
    
  * Bir çizginin çatallaşıp kısa bir mesafe sonra tekrar birleşmesi sonucunda oluşan kapalı yapıya göl (lake) adı verilir.  
	![Parmak İzi](/assets/images/biyometri/9.jpg)
	
  * Paralel giden iki çizgiyi birleştiren kısa çizgilere de köprü (bridge) adı verilir.  
    ![Parmak İzi](/assets/images/biyometri/10.jpg)

Parmak izi tanıma işlemi korelasyon yöntemiyle yapıldığı gibi yukarıda belirtilen özel noktaların yer ve sırasına göre de yapılabilir. İkinci işlem için graf yapısı oluşturulmalıdır. Korelasyon işleminin doğru sonuç verebilmesi yön bilgisine de bağlı olduğundan örnek alınırken buna dikkat edilmelidir.

Parmak izinden gerekli özellikleri çıkarmak için belli başlı görüntü işleme tekniklerini uygulanmaktadır.

  * Görüntünün gürültülerden arındırılması
  * Kenar algılama
  * Özelliklerin çıkarılması

Parmak izinin gürültülerden arındırılması işleminde belirli filtreler kullanılır. Median, mean ve gaussian gibi filtreler bunlardan bazılarıdır.

Kenar algılama filtreleri olarak sobel, gradient, prewitt gibi filtrelerl kullanılır.

Özellik çıkarma işlemi için kenar algılama sonucunda elde edilen görüntüde inceltme algoritmaları uygulanıp çizgiler özellik çıkarma için uygun hale getirilir. Daha sonra çizgilerin bitiş ve çatal noktaları elde edilir.

**Avantajları:**

  * Parmak izinin kolaylıkla alınabilmesi.
  * İkizlerde bile farklılık gösterir.
  * Parmak izinin değiştirilip bir başka parmak izine benzetilmesi zordur
  * Belirli özelliklerinin çıkarılıp sadece bu özelliklerin saklanması sayesinde hızlı arama yapılabilir.

**Dezavantajları:**

  * Örnek alınan parmağın yıpranması sonucu aynı izin tekrar elde edilemeyebilir.
  * Kişinin kilo alması gibi fiziksel değişimlerden parmağında etkilenmesi ve parmak izinin eskisiyle örtüşmeyecek hale gelmesi mümkündür.
  * Parmak izinin kalıbının kendisi yerine kullanılma ihtimali vardır.

**ii.    Yüz Tanıma**  

**Tarihçe:**  
İnsan yüzü parmakta olduğu gibi özelliklerinin kolay çıkarılabileceği bir yapıya sahip olmadığınadan yüz tanımanın gelişimi ve kullanımı parmak izinde olduğu kadar eskiye dayanmamaktadır. Yüzümüzün içerdiği özelliklerin fazlalığı bu özellikleri kullanacak yöntemlerin sayısını da arttırmıştır. Değişik özellikleri kullanan değişik yöntemler ortaya çıkmıştır. Bunlardan ilki sayılabilecek yöntem ‘eigenfaces’ Matthew Turk ve Alex Pentland 1987 yılında ortaya atılmıştır. Yüz tanımada kullanılan başlıca yöntemler aşağıdaki gibidir:

  * PCA
  * ICA
  * LDA
  * EP
  * EBGM
  * Kernel Methods
  * Trace Transform
  * AAM
  * 3-D Morphable Model
  * 3-D Face Recognition
  * Bayesian Framework
  * SVM
  * HMM
  * Boosting & Ensemble

<p style="text-align: center;">
![Eigen Face - Örnek](/assets/images/biyometri/11.jpg)
</p>

<p style="text-align: center;">
  ‘Eigenface’ örnekleri
</p>

<p style="text-align: left;">
  Yüz tanıma yöntemi kullanılarak 2000  yılında Meksika’da  yapılan seçimlerde birden fazla oy kullanılmasını engelleyecek bir sistem oluşturulmuştur. Ayrıca 2001 yılında ABD’de yapılan NFL (National Football League) finalinde 19 suçlu yakalanmıştır. ABD’de verilen ehliyet, kimlik gibi belgelerde bir kişinin farklı adlarla kayıt yaptırmaması amacıyla yüz tanıma sistemi kullanılmaktadır.
</p>

<p style="text-align: left;">
  <strong> Özellikleri:</strong><br /> Yüz tanıma yönteminde kişilerden örnek almak diğer yöntemlere göre çok daha zordur.  Sıradan bir kamera ile çevreden birçok yüz görüntüsü alınabilir. Ancak burada başka bir sorun ortaya çıkmaktadır. Kamera tarafından alınan görüntüde tamamen yüze ait bölge bulunmalıdır. Bunun için ‘Face Detection’ yani yüz bulma algoritmaları kullanılmaktadır. Yüz bölgesi bulunduktan sonra işlemeler burada devam etmektedir.
</p>

Bu adımdan sonra değişik yollar izlenerek yüz tanıma işlemi yapılabilir. Bazı yöntemler yüzde bulunan oranları karşılaştırıken bazılar YSA ile öğreterek tanıma yapmaktadır. Bu yöntemlerin çalışma şekilleri aşağıda kısaca açıklanmıştır.

<p style="text-align: left;">
  <strong>PCA </strong>yönteminde tanıma işleminin yapılabilmesi için alınan örneklerin veritabanında bulunanlar ile aynı boyutta olması gereklidir. PCA tekniği temel olarak çok boyutlu veri kümelerini analiz edilebilmesi için daha az boyutlu kümelere dönüştürür. Bu yöntemde yapılan işlem Karhunen-Loève transformu olarak da bilinmektedir. PCA yönteminde veritabanında saklanan görüntüler küçültülmüş ve sıkıştırılmış olarak saklanmaktadır. Bu sayede vertabanın yükü azaltılmış ayrıca arama hızı arttırılmıştır.<br /> <strong></strong>
</p>

**ICA**(Independent component analysis) yöntemi çok değişkenli işaretleri alt parçalara bölerek işlem yapmaya dayalı bir hesaplama metodudur.  

**LDA**(Linear Discriminant Analysis)  elde varolan sınıfların özelliklerini ölçerek yeni gelen örneklerin sınıflandırılmasını sağlayan bir yöntemdir. Sınıflar arasında farklılıklar arttırılmaya çalışılırken sınıf içindeki örneklerin arasındaki farklar azaltılmaya çalışılır. LDA sadece sınıflandırma yapmaya yarayan bir yöntemdir. Veri tipi hakkında herhangi bir bilgi vermez.

**EP**(Evolutionary Pursuit) genetik algorimtaları kullanarak sınıflandırma yapan bir yöntemdir. Karşılaştırılacak örnek sayısı (durum uzayı) çok büyük olduğu zaman genetik algoritmalara başvurmak hızlı bir çözüm elde etmemize yardımcı olmaktadır.

**EBGM** (Elestic Bunch Graph Matching) yönteminde insan yüzünü graf olarak ifade eder. Graftaki düğümler burun, göz gibi belirgin noktalardan oluşur. Kenarlar, noktalar arasındaki 2boyutlu uzaklıklar ile ağırlıklandırılır.  Her düğümde farklı faz ve genlikte oluşturulmuş 40 adet Gabor wavelet katsayısı bulunur. Bu katsayılara ‘jet’ denilmektedir. Tanıma işlemi jet’ler ve ağırlıklandırılmış kenarlar ile yapılır.  


**Trace Transform Radon** dönüşümünün genelleştirilmiş halidir. Radon dönüşümü iki boyutlu uzayda düz çizgilere uygulanan intergral dönüşümüdür. Ters radon dönüşümü ile görüntülerin tekrar oluşturulması sağlanabilir. Trace transform sayesinde cisimleri tanırken rotasyon, boyutlandırma gibi transformasyonların ektileri ortadan kaldırılır. Bu sayede farklı açılardan görüntüsü alınan cisimlerde tanınabilir.

**AAM**(Active Appearance Model) nesnelerin şekillerini istatistiksel bir modelidir ve iki resmin eşleştirilmesi için kullanılan bir hesaplama yöntemidir. Algoritma gri seviye resimler üstünde tahmin edilen nokta ile hedef nokta arasındaki farkların hesaplanmasıyla (least squares) çalışır.  
![Active Appearance Model](/assets/images/biyometri/12.jpg)

**3-D Morphable Model** yukarıda kullanılan tekniklere göre daha değişik bir yaklaşım ile yüz resimlerini 3 boyutlu olarak inceler. Örnek olarak alınan resmin çekildiği ortam ile veri tabanındakini karşılaştırırken çevre koşullarının değişimini 3 boyutlu görüntüye uyarlayarak elde ettiği sonuç ile karşılaştırma yapabilir. Bu yöntemi açıkayacan örnek programın videosunu <a href="http://www.youtube.com/watch?v=nice6NYb_WA" target="_blank">izleyebilirsiniz. </a>Verilen resimden 3boyutlu görüntüyü çıkarması ve transformasyonlardan bağımsız olması bu yöntemi güçlü kılmakla beraber uygulanmasını da bir o kadar zorlaştırmaktadır.

**3-D Face Recognition** bu yöntemin getirdiği en büyük yenilik yüz görüntüsünde kişinin doğal ifadeleriden bağımsız olarak tanıma yapabilmesidir. Öncelikle yüz bölgesi ve dokusu belirlenir.  Daha sonra bu bölge içinden gereksiz ve tanımayı zorlaştıracak bölümler (saç, vs) atılır. Bu işlemin ardından yüzün 3boyutlu gösterimi elde edilir. Bu elde edilen görüntü tanıma işlemi için kullanılmaktadır.  

**Bayesian Framework**Bayes teoremine dayanan ve olasılıksal benzerlikleri ölçen bir yöntemdir. Bu yönteme göre iki çeşit yüz görüntüsü varyasyonu vardır: intrapersonal (kişinin içinde gelişen) ve extrapersonal (kişinin dışında gelişen). Yüzler arasındaki benzerlik Bayesian kuralına göre ölçülmektedir.  


**SVM** (Support Vector Machine) yöntemi verilen noktaları destek vektörleri ile ifade eder ve aynı sınıfa ait noktaları bir bölümde tutacak bir hiperbol çizmeye çalışır. PCA yöntemiyle özellik çıkarımı yapıldıktan sonra SVM yöntemiyle görüntü ikilieri arasındaki farklar araştırılır. Yani veri tabanındaki görüntülere ait vektörler ile alınan örnek vektörleri karşılaştırılır.  SVM yöntemiyle resimde işaretlenen belirli noktaların takibi de yapılabilir. Kamera karşısında bulunan bir insanın yüzünü göz-ağız gibi bölgelere ayırarak bunların takibini yapan SVM yöntemiyle insanın ruh halini gösteren bir videoyu <a href="http://www.youtube.com/watch?v=V25qu1xpJOc" target="_blank">izleyebilirsiniz</a>.

<p style="text-align: center;">
  ![Support Vector Machine](/assets/images/biyometri/13.jpg)
</p>

<p style="text-align: center;">
  <p>
    <strong>HMM </strong>(Hidden Markov Models) bir istatsitiksel model olup bir işareti karakterize etmek için kullanılır. HMM işlemi bilinmeyen parametreleri gözlenebilir parametreler ile elde etmeye yardımcı olur. Ortaya çıkarılan model parametreler &#8216;doku eşleştirme&#8217; &#8211; &#8216;pattern matching&#8217; için kullanılır. HMM yöntemi Bayesian ağı yönteminin basit bir hali olarakta nitelendirilebilir.
  </p>
  
  <p style="text-align: center;">
  ![Hidden Markov Models](/assets/images/biyometri/14.jpg)
  </p>
  
  <p>
    <strong>Avantajları:</strong>
  </p>
  
  <ul>
    <li>
      İnsan yüzlerinin tek yumurta ikizleri haricinde birbirnden tamamen farklıdır.
    </li>
    <li>
      Parmak izindeki kadar kolay taklit edilemeyecek özellikleri barındırırır. Bundan dolayı taklit edilmesi oldukça zor bir tanıma yöntemidir.
    </li>
    <li>
      Örnek alma işleminin sadece bir kamera ile kolaylıkla yapılabilinir.
    </li>
  </ul>
  
  <p>
    <strong>Dezavantajları:</strong>
  </p>
  
  <ul>
    <li>
      Uygulanması diğer yöntemlere göre oldukça zordur.
    </li>
    <li>
      Çevre koşullarından çok fazla etkilenmesi.
    </li>
    <li>
      Kişilerin yüzündeki ufak mimiklerden bile tanımanın yanlış sonuçlar verebilme ihtimali vardır.
    </li>
    <li>
      Yüzde oluşacak bir yara ve hasarın tanımayı olumsuz etkilemesi söz konusudur.
    </li>
  </ul>
  
  <p>
    <strong>iii.    İris Tanıma</strong>
  </p>
  
  <p>
    <strong> Tarihçe:</strong><br /> 1936 yılında Frank Burch isimli göz doktoru bir bireyi tanımak için iris desenlerinin kullanılabileceği fikrini öne sürdü. 1985 yılında Dr. Leonard Flom ve Dr. Aran Safir tüm irislerin eşsiz olduğunu ispatlayarak 1987 iris tanıma ile ilgili patentlerini aldılar. Dr. Flom, Dr. John Daugman’dan iris tanımayı otomatik hale getirecek bir algoritma geliştirmesini istemiştir. 1993 yılında ABD’de Defense Nuclear Agecny bu işlemi yapacak bir prototip üstünde çalışmalara başlamıştır. 1995 yılında tamamlanan sistem Dr. Daugman’a bu dalda bir patent kazandırmıştır. 1995 yılında otomatik iris tanıma yapabilen cihazlar piyasaya çıkmaya başlamıştır.<br /> <strong></strong>
  </p>
  
  <p>
    <strong> Özellikleri:</strong>
  </p>
  
  <p>
    İris tanıma sistemleri yüz ve parmak tanımada olduğu gibi özel noktaların çıkarılmasıyla yapılamamaktadır. Daha çok ‘pattern recognition’ olarak bilinen doku arama yöntemiyle yapılır.
  </p>
  
  <p>
    İris tanımada ilk adım göz resminden iris bölgesinin bulunmasıdır. Bunun için iris şeklinden yararlanılabilineceği gibi göz bebeğinin siyah renginden de yararlanılıp histogramdan da bu bölge çıkarılabilir. Ayrıca sobel kenar algılama algoritması ile kenarlar bulunup ‘circle detection’ algoritmalarıyla da göz bebeği ve iris bulunabilir. Göz kapağının tamamen açık olmadığı durumlarla da karşılaşılabileceği için önce göz bebeği ardından irisin bulunması daha iyi sonuçlar vercektir.<br />
	![İris Tanıma](/assets/images/biyometri/15.jpg)
  </p>
  
  <p>
    İris bölgesi seçildikten sonra bu bölge üzerinden dokuya dayalı olarak özellik çıkarma işlemleri yapılır. Bu özellik çıkarma ve karşılaştırma işlemininde birden fazla yolu bulunmaktadır.
  </p>
  
  <p>
    Bu yöntemlerden biri göz bebeğinin etrafından alınan parçalar üzerinde işlem yapmaktır. Tüm iris üzerinde işlem yapılmamasının bir diğer sebebi ise göz kapağının yarı kapalı olması ve kirpiklerin irisi örtmesidir. İris üzerinden göz bebeğine bitişik yerlerden belirli sayıda parça alınarak bu karşılaştırma yapılabilir.
	![İris Tanıma](/assets/images/biyometri/16.jpg)
  </p>
  
  <p>
    Yukarıdaki şekilde olduğu gibi göz bebeğinin sağından solundan ve altından belirli sabit büyüklükte parçalar alınır. Bu parçaların büyüklüğünün her zaman eşit olduğuğunu garanti altına almak için örnek olarak alınan görüntülerin boyutları sabit olmalıdır. İşleme başlamadan önce resmi tekrar boyutlandırmak gerekebilir. Görüntüden örnek olarak alınan bu üç parça birleştirilerek bu üçlü parçaya ait co-occurance matrisi oluşturulur.
  </p>
  
  <p>
    Belli bir yönde &#8216;d&#8217;, belli bir mesafede &#8216;a&#8217; belirlenen gri seviye değerleriyle iki pikselin resim üzerinde hangi sıklıkta bulunduğunu belirten matrise co-occurance matris denir. Herhangi d ve a değerleri kullanılabilir, bu değerlerin seçimi bir kurala tabi değildir.
  </p>
  
  <p>
    Yönü belirten açı değeri 0; I, gri seviyeye sahip resmimizde mesafeyi ‘a’ olarak alırsak ; co-occurance matris de p ile simgelensin, i = I (x,y) , j = I (x+a,y) => p (i,j) değeri bir arttırılır. Bu işlem resmin tamamına uygulanır ve sonuçta co-occurance matris oluşturulmuş olur.
  </p>
  
  <p>
    Bu matris oluşturulduktan sonra yapay sinir ağlarını eğitmekte kullanılır. Daha sonra alınan örnekler üzerinde de aynı işlem yapıldıktan sonra YSA ile sınıflandırma yapılarak eşleştirme sonucu elde edilir.
  </p>
  
  <p>
    <strong> Avantajları:</strong>
  </p>
  
  <ul>
    <li>
      İris parmak veya yüz gibi vücud dışında olan bir organ olmadığından dolayı zarar görme olasılığı daha düşüktür.
    </li>
    <li>
      Parmak izi gibi yöntemlerde örnek alınırken fiziksel olarak temas olduğundan dolayı örnek alma sırasında yanlış veriler alınabilir. İris örneği alınırken ~10cm mesafeden bir resim çekilmesi yeterlidir.
    </li>
    <li>
      Tek yumurta ikizlerinde bile iris yapıları farklıdır. Yani iris dokusu tamamen kişiye özel bir yapıdadır.
    </li>
    <li>
      Doğumdan sonra oluşan iris dokusu dışardan bir etki gelmediği sürece ölene kadar değişmez.
    </li>
    <li>
      Göz, insanın ölümünden sonra en kısa sürede değişime uğrayan organlardan biridir.
    </li>
  </ul>
  
  <p>
    <strong>Dezavantajları:</strong>
  </p>
  
  <ul>
    <li>
      Tanımanın yapılabilmesi için çekilen resmin çözünürlüğünün ve kalitesinin çok iyi olması gerekir.  Aksi halde beklenen sonuçlar elde edilmeyebilir.
    </li>
    <li>
      Yüksek çözünürlüklü iris resimleri ve üzerine iris deseni basılmış lensler ile varolan sistemleri aşmak mümkün olabilir.
    </li>
  </ul>
  
  <p>
    <strong>iv.    Retina Tanıma</strong>
  </p>
  
  <p>
    Retina tanıma işlemi insanın göz bebeği arkasındaki damar tabakanın tanınmasıdır. Bu bölgedeki damarlar kişiden kişiye değişmesine rağmen damar ve göz hastalıklarından (ör:diabet) damarların etkilenmesi söz konusu olduğundan pek yaygınlaşmış bir yöntem değildir. Ayrıca örnek alma sırasında kişinin belirli bir noktaya bakması da bu işlemi zorlaştırmakta ve yöntemin az tercih edilmesine yol açmıştır.
  </p>
  
  <p>
    Retina resmi çekildikten sonra elde edilen görüntüde eşikleme yapılarak damar görüntüsü elde edilir. Bu eşikleme işlemi için gerekli olan değer dinamik olarak (genellikle otsu algoritmasıyla) elde edilir. Daha iyi sonuç almak için eşikleme işlemi ardışıl olarak yapılır ve birden çok eşik değeri alınarak adım adım damar görüntüsü elde edilir. Ortaya çıkan son görüntü üzerinde özellik çıkarma işlemleri yapılır. Buradan sonraki işlemler parmak izindeki yöntemlere benzemektedir.
  </p>
  
  <p>
    <strong>v.    Damar Tanııma</strong>
  </p>
  
  <p>
    Damar tanıma retina tanıma ile aynı algoritma ile çalışır. Ancak bu yöntemde örnekler göz arkasında bulunan damarlar yerine el üzerinde ki damarlardır.  Bu yöntemde de el resmi çekildikten sonra damar yapısı ortaya çıkarılır ve tanıma işlemi retina yönteminde olduğu gibi yapılır. Elde bulundan damarlarda kişiye özgü olduğundan dolayı geçerliliği olan bir yöntemdir. Ayrıca retina yönteminin aksine elden örnek resim alması daha kolay olmaktadır. Buna rağmen fiziksel olarak değişime ve deformasyona açık olan bir bölge olan el üstünde yara vs gibi değişimler olduğu zaman tanıma işlemi olumsuz sonuç vermektedir.
  </p>
  
  <p>
    <strong> vi.    El Yazısı Tanıma</strong>
  </p>
  
  <p>
    El yazısı tanıma işlemi ilk bakışta kesin bir sonuç vermeyeceği düşüncesi uyandırmasına rağmen tanıma işlemini başarıyla gerçekleştirmektedir. Kişilerin el yazısında kullandıları harflerin biçimleri birbirinden farklılık göstermesinin yanı sıra bu harfleri oluşturma biçimleri de dikkate alınır ve yöntemin başarı oranı arttırılır.  Harfleri oluşturma sırası, noktaları ve çizgileri çizme sırası da dikkate alınabilecek bir takım özelliklerdendir.
  </p>
  
  <p>
    Varolan bir yazıdan tanıma yapılırsa birçok özellik kaybolabilir ve taklidi muhtemel bir hale gelir. Bundan dolayı yazı yazılırken yapılan tespit hem daha doğru sonuçlar verir hemde güvenliği artırır.
  </p>
  
  <p>
    Diğer tanıma yöntemlerinde örneğin alındığı cihazın (ör:kamera) sadece o iş için üretilmemiş olması yani başka amaçlarda da kullanılmasının yanı sıra el yazsını tanımak için kullanılan cihazlar bu amaca özel hizmet eden cihazlardır. Bundan dolayı maliyeti diğer yöntemlerde kullanılan cihazlara göre daha fazla olabilir.
  </p>
  
  <p>
    <strong>Biyometrinin Geleceği</strong>
  </p>
  
  <p>
    Yakın gelecekte biyometrik kimliklerimiz bizleri yanımızda taşıdığımız kimliklerden, şifrelerden, kartlardan tamamen kurtaracaktır. Günlük hayatta birçok işlemimizi bu yöntemlerle yapabileceğiz. Örneğin kredi kartı kullanılmaya başladıktan sonra insanlar nakit para taşımak yerine bu kartları taşımaya başladılar. Daha sonraları ise kartların çalınmasıyla gerek bankalar gerek kullanıcılar birçok sorunla karşılaştılar. Eğer biyometrik tanıma yöntemleri bu alanda kullanılırsa alışveriş sonrası kasada sadece parmağımızı yada bakışımızı (iris- retina vs ) kullanarak paramızı ödeyebileceğiz.
  </p>
  
  <p>
    Bu tip sistemler insanların tamamen kayıt altına aldığı için bu tip verilerin saklandığı veritabanlarının güvenliği en üst düzeyde olmalıdır. Ayırca sahte kimlik veya kredi kartı gibi olayların da önüne geçilmesi için mükemmele yakın bir çözüm üretmektedir. Yeterince yaygın kullanıma eriştiği zaman suç oranında etkisi hissedilir şekilde düşüşler yaşanacağı kesindir.
  </p>
