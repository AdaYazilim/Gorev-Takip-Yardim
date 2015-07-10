# Ada Yazılım Görev Takip WEB API

Sistemimiz, linklere gerekli parametrelerin json yapısında gönderilmesi üzerinde kuruludur. Login gerekli olan işlemler için öncelikle login isteğine başarılı cevap almalısınız, ardından yetki gerektiren işlemi yapabilirsiniz. Dikkat edilmesi gereken konu ise bu işlemlerin aynı sessionda yapılmasıdır.

1.  ## Kullanıcı Girişi

Yetkiye bağlı servisleri çağırabilmeniz için login işlemini yapmış olmanız gerekmektdir. Dikkat edilmesi gereken iki nokta vardır. Bir, kullanıcı adı diğer sistemlerle farklılık gösterebilmektedir. İki, şifrenizi “sha256” ile şifreleyerek göndermelisiniz.

<font color="#222222"><font face="Calibri Light, serif"><font size="3">**<span style="background: #ffffff">Link:</span>**</font></font></font> "http://www.gorevtakip.com/Index.Login.iam"

<font color="#222222"><font face="Calibri Light, serif"><font size="3">**<span style="background: #ffffff">Parametreler:</span>**</font></font></font> KullanıcıAdı ve Kullanıcı şifresi (Bu bilgileri acenteden temin edebilirsiniz) .

### <a name="_GoBack"></a>Örnek İstek:

<font size="1" style="font-size: 8pt"><font size="1" style="font-size: 8pt">["kullaniciAdi","Sifre"]</font></font>

<font color="#222222"><font face="Calibri Light, serif"><font size="3">**<span style="background: #ffffff">Örnek Cevap:</span>**</font></font></font>

<font size="1" style="font-size: 8pt"><font size="1" style="font-size: 8pt">{"Basarili":true,"Mesaj":""}</font></font>

1.  ## Yeni İş Başlat

Yeni iş başlatmak istediğinizde bu fonksiyonu kullanabilirsiniz. Dikkat edilmesi gereken Elemanların başlatılmak istenen işe göre değişiklik göstereceğidir. Elemanların listesini acentenizden temin edebilirsiniz.

<font color="#222222"><font face="Calibri Light, serif"><font size="3">**<span style="background: #ffffff">Link:</span>**</font></font></font> " http://www.gorevtakip.com/YeniAkis.IsiYarat.iam"

<font color="#222222"><font face="Calibri Light, serif"><font size="3">**<span style="background: #ffffff">Parametreler:</span>**</font></font></font> YeniIs Nesnesi

<font color="#222222"><font face="Calibri Light, serif"><font size="3">**<span style="background: #ffffff">Örnek İstek:</span>**</font></font></font> <span style="background: #ffffff"> </span>

<font size="1" style="font-size: 8pt">{</font>

<font size="1" style="font-size: 8pt">'GenelBilgiler': {</font>

<font size="1" style="font-size: 8pt">'TanimAd': 'Teklif Ver',</font>

<font size="1" style="font-size: 8pt">'Baslik': ' '34ABC789 - HALK SİGORTA A.Ş -Trafik',</font>

<font size="1" style="font-size: 8pt">'DeadlineTarih': '2015-06-11',</font>

<font size="1" style="font-size: 8pt">'DeadlineSaat': '01:47',</font>

<font size="1" style="font-size: 8pt">'Oncelik': 7,</font>

<font size="1" style="font-size: 8pt">'Baslatan': 'KullaniciAdi',</font>

<font size="1" style="font-size: 8pt">'Elemanlar': [{</font>

<font size="1" style="font-size: 8pt">'KisaAd': 'Sirket',</font>

<font size="1" style="font-size: 8pt">'Deger': '015',</font>

<font size="1" style="font-size: 8pt">'UzunDeger': 'HALK SİGORTA A.Ş.'</font>

<font size="1" style="font-size: 8pt">}</font>

<font size="1" style="font-size: 8pt">]</font>

<font size="1" style="font-size: 8pt">},</font>

<font size="1" style="font-size: 8pt">'IlkFaaliyet': {</font>

<font size="1" style="font-size: 8pt">'Tamamlayan': 'KullaniciAdi',</font>

<font size="1" style="font-size: 8pt">'Elemanlar': [{</font>

<font size="1" style="font-size: 8pt">'KisaAd': 'SirketAd',</font>

<font size="1" style="font-size: 8pt">'Deger': 'HALK SİGORTA A.Ş.',</font>

<font size="1" style="font-size: 8pt">'UzunDeger': 'HALK SİGORTA A.Ş.'</font>

<font size="1" style="font-size: 8pt">}, {</font>

<font size="1" style="font-size: 8pt">'KisaAd': 'Plaka',</font>

<font size="1" style="font-size: 8pt">'Deger': '34ABC789',</font>

<font size="1" style="font-size: 8pt">'UzunDeger': '34ABC789'</font>

<font size="1" style="font-size: 8pt">}, {</font>

<font size="1" style="font-size: 8pt">'KisaAd': 'KimlikNo',</font>

<font size="1" style="font-size: 8pt">'Deger': '12345678912',</font>

<font size="1" style="font-size: 8pt">'UzunDeger': '12345678912'</font>

<font size="1" style="font-size: 8pt">}]</font>

<font size="1" style="font-size: 8pt">}</font>

<font size="1" style="font-size: 8pt">}</font>

### Örnek Cevap:

Sonuç başarılı ise dönen mesaj değeri kaydedilen iin ID sini döndürür.

<font size="1" style="font-size: 8pt">{"Basarili":true,"Mesaj":"124563"}</font>

1.  ## Veri Yapıları

### YeniIs

<font size="1" style="font-size: 8pt">{</font>

<font size="1" style="font-size: 8pt">**GenelBilgiler** GenelBilgiler,</font>

<font size="1" style="font-size: 8pt">**Faaliyet** IlkFaaliyet</font>

<font size="1" style="font-size: 8pt">}</font>

### GenelBilgiler

<font size="1" style="font-size: 8pt">{</font>

<font size="1" style="font-size: 8pt">**String** TanimAd, (Başlatılacak İşin Tanım Adı (Acenteden Alabilirsiniz.))</font>

<font size="1" style="font-size: 8pt">**String** Baslik,</font>

<font size="1" style="font-size: 8pt">**String** DeadlineTarih,</font>

<font size="1" style="font-size: 8pt">**String** DeadlineSaat</font>

<font size="1" style="font-size: 8pt">**İnt** Oncelik,</font>

<font size="1" style="font-size: 8pt">**String** Baslatan, (Kullanıcı Adı)</font>

<font size="1" style="font-size: 8pt">**Eleman[]** Elemanlar</font>

<font size="1" style="font-size: 8pt">}</font>

### Faaliyet

<font size="1" style="font-size: 8pt">{</font>

<font size="1" style="font-size: 8pt">**String** Tamamlayan, (Kullanıcı Adı)</font>

<font size="1" style="font-size: 8pt">**Eleman[]** Elemanlar</font>

<font size="1" style="font-size: 8pt">}</font>

### Eleman

<font size="1" style="font-size: 8pt">{</font>

<font size="1" style="font-size: 8pt">**String** KisaAd,</font>

<font size="1" style="font-size: 8pt">**String** Deger,</font>

<font size="1" style="font-size: 8pt">**String** UzunDeger</font>

<font size="1" style="font-size: 8pt">}</font>

<div type="FOOTER">

<sdfield type="PAGE" subtype="RANDOM" format="PAGE">5</sdfield> 29.06.2015

</div>