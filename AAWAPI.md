# Ada Yazılım Acente Cari WEB API

Sistemimiz, linklere gerekli parametrelerin json yapısında gönderilmesi üzerinde kuruludur. Login gerekli olan işlemler için öncelikle login isteğine başarılı cevap almalısınız, ardından yetki gerektiren işlemi yapabilirsiniz. Dikkat edilmesi gereken konu ise bu işlemlerin aynı sessionda yapılmasıdır.

###1. Kullanıcı Girişi

**Link:**"http://localhost/ada/Login.GirisYap.aaw"

**Parametreler:** KullanıcıAdı ve Kullanıcı şifresi (Bu bilgileri acenteden temin edebilirsiniz.)

##### Örnek İstek:

["kullaniciAdi","Sifre"]

##### **Örnek Cevap:**

{"Basarili":true,"Mesaj":""}

###2. Poliçe Arama

**Link:**" [http://localhost/ada/Police.PoliceAra.aaw"

**Parametreler:** Query (Bu bilgi " **PoliceNo/SigortalıAdı/KimlikNo/Plaka/Marka**"  alanları için geçerlidir. yazacağınız query bilgisi bu alanlarla karşılaştırılır ve uygun kayıtlar getirilir.)

##### **Örnek İstek:**

    ["0330011122"]

##### Örnek Cevap:

    [{
     "FprkPol": 176529, //Cari veritabanında kayıtlı poliçe keyidir.
     "Tanzim": "2015-03-24T00:00:00", //Poliçe Tanzim Tarihidir.
     "Baslangic": "2015-03-20T00:00:00", //Poliçe Başlangıç Tarihidir.
     "Bitis": "2015-03-20T00:00:00", //Poliçe Bitiş Tarihidir.
     "Brans":"412", // Cari veritabanında Tanımlı Poliçe Brans Kodudur.
     "PolGrp":"NAK", // Poliçe Grubudur.
     "PoliceNo": "24370032", //Şirket Poliçe Numarasıdır.
     "TecditNo":"", //Şirket Tecdit Numarasıdır.
     "ZeyilNo": "1", //Şirket Zeyil Numarasıdır.
     "FfrkSir": 26, //Cari veritabanında kayıtlı Şirket Kodudur.
     "FfrkMus": 73376, //Cari veritabanında kayıtlı Müşteri keyidir.
     "Sigortali": "ABC TEKSTİL İHRACAT PAZARLAMA A.Ş.",Poliçede Kayıtlı Sigortalı Adıdır.
     "Plaka": "",//Poliçede Kayıtlı Plaka bilgisidir. Bazı Poliçe gruplarında boş gelir.
     "TeklifDurumu": 0,
     "Il": 34,//Poliçenin İl Bilgisi
     "Ilce": "GÜMÜŞSUYU",//Poliçenin İlçe Bilgisi
     "FyrlkDrm": 2, //Poliçe Yürürlük Durumu
     "PolTek": 1,//Poliçe Sınıfı
     "FfrkTt": 0,//Tecdit Tipi
     "FpolTip": 0, //Poliçe Tipi
     "FTcKimNo": "",//Sigortalı TC Kimlik Numarası
     "FVerKimNo": "0330011122", //Sigortalı VergiNumarası
     "Marka": "",//Poliçede Kayıtlı Araç Marka bilgisidir. Bazı Poliçe gruplarında boş gelir.
     "FfrkMizBlg": 0//ŞubeKodu
    }]

###3. Detaylı Poliçe Arama
**Link:**"http://localhost/ada/Police.DetayliPoliceArama.aaw"

**Parametreler:**

_Sorgu:_ Poliçe numarası, KimlikNo, VergiNo, Sigortalı, Plaka, Marka bilgileri için ortak alandır.

_EkAlanlar:_ Standart alanlara ek olarak istenen diğer alanlar liste olarak alınır. Poliçe alanları başlığından eklemeler yapabilirsiniz. Eksik alanlar için iletişime geçebilirsiniz.

_Yururlukte:_ Poliçenin yürürlükte durumunu belirtir. Alttaki değerleri alabilir. Acente Cari porogramından toplu olarak güncellenmekte olduğu unutulmamalıdır.

|  Yürürlük Durumu | Kod |
| --- | --- |
| Hepsi (varsayılan) | 0 |
| Yürürlükte | 1 |
| Yürürlükte Değil | 2 |

Not: Poliçe aramada gelen sonuçlardaki alan adlarına göre farklılıklar vardır.

##### Örnek İstek:

    {Sorgu:'78545625859', EkAlanlar:['feposta','ftelno','SirketAdi','fsigdogtar','fsigetdtar'],Yururlukte:1}

##### Örnek Cevap:

    [{
        "Alanlar": [
            {
                "Soru": "fPrkPol",
                "Cevap": "38"
            },
            {
                "Soru": "fTnzTar",
                "Cevap": "29.09.2006"
            },
            {
                "Soru": "Fbastar",
                "Cevap": ""
            },
            ...
        ],
            "OdemePlani": {
        "Taksitler": [
            {
                "FPrkOpl": 1259,
                "fFrkPol": 0,
                "MusteriTarihi": "2006-11-06T00:00:00",
                "MusteriOdemeTutari": {},
                "MusteriIptalTutari": {},
                "AcenteTarihi": "2007-01-04T00:00:00",
                "AcenteTutar": {},
                "Kapamalar": [
                    {
                        "TahsilatList": [
                            {
                                "SimdiyeKadarKapananTutar": {},
                                "TahsilatTutari": {},
                                "KapamaIcinKullanilabilecekTutar": {},
                                "Alanlar": {
                                    "fAci": {
                                        "$type": "AdaGenel.Cesitli.NesneAlan, AdaGenel",
                                        "SaltOkunur": false,
                                        "Soru": "fAci",
                                        "Cevap": "(00118561-1) POLİÇE KAPAMASI                                    "
                                    },
                                    ...
                                }
                            }
                        ],
                        "KapananTutar": 206.2
                    }
                ],
                "PoliceNo": null,
                "TecditNo": null,
                "ZeyilNo": null,
                "Sirket": null,
                "TaksitKodu": null,
                "Sigortali": null,
                "Plaka": null,
                "MusteriOdemesiGerekenTutar": {},
                "ToplamKapananTutar": {},
                "IlgiliTahsilatIleKapananTutar": {},
                "KalanBorcu": {},
                "Isaretli": false,
                "IlkGiristeIsaretli": false,
                "IlkGiristeKapaliTutar": {}
            }},
            ...
        ]
    },
    "Hasarlar": [],
    "Teminatlar": [],
    "Sigortalilar": [
        {
            "Ad": "BURCU",
            "Soyad": "İNANÇ",
            "Cinsiyet": "K",
            "KimlikNo": "22870344190",
            "Yakinlik": 1,
            "DogumTarihi": "1957-07-30T00:00:00"
        },
        ...    
        ]
    }
    ]

###4. Poliçe Bilgilerini Al

**Link:**"http://localhost/ada/Police.PoliceBilgileriniAl.aaw"

**Parametreler:** adayazılım sisteminde tanımlı poliçe numarası (fprkPol) ve istenen ek alanlar gönderilmelidir.

##### Örnek İstek:


    [3488,['feposta','ftelno','SirketAdi','fsigdogtar','fsigetdtar']]

##### Örnek Cevap:


    {
    "Alanlar": [
        {
            "Soru": "fPrkPol",
            "Cevap": "3488"
        },
        {
            "Soru": "fTnzTar",
            "Cevap": "04.01.2007"
        },
        {
            "Soru": "Fbastar",
            "Cevap": ""
        },
        {
            "Soru": "Fbittar",
            "Cevap": ""
        },
        {
            "Soru": "Brans",
            "Cevap": "608"
        },
        {
            "Soru": "PolGrp",
            "Cevap": "SAG"
        },
        ...
    ],
    "OdemePlani": {
        "Taksitler": [
            {
                "FPrkOpl": 1259,
                "fFrkPol": 0,
                "MusteriTarihi": "2006-11-06T00:00:00",
                "MusteriOdemeTutari": {},
                "MusteriIptalTutari": {},
                "AcenteTarihi": "2007-01-04T00:00:00",
                "AcenteTutar": {},
                "Kapamalar": [
                    {
                        "TahsilatList": [
                            {
                                "SimdiyeKadarKapananTutar": {},
                                "TahsilatTutari": {},
                                "KapamaIcinKullanilabilecekTutar": {},
                                "Alanlar": {
                                    "fAci": {
                                        "$type": "AdaGenel.Cesitli.NesneAlan, AdaGenel",
                                        "SaltOkunur": false,
                                        "Soru": "fAci",
                                        "Cevap": "(00935421-1) POLİÇE KAPAMASI                                    "
                                    },
                                    ...
                                }
                            }
                        ],
                        "KapananTutar": 206.2
                    }
                ],
                "PoliceNo": null,
                "TecditNo": null,
                "ZeyilNo": null,
                "Sirket": null,
                "TaksitKodu": null,
                "Sigortali": null,
                "Plaka": null,
                "MusteriOdemesiGerekenTutar": {},
                "ToplamKapananTutar": {},
                "IlgiliTahsilatIleKapananTutar": {},
                "KalanBorcu": {},
                "Isaretli": false,
                "IlkGiristeIsaretli": false,
                "IlkGiristeKapaliTutar": {}
            }},
            ...
        ]
    },
    "Hasarlar": [],
    "Teminatlar": [],
    "Sigortalilar": [
        {
            "Ad": "BURCU",
            "Soyad": "İNANÇLı",
            "Cinsiyet": "K",
            "KimlikNo": "22720347190",
            "Yakinlik": 1,
            "DogumTarihi": "1957-07-30T00:00:00"
        },
        {
            "Ad": "HİLMİ",
            "Soyad": "İNANÇLI",
            "Cinsiyet": "E",
            "KimlikNo": "24443304756",
            "Yakinlik": 3,
            "DogumTarihi": "1982-05-31T00:00:00"
        },
        {
            "Ad": "BUSE",
            "Soyad": "İNANÇLI",
            "Cinsiyet": "K",
            "KimlikNo": "24731845762",
            "Yakinlik": 3,
            "DogumTarihi": "1985-07-03T00:00:00"
        }
    ]
    }

###5. Poliçe Ekleme

**Link:**" [http://localhost/ada/Police.PoliceEkle.aaw"

**Parametreler:** poliçenin bilgilerini SoruCevap listesi olarak almaktadır. Sorular ve açıklamalarına "Poliçe Alanları ve Karşılıkları" alanından ulaşabilirsiniz. Örnekte gösterilen alanlar zorunlu alanlardır.

##### Örnek İstek:

    [
    [
        {
            "Soru": "SigAdi",
            "Cevap": "Deneme Müşterisi"
        },
        {
            "Soru": "fSirPolNo",
            "Cevap": "4587456"
        },
        {
            "Soru": "fFrkMus",
            "Cevap": "1"
        },
        {
            "Soru": "fFrkSir",
            "Cevap": "1"
        },
        {
            "Soru": "fTnzTar",
            "Cevap": "04.01.2007"
        },
        {
            "Soru": "fTnzTar",
            "Cevap": "04.01.2007"
        },
        {
            "Soru": "fBasTar",
            "Cevap": "04.01.2007"
        },
        {
            "Soru": "fBitTar",
            "Cevap": "04.01.2008"
        },
        {
            "Soru": "Brans",
            "Cevap": "608"
        },
        {
            "Soru": "PolGrp",
            "Cevap": "SAG"
        },
        {
            "Soru": "fPolTek",
            "Cevap": "3"
        },
        ....
    ]
    ]

##### Örnek Cevap:

    {
        "Prk": 239759,
        "Basarili": true,
        "Mesaj": null
    }

###6. Müşteri Arama

**Link:**"http://localhost/ada/Musteri.MusteriAra.aaw"

**Parametreler:** Sorgu, Müşteri Tipi ve istenen ek alanlar gönderilmelidir. Sorgu alanı ad ve soyad, TC Kimlik ve Vergi Numarasına göre arama yapmaktadır. Müşteri Tipi alanı null girilirse tipten bağımsız arama yapmaktadır. Alabildiği değerler "Bazı alanlar ve Alabildiği Değerler" kısmında belirtilmiştir.

##### Örnek İstek:

    [{Sorgu:'',MusteriTipi:null,EkAlanlar:["fMusKimNo","fMusTcKimN"]}]

##### Örnek Cevap:

    [
    {
        "Alanlar": [
            {
                "Soru": "fKulHesKod",
                "Cevap": ""
            },
            {
                "Soru": "fMusAdi",
                "Cevap": ""
            },
            {
                "Soru": "fMusKimNo",
                "Cevap": ""
            },
            {
                "Soru": "fMusSoyadi",
                "Cevap": ""
            },
            {
                "Soru": "fMusTcKimN",
                "Cevap": ""
            },
            {
                "Soru": "fMusTip",
                "Cevap": "1"
            },
            {
                "Soru": "fPrkMus",
                "Cevap": "18580"
            }
        ]
    },
    {
        "Alanlar": [
            {
                "Soru": "fKulHesKod",
                "Cevap": "1.1.1463"
            },
            {
                "Soru": "fMusAdi",
                "Cevap": "deneme Müşterisi"
            },
            {
                "Soru": "fMusKimNo",
                "Cevap": ""
            },
            {
                "Soru": "fMusSoyadi",
                "Cevap": ""
            },
            {
                "Soru": "fMusTcKimN",
                "Cevap": "00000078842"
            },
            {
                "Soru": "fMusTip",
                "Cevap": "1"
            },
            {
                "Soru": "fPrkMus",
                "Cevap": "12841"
            }
    ]

###7. Müşteri Bilgilerini Al

**Link:**"http://localhost/ada/Musteri.MusteriAl.aaw"

**Parametreler:** Müşteri Numarası ve ek olarak istenen Müşteri ek alanları Gönderilir..

##### Örnek İstek:

    [19828, ["fMusKimNo","fMusTcKimN"]]

##### Örnek Cevap:

    {
    "Nesne": {
        "Alanlar": [
            {
                "Soru": "fPrkMus",
                "Cevap": "19828"
            },
            {
                "Soru": "fmuskod",
                "Cevap": ""
            },
            {
                "Soru": "fMusAdi",
                "Cevap": "zerrin.."
            },
            {
                "Soru": "fMusSoyadi",
                "Cevap": ""
            },
            {
                "Soru": "fMusUnv",
                "Cevap": ""
            },
            {
                "Soru": "fMusKimNo",
                "Cevap": ""
            },
            {
                "Soru": "fMusTcKimN",
                "Cevap": ""
            },
            {
                "Soru": "fMusTip",
                "Cevap": "1"
            },
            {
                "Soru": "fMusKimNo",
                "Cevap": ""
            },
            {
                "Soru": "fMusTcKimN",
                "Cevap": ""
            }
        ]
    },
    "Basarili": true,
    "Mesaj": ""
    }

###8. Müşteri Ekle

**Link:**"http://localhost/ada/Musteri.MusteriEkle.aaw"

**Parametreler:** Eklemek istediğiniz Müşteriye ait alanları Soru Cevap listesi olarak göndermeniz gerekmektedir

Not: İnternet Müşterisi olarak işaretlenmek istenen müşterilerde "fIntntMus" alanının değeri 1 olarak ayarlanmalıdır.

##### Örnek İstek:

    [[
       {
        Soru: "fMusAdi",
         Cevap: "zerrin.."
       },
       {
        Soru: "fIntntMus",
        Cevap: "1"
       },
        ....
 ]]

##### Örnek Cevap:

    {
    "Prk": 19829,
    "Basarili": true,
    "Mesaj": null
    }

###9. Müşteri Güncelle

**Link:**"http://localhost/ada/Musteri.MusteriGuncelle.aaw"

**Parametreler:** Güncellemek istediğiniz Müşteriye ait alanları Soru Cevap listesi olarak göndermeniz gerekmektedir. Gönderdiğiniz alanlar güncellenecektir diğer alanlarda herhangibir değişiklik yapılmayacaktır. Soru cevap Listenizde "fPrkMus" alanı ile müşteri numarasının belirtilmesi zorunludur.

##### Örnek İstek:

    [[
    {Soru:"fPrkMus",Cevap:"19829"},
    {Soru:"fMusAdi",Cevap:"zerrin.."},
    ...
    ]]

##### Örnek Cevap:

    {
        "Prk": 19829,
        "Basarili": true,
        "Mesaj": null
    }

###10. Ek Servisler

Sistemdeki bazı sabitlerin değerlerinin alınabilmesi için hazırlanmış bazı fonksiyonlar ve tablolar vardır.

#### Sigorta Şirketleri

_Link:_ "http://localhost/ada/CariSabitleri.SigortaSirketleri.aaw"

_Parametreler:_ parametre almamaktadır.

##### Örnek İstek:

    []

##### Örnek Cevap:

    [
         {
            "PrkSir": 54,// adayazılımın verdiği şirket kodu
            "BirlikKod": 5,//Birlik şirket Kodu
            "SirKod": "AIG",//Şirket Kodu
            "SirAdi": "AIG SİGORTA" // Şirket Adı
        }                              
    ]

#### Araç Kullanım Tarzları

_Link:_ "http://localhost/ada/CariSabitleri.AracKullanimTarzlari.aaw"

_Parametreler:_ parametre almamaktadır.

#####Örnek İstek:

    []

#### Örnek Cevap:

    [
        {
            "TarzKodu": 16,// adayazılımın verdiği Tarzkodu
            "TarzAdi": "Çekici"// tarz adı
        },
         ...
    ]

#### Branşlar

Acente sisteminde tanımlı branş bilgilerinin alınmasını sağlayan servistir.

_Link:_ "http://localhost/ada/CariSabitleri.Branslar.aaw"

_Parametreler:_ parametre almamaktadır.

##### Örnek İstek:

    []

##### Örnek Cevap:

    [
       {
            "fPrkBrn": 1100100,
            "fBrnKod": "100",// adayazılımın verdiği Branş Kodu
            "fAltBrnKod": "100",// adayazılımın verdiği Alt Branş Kodu
            "fSirBrnkod": "1350",//Şirketin verdiği BranşKodu
            "fBrnAdi": "YANGIN KOMBİNE",// adayazılımın verdiği Branş Adı
            "fDomPolGrp": "YNG",// adayazılımın verdiği Branş Grubu
            "fFrkSir": "1",// adayazılımın verdiği Şirket kodu
            "fAcoBrnAd2": "YANGIN",//Acentenin Verdiği Branş Adı 2
            "fAcoBrnKod": "YNG",//Acentenin Verdiği Branş Kodu
            "fAcoBrnAdi": "YANGIN"//Acentenin Verdiği Branş Adı
        }
    ]

### Şirket Branşlarının Tanımlarını Al

Şirket branşlarındaki Teminat tanımlarınınalınmasını sağlayan servistir.

_Link:_ "http://localhost/ada/CariSabitleri.SirketBranslarininTanimlariniAl.aaw"

_Parametreler:_ adayazılımın verdiği Şirket kodu ve adayazılımın verdiği Branş Kodu

#### Örnek İstek:

    ['1','100']

#### Örnek Cevap:

    [
        {
            "fPrkTei": 1,
            "fFrkBrn": "1100100",
            "TAdi": "YANGIN BİNA",
            "tKodu": "011",
            "fBina": true,
            "fEsya": false,
            "fAracTem": false
        },
        ...
    ]

###11. Sistem Ek Özellikleri

##### Aynı Oturumda Birden Fazla İstekde Bulunma

Aynı oturumda ".aaw" uzantısı ile çağıracağınız iki istek sırayla çalışmaktadır. Aynı anda yapacağınız istekleriniz için ".aaws" uzantısı ile istekte bulunabilirsiniz(".aaws" uzantısı session yazım izni olmadığından, bazı servislerde hata verebilir).

##### Birden Fazla Cari Veritabanı Kulanma

Bazı acentelerimiz Cari programda birden fazla veritabanı kullanmaktadır. Farklı veritabanlarında işlem yapmak için, isteklerinize Headers olarak "VeritabaniNumarasi" değerini eklemeniz gerekmektedir. Alabileceği değerler acenteye göre değişikilk gösterdiğinden, bu bilgileri, acenteniz aracılığı ile adayazılım dan öğrenebilirsiniz. Gerekirse tanımlama işlemleride yapılarak size bilgi verilecektir.

###12. Alanlar ve Açıklamaları

##### Poliçe Alanları ve Karşılıkları

| Genel Alanlar |
| --- |
| fPrkPol | Adayazılımın verdiği poliçe numarası |
| fTnzTar | Tanzim tarihi |
| fBasTar | Başlangıç tarihi |
| fBitTar | Bitiş tarihi |
| Brans | Adayazılımın verdiği Branş |
| PolGrp | Adayazılımın verdiği Poliçe grubu |
| fSirPolNo | Şirketin Verdiği Poliçe Numarası |
| Tecdit\_no | Tecdit Numarası |
| Zeyl\_no | Zeyil Numarası |
| fFrkSir | Adayazılımın verdiği şirket Kodu |
| fFrkMus | Müşteri Numrası |
| fFrkTa | Tali Müşteri Numarası |
| fFrkSat | Satıcı Müşteri Numarası |
| fFrkSor | Sorumlu Müşteri Numarası |
| SigAdi | Şirket Adı |
| Plaka | Plaka |
| fTeklifDrm | Teklif Durumu |
| fYrlkDrm | Yürürlük Durumu |
| fPolTek | Poliçe Sınıfı |
| fPolTip | Poliçe Tipi |
| fVerKimNo | Vergi Numarası |
| fTCKimNo | TC Kimlik Numarası |
| fFrkMizBlg | Müşterinin Bölgesi |
| fBrtPrm | Bürüt Prim |
| RizIl | Riziko İl |
| RizIlce | Riziko İlçe |
| fPolAltGrp | Alt Brans Grubu (örn; KNT) |

| Ek Alanlar |
| --- |
| feposta | Eposta Adresi |
| ftelno | Telefon Numarası |
| SirketAdi | Şirket Adı |
| fsigdogtar | Sigortalı Doğum Tarihi |
| fsigetdtar | Sigorta Ettiren Doğum Tarihi |

| Trafik Kasko Ek Alanları |
| --- |
| fegmblgno | EgmBelge Numarası/Asbis numarası |
| fArcKod | Araç Kodu |
| Marka | Araç Marka |
| Model | Araç Model |
| ModYil | Araç Model Yılı |

| Dask Ek Alanları |
| --- |
| fTopKatSay | Toplam Kat Sayısı |
| fBrtM2 | Bürüt Metre Kare |
| fInsYil | İnşaat Yılı |
| fuavtadres | UAVT adres Kodu |
| fRizDaire | Riziko Adresi |
| fDskPolNo | Dask Poliçe Numarası |

| Bes Ek Alanları |
| --- |
| fTaksitTut | Taksit Tutarı |
| fFonTutar | Fon Tutarı |
| fEkKatPay | Aylık Katkı Payı |
| fBasKatPay | Başlangıç Katkı Payı |
| fDevAidat | Devreden Katkı Payı |
| fYilPrm | Yıllık Prim |
| fBesOdeSek | Ödeme Şekli |
| fTakBnkSic | Takas Bank Sicil Numarası |
| fSozFonTut | Fon Dağılımı |

##### Müşteri Alanları ve Karşılıkları

| Genel Alanlar |
| --- |
| fPrkMus | Müşteri Numarası |
| fMusAdi | Adı |
| fMusSoyadi | Soyadı |
| fMusTip | Müşeri Tip |
| fKulHesKod |   |

| Ek Alanlar |
| --- |
| fmuskod | Müşteri Kodu |
| fMusUnv | Ünvanı |
| fMusKimNo | VergiNumarası |
| fMusTcKimN | TC Kimlik Numarası |
| fmuscins | Müşteri Cinsi |
| fKisiFirma | Tüzel/Gerçek |
| fMusHesKod | Muhasebe Hgesa Kodu |
| fMusBabaAd | Baba Adı |
| fMusUyruk | Uyruk |
| fMusAdr1 | Adres 1 |
| fMusAdr2 | Adres 2 |
| fmah | Mahalle |
| faptadi | Apartman Ad |
| fsemt | Semt Ad |
| filKodu | İl Kodu |
| fMusIlce | İlçe Adı |
| fmusemail | E-Posta |
| fMusEvTel | Ev Telefonu |
| fMusFax | Fax |
| fMusTel | Telefon |
| fTel1Aci | Telefon 1 Açıklaması |
| fMusTel2 | Telefon 2 |
| fTel2Aci | Telefon 2 Açıklaması |
| fmusemail | Eposta Adresi |
| fIntntMus | İnternet Müşterisi mi(1/0) |

##### Bazı alanlar ve Alabildiği Değerler

##### PolGrp

| Poliçe Grubu | Kod |
| --- | --- |
| Bireysel Emeklilik | BES |
| Dask | DSK |
| Hayat | HAY |
| Kasko | KKO |
| Kaza | KZA |
| Mühendislik | MHE |
| Nakliyet | NAK |
| Sağlık | SAG |
| Trafik | TRF |
| Yangın | YNG |

##### TeklifDurumu

| Teklif Durumu | Kod |
| --- | --- |
| Ayarlanmadı | 0 |
| Teklif Verildi | 1 |
| Teklif Onaylandı | 2 |
| Teklif Onaylanmadı | 3 |
| Poliçe Yapıldı | 4 |

##### FyrlkDrm

| Yürürlük Durumu | Kod |
| --- | --- |
| Yürürlükte | 0 ve 1 |
| Yürürlükte Değil | 2 ve 3 |

##### fPolTek

| Poliçe Sınıfı | Kod |
| --- | --- |
| Ayarlanmadı | 0 |
| Poliçe | 1 |
| Teklif | 2 |
| Potansiyel  | 3 |
| Teklif Öncesi | 4 |

##### FfrkTt

| Tecdit Tipi | Kod |
| --- | --- |
|   |   |

Bu alan kullanılmamaktdır.

##### FpolTip

| Poliçe Tipi | Kod |
| --- | --- |
|   |   |

Bütün acentelerde kullanılmamakta, acenteniz kullanıyorsa acentenizden bilgi alabilirsiniz.

##### Cinsiyet

| Cinsiyet | Kod |
| --- | --- |
| Erkek | E |
| Kadın | K |
| Bilinmiyor |   |

##### Sigortalı Yakınlık

| Yakınlık | Kod |
| --- | --- |
| Kendisi | 1 |
| Eşi | 2 |
| Çocuğu | 3 |
| Bilinmiyor |   |

##### fKisiFirma

| Kişi / Firma | Kod |
| --- | --- |
| Şahıs | 1 |
| Firma | 2 |
| Bilinmiyor | 3 |

##### fMedDrm

| Kişi / Firma | Kod |
| --- | --- |
| Ayrı | 1 |
| Bekar | 2 |
| Dul | 3 |
| Evli | 4 |
| Bilinmiyor | 5 |

##### fMusTip

| Müşteri Tipi | Kod |
| --- | --- |
| Müşteri | 1 |
| TaliAcente | 2 |
| Satıcı | 3 |
| Sorumlu | 4 |
| Tahsildar | 5 |
| PoliceKesen | 6 |
| Bolge | 7 |
| Grup | 8 |
| Diger | 9 |

##### fBesOdeSek

| Bes Ödeme Şekli | Kod |
| --- | --- |
| Yıllık | 1 |
| Altı Aylık | 2 |
| Üç Aylık | 3 |
| Aylık | 4 |