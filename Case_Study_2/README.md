# 📊 Enerji Perakende Veri Analizi Case Study

## 🎯 Proje Hakkında

Bu proje, **Ahmet Çalık Vakfı İleri Veri Analitiği Eğitimi** kapsamında hazırlanmış olan gerçek enerji sektörü verilerine dayalı kapsamlı bir veri analizi çalışmasıdır. Amasya ili ve ilçelerindeki (Hamamözü, Gümüşhacıköy, Göynücek) elektrik tüketim ve tahsilat verileri kullanılarak müşteri davranışları, mevsimsel trendler ve ödeme alışkanlıkları analiz edilmiştir.

**Veri Dönemi:** Ocak 2023 - Temmuz 2025  
**Toplam Kayıt:** ~2.74M kayıt  
**Müşteri Sayısı:** ~28,299 benzersiz müşteri  
**Analiz Aracı:** Python (Pandas, Matplotlib, Seaborn, Scikit-learn)

---

## 📁 Proje Yapısı

```
case_study_02/
├── README.md                              # Proje dokümantasyonu    
├── notebooks/
│   ├── notebook_01_veri_kesfi.ipynb      # Veri keşfi ve tanımlayıcı istatistik
│   ├── notebook_02_gorsellestirme.ipynb  # Görselleştirme ve karşılaştırmalı analiz
│   └── notebook_03_veri_hikayesi.ipynb   # Müşteri segmentasyonu ve veri hikayesi
---
```

## 📊 Veri Seti Genel Bakış

### Veri Kaynakları

| Sayfa | Açıklama | Kayıt Sayısı | Ana Sütunlar |
|-------|----------|--------------|-------------|
| **Tahsilat** | Ödeme işlemleri | 636,993 | Şube, İlçe, Tahsilat Tarihi, Ödeme Tutarları |
| **Tahsilat 1** | Fatura bazlı ödeme zamanlaması | 917,632 | Mali Yıl/Dönem, Hesap Sınıfı, Zamanında/Geç Ödeme |
| **Tahakkuk** (Hamamözü) | Elektrik tüketimi | 124,818 | Tarih, kWh, Hesap Sınıfı |
| **Tahakkuk 1** (Gümüşhacıköy) | Elektrik tüketimi | 765,657 | Tarih, kWh, Hesap Sınıfı |
| **Tahakkuk 2** (Göynücek) | Elektrik tüketimi | 295,223 | Tarih, kWh, Hesap Sınıfı |

### Temel İstatistikler

- **Ortalama Tüketim:** 92.6 kWh (Medyan: 46.6 kWh)
- **Mesken Oranı:** %86.6
- **Zamanında Ödeme Oranı:** %69.2
- **Banka Tahsilatı Oranı:** %98.7

---

## 🔍 Analiz Aşamaları

### 📘 Notebook 01: Veri Keşfi ve Tanımlayıcı İstatistik

**Amaç:** Veri kalitesini değerlendirmek ve temel istatistikleri çıkarmak

**Gerçekleştirilen Analizler:**
- ✅ Veri setlerinin yüklenmesi ve yapısal incelemesi (`.info()`, `.describe()`, `.head()`)
- ✅ Veri tiplerinin düzenlenmesi (kategorik, datetime, numeric dönüşümleri)
- ✅ Eksik veri analizi ve yorumlama
- ✅ İlçe bazlı benzersiz müşteri sayısı hesaplama
- ✅ Tahakkuk verilerinin birleştirilmesi (`pd.concat`)
- ✅ Negatif ve aykırı tüketim değerlerinin tespiti (IQR yöntemi)
- ✅ Hesap sınıfına göre toplulaştırma analizi

**Önemli Bulgular:**
- Toplam **48,554 outlier** tespit edildi (%4.09)
- **Karayolları Aydınlatma** hesap sınıfı en yüksek ortalama tüketime sahip (30,203 kWh)
- Mesken aboneleri en homojen tüketim davranışını sergiliyor
- 899 müşteriye ait tahsilat kaydı eksik (veri kalitesi uyarısı)

---

### 📗 Notebook 02: Veri Görselleştirme ve Karşılaştırmalı Analiz

**Amaç:** İlçeler, hesap sınıfları ve zaman boyutunda karşılaştırmalı analiz yapmak

**Gerçekleştirilen Analizler:**
- 📊 İlçelere göre hesap sınıfı dağılımları (oransal karşılaştırma)
- 📈 Aylık ve mevsimsel tüketim trendleri (line chart)
- 🏦 Tahsilat işlemlerinin şube ve ilçe bazlı dağılımı (bar chart)
- 💳 Zamanında ve geç ödeme oranları (pie chart analizi)
- 📦 kWh tüketim dağılımı (histogram ve box plot)

**Önemli Bulgular:**
- **Temmuz ayı** tüm ilçelerde en yüksek tüketim dönemi (133.85 kWh ortalama)
- **Göynücek** en yüksek mevsimsel oynaklığa sahip (Kış/Yaz farkı: %45.9)
- **Hamamözü** dengeli tüketim profili sergiliyor (yıl boyunca ~70 kWh)
- **Gümüşhacıköy** hem yüksek tüketim hem yüksek abone sayısına sahip
- Ödeme işlemlerinin %98.7'si banka kanalıyla gerçekleşiyor

---

### 📕 Notebook 03: Veri Hikayesi Anlatımı - Açık Uçlu Analiz

**Amaç:** İş değeri yaratacak derinlemesine analizler ve müşteri segmentasyonu

#### 🔹 İlçe Karşılaştırma Analizi

**Bulgular:**

| İlçe | Ort. Tüketim | Medyan | Kayıt Sayısı | Zamanında Ödeme |
|------|--------------|--------|--------------|-----------------|
| **Gümüşhacıköy** | 97.34 kWh | 48.31 kWh | 765,657 (%65) | %69.06 |
| **Göynücek** | 89.67 kWh | 45.09 kWh | 295,223 (%25) | %62.42 |
| **Hamamözü** | 70.87 kWh | 40.56 kWh | 124,818 (%10) | %68.48 |

**Kritik İçgörüler:**
- Ortalama ve medyan arasındaki fark, **yüksek tüketimli az sayıda abonenin** ortalamayı yukarı çektiğini gösteriyor
- Gümüşhacıköy'de **kamu idareleri** ve Göynücek'te **tarımsal faaliyetler** aykırı tüketim kaynağı
- Hamamözü'nün düşük tüketimi, **%88.9 mesken abone** oranından kaynaklanıyor

---

#### 🔹 Müşteri Segmentasyonu (K-Means Clustering)

**Metodoloji:**
- **Değişkenler:** Ortalama tüketim, tüketim std sapması, zamanında ödeme oranı, ortalama gecikme
- **Ön İşleme:** Winsorization (%1-%99 percentile), StandardScaler normalizasyonu
- **Küme Sayısı:** Elbow Method ile 4 segment belirlendi
- **Algoritma:** K-Means clustering

**Segmentler ve Karakteristikleri:**

| Segment | Müşteri Sayısı | Oran | Ort. Tüketim | Zamanında Ödeme | Risk Durumu |
|---------|----------------|------|--------------|-----------------|-------------|
| **Orta Tüketim - Düzenli** | 19,375 | %68 | Orta | Yüksek | Düşük Risk ✅ |
| **Riskli Müşteriler** | 7,509 | %27 | Orta-Düşük | Düşük | Yüksek Risk ⚠️ |
| **Düşük Tüketim - İyi** | 957 | %3 | Düşük | Yüksek | Düşük Risk ✅ |
| **Yüksek Tüketim - Riskli** | 449 | %2 | Çok Yüksek | Düşük | Kritik Risk 🚨 |

---

#### 🔹 Segmentlerin İlçelere Göre Dağılımı

**Göynücek:**
- En yüksek riskli müşteri oranı (%32)
- Özellikle tarımsal sulama kaynaklı yüksek tüketim

**Gümüşhacıköy:**
- En yüksek düzenli müşteri oranı
- Riskli segment %25 ile en düşük

**Hamamözü:**
- Göynücek'e benzer risk profili (%31 riskli müşteri)
- Daha küçük abone tabanı

---

## 📊 Önemli Bulgular Özeti

### Tüketim Davranışı
- 🔴 **Yaz ayları kritik:** Temmuz'da ortalama tüketim %60+ artıyor
- 🔵 **İlçe farklılıkları:** Gümüşhacıköy > Göynücek > Hamamözü
- 🟢 **Hesap sınıfı:** Mesken %86.6, geri kalanı ticari ve tarımsal

### Ödeme Davranışı
- ✅ %69.2 zamanında ödeme (iyi performans)
- ⚠️ %27.2 gecikmeli ödeme (takip gerektirir)
- ❌ %2.55 hiç tahsilat yok (veri kalitesi sorunu)

### Müşteri Segmentasyonu
- 💚 %68 düzenli müşteri (portföy çekirdeği)
- 🟡 %27 riskli müşteri (tahsilat odağı)
- 🔴 %2 yüksek tüketim-riskli (kritik segment)


---

## 🙏 Teşekkürler

- **Çalık Enerji Yapay Zeka Ekibi:** Gerçek veri seti için
- **Ahmet Çalık Vakfı:** Eğitim programı için
- **Eğitmenler:** Rehberlik ve geri bildirimler için
