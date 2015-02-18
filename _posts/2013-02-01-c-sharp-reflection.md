---
title: 'C# ve Reflection &#8211; 1'
author: Ahmet Kakıcı
excerpt: "C#'ta Reflection temel işlemleri."
layout: post
permalink: /programlama/c-sharp-reflection/
views:
  - 3915
categories:
  - Programlama
tags:
  - c
  - csharp
  - reflection
---
C# ile yazılım geliştirmeye başladığımdan bu yana ne zaman başım sıkışsa ve daha esnek bir yapı tasarlamaya çalışsam imdadıma yetişen bir yöntem vardı: Reflection.

Reflection sayesinde çalıştığınız objelere ait verileri çalışma anında (run-time) okuyup düzenleyebilir hatta Reflection ile yine çalışma anında dinamik olarak mevcut sınıflarınızdan yeni objeler türetebilirsiniz.

Uzun uzun tanımını yapacak ve teorik bilgiye doymanızı sağlayacak bir blog yazısı yazmak yerine elimden geldiğince bol bol örnek vererek Reflection&#8217;ı iş başında görmenizi yardımcı olmaya çalışacağım.

<!--more-->

Öncelikle Console Application türünde yeni bir Visual Studio projesi açarsanız aşağıda vereceğim kodları hızlı bir şekilde deneyip sonuçları görebilirsiniz.

Reflection&#8217;ın bize sunduğu fonksiyonları üzerinde denemek üzre bir User sınıfı oluşturalım.

<pre class="brush: csharp; title: ; notranslate" title="">public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Surname { get; set; }
}
</pre>

Console Application türünde bir proje yarattıysanız Program.cs adında bir sınıf otomatik olarak projenize eklenmiş olacaktır. Bu proje içinde User sınıfından bir obje oluşturup üzerinde oynamaya başlayabiliriz.

<pre class="brush: csharp; title: ; notranslate" title="">var user = new User
    {
        Id = 1,
        Name = "Ahmet",
        Surname = "Kakıcı"
    };
</pre>

Bildiğiniz üzere C# dilinde bütün sınıflar Object sınıfından türetilmiştir. Bundan dolayı Object sınıfında olan ToString, Equals, GetType fonksiyonları diğer sınıflarda da mevcuttur. İşte bu fonksiyonlardan GetType fonksiyonu bize Reflection&#8217;ın kapılarını açmaktadır. GetType fonksiyonundan bize Type türünde bir nesne dönmekte ve bu sayede ilgili obje sınıfı üzerinde işlem yapabilmekteyiz.

Reflection ile bir nesnenin özellikleri üzerinde değişiklik yapmak istiyorsanız Type sınıfındaki GetProperties fonksionu ile ilgili nesneye ait özelliklerin bir listesini alabilirsiniz. Bu fonksiyon bize PropertyInfo tipinde bir dizi gönderecektir. Her bir dizi elemanı sınıfın içindeki bir özelliğin bilgilerini tutmaktadır. Hangi bilgilerin tutulduğunu merak ediyorsanız [PropertyInfo][1] sınıfını inceleyebilirsiniz. user nesnesindeki özellikleri aldığınızda aşağıdaki gibi bir görüntü elde edeceksiniz:

<div class="ngg-gallery-singlepic-image ngg-left" style="max-width: 298px">
  <a href="http://www.ahmetkakici.com/wp-content/gallery/reflection/1.png"
		     title=""
             data-src="http://www.ahmetkakici.com/wp-content/gallery/reflection/1.png"
             data-thumbnail="http://www.ahmetkakici.com/wp-content/gallery/reflection/thumbs/thumbs_1.png"
             data-image-id="115"
             data-title="Reflection-1"
             data-description=""
             target='_self'
             class="thickbox" rel="89b1c94a03ac705e5d7833ef519ab4d2"> <img class="ngg-singlepic"
             src="http://www.ahmetkakici.com/wp-content/gallery/reflection/dynamic/1-nggid03115-ngg0dyn-320x240x100-00f0w010c010r110f110r010t010.png"
             alt="Reflection-1"
             title="Reflection-1"
              width="298" /> </a>
</div>

<span></span> 

GetProperties fonksiyonu ilgili sınıfa ait tüm public özellikleri verecektir, bu noktada eğer bir filtreleme uygulamak istiyorsanız GetProperties fonksiyonunun [BindingFlags][2] tipinde bir parametre alan overload&#8217;u da bulunmaktadır. Bu sayede istediğiniz özellikleri filtreleyebilirsiniz. Tüm özellikleri değil de tek bir özelliği almak istiyorsanız GetProperties fonksiyonu yerine GetProperty fonksiyonuna alacağınız özelliğin adını string tipinde bir parametre ile kullanabilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">var nameProperty = user.GetType().GetProperty("Name");
</pre>

İstediğimiz özellik veya özellikleri aldığımıza göre artık bu özelliklerin değerlerini okuma ve bu değerleri güncelleme işlemlerini yapabiliriz. Bunun için PropertyInfo sınıfında bulunan [GetValue][3] ve [SetValue][4] fonksiyonlarını kullanacağız.

SetValue fonksiyonu PropertInfo üzerinden çağırıldığı için herhangi bir nesne ile birebir bağı bulunmamaktadır. Bunun için güncelleyeceğimiz özelliğin ait olduğu nesneyi SetValue fonksiyonuna parametre olarak vermemiz gerekiyor. İkinci parametrede ise özelliğe yazılacak değeri veriyoruz, son parametre ise eğer bu özellik index&#8217;li bir özellik ise ilgili özellikte bulunan index&#8217;i belirtmektedir. Bizim özelliğimiz bir string olduğu için son parametreye null veriyoruz.

<pre class="brush: csharp; title: ; notranslate" title="">var name = nameProperty.GetValue(user, null);
nameProperty.SetValue(user, "ahmeTT", null);
name = nameProperty.GetValue(user, null);
</pre>

Yukarıdaki kodu çalıştırdığınızda name değişkenine en başta nesneyi oluştururken verdiğimiz  &#8216;Ahmet&#8217; değerini atayacaktır, daha sonra SetValue ile nesneyi güncelleyip aynı özelliği okuduğumuzda ise &#8216;ahmeTT&#8217; değerini okuyacağız.

Eğer reflection ile nesnelere ait özelliklerden veri okuma ve yazma işlerini dinamik bir şekilde yapıyorsanız SetValue ve GetValue fonksiyonlarını sarmayalayacak bir fonksiyon yazıp güncelleyeceğiniz nesneyi, özellik adını ve özellik değerini parametre olarak alabilirsiniz. Bunu yaptığınız zaman parametre nesne ve özelliğe yazılacak değer için veri tipini object yaparsanız üzerinde çalıştığınız projeden olabildiğince bağımsız bir hale geleceksiniz.

<pre class="brush: csharp; title: ; notranslate" title="">public static void SetValue(object container, string propertyName, object value)
{
    container.GetType().GetProperty(propertyName).SetValue(container, value, null);
}
</pre>

Bu sayede tip ve özelliklerle birebir uğraşmadan özelliklerinize yeni değer atama işlemini kolayca yapabilirsiniz.

<pre class="brush: csharp; title: ; notranslate" title="">SetValue(user, "Name", "ahmeTT");
SetValue(user, "Name", 5);
</pre>

Yukarıdaki kodu çalıştırdığınızda ilk satırı hatasız bir şekilde çalıştırabilseniz de ikinci satırda &#8220;Object of type &#8216;System.Int32&#8242; cannot be converted to type &#8216;System.String'&#8221; şeklinde bir hata mesajı alacaksınız. Bunun sebebi bizim özelliğimizin veri tipinin String olmasına rağmen inatla içine int32 tipinde bir değer yazmaya çalışmamız. Eğer tipi farklı olsa da bu tip bir atamayı yapmak istiyorsanız elinizde özelliğe ait tip bilgisi de mevcut olduğundan dolayı aynı şekilde tip dönüşümünü de yaparak fonksiyonumuzu aşağıdaki şekilde güncelleyebilir ve GetValue için de benzer bir fonksiyon yazabiliriz:

<pre class="brush: csharp; title: ; notranslate" title="">public static void SetValue(object container, string propertyName, object value)
{
    var propertyInfo = container.GetType().GetProperty(propertyName);
    propertyInfo.SetValue(container, Convert.ChangeType(value, propertyInfo.PropertyType), null);
}

public static object GetValue(object container, string propertyName)
{
    return container.GetType().GetProperty(propertyName).GetValue(container, null);
}
</pre>

Özellikleri düzenlemenin haricinde reflection ile nesneler üzerindeki fonksiyonları çağırabiliriz. Nesneye ait olan generic tipteki fonksiyonlara bu tipleri dinamik bir şekilde vererek de çağırabiliriz. Tabii tüm bu nesneleri string olarak adından türetmemiz de mümkündür. Bunlara ek olarak Attribute sınıfını miras alıp oluşturacağımız attribute&#8217;lar ile işaretlenmiş özellikler ve sınıflar üzerinde reflection ile işlem yapma konusunda da yazacaklarım var. 

Bir sonraki yazıda görüşmek üzere.

 [1]: http://msdn.microsoft.com/en-us/library/system.reflection.propertyinfo.aspx "Property Info - MSDN "
 [2]: http://msdn.microsoft.com/en-us/library/system.reflection.bindingflags.aspx "BindingFlags - MSDN"
 [3]: http://msdn.microsoft.com/en-us/library/b05d59ty.aspx "GetValue - MSDN"
 [4]: http://msdn.microsoft.com/en-us/library/axt1ctd9.aspx "SetValue - MSDN"