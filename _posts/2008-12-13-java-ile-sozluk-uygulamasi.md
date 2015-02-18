---
title: Java ile Sözlük Uygulaması
author: Ahmet Kakıcı
layout: post
permalink: /programlama/java-ile-sozluk-uygulamasi/
views:
  - 4983
categories:
  - Programlama
tags:
  - java
  - kod
---
Çok mükemmel bir sözlük değil ama örnek olması açısından işe yarayacağını düşünüyorum. Düzenli ifadeler ile arama yapan bir sözlük denemesi hani şu yazmaya başladığınızda arama yapanlardan. Sözlük herhangi bir veri tabanı kullanmıyor sadece bir txt dosyasından okuma yapıyor. kelimeler.txt adında bir dosya oluşturup içine istediğiniz kelimeleri girebilirsiniz. Ancak formatı şu şekilde olmalıdır : İngilizce**\t**Türkçe. İngilizce kelime ardından bir tab karakteri ve sonra türkçe anlamı gelmelidir. Kendi kullandığım kelimeler.txt dosyasını da örnek olsun diye [veriyorum][1]. Dosyaya dilediğiniz gibi kelime ekleyip çıkarabilir hatta okuma kaynağını değiştirip herhangi bir sitden vs arama da yapabilirsiniz diyor ve kodu sunuyorum:

<!--more-->

<pre class="brush: java; title: ; notranslate" title="">import java.io.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import java.util.*;
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.awt.datatransfer.Clipboard;

public class SozLook extends JFrame implements ActionListener,KeyListener
{

public File dosya;					//Kelimelerin okunacağı dosya
public FileReader acilan_dosya;
public BufferedReader girdi;
public String yazilar="";			//Dosyadan okunan veriler
public int myIndex;					//TR-&gt;ING  ING-&gt;TR çevrim türünü tutuyor

public JTextField Word;				//Kelime girilen TextField
public JTextField Sonuc;			//Sonucu gösteren TextField
public JPanel myPanel1,myPanel2;

public JList list;					//Seçim listesi
public JListData ldata;

public JRadioButton trButton,ingButton;
public ButtonGroup 	myGroup;

public String urlString;
public String gelen;
public Boolean bulundu=false;
public Pattern urlPattern;
public Matcher urlMatcher;

public void init()
{
Container container = getContentPane();
container.setLayout(new BorderLayout(25,5));

myPanel1 = new JPanel();
myPanel1.setLayout(new BorderLayout(25,5));

myPanel2 = new JPanel();
myPanel2.setLayout(new FlowLayout());

Word = new JTextField(25);
Word.addKeyListener(this);

Sonuc = new JTextField(50);
Sonuc.setEditable(false);

ingButton = new JRadioButton("İngilizce -&gt; Türkçe", true);
trButton  = new JRadioButton("Türkçe -&gt; İngilizce", false);
trButton.addActionListener(this);
ingButton.addActionListener(this);

myGroup= new ButtonGroup();
myGroup.add(trButton);
myGroup.add(ingButton);

myPanel2.add(ingButton);
myPanel2.add(trButton);
myPanel1.add(Word,BorderLayout.NORTH);
myPanel1.add(Sonuc,BorderLayout.SOUTH);

JScrollPane sp = new JScrollPane();
myPanel1.add("Center", sp);

ldata = new JListData();
list= new JList(ldata); 	//data verisiyle yeni liste oluşturuyor
sp.getViewport().add(list); //scrollpane

container.add(myPanel1,BorderLayout.CENTER);
container.add(myPanel2,BorderLayout.SOUTH);

setSize(500,300);
setResizable(false);

list.addMouseListener(new MouseAdapter()
{
public void mouseReleased( MouseEvent e )
{
if(!list.isSelectionEmpty())
elemanSecildi();
}
}
);

}

public SozLook()
{
super("SözLook - KTÜ");
init();
setVisible(true);
}

public static void main(String args[])
{
new SozLook();
}

public void actionPerformed( ActionEvent actionEvent )
{
Sonuc.setText("");
ldata.temizle();
ldata.addElement("");
list.disable();
harfYazildi();
return;
}

public void keyPressed( KeyEvent event )
{
}
public void keyTyped( KeyEvent event )
{
}
public void keyReleased( KeyEvent event )
{
harfYazildi();
}

public void harfYazildi()
{
Sonuc.setText("");
if(Word.getText().toLowerCase().length()==0)
{
ldata.temizle();
ldata.addElement("");
list.disable();
return;
}

bulundu=false;
ldata.temizle();
list.enable();
list.clearSelection();

if(ingButton.isSelected())
urlString ="^"+Word.getText().toLowerCase()+"[^\t]*";
else
urlString ="\t"+Word.getText().toLowerCase()+".*$";

bul(0);
}

public void elemanSecildi()
{
if(ingButton.isSelected())
{
urlString ="^"+list.getSelectedValue().toString()+".*\t.*";
myIndex=1;
}
else
{
urlString ="^.*"+list.getSelectedValue().toString()+".*$";
myIndex=0;
}
bul(1);
}

public void bul(int tur)
{
try
{
dosya = new File( "kelimeler.txt" );
acilan_dosya = new FileReader ( dosya );
girdi = new BufferedReader ( acilan_dosya );
urlPattern = Pattern.compile(urlString);

while ( (yazilar=girdi.readLine()) != null )
{
urlMatcher = urlPattern.matcher(yazilar);
if(urlMatcher.find())
{
if(tur==0)	//harfe göre kelime aranıyor
{
bulundu=true;
ldata.addElement(urlMatcher.group());
}
else		//listeden seçilen kelimenin karşılığı aranıyor
{
String [] bulunan=urlMatcher.group().split("\t");
Sonuc.setText(bulunan[myIndex]);
break;
}
}
if(yazilar.toLowerCase().toCharArray()[0]&gt;Word.getText().toLowerCase().toCharArray()[0])
break;
}

if(tur==0 &amp;amp;amp;&amp;amp;amp; !bulundu)
{
ldata.addElement("");
list.disable();
return;
}

}
catch ( IOException exception )
{
System.out.println("Dosyadan okurken hata oluştu");
}
finally
{
try
{
girdi.close();
}
catch( IOException exception )
{
System.out.println("Dosya kapatılırken hata oluşturuldu.");
}
}

}

}

class JListData extends AbstractListModel {
private Vector dlist;

public JListData()
{
dlist = new Vector();
makeData();
}
public int getSize()
{
return dlist.size();
}
private Vector makeData()
{
dlist = new Vector();
return dlist;
}
public Object getElementAt(int index)
{
return dlist.elementAt(index);
}
public void addElement(String s)
{
dlist.addElement(s);
fireIntervalAdded(this, dlist.size()-1, dlist.size());
}
public void temizle()
{
dlist.clear();
}
}
</pre>

 [1]: http://www.ahmetkakici.com/wp-content/uploads/2008/12/kelimeler.rar