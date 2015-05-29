<h1>JQuery  Notlarım</h1>
Query notlarımı bir araya getirerek JQuery öğrenmek  ya da takıldıkları noktalarda yardım almak isteyenler için sade ve öz bir rehber olarak sunmaya çalıştım. Bu doküman için en azından temel programlama bilgisi ya da temel seviyede JavaScript bilgisi gerekebilir.
[JQuery Dökümantasyon](http://api.jquery.com/)
<h2>İçerik</h2>

 1. Elementleri Seçmek
 2. Sayfayı Manipüle Etmek
 3. Olaylar
 4. Animasyonlar
 5. AJAX
 6. Stiller


----------
<h1>1-Elementleri Seçmek</h1>

 - etikete göre seç: `$("p")` 
 - ilk paragrafı seç: `$("p:first")` 
 - id ye göre seç: `$("#id")` ya da`$("h1[id=konu1]")` 
 - haricindekileri seç: `$("h1:not(.class)")` 
 - çocuk elementleri seç (`div` in çocukları olan `p` ler): `$("div > p")`
 - elementlerden belirli class a sahip olanları seç (`p` lerden `asya`
   class ına sahip olanlar): `$("p.asya")` 
 - elementten hemen sonraki elementi seç (`h1` den hemen sonraki `p`): `$("h1 + p")` 
 - elementten sonra gelen elementleri seç (`baslik` class ından sonra gelen `p`
 - herhangi bir class a sahip olanları seç:  `$("p[class]")` 
 - belirtilen kelimeyle başlayanları seç (id si "`kon`" ile başlayanlar): `$("[id^=kon]")`
 - `p` ler içinde id si `kon` ile başlayan ve `lang` özelliği `tr-` içerenleri seç: `$("p[id^=kon][lang*=tr-]")`

**Filte** | **Özellik**
--- | ---
:first | eşleşen ilk elementi seç
:last | eşleşen son elementi seç
:even |eşleşenler arasından çift indexlileri seç
:odd | eşleşenler arasından tek indexlileri seç
:gt() | belirtilen index numarasından büyük olanları seç
:lt() | index numarasından küçük olanları seç
:eq() | index numarasına eşit olanı seç
:animated | animasyondakileri seç
:focus | o andaki odaklanılmış olan elementi seç
:not(koşul) | koşulu sağlamayanları seç
:contains('kelime') | belirtilen kelimeyi içerenleri seç
:parent | parent özelliği olan, yani en azından bir çocuk elementi bulunanları seç
:has(koşul) | koşula uyanları seç
:first-child | ilk çocuk elementi seç
:last-of-type | belirtilen element tipinden son olanı seç
:nth-child(2) | İkinci sıradakini seç 
:nth-child(2n) | 2 nin katları olanları seç
**Örnek:**
`asya` id sine sahip `div` in çocuk elementlerini seç ve arkaplanlarını sarı yap

    $("#asya").children().css("backgroundColor", "yellow")
**Örnek:**
	`next()` bir sonraki komşu elementi seçer
	`prev()` bir önceki komşu elementi seçer
	`parents()` elementin tüm parent (baba) elementlerini seçer
	`parentsUntil()` belirtilen elemente ulaşana kadarki olan parent elementleri seçer
	
    var e = $("#ad");
    e.next().css("border", "2px solid red");
    e.prev().css("border", "2px solid blue");
    e.parents().css("border", "2px solid yellow");
    e.parentsUntil($("body")).css("border", "2px solid green");

**Örnek:**

`each()` belirtilen elementin sahip olduğu her bir elementi döndürür. `index`, index numarasını, `element` DOM elementlerini belirtiyor.

    var kenarlik = 2;
    $("#ornek p").each(function(index, element){
        $(element).css("border", kenarlik + "px solid green");
        kenarlik += kenarlik;
    });

----------
<h1>2-Sayfayı Manipüle Etmek</h1>
<h2>İçeriğe Ekleme Yapmak</h2>
Fonksiyon |  Açıklama
--- | ---
`append()` | eşleşen elementin içinin sonuna ekleme yapar
`prepend()` | eşleşen elementin içinin başına ekleme yapar
`appendTo()` | `append()` ile aynı işlemi yapar. sytnax farklı
`prependTo()` | `prepend()` ile aynı. sytnax farklı
`after()` | eşleşen elementten hemen sonra ekleme yapar. (elementin dışına)
`before()` | eşleşen elementten hemen önce ekleme yapar. (elementin dışına)
`insertAfter()` | `after()` ile aynı işlemi yapar ve geriye eklenen elemanları döndürür
`insertBefore()` | `before()` ile aynı işlemi yapar 

**Örnek 1:**
	
	$("#ornek").append("metin")
    $("<p>metin</p>").appendTo("#ornek")
    
**Örnek 2:**

    var paragraf = $("<p>");
    paragraf.append("<strong>lorem ipsum</strong>")
    $("#ornek").html(paragraf)

**Örnek 3:**

    $("#ornek").html("<h2>güzel gören güzel düşünür</h2>")
`ornek` idsine sahip alan artık bundan ibaret olacaktır.

**Örnek 4:**

    $("#ornek").text("<h2>güzel gören güzel düşünür</h2>")
`text()` etiketleri dönüştürmeden, yazı olarak basar.

<h2>İçeriği Modifiye Etmek</h2>

Fonksiyon | Örnek | Açıklama 
--- | --- |---
`wrap()` | `$("#sehirler li").wrap("<div>")` | `#sehirler` içinde bulunan her bir `li` yi `<div></div>` arasına al
`wrapAll()` | `$("#sehirler li").wrapAll("<div>")` | hepsini kapsayan tek bir `<div></div>` içine al
`empty()` | `$("#sehirler").empty()` | `#sehirler` elementinin içini boşaltır
`remove()` | `$("#sehirler li.x, #sehirler li.y").remove()` | Elementi tüm ilişkileriyle beraber sayfadan kaldırır.
`detach()` | `$("#sehirler li.x, #sehirler li.y").detach()` | elementi sayfadan kaldırır ama ilişkilerini korur
`replaceAll()` | `$("<li>abc</li>").replaceAll("#sehirler li[data-type='buyuk']")` | eşleşen elementleri `<li>abc</li>` ile değiştir 
`replaceWith()`  | `$("#restaurants li[data-type='veg']").replaceWith("<li>abc</li>")` | `replaceAll()` ile aynı görevi yapar. Farklı olarak fonksiyon geçilebilir

**Örnek:**

    $("#a li[data*='b']").replaceWith(degistir);
    
    function degistir() {
      return '<li>yeni</li>';
    }

<h2>Özelliklere (attribute) Müdahele</h2>
**Örnek 1:**
Tüm linklerin title özelliğini düzenle

    $("a").attr("title", "Yeis, mâni-i herkemâldir");
**Örnek 2:**
Linkleri yeni pencere de aç

    $("a").attr("target", "_blank");
**Örnek 3:**
Linklerin referanslarını kaldır

    $("a").removeAttr("href");
**Örnek 4:**
Aynı anda birden fazla özelliğe müdahele

    $("a").attr({target: "_blank", title: "Nefsini ıslah edemeyen başkasını ıslah edemez"});

----------
<h1>3-Olaylar</h1>

	    //#ornek üzerinde imleç hareket edince mouseHareket fonk. çağır
	    $("#ornek").on("mousemove", mouseHareket);
	    
	    //#ornek üzerinde tıklama ya da imlec üzerinden ayrılınca tiklama fonk. çağır
        $("#ornek").on("click mouseleave", tiklama);
        
        //#ornek üzerinden imleç ayrılırsa fonk. çağır
        $("#ornek").on("mouseleave", function () {
            $("#ornek").text('mouse imleci burada değil');
        });
    
        function mouseHareket(olay) {
           $("#ornek").text("olay: " + olay.type + " x: " + olay.pageX + " y: " + olay.pageY);
        }
    
        function tiklama() {
	        //mousemove dinleyicisini kapat
            $("#ornek").off("mousemove", mouseHareket);
        }
Olayları dinlemek için `on()` yerine aynı görevi yapmak için hazırlanmış fonksiyonları (shortcut) da kullanabiliriz.

    $( "#ornek" ).blur(function() {
      alert( ".blur() çalıştı" );
    });
    
    $( "#ornek" ).click(function() {
      alert( ".click() çalıştı" );
    });


----------
<h1>4-Animasyonlar</h1>

    $("#ornek").animate({width: 300}, 500)
                .animate({height: 100}, 500)
                .animate({left: 100}, 300)
                .animate({borderWidth: 15}, "slow");
`animate()` fonksiyonuna ilk parametre olarak özellik ve değerleri, ikinci parametre olarak animasyonun gerçekleşeceği milisaniyeyi gönderiyoruz.


----------
<h1>5-AJAX</h1>
**Veri Çekmek**

	    $.ajax(
                'liste.txt',
                {success: calis,
                type: 'GET',
                dataType: 'text'}
        );
    
        function calis(data, status, jqxhr) {
            $("#ornek").text(data);
        }
liste.txt dosyasına GET eylemi ile ulaş ve başarılı olurse `calis` fonksiyonunu çalıştır.
**HTML Dökümanını Yükle**

    $("#ornek").load("asya.html");


----------
<h1>6-Stiller</h1>

CSS özelliklerini camelCase yazım kuralına göre adlandırmak gerekiyor.

    $("p").css("border", "2px dashed blue")
    $("p").css("backgroundColor", "yellow")
    
Fonksiyon | Açıklama
--- | --- 
`css(ozellikAdi)` | Özelliğin değerini getirir
`css(ozellik, deger)` | Özelliğe değer ver
`css(ozellik, fonksiyon)` | Özelliğe fonksiyonun döndürdüğü değere göre değer ver
`css({ozellik: deger, ozellik2: deger2})` | tek seferde çoklu değer
`hasClass(classAdi)` | classa sahip olanlar
`addClass(classAdi)` | elemente class ı ekle
`removeClass(classAdi)` | elementten classı kaldır
`toogleClass(classAdi)` | element class a sahipse kaldır değilse ekle



----------



