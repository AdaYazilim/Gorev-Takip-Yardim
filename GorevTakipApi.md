<h1>Ada Yazılım Görev Takip WEB API</h1>

Sistemimiz, linklere gerekli parametrelerin json yapısında gönderilmesi üzerinde kuruludur. Login gerekli olan işlemler için öncelikle login isteğine başarılı cevap almalısınız, ardından yetki gerektiren işlemi yapabilirsiniz. Dikkat edilmesi gereken konu ise bu işlemlerin aynı sessionda yapılmasıdır.

<h1>Servisler</h1>

<h3>1.Kullanıcı Girişi</h3>
Yetkiye bağlı servisleri çağırabilmeniz için login işlemini yapmış olmanız gerekmektdir. Dikkat edilmesi gereken iki nokta vardır. Bir, kullanıcı adı diğer sistemlerle farklılık gösterebilmektedir. İki, şifrenizi “sha256” ile şifreleyerek göndermelisiniz.

**Link:** "http://www.gorevtakip.com/Index.Login.iam"

**Parametreler:** KullanıcıAdı ve Kullanıcı şifresi (Bu bilgileri acenteden temin edebilirsiniz) .

<h5>Örnek İstek:</h5>
<pre>
["kullaniciAdi", "Sifre"]
</pre>

<h5>Örnek Cevap:</h5>

<pre>
{
    "Basarili": true,
    "Mesaj": ""
}
</pre>

<h3>2.Yeni İş Başlat</h3>

Yeni iş başlatmak istediğinizde bu fonksiyonu kullanabilirsiniz. Dikkat edilmesi gereken Elemanların başlatılmak istenen işe göre değişiklik göstereceğidir.  Elemanların listesini "Yeni İş Başlat Yardım" servisinden edebilirsiniz.

Göndereceğiniz her eleman için; "KisaAd" ve "Deger" zorunlu alanlardır. "UzunDeger" alanı eleman değeri için açıklayıcı nitelik taşıyan veridir. Özellikle Seçenekli Elemanlarda seçeneğin "Metin" kısmını gönderilebilirsiniz. Diğer zamanlarda "UzunDeger ve "Deger" bilgilerini aynı olarak gönderebilirsiniz.

**Link:** " http://www.gorevtakip.com/YeniAkis.IsiYarat.iam"

**Parametreler:** YeniIs Nesnesi

<h5>Örnek İstek:</h5>

<pre>
{
    'GenelBilgiler': {
        'TanimAd': 'Teklif Ver',
        'Baslik': '34ABC789 - HALK SİGORTA A.Ş -Trafik',
        'DeadlineTarih': '2015-06-11',
        'DeadlineSaat': '01:47',
        'Oncelik': 7,
        'Baslatan': 'KullaniciAdi',
        'Elemanlar': [{
            'KisaAd': 'Sirket',
            'Deger': '015',
            'UzunDeger': 'HALK SİGORTA A.Ş.'
        }]
    },
    'IlkFaaliyet': {
        'Tamamlayan': 'KullaniciAdi',
        'Elemanlar': [{
            'KisaAd': 'SirketAd',
            'Deger': 'HALK SİGORTA A.Ş.',
            'UzunDeger': 'HALK SİGORTA A.Ş.'
        }, {
            'KisaAd': 'Plaka',
            'Deger': '34ABC789',
            'UzunDeger': '34ABC789'
        }, {
            'KisaAd': 'KimlikNo',
            'Deger': '12345678912',
            'UzunDeger': '12345678912'
        }]
    }
}
</pre>

<h5>Örnek Cevap:</h5>

Sonuç başarılı ise dönen mesaj değeri kaydedilen iin ID sini döndürür.

<pre>
{
    "Basarili": true,
    "Mesaj": "124563"
}
</pre>

<h3>3.Yeni İş Başlat Yardım</h3>

İş Akış Tanımının Genel ve ilk Faaliyet alanlarında tanımlı ve faaliyete göre değişen eleman lsitesini almak için kullanılabilirsiniz.

Her bir eleman için; "KisaAd", "Deger", "UzunDeger" alanlarının yanısıra "Secenekler" alanıda gelir. Bu alanda bulunan liste Elemanın alabileceği değerleri göstermektedir. Liste yoksa veya boş ise Herhangi bir değer gönderilebilinir.

**Link:** " http://www.gorevtakip.com/YeniAkis.IsiYaratYardim.iam"

**Parametreler:** İş Akışının Tanım adı(acentenizden temin edebilirsiniz.)

<h5>Örnek İstek:</h5>
<pre>
["Akis Adi"]
</pre>

<h5>Örnek Cevap:</h5>
<pre>
{
    "GenelDegiskenler": [
        {
            "Aciklama": "Poliçe Numarası",
            "Tip": "Sayi",
            "Zorunlu": false,
            "KisaAd": "polno",
            "Deger": "",
            "UzunDeger": "",
            "Secenekler": []
        }
    ],
    "IlkFaaliyetDegiskenler": [
        {
            "Aciklama": "Teknik Sorumlu",
            "Tip": "Liste",
            "Zorunlu": false,
            "KisaAd": "tekniksorumlu",
            "Deger": "",
            "UzunDeger": "",
            "Secenekler": [
                {
                    "Metin": "Görev Yoneticisi",
                    "Deger": "1"
                },
                {
                    "Metin": "Veli Ali",
                    "Deger": "2"
                },
                {
                    "Metin": "Ali Veli",
                    "Deger": "3"
                }
            ]
        },
        {
            "Aciklama": "Poliçe Numarası",
            "Tip": "Sayi",
            "Zorunlu": false,
            "KisaAd": "polno",
            "Deger": "",
            "UzunDeger": "",
            "Secenekler": []
        }
    ]
}
</pre>


<h3>4.İşi Sonlandır</h3>

Mevcut işi Herhangi Bir faaliyette sonlandırmak için kullanılır. "İş Akışı Sonlandırabilir" rolü Gerektirir.

**Link:** "http://www.gorevtakip.com/Gorev.IsSonlandir.iam"

**Parametreler:** İş Akışı instance Id

<h5>Örnek İstek:</h5>

<pre>
[123456789]
</pre>

<h5>Örnek Cevap:</h5>

Dönen cevaptaki Basarili ve Mesaj alanları işlemin nasıl tamamlandığını ve olası açıklamaları döndürür.

<pre>
{
    "KullaniciYonetimYapabilir": ...,
    "Is": {...},
    "Basarili": true,
    "Mesaj": ""
}
</pre>


<h1>Veri Yapıları</h1>

<h5>YeniIs</h5>
<pre>
{
    <strong>GenelBilgiler</strong> GenelBilgiler,     (Başlatılacak işin genel bilgileri)
    <strong>Faaliyet</strong> IlkFaaliyet             (Başlatılacak işin ilk faaliyeti)
}
</pre>
<h5>GenelBilgiler</h5>

<pre>
{
    <strong>String</strong> TanimAd,         (Başlatılacak İşin Tanım Adı (Acenteden Alabilirsiniz.))
    <strong>String</strong> Baslik,          (Görevin başlığı)
    <strong>String</strong> DeadlineTarih,   (Görevin en son bitmesi öngörülen tarih.)
    <strong>String</strong> DeadlineSaat     (Görevin en son bitmesi öngörülen saat.)
    <strong>int</strong> Oncelik,            (Görevin önemini belirten 1(düşük)-10(yüksek) arasında derecelendirme.)
    <strong>String</strong> Baslatan,        (Kullanıcı Adı)
    <strong>Eleman[]</strong> Elemanlar      (Görevin her faaliyette değeri değiştirilebilinen elemanları)
    <strong>Bool</strong> Ertelenmis,   (Görevin ileri tarihte sorumlulara atılacağını gösterir)
    <strong>String</strong> ErtelemeBitisTarihi,   (Görevin sorumlulara iş olarak düşeceği tarih.)
}
</pre>


<h5>Faaliyet</h5>

<pre>
{
    <strong>String</strong> Tamamlayan,      (Kullanıcı Adı)
    <strong>Eleman[]</strong> Elemanlar      (Faaliyette bulunan elemanlar)
}
</pre>

<h5>Eleman</h5>
<pre>
{
    <strong>String</strong> KisaAd,         (Elemanı diğer elemanlardan ayıran anahtar kelime)
    <strong>String</strong> Deger,          (Elemana verilen değer)
    <strong>String</strong> UzunDeger       (Elemanın açıklamalı değeri)
}
</pre>
