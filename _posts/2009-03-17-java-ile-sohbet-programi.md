---
title: Java ile Sohbet Programı
author: Ahmet Kakıcı
layout: post
permalink: /programlama/java-ile-sohbet-programi/
views:
  - 19316
categories:
  - Programlama
tags:
  - java
  - Programlama
  - socket
  - tcp
  - udp
---
<pre><span style="font-family: Georgia, 'Times New Roman', 'Bitstream Charter', Times, serif; font-size: 13px; line-height: 19px;">Sonunda uzun zamandır ertelediğim bu yazıyı da yayınladım ve kafamdan sildim. Aşağıda göreceğiniz kodlar basit bir sohbet programının kodlarıdır. Ayırca java'da soket programlama için de bir örnek teşkil etmektedir. Programı NetBeans ile yazdım ve NetBeans tarafından otomatik olarak eklenen kodlar aşağıda yer almamaktadır.</span></pre>

Kodları ve programın işleyişini daha iyi anlayabilmeniz için bir takım terimleri ve yapıları bilmeniz gerektiğini düşünerekten öncelikle bu bilgileri verelim.

**Protokol Nedir?**

Herhangi bir ağ içerisinde bulunan cihazların birbirleriyle haberleşmeleri için bellirli protokoller tanımlanmıştır. Bu protokoller sayesinde kullanıcılar alt yapıdaki detaylarla uğraşmadan veri alışverişini gerçekletirebilir.<!--more-->

Farklı amaçlar için farklı protokoller geliştirilmiştir. Bu farklı protokollerin birbirlerine göre üstünlük ve zayıflıkları vardır. Kullanım alanına göre doğru protokol seçilmelidir.

Yaztığım programda User Datagram Protokol  &#8211; UDP protokolünü kullandım.  UDP protokolü veri iletişimini bağlantı kurmaksızın paketler gönderir. Bağlantı kurulmadığından dolayı protokolden mesajın iletildiğine dair herhangi bir bilgi edinilemez. Bu tip bir onay sistemi kullanıcı tarafından isteğe bağlı olarak ayrıca yazılmalıdır. UDP’de gönderilen paketlerin herhangi bir sıra numarası ve sırayla ulaşma garantisi de yoktur. Bu tip özellikler için ekstra başlık bigileri gerekmektedir, UDP bu başlık bilgilerini içermediğinden başlık bilgisi de diğer protokllere göre (ör:TCP) daha küçüktür. Başlık bilgilerinin küçük olması sayesinde UDP daha az bant genişliğine ihtiyaç duyar. Bu avantajından dolayı gerçek zamanlı ses veya görüntü iletişiminde tercih edilir.

**Port Nedir ?**

Portlar bir bilgisayarın ağda sahip olduğu IP adresinden dışarıya açılan birbirinden bağımsız kapılar olarak tanımlanabilir. Port numaraları 16bit ile ifade edildiğinden 65536 adet port mevcuttur. Herhangi bir uygulamanın kullanacağı port numarası seçilirken daha önceden başka bir programın bu portu kullanıp kullanmadığına dikkat edilmelidir. Aksi halde iki uygulama da düzgün çalışmayabilir.

UDP protokolünde veri iletişimi yapmak için IP ve PORT ikilisini kullanarak adresleme yapmak gerekir. Bu ikili kullanar bir soket yaratılır ve iletişim soket üzerinden yapılır.

**Soket Nedir ?**

Soket IP adresi ve Port birleşiminden oluşan uygulamalarda ağ içerisinde bulunan alt düzey ayrıntılarla uğraşmadan veri alışverişi yapmayı sağlayan ve unix sistemlerde bulunan dosya yapısına benzer bir yapıdır.  TCP/IP protokolünde mevcut olan soketler uygulama seviyesinde bağlantıları simgelemeye yarar.

Yaygın olarak kullanılan iki türlü soket yapısı mevcuttur. Bunlardan biri SOCK\_STREAM ile tanımlanan ve streaming yapmaya yarıyan soket tipidir. Bu soket yapısında bağlantılı (connection oriented) haberleşme kullanılır. Yani haberleşme sırasında aktif olan bağlantı ve soket yapısı mevcuttur. TCP protokolü SOCK\_STREAM tipinde soketler üzerinden haberleşme yapar. Bu soketlerden yapılan iletişim tamamen güvenlidir. Yani yanlış veri iletimi olması durumunda protokolden dolayı sistem kararlı ve doğru veriyi iletene kadar tekrar gönderme/isteme işlemini yapar. Ayrıca bu soketler üzerinden gönderilern verilerin alıcı tarafa da aynı sırayla ulaşacağı garanti edilmiştir. “A” ve “B” datasını içeren iki mesajı gönderdiğimizde alıcı tarafta yine “A” ve “B” sırasıyla alınacağı garanti edilmiştir.

Diğer bir soket türü ise SOCK_DGRAM ile tanımlanan datagram tipi soketlerdir. TCP’ye göre güvensiz veri iletişimi yapar. Bunun nedeni gönderilerecek datayı UDP protokolü üzerinden yollaması ve paketi bir kez ağa bıraktıktan sınra herhangi bir takip işlemi yapmamasıdır. Yani kullanıcıya verinin ulaşıp ulaşmadığına dair herhangi bir bilgi sağlamaz. Buna karşılık alıcıdan onay mesajı yollatarak iletimi biraz daha olsun kararlı hale getirebilinir. Bu soketin tercih edilme sebebi ise stream türünde yayınlardır. Her ne kadar streaming soket “streaming” için daha uygun gibi görünsede datagram tipi soketler bu iş için daha uygundur. Bunun sebebi kayıp paketlerin tekrar yollanması, aşırı başlık bilgisi, çok bant genişliği harcaması, bağlantının sürekli olarak aktif kalması gibi dezavantajlarından dolayı datagram soketler streaming işlemi için tercih edilmektedir.

**Paket Nedir ?**

UDP ile bağlantısız haberleşme yapıldığından veriler birbirinden bağımsız paketler ile gönderilir. TCP protokolünde bağlantılı haberleşme yapıldığından veri iletişimi başlarken bir bağlantı kurulur ve sürekli olarak bu bağlantı üzerinden haberleşme sağlanır. Veri iletişimi olmasa dahi bağlantı açık kalır. UDP  protokolü için Java dilinde belirlenen paket değişken tipi  Datagram Packet’dir.  Her bir paket içerisinde gönderilecek veri ve paketteki veri miktarını belirten değişkenler vardır. Bunun yanı sıra paketi gönderdiğimiz bilgisayarın IP adresi ve port numarası da pakete dahil edilmelidir.

Gönderici ve alıcı adresleri de UDP paketinin içinde olmasına rağmen bu paketler tek başına iletişim için yeterli değildir. UDP paketleri de ağda iletim için IP protokolünü kullanır. Bundan dolayı her paketin başına IP başlık bilgileri de eklenir. Aşağıdaki şekilde bir IP başlığı ve altında ise UDP paketinin temel yapısı gösterilmiştir:

[<img class="ngg-singlepic ngg-center" alt="paket.jpg" src="http://www.ahmetkakici.com/wp-content/gallery/java-sohbet/paket.jpg" />][1]{.thickbox}

[<img class="ngg-singlepic ngg-center" alt="udp.jpg" src="http://www.ahmetkakici.com/wp-content/gallery/java-sohbet/udp.jpg" />][2]{.thickbox}

**Programın Genel Yapısı**

Program sunucu/istemci mimarisine dayanarak çalışmaktadır. İstemci kısmı Applet olarak yazıldı ve web üzerinden sohbet edebilme imkanı sağlamaktadır. Sunucu kısmı ise masaüstü uygulaması olarak yazılmıştır. Sunucu çalışmaya başlar başlamaz ilgili portu dinleyerek gelen paketleri değerlendirerek mesajları istemciler arasında iletmektedir. İstemciler birbirleri arasında direk mesajlaşmak yerine sunucu üzerinden mesajlaşmaktadır. Bundan dolayı istemcilerde diğer istemcilerin adresleri yerine sadece isimleri tutulmaktadır.

**İstemci Tarafı**

İstemci kodu iki temel sınıftan oluşmaktadır. ClientMsgHandler ve ClientGUI. ClientMsgHandler veri iletim fonksiyonlarını içermektedir. ClientGUI ise arayüzü ve ClientMsgHandler’dan gelen verileri kullanıcıya göstermektedir. ClientMsgHandler thread sınıfını implement ederek oluşturulmuştur. Bu sayede arayüzde herhangi bir takılma olmadan veri iletişim işlemleri eş zamanlı olarak yapılmaktadır.

Programda iki türde istemci vardır. Birincisi sunucu üzerinde çalışan ve web üzerinden hizmet veren istemcidir. Web üzerinden sunucuya bağlanan istemciler için yazılmıştır ve sunucu adresini bilmeksizin her istemci bu sunucuya bağlanabilir. Diğer istemci türünde ise istemci kodu bilgisayara indirilip web tarayıcısı üzerinden local olarak çalıştırılabilir. Bu istemcide ise sunucunun ip adresini de ayrıca bilmek gerekmektedir.

**İstemci Tarafındaki Sınıflar ve Fonksiyonları**

**ClientMsgHandler** sınıfına ait fonksiyonlar:  
**Send:**String tipinde tutulan gönderilecek mesajı byte dizisine çevirir. Daha sonra DatagramSocket üzerinden yollamak üzere yeni bir PatagramPacket hazırlayak oluşturulan byte dizsini, alıc adresini ve iletişimde kullanılacak port numarasını da pakete ekler. Son olarak paketi DatagramSocket üzerinden gönderir.

**Recieve**: DatagramSocket üzerinden gelen paketi alabilmek için yeni bir DatagramSocket yaratır. Okunan veriyi bu pakete yazdıktan sonra mesaj kısmını byte dizisinden string tipine çevirir. Daha sonra mesajı işlemek üzere ParseMsg ve HandleMsg fonkisyonlarını çağırır.

**SetHost**: Parametre olarak host adresini alıp bu adresi InetAddress türüne çevirir.  
****

**BuildMsg**: Parametre olarak aldığı mesaj türüne göre gönderilecek mesajı string olarak oluşturur. String türündeki mesajın formatı aşağıdaki gibidir:  
gönderici\_adı  > alıcı\_adı > mesaj\_türü > mesaj\_içeriği  
Bu yapıda “>” sembolü ayraç olarak kullanılmıştır.  
Mesaj türleri ise aşağıdaki şekildedir:

**ADD_ME** – Kullanıcı ekleme  
**REMOVE_ME** – Kullanıcı silme  
**SEND_MSG** – Normal mesaj  
**GET_USERS** – Kullanıcı listesi isteği  
**ACK_MSG** – Onay mesajı

**ParseMsg**: Alınan mesajı “>” ayracına göre bölümleyerek mesajın içeriğini gerekli değişkenlere atar.

**HandleMsg**: Parse edilen mesajın türüne bağlı olarak işlemleri gerçekleştirir.  Mesaj türlerine göre yaptığı işlemler aşağıdaki gibidir:  
****

**SEND_MSG**: Gelen mesajı arayüzde göstermek üzere ClientGUI sınıfına gönderir.****

**REMOVE_ME**: Gelen kullanıcı adını ClientGUI’de gösterilen listeden silmek üzere ClientGUI sınıfına iletir. Aynı zamanda istemcilerin tutulduğu vector yapısından ilgili istemciyi silmesi için RemoveClient fonksiyonuna kullanıcı adını iletir.****

**ACK_MSG**: Bağlantının kurulduğunu onaylayan bu mesaj alındığı zaman arayüzde gerekli değişiklikler yapılarak mesaj iletimine uygun yapı oluşturulur.****

**ADD_ME**: Gelen kullanıcı adını istemcilerin tutulduğu vector yapısına ekler ve arayüz sınıfının da bu kullanıcı adını göstermesini sağlar.****

**GET_USERS**: Kullanıcı isteğinin karşılığı niteliğindedir. İlk  kez bağlantı kuruluduğunda liste alınarak arayüzde gösterilir. Aynı zamanda istemcilerin her birini vector yapısına ekler. Bu mesaj alındıktan sonra bağlantı tamamlanmış ve kullanıcı listesi alınmış olduğundan dolayı mesaj dinleme işlemini başlatacak thread çalıştırılr. Sonsuz bir döngü içinde ilgili port sürekli olarak dinlenir.

**Connect**: ClientGUI’den alınan kullanıcı adını içeren bir mesaj ile sunucuya bağlantı isteğini gönderir. Send methodunu çağırarak mesajın iletimini sağlar, daha sonra Recieve methoduyla bağlantı isteğine gelcek cevabı bekler. Cevap gelmeme ihtimaline karşı soket’in bloklanma süresi 2sn olarak ayarlanmıştır. Sunucundan cevap alınırsa veya soket süresi dolarsa bağlantı kurulamadığı ClientGUI’de gösterilir ve soket’in bloklanma süresi tekrar sıfıra setlenir (sonsuz).

**Disconnect**: Sunucuylya yapılan bağlantının bitirilmesi isteğini gönderir. Bu sayede bağlantıyı kapatan istemciler diğer istemcilerin listesinden silinecektir. UDP gibi bağlantısız bir iletişim protokolü kullanıldığından dolayı bu işlem gereklidir. Aksi halde sunucu  &#8211; istemci arasında sürekli ping gönderek her iki tarafında hala hatta olduğu kontrol edilmelidir.

**GetClientList**: Sunucu ile ilk defa bağlantı kurulduğu zaman varolan istemcilerin listesini almak için gerekli mesajı oluşturup gönderir ve cevabı alır. Kullanıcı listesi alınmadan önce ilgili port ayrı bir thread ile dinlenmediği için bu fonksiyon içinden Recieve fonkisyonu çağrılmıştır.

**BuildClientList**:  Sunucu istemciye diğer istemcilerin isim listesini gönderirken isimleri “|” ayracı ile ayırır. HandleMsg fonksiyonu bu ayraça göre gelen veriyi bölerek BuildClientList fonksiyonuna string dizisi olarak iletir. BuildClientList fonksiyonu ise gelen bu diziyi vector yapısına çevirerek kaydeder. Vector yapısı kullanılmasının amacı istemci sayısının dinamik olarak değişmesi ve ClientGUI’de ki listede istemcilerin kolaylıkla gösterilmesidir.

**RemoveClient**: Herhangi bir istemci sunucuya ayrıdığını bildirdiğinde sunucu geride kalan bütün istemcilere bu mesajı iletir ve istemciler bu fonksiyon ile ayrılan istemcinin adını vector yapısından ve ClientGUI’de kullanılan listeden siler.

**ClientGUI **sınıfına ait fonkisyonlar:

**SendMessage**: TextField2’ye girilen mesajı ve JList1’den seçilen kullanıcı adını ClientMsgHandler sınıfına göndererek mesajın sunucuya iletilmesini sağlar.

**AddMessage**: ClientMsgHandler tarafından alınan mesajları jTextArea’ya kimden geldiğini göstererek ekler.

**UpdateUserList**: Sunucuya herhangi bir istemci bağlandığında veya ayrıldığında arayüzde gösterilen istemci isimlerini yeniler.

**SetStatus**: Sunucuya bağlanıp bağlanılmadığını ve mesaj gönderirken hangi kullanıcının seçildiğini jTextFeild3’e yazdırır.

**Connect**: Bağlan butonuna basıldığı zaman kullanıcıdan alınan ip adresi (veya host adı) ve kullanıcı adıyla sunucuya bağlanmak için ClientMsgHandler’da bulunan Connect fonksiyonun çağırır.

**Destroy**: Kullanıcı tarayıcıyı kapattığı zaman sunucuya bağlantıyı sonlandırma mesajını gönderir.

**Sunucu Tarafı **

Sunucu işlemleri genel olarak istemcilerin listesini tutmak ve gelen mesajları iletmek üzerine kuruludur.  ClientHandler sınıfı sürekli olarak ilgili portu dinleyerek mesaj iletim işini üstlenmektedir. Onun haricinde serverGUI mesajlaşmaların ve sisteme gelip giden istemcilerin özetini gösteren bir arayüz oluşturmaktadır.

**ClientHandler **sınıfına ait fonksiyonlar:  
****

**BuildMsg**: Parametre olarak aldığı mesaj türüne göre gönderilecek mesajı string olarak oluşturur. String türündeki mesajın formatı aşağıdaki gibidir:  
gönderici\_adı  > alıcı\_adı > mesaj\_türü > mesaj\_içeriği  
Bu yapıda “>” sembolü ayraç olarak kullanılmıştır.  
Mesaj türleri ise aşağıdaki şekildedir:  
****

**ADD_ME** – Kullanıcı ekleme  
**REMOVE_ME** – Kullanıcı silme  
**SEND_MSG** – Normal mesaj  
**GET_USERS** – Kullanıcı listesi isteği  
**ACK_MSG** – Onay mesajı

**ParseMsg**:  Alınan mesajı “>” ayracına göre bölümleyerek mesajın içeriğini gerekli değişkenlere atar.

**HandleMsg**: Parse edilen mesajın türüne bağlı olarak işlemleri gerçekleştirir.  Mesaj türlerine göre yaptığı işlemler aşağıdaki gibidir:  
****

**SEND_MSG**: Mesaj gönderilecek istemcinin adını clients vector yapısı içinde arar. Bulduğu elemandan adresi alarak mesajı  ilgili istemciye gönderir.  Ayrıca sunucu arayüzünde de mesajı ve kimden kime gönderildiğini yazar.  
****

**REMOVE_ME**:  İstemci sunucudan ayrıldığı zaman client vector yapısı içinden bu istemciyi siler ve diğer tüm istemcilere ilgili istemci adını yollayarak listelerinden silmesini bildirir. Buna ek olarak sunucu arayüzünde de çıkan istemcinin adını yazar.

**ADD_ME**: Yeni istemcinin adını ve adresini arayüzde gösterir. Daha sonra istemcilerin tutulduğu vektöre yeni bir istemci sınıfı nesnesi yaratıp ekler. Bundan sonra ise istemciye bağlantının kabul edildiğine dair bir onay mesajı yollar. Yeni gelen kullanıcıya onay mesajı gönderip bağlantıyı kabul ettikten sonra önceden bağlanan istemcilere yeni gelen istemcinin adını gönderir.

**GET_USERS**:  Bu mesajdan sonra sunucu mesajı gönderen istemciye o anda bağlı olan istemcilerin isimlerini gönderir. İsimler birbirinden “|” ayracı ile ayrılmıştır.

**ServerSend**: Gönderilecek mesajı byte dizisine çevirerek datagram paketi içine koyar ve datagram soketi üzerinden gönderir.

**ServerRecieve**: İlgili portu dinleyerek gelen mesajları string tipine çevirir. Ayrıca gönderenin adresini de datagram paketinden çıkararak kaydeder.

**NotifyAllClients**:  Belirlenen mesajı o anda bağlı olan istemcilerin hepsine gönderir.

**BuildClientList**: Bağlı olan istemcilerin isimlerini bir string’de birleştirerek mesajı gönderilmeye hazır hale getirir.

**GetReceiverAddressByName**: Sunucuya gelen mesajlarda sadece gönderilecek istemcinin adı bulunmaktadır. Adresler ise sunucuda tutulan clients vector yapısındadır. Bu fonksiyon mesaj gönderilecek istemcinin adını vector elemanlarıyla karşılaştırıp ilgili adresi bulur.

**RemoveClient**: Parametre olarak aldığı kullanıcı adını clients vector yapısında arar ve ilgili istemciyi  vector’den siler. Daha sonra geride kalan istemcilere bu silme işlemini bildirir.

<noscript>
  <pre><code class="language-java java">/**
 *
 * @author Ahmet
 */
import java.io.*;
import java.net.*;
import java.util.*;

public class clientMsgHandler extends Thread {

    private DatagramSocket socket;
    private DatagramPacket giden;
    private DatagramPacket gelen;
    private InetAddress address;

    private int msgType;
    private String received;
    private String[] parsedMsg;
    public String myName;
    public String message;
    public String receiverName;
    public String senderName;

    private static final int PORT = 4444;
    private static final String MSG_SEPERATOR = "&gt;";
    private static final int ADD_ME = 0;
    private static final int REMOVE_ME = 1;
    private static final int SEND_MSG = 2;
    private static final int GET_USERS = 3;
    private static final int ACK_MSG = 4;
    public clientGUI parent;

    public boolean connected = false;
    public String hostname;
    public String msg2send;
    public Vector clients = new Vector();

    public clientMsgHandler(String argHostname) throws IOException {
        hostname = argHostname;
        address = InetAddress.getByName(hostname);
        socket = new DatagramSocket();
        socket.setSoTimeout(0);
    }

    @
    Override
    public void run() {
        while (true) {
            try {
                Recieve();
                socket.setSoTimeout(0);
            } catch (Exception e) {}
        }

    }
    public void SetHost(String argHostname) throws UnknownHostException {
        hostname = argHostname;
        address = InetAddress.getByName(hostname);
    }
    private void Send() {
        byte[] buf = new byte[msg2send.length()];
        buf = msg2send.getBytes();
        giden = new DatagramPacket(buf, buf.length, address, PORT);
        try {
            socket.send(giden);
        } catch (Exception e) {}
        System.out.println("Giden mesaj: " + msg2send);
    }

    public void Recieve() {
        byte[] buf = new byte[256];
        gelen = new DatagramPacket(buf, buf.length);
        try {
            socket.receive(gelen);
        } catch (Exception e) {}
        received = new String(gelen.getData(), 0, gelen.getLength());
        System.out.println("Gelen mesaj: " + received);
        ParseMsg();
        HandleMsg();
    }

    private void BuildMsg(int argFlag) {
        msg2send = myName + MSG_SEPERATOR + receiverName + MSG_SEPERATOR + argFlag + MSG_SEPERATOR + message;
    }

    public void SendMsg() {
        BuildMsg(SEND_MSG);
        Send();
    }

    public void ParseMsg() {

        try {
            parsedMsg = received.split(MSG_SEPERATOR);
            senderName = parsedMsg[0];
            msgType = Integer.parseInt(parsedMsg[1]);
            message = parsedMsg[2];
        } catch (Exception exception) {
            parent.SetStatus("Bağlantı kurulamadı.");
            msgType = -1;
            message = "";
        }
    }

    public void Connect() {
        try {
            message = myName;
            receiverName = "Server";
            BuildMsg(ADD_ME);
            Send();
            socket.setSoTimeout(2000);
            Recieve();
            socket.setSoTimeout(0);

        } catch (SocketException ex) {}
    }

    public void Disconnect() {
        receiverName = "Server";
        BuildMsg(REMOVE_ME);
        Send();
        connected = false;
    }

    public void HandleMsg() {
        if (msgType == SEND_MSG) {
            parent.AddMessage(message, senderName);
        } else if (msgType == REMOVE_ME) {
            RemoveClient(message);
            parent.UpdateUserList();
        } else if (msgType == ACK_MSG) {
            connected = true;
        } else if (msgType == ADD_ME) {
            clients.add(message);
            parent.UpdateUserList();
        } else if (msgType == GET_USERS) {
            String[] clientList = parsedMsg[2].split("\\|");
            BuildClientList(clientList);
            start();
        }
    }

    public void GetClientList() {
        message = myName;
        BuildMsg(GET_USERS);
        Send();
        Recieve();
    }

    private void BuildClientList(String[] clientList) {
        clients.removeAllElements();
        for (int i = 0; i &lt; clientList.length; i++) {
            if (!myName.equalsIgnoreCase(clientList[i].toString()))
                clients.add(clientList[i]);
        }
    }

    private void RemoveClient(String argName) {
        for (int i = 0; i &lt; clients.size(); i++) {
            String tmp = (String) clients.elementAt(i);
            if (tmp.equals(argName)) {
                clients.remove(i);
                break;
            }
        }
    }
}</code></pre>
  
  <pre><code class="language-java java">import java.io.IOException;

/*
 * clientGUI.java
 *
 * Created on 16 Nisan 2008 &Ccedil;arşamba, 21:26
 */
import java.net.UnknownHostException;
import javax.swing.JOptionPane;

/**
 *
 * @author  Ahmet
 */
public class clientGUI extends javax.swing.JApplet {

    private clientMsgHandler tr;

    private void jTextField1ActionPerformed(java.awt.event.ActionEvent evt) {
        // Kullanıcı adı girişi
        Connect();
    }

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {
        // Bağlan butonu
        Connect();
    }

    private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {
        // G&ouml;nderme işlemi
        int selected = jList1.getSelectedIndex();
        if (selected &gt; -1)
            SendMessage();
        jTextField2.requestFocusInWindow();
    }

    private void jTextField2ActionPerformed(java.awt.event.ActionEvent evt) {
        // G&ouml;nderme işlemi
        int selected = jList1.getSelectedIndex();
        if (selected &gt; -1)
            SendMessage();
    }

    private void jList1ValueChanged(javax.swing.event.ListSelectionEvent evt) {
        // Listeden kişi se&ccedil;ildiğinde:
        jTextField3.setText(jList1.getSelectedValue().toString());
        jButton2.setEnabled(true);
    }

    private void jTextField1FocusGained(java.awt.event.FocusEvent evt) {
        // Kullanıcı adı girişi
        if (jTextField1.getText().equalsIgnoreCase("Kullanıcı Adı"))
            jTextField1.setText("");
    }

    private void jTextField4FocusGained(java.awt.event.FocusEvent evt) {
        // Server IP
        if (jTextField4.getText().equalsIgnoreCase("Server IP"))
            jTextField4.setText("");
    }

    public void SendMessage() {
        tr.message = jTextField2.getText();
        tr.receiverName = jList1.getSelectedValue().toString();
        tr.SendMsg();
        AddMessage(tr.message, tr.myName);
        jTextField2.setText("");
    }

    public void AddMessage(String argMsg, String argSender) {
        jTextArea1.append("\n" + argSender + ":" + argMsg);

    }

    public void UpdateUserList() {
        jList1.removeAll();
        jList1.setListData(tr.clients);
    }

    public void Connect() {
        try {
            tr.myName = jTextField1.getText();
            tr.SetHost(jTextField4.getText());
            tr.Connect();
            if (tr.connected) {
                jList1.setVisible(true);
                jTextField2.setVisible(true);
                jButton2.setVisible(true);
                jTextField1.setEnabled(false);
                jTextField4.setEnabled(false);
                tr.GetClientList();
                jList1.setListData(tr.clients);
                jButton1.setEnabled(false);
                SetStatus("Bağlantı Kuruldu");
            }
        } catch (UnknownHostException ex) {

        }
    }

    public void SetStatus(String argMsg) {
        jTextField3.setText(argMsg);
    }
}</code></pre>
  
  <pre><code class="language-java java">class ClientHandler extends Thread {

    private static final int PORT = 4444;
    private static final int BUFFER_LENGTH = 256;
    private static final String MSG_SEPERATOR = "&gt;";

    private static final int ADD_ME = 0;
    private static final int REMOVE_ME = 1;
    private static final int SEND_MSG = 2;
    private static final int GET_USERS = 3;
    private static final int ACK_MSG = 4;

    public Vector clients = new Vector();
    protected DatagramSocket socket = null;

    String receivedMsg; // Parse edilmemis mesaj
    private String message; // Mesajin icerigi - yazi
    private int msgType; // Mesaj turu
    private String msg2send; // Gonderilecek mesaj
    private SocketAddress receiverAdress; // Mesajin gidecegi adres
    private SocketAddress senderAddress; // Mesajin geldigi adres
    private String receiverName; // Mesajin gidecegi kisi
    private String senderName; // Mesaj gonderen kisi
    public ServerGUIView parent;

    @
    Override
    public void run() {
        while (true) {
            try {
                ServerReceive();
                ParseMsg();
                HandleMsg();
            } catch (Exception e) {}

        }
    }

    public ClientHandler() throws IOException {
        super("ClientHandler");
        socket = new DatagramSocket(PORT);
    }

    public void RemoveClient(String argName) {
        for (int i = 0; i &lt; clients.size(); i++) {
            Client tmp = (Client) clients.get(i);
            if (tmp.clientName.equals(argName)) {
                clients.remove(i);
                break;
            }
        }
    }

    public void GetReceiverAddressByName() {
        for (int i = 0; i &lt; clients.size(); i++) {
            Client tmp = (Client) clients.get(i);
            if (tmp.clientName.equalsIgnoreCase(receiverName)) {
                receiverAdress = tmp.clientAddress;
                break;
            }
        }
    }
    private void BuildClientList() {
        message = "";
        for (int i = 0; i &lt; clients.size(); i++) {
            Client tmp = (Client) clients.get(i);
            message += tmp.clientName + "|";
        }

    }

    private void NotifyAllClients() {
        message = senderName;
        senderName = "Server";
        for (int i = 0; i &lt; clients.size(); i++) {
            Client tmp = (Client) clients.get(i);
            if (!tmp.clientName.equalsIgnoreCase(message)) {
                receiverAdress = tmp.clientAddress;

                ServerSend();
            }

        }
    }

    private void BuildMsg(int argFlag) {
        msg2send = senderName + MSG_SEPERATOR + argFlag + MSG_SEPERATOR + message;
    }

    public void ServerReceive() throws IOException {
        byte[] buffer = new byte[BUFFER_LENGTH];
        DatagramPacket gelenPaket = new DatagramPacket(buffer, BUFFER_LENGTH);
        try {
            socket.receive(gelenPaket);
        } catch (Exception e) {}
        receivedMsg = new String(gelenPaket.getData(), 0, gelenPaket.getLength());
        senderAddress = gelenPaket.getSocketAddress();
    }

    public void ServerSend() {
        try {
            byte[] buffer = new byte[msg2send.length()];
            buffer = msg2send.getBytes();
            DatagramPacket gidenPaket = new DatagramPacket(buffer, buffer.length, receiverAdress);
            socket.send(gidenPaket);
        } catch (Exception e) {

        }
    }

    private void ParseMsg() {
        String[] parsedMsg = receivedMsg.split(MSG_SEPERATOR);
        senderName = parsedMsg[0];
        receiverName = parsedMsg[1];
        msgType = Integer.parseInt(parsedMsg[2]);
        message = parsedMsg[3];
    }

    public void HandleMsg() throws IOException {
        if (msgType == ADD_ME) {
            parent.AddTextarea("Yeni kullanici: " + message + ", adresi:" + senderAddress + "\n");
            clients.add(new Client(message, senderAddress));
            receiverAdress = senderAddress;
            BuildMsg(ACK_MSG);
            ServerSend();
            BuildMsg(ADD_ME);
            NotifyAllClients();
        } else if (msgType == SEND_MSG) {
            GetReceiverAddressByName();
            parent.AddTextarea(senderName + " -&gt; " + receiverName + " mesaj gonderiyor :'" + message + "'\n");
            BuildMsg(SEND_MSG);
            ServerSend();
        } else if (msgType == REMOVE_ME) {
            parent.AddTextarea(senderName + ", bağlantıyı sonlandırdı.\n");
            RemoveClient(senderName);
            message = senderName;
            BuildMsg(REMOVE_ME);
            NotifyAllClients();
        } else if (msgType == GET_USERS) {
            parent.AddTextarea(senderName + " kullanicisina liste yollaniliyor.\n");
            BuildClientList();
            senderName = "Sunucu";
            receiverAdress = senderAddress;
            BuildMsg(GET_USERS);
            ServerSend();
        }
    }
}

class Client {
    String clientName;
    SocketAddress clientAddress;

    public Client(String argName, SocketAddress argAddress) {
        clientName = argName;
        clientAddress = argAddress;
    }
}</code></pre>
</noscript>

 [1]: http://www.ahmetkakici.com/wp-content/gallery/java-sohbet/paket.jpg
 [2]: http://www.ahmetkakici.com/wp-content/gallery/java-sohbet/udp.jpg