# 1.Ada Yazılım Acente Cari WEB API

Sistemimiz, linklere gerekli parametrelerin json yapısında gönderilmesi üzerinde kuruludur. Login gerekli olan işlemler için öncelikle login isteğine başarılı cevap almalısınız, ardından yetki gerektiren işlemi yapabilirsiniz. Dikkat edilmesi gereken konu ise bu işlemlerin aynı sessionda yapılmasıdır.

###1. Kulanıcı Girişi

Login Linki:" [http://localhost/ada/Login.GirisYap.aaw](http://localhost/ada/Login.GirisYap.aaw)"

Parametreler; KullanıcıAdı ve Kullanıcı şifresi (Bu bilgileri acenteden temin edebilirsiniz.)

#####Örnek İstek:
["kullaniciAdi","Sifre"]

#####Örnek Cevap:  
{"Basarili":true,"Mesaj":""}

###1. Poliçe Arama

Poliçe Arama Linki: " [http://localhost/ada/Police.PoliceAra.aaw](http://localhost/ada/Police.PoliceAra.aaw)"

Parametreler: Query (Bu bilgi " **PoliceNo/SigortalıAdı/KimlikNo/Plaka/Marka**"  alanları için geçerlidir. yazacağınız query bilgisi bu alanlarla karşılaştırılır ve uygun kayıtlar getirilir.)

#####Örnek İstek:  
["0330011122"]

#####Örnek Cevap:

     [{

     "FprkPol":176529, //Cari veritabanında kayıtlı poliçe keyidir.

     "Tanzim":"2015-03-24T00:00:00", //Poliçe Tanzim Tarihidir.

     "Baslangic": "2015-03-20T00:00:00", //Poliçe Başlangıç Tarihidir.

     "Bitis": "2015-03-20T00:00:00", //Poliçe Bitiş Tarihidir.

     "Brans":"412", // Cari veritabanında Tanımlı Poliçe Brans Kodudur.

     "PolGrp":"NAK", // Poliçe Grubudur.

     "PoliceNo": "24370032", //Şirket Poliçe Numarasıdır.

     "TecditNo":"", //Şirket Tecdit Numarasıdır.

     "ZeyilNo": "1", //Şirket Zeyil Numarasıdır.

     "FfrkSir": 26, //Cari veritabanında kayıtlı Şirket Kodudur.

     "FfrkMus": 73376, //Cari veritabanında kayıtlı Müşteri keyidir.

     "Sigortali": "AK-PA TEKSTİL İHRACAT PAZARLAMA A.Ş.",Poliçede Kayıtlı Sigortalı Adıdır.

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

### Bazı alanlar ve Alabildiği Değerler

#####PolGrp

|Poliçe Grubu | Kod |
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

#####TeklifDurumu

| Teklif Durumu | Kod |
| --- | --- |
| Ayarlanmadı | 0 |
| Teklif Verildi | 1 |
| Teklif Onaylandı | 2 |
| Teklif Onaylanmadı | 3 |
| Poliçe Yapıldı | 4 |

#####FyrlkDrm

| Yürürlük Durumu | Kod |
| --- | --- |
| Yürürlükte | 0 ve 1 |
| Yürürlükte Değil | 2 ve 3 |



#####PolTek

| Poliçe Sınıfı | Kod |
| --- | --- |
| Ayarlanmadı | 0 |
| Poliçe | 1 |
| Teklif | 2 |
| Potansiyel        | 3 |



#####FfrkTt

| Tecdit Tipi | Kod |
| --- | --- |
|   |   |

Bu alan kullanılmamaktdır.

##### FpolTip

| Poliçe Tipi | Kod |
| --- | --- |
|   |   |

Bütün acentelerde kullanılmamakta, acenteniz kullanıyorsa acentenizden bilgi alabilirsiniz.