<h1>Ada Yazılım Görev Takip WEB API</h1>

Sistemimiz, linklere gerekli parametrelerin json yapısında gönderilmesi üzerinde kuruludur. Login gerekli olan işlemler için öncelikle login isteğine başarılı cevap almalısınız, ardından yetki gerektiren işlemi yapabilirsiniz. Dikkat edilmesi gereken konu ise bu işlemlerin aynı sessionda yapılmasıdır.

<h1>Servisler</h1>

<h3>1.Kullanıcı Girişi</h3>
Yetkiye bağlı servisleri çağırabilmeniz için login işlemini yapmış olmanız gerekmektdir. Dikkat edilmesi gereken iki nokta vardır. Bir, kullanıcı adı diğer sistemlerle farklılık gösterebilmektedir. İki, şifrenizi “sha256” ile şifreleyerek göndermelisiniz.

**Link:** "http://www.gorevtakip.com/Index.Login.iam"

**Parametreler:** KullanıcıAdı ve Kullanıcı şifresi (Bu bilgileri acenteden temin edebilirsiniz) .

<h5>Örnek İstek:</h5>

["kullaniciAdi","Sifre"]

<h5>Örnek Cevap:</h5>

{"Basarili":true,"Mesaj":""}

<h3>2.Yeni İş Başlat</h3>

Yeni iş başlatmak istediğinizde bu fonksiyonu kullanabilirsiniz. Dikkat edilmesi gereken Elemanların başlatılmak istenen işe göre değişiklik göstereceğidir. Elemanların listesini acentenizden temin edebilirsiniz.

**Link:** " http://www.gorevtakip.com/YeniAkis.IsiYarat.iam"

**Parametreler:** YeniIs Nesnesi

<h5>Örnek İstek:</h5>

{

'GenelBilgiler': {

'TanimAd': 'Teklif Ver',

'Baslik': ' '34ABC789 - HALK SİGORTA A.Ş -Trafik',

'DeadlineTarih': '2015-06-11',

'DeadlineSaat': '01:47',

'Oncelik': 7,

'Baslatan': 'KullaniciAdi',

'Elemanlar': [{

'KisaAd': 'Sirket',

'Deger': '015',

'UzunDeger': 'HALK SİGORTA A.Ş.'

}

]

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

<h5>Örnek Cevap:</h5>

Sonuç başarılı ise dönen mesaj değeri kaydedilen iin ID sini döndürür.

{"Basarili":true,"Mesaj":"124563"}

<h1>Veri Yapıları</h1>

<h5>YeniIs</h5>

{

<strong>GenelBilgiler</strong> GenelBilgiler,

<strong>Faaliyet</strong> IlkFaaliyet

}

<h5>GenelBilgiler</h5>

{

<strong>String</strong> TanimAd, (Başlatılacak İşin Tanım Adı (Acenteden Alabilirsiniz.))

<strong>String</strong> Baslik,

<strong>String</strong> DeadlineTarih,

<strong>String</strong> DeadlineSaat

<strong>int</strong> Oncelik,

<strong>String</strong> Baslatan, (Kullanıcı Adı)

<strong>Eleman[]</strong> Elemanlar

}

<h5>Faaliyet</h5>

{

<strong>String</strong> Tamamlayan, (Kullanıcı Adı)

<strong>Eleman[]</strong> Elemanlar

}

<h5>Eleman</h5>

{

<strong>String</strong> KisaAd,

<strong>String</strong> Deger,

<strong>String</strong> UzunDeger

}
