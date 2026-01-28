# 🔌 Elektrik Tüketim Verilerinde Anomali Analizi Case Study - YEDAŞ
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-FF6F00?style=for-the-badge&logo=microsoft&logoColor=white)

Power BI kullanılarak elektrik dağıtım şebekelerinde veri odaklı karar destek sistemleri geliştirerek operasyonel verimliliği artırmak amacıyla gerçekleştirilen kapsamlı anomali tespit ve analiz projesi.

Bu proje, elektrik abonelerine ait ölçüm verileri kullanılarak **normal dışı enerji tüketim davranışlarını tespit etmeyi** ve **operasyonel aksiyonlar için somut içgörüler üretmeyi** amaçlamaktadır.

 **Proje Hedefleri**

-  Normal dışı enerji tüketim davranışlarını tespit etmek
-  Olası kaçak kullanım, sayaç arızası veya şebeke problemi senaryolarını belirlemek
-  Analiz sonuçlarını yönetim kararlarını destekleyecek görsel çıktılara dönüştürmek

---


### 📊 Veri Seti

#### Veri Kaynağı
Elektrik sayaçlarından **her 15 dakikada bir** elde edilen ölçüm verileri (CSV formatında). Her kayıt bir abonenin 15 dakikalık elektriksel parametrelerini içerir.

#### Veri Alanları

##### Kimlik & Lokasyon
- `tesisat_no_id`: Tesisat numarası (benzersiz tanımlayıcı)
- `il`: İl bilgisi
- `ilce`: İlçe bilgisi
- `gerilim_seviyesi`: Gerilim seviyesi
- `marka`: Sayaç markası
- `model`: Sayaç modeli
- `abone_grubu`: Abone kategorisi (Ticari, Mesken, Sanayi vb.)
- `carpan_degeri`: Çarpan değeri

##### Elektrik Ölçümleri
- `l1, l2, l3`: Faz akımları (Amper)
- `v1, v2, v3`: Faz gerimleri (Volt)
- `t0`: Aktif enerji tüketimi (kWh)

##### Reaktif Değerler
- `ri`: İndüktif reaktif enerji
- `rc`: Kapasitif reaktif enerji

##### Zaman
- `load_profile_date`: Ölçüm tarihi ve saati (15 dakikalık aralıklar)

#### Veri Kalitesi
- **Gerilim alanlarında:** %21,3 eksik veri
- **Reaktif değerlerde:** Sınırlı eksiklik
- **Ölçüm frekansı:** Her 15 dakikada bir 
- **Toplam kayıt sayısı:** 354 Bin
- **Toplam anomali sayısı:** 88 Bin
- **Anomali oranı:** %24,8
- **Analiz edilen tesisat sayısı:** 74

---

### 🔬 Metodoloji

####  Veri Hazırlığı (Power Query)
Power Query Editor kullanılarak gerçekleştirilen veri ön işleme adımları:
- Eksik değer analizi ve imputation
- Negatif veya sıfır tüketim değerlerinin kontrolü ve değerlendirilmesi
- Tarih alanının datetime formatına çevrilmesi
- Veri tipi dönüşümleri ve standardizasyon

#### Feature Engineering (DAX)
DAX formülleri ile yeni metrikler oluşturuldu:
- `Ortalama_Akim`: (l1 + l2 + l3) / 3
- `Ortalama_Gerilim`: (v1 + v2 + v3) / 3
- `Faz_Dengesizligi`: max(l1, l2, l3) - min(l1, l2, l3)
- `Aktif_Tüketim_Farki`: Her 15 dk arası tüketim farkı
- `Saat_Dilimi`: Gece / Gündüz / Mesai Saati
- `Hafta_HaftaSonu`: Hafta içi / Hafta sonu ayrımı
- `Full_Location`: İl + İlçe birleşik konum

####  Anomali Tespiti (DAX Logic)
Çoklu koşul kontrollü DAX formülleri ile kural tabanlı anomali tespit sistemi geliştirildi.

---

#### 🚨 Anomali Tipleri

Projede **7 farklı anomali tipi** tespit edilmiştir:

| Anomali Tipi | Açıklama | Operasyonel Risk |
|--------------|----------|------------------|
| **Negatif Tüketim - Kritik** | Negatif veya sıfır aktif tüketim farkı | Sayaç ters çalışma, veri hatası |
| **Akım Var Tüketim Yok** | Akım ölçülüyor ancak tüketim kaydedilmiyor | Potansiyel kaçak kullanım |
| **Tüketim Var Akım Düşük** | Yüksek tüketim kaydı ancak düşük akım | Sayaç hatası/kalibrasyon sorunu |
| **Dengesiz Faz - Kritik** | Fazlar arası ciddi dengesizlik + yüksek akım | Ekipman arıza riski, yangın tehlikesi |
| **Gece Yüksek Tüketim** | Gece saatlerinde anormal yüksek tüketim | İzinsiz kullanım, güvenlik riski |
| **Tüm Fazlar Sıfır** | Tüm fazlarda sıfır akım | Sayaç arızası, bağlantı kopukluğu |
| **Normal** | Anomali tespit edilmedi | Risk yok |


---

### 🔍 Temel Bulgular

#### Anomali İstatistikleri
- **Toplam veri kaydı:** 354 Bin
- **Tespit edilen anomali:** 88 Bin kayıt
- **Genel anomali oranı:** %24,8
- **En yaygın anomali:** Gece Yüksek Tüketim (58,17%)

#### Bölgesel Dağılım
- **En yüksek anomali oranı:** ORDU ili (%46,6)
- **İlçe bazında lider:** Gölköy (ORDU)  %77,9
- **Toplam analiz edilen tesisat:** 74 adet

#### Abone Grubu Analizi
- **En riskli segment:** Tek Terimli Ticarethane AG
- **Toplam Top 10 tesisattaki anomali:** %6,7 (23.863 kayıt) 

#### Sayaç Analizi
- **MAKEL:** 60+ Bin anomali
- **LUNA:** 30+ Bin anomali
- Gerilim verisi eksikliği: %21,3

#### Zaman Bazlı Bulgular
- Gece saatlerinde (00:00-06:00) anomali yoğunluğu artışı
- Hafta içi anomali oranı %70,83

#### Anomali Dağılımı (%)
- **Gece Yüksek Tüketim:** %58,17 (51 Bin)
- **Negatif Tüketim - Kritik:** %35,37 (31 Bin)
- **Dengesiz Faz - Kritik:** %4,77 (4 Bin)
- **Diğer Anomaliler:**  %1,69%

---


#### 🙏 Teşekkürler

- YEDAŞ (Yeşilırmak Elektrik Dağıtım A.Ş.)'a veri seti için
- Ahmet Çalık Vakfı'na eğitim programı için
