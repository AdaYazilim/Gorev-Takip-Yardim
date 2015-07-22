# Ada Yazılım Görev Takip WEB API

Sistemimiz, linklere gerekli parametrelerin json yapısında gönderilmesi üzerinde kuruludur. Login gerekli olan işlemler için öncelikle login isteğine başarılı cevap almalısınız, ardından yetki gerektiren işlemi yapabilirsiniz. Dikkat edilmesi gereken konu ise bu işlemlerin aynı sessionda yapılmasıdır.

### 1.Kullanıcı Girişi

Yetkiye bağlı servisleri çağırabilmeniz için login işlemini yapmış olmanız gerekmektdir. Dikkat edilmesi gereken iki nokta vardır. Bir, kullanıcı adı diğer sistemlerle farklılık gösterebilmektedir. İki, şifrenizi “sha256” ile şifreleyerek göndermelisiniz.

**Link:** "http://www.gorevtakip.com/Index.Login.iam"

**Parametreler:** KullanıcıAdı ve Kullanıcı şifresi (Bu bilgileri acenteden temin edebilirsiniz) .

#####Örnek İstek:

["kullaniciAdi","Sifre"]

#####Örnek Cevap:

{"Basarili":true,"Mesaj":""}

### 2.Yeni İş Başlat

Yeni iş başlatmak istediğinizde bu fonksiyonu kullanabilirsiniz. Dikkat edilmesi gereken Elemanların başlatılmak istenen işe göre değişiklik göstereceğidir. Elemanların listesini acentenizden temin edebilirsiniz.

**Link:** " http://www.gorevtakip.com/YeniAkis.IsiYarat.iam"

**Parametreler:** YeniIs Nesnesi

#####Örnek İstek:

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

#####Örnek Cevap:

Sonuç başarılı ise dönen mesaj değeri kaydedilen iin ID sini döndürür.

{"Basarili":true,"Mesaj":"124563"}

###3.Veri Yapıları

##### YeniIs

{

**GenelBilgiler** GenelBilgiler,

**Faaliyet** IlkFaaliyet

}

##### GenelBilgiler

{

**String** TanimAd, (Başlatılacak İşin Tanım Adı (Acenteden Alabilirsiniz.))

**String** Baslik,

**String** DeadlineTarih,

**String** DeadlineSaat

**İnt** Oncelik,

**String** Baslatan, (Kullanıcı Adı)

**Eleman[]** Elemanlar

}

##### Faaliyet

{

**String** Tamamlayan, (Kullanıcı Adı)

**Eleman[]** Elemanlar

}

##### Eleman

{

**String** KisaAd,

**String** Deger,

**String** UzunDeger

}
