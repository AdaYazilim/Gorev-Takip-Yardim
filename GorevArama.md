<h3>Görev Arama</h3>
Yetkiniz dahilindeki işlerde arama yaparak kısıtlı bilgilerini albileceğiniz servistir.
"Query" oluşturmada "GorevListesi.IntellisenseListeleriniAl.iam" servisinden alacağınız anahtar kelime ve cevapları kullanabilirsiniz.

**Link:** "http://www.gorevtakip.com/GorevListesi.GorevListesiAl.iam"

**Parametreler:** "GorevleriAlInput" nesnesini göndermeniz yeterlidir.

<h5>Örnek İstek:</h5>
<pre>
{
  Query:'is-degisken:Musteri(1059)', 
  KayitNo:''
}
</pre>

<h5>Örnek Cevap:</h5>
Bu servis, Sorguya uyan işleri ilgili panolara dağıtılarak "BasitIsAkisiListesi" nesnesi döndürür. 
Not: Eğer işler herhangi bir panoya eklenmedi ise(Bu işlem şuanda yalnızca ekrandan yapılabilmektedir.), "DigerIslerPanosu" değeri true olan panoya girecektir.

<pre>
{
     "Panolar": [
        {
            "Id": -1,
            "Ad": "Yakın Takipteki İşler",
            "Gosteriliyor": true,
            "GizlenmislerGosteriliyor": false,
            "AdDegistiriliyor": false,
            "Isler": [],
            "SiralamaBilgileri": {
                "GorevAramaAnahtari": null,
                "AttributeAdi": "OlusturmaTarihi",
                "Artarak": false,
                "GorunurIsim": "Oluşturma Tarihi"
            },
            "DeadlineFiltrelemeBilgileri": {
                "GorevAramaAnahtari": null,
                "AttributeAd": "deadline",
                "GorunurIsim": "Tüm Görevler",
                "FiltreString": "tumu"
            },
            "SiraNo": -1,
            "DigerIslerPanosu": false,
            "YakinTakipPanosu": true,
            "PanoSiralamaIstegiIsleniyor": false,
            "DragOverDurumunda": false,
            "ProjeId": 0
        },
        {
            "Id": 748,
            "Ad": "Diğer Her Şey",
            "Gosteriliyor": true,
            "GizlenmislerGosteriliyor": false,
            "AdDegistiriliyor": false,
            "Isler": [
                {
                    "IsAkisiInstanceId": 153674,
                    "Baslik": "Dinkal sigorta / Görev takibe giden işlerde işi sonlandırma olsun",
                    "Aciklama": "Yazılım Talep",
                    "Deadline": "0001-01-01T00:00:00",
                    "OlusturmaTarihi": "2015-12-08T10:48:32",
                    "SonlanmaTarihi": "2015-12-10T12:17:37",
                    "Durum": 2,
                    "OlusturanId": 1040,
                    "AktifFaaliyetler": [],
                    "TamamlanmisFaaliyetler": null,
                    "Oncelik": 5,
                    "OkuyanKullaniciIdler": null,
                    "GizleyenKullaniciIdler": null,
                    "Acil": false,
                    "AcilSiraNo": 0,
                    "IsKisaAd": "yazilimtalep",
                    "SonIslemTarihi": "2015-12-10T12:17:37",
                    "Etiketler": [],
                    "Tenant": {
                        "TenantId": 63
                    },
                    "OlusturanKullaniciAdi": "ayse",
                    "Gizlenmis": false,
                    "Okunmus": true,
                    "PanoId": 748,
                    "PanoSiraNo": 0,
                    "DragOverDurumunda": false,
                    "Surukleniyor": false,
                    "Sonlanmis": true,
                    "Ertelenmis": false,
                    "Aktif": false
                },
                ...
            ],
            "SiralamaBilgileri": {
                "GorevAramaAnahtari": null,
                "AttributeAdi": "OlusturmaTarihi",
                "Artarak": false,
                "GorunurIsim": "Oluşturma Tarihi"
            },
            "DeadlineFiltrelemeBilgileri": {
                "GorevAramaAnahtari": null,
                "AttributeAd": "deadline",
                "GorunurIsim": "Tüm Görevler",
                "FiltreString": "tumu"
            },
            "SiraNo": 600,
            "DigerIslerPanosu": true,
            "YakinTakipPanosu": false,
            "PanoSiralamaIstegiIsleniyor": false,
            "DragOverDurumunda": false,
            "ProjeId": 0
        }
    ],
    "Basarili": true,
    "Mesaj": ""
}
</pre>


<h3>Intellisense Listelerini Al</h3>
Aramalarda kullanabileceğiniz Anahtar Kelimelere ve gerekli yerlerde kullanabileceğiniz sabit bilgileri döner.

**Link:** "http://www.gorevtakip.com/GorevListesi.IntellisenseListeleriniAl.iam"

**Parametreler:** Parametre almaz.

<h5>Örnek İstek:</h5>
<pre>
    []
</pre>

<h5>Örnek Cevap:</h5>

<pre>
{
    "AnahtarKelimeler": [
        {
            "IfadeListesi": [
                "alt-deadline:",
                "altdeadline:"
            ],
            "Aciklama": "",
            "OrnekKullanimlar": [
                "alt-deadline:bugün"
            ]
        },
        {
            "IfadeListesi": [
                "is-degisken:",
                "isdegisken:"
            ],
            "Aciklama": "İş değişkeninin değerine göre aramak için kullanılır.",
            "OrnekKullanimlar": [
                "is-degisken:KisaAd(Deger)",
                "is-degisken:KisaAd(Deger1,Deger2)"
            ]
        },
        ...
    ],
    "Kullanicilar": [
        "ADAYAZILIM",
        ...
    ],
    "Isler": [
        "Hızlı Teklif",
        ...
    ],
    "Durumlar": [
        "Aktif",
        "Tamamlandı",
        "Ertelendi"
    ],
    "Tarihler": [
        "dün",
        "bugün",
        "yarın"
    ]
}
</pre>


<h2>Veri Yapıları</h2>
<h3>GorevleriAlInput</h3>
<pre>
{
	<strong>String</strong> Query,     (Arama Sorgusu)
    <strong>String</strong> KayitNo    (Kayıtlı Sorgu Id)
}
</pre>

<h3>BasitIsAkisiListesi</h3>
<pre>
{
	<strong>List<Pano></strong> Panolar,     (İş Panoları)
	<strong>Bool</strong> Basarili,     (Sorgu Başarıyla Tamamlandı mı)
    <strong>String</strong> Mesaj    (Olası Bilgi Mesajı)
}
</pre>

<h3>Pano</h3>
<pre>
{
    <strong>Int</strong> Id,     (Pano Id)
    <strong>String</strong> Ad,     (Pano Adı)
    <strong>List<AramaSonucuIsAkisiInstance></strong> Isler    (İşler)
    <strong>bool</strong> DigerIslerPanosu,    (İş default Panoda ise true dur)
    ...
}
</pre>

<h3>AramaSonucuIsAkisiInstance</h3>
<pre>
{
	<strong>int</strong> IsAkisiInstanceId, (iş Id)
    <strong>string</strong> Baslik,   
    <strong>string</strong> Aciklama,
    <strong>DateTime</strong> Deadline,
    <strong>DateTime</strong> OlusturmaTarihi,
    <strong>DateTime</strong> SonlanmaTarihi,
    <strong>IsDurum</strong> Durum,
    <strong>bool</strong> Sonlanmis,  (Durum == IsDurum.Tamamlandi)
    <strong>bool</strong> Ertelenmis, (Durum == IsDurum.Ertelendi)
    <strong>bool</strong> Aktif,      (Durum == IsDurum.Aktif)
    <strong>int</strong> OlusturanId,
    <strong>List<AktifFaaliyet> AktifFaaliyetler,
    <strong>List<TamamlanmisFaaliyet> TamamlanmisFaaliyetler,
    <strong>int</strong> Oncelik,
    <strong>List<int></strong> OkuyanKullaniciIdler,
    <strong>List<int></strong> GizleyenKullaniciIdler,
    <strong>bool</strong> Acil,
    <strong>int</strong> AcilSiraNo,
    <strong>string</strong> IsKisaAd,
    <strong>DateTime</strong> SonIslemTarihi,
    ...
}
</pre>


<h3>IsDurum</h3>
  <table>
    <tr>
      <th>Metin</th>
      <th>Deger</th>
    </tr>
    <tr>
      <td>Bos</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Aktif</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Tamamlandi</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Ertelendi</td>
      <td>3</td>
    </tr>
  </table>
  
  
<h3>AktifFaaliyet</h3>
<pre>
{
    <string>string</strong> Ad,                    (Normalize edilmiş ad)
    <string>string</strong> AcikAd,                (Ad)
    <string>int</strong> FaaliyetInstanceId,
    <string>List<string></strong> Sorumlular,      (Normalize edilmiş sorumlu kullanıcı adları)
    <string>List<string></strong> AcikSorumlular,  (Sorumlu kullanıcı adları)
    <string>bool</strong> KullaniciUstlenebilir
}
</pre>

<h3>TamamlanmisFaaliyet</h3>
<pre>
{
    <string>string</strong> Ad,
    <string>string</strong> AcikAd,
    <string>int</strong> FaaliyetInstanceId,
    <string>List<string></strong> Sorumlular,
    <string>List<string></strong> AcikSorumlular,
    <string>bool</strong> KullaniciUstlenebilir,
    <string>DateTime</strong> TamamlanmaTarihi,
    <string>int</strong> Tamamlayan                 (Tamamlayan KullanıcıId)
}
</pre>

<h3>IntellisenseListeleri</h3>
<pre>
{
    <string>List<AnahtarKelimeOzellik></strong> AnahtarKelimeler,
    <string>List<string></strong> Kullanicilar,
    <string>List<string></strong> Isler,
    <string>List<string></strong> Durumlar,
    <string>List<string></strong> Tarihler,
}
</pre>

<h3>AnahtarKelimeOzellik</h3>
<pre>
{
    <string>List<string></strong> IfadeListesi,     (Anahtar Kelimenin desteklenen şekilleri)
    <string>string</strong> Aciklama,               
    <string>List<string></strong> OrnekKullanimlar  
}
</pre>
