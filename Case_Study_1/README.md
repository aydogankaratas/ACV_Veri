# 💳 Kredi Kartı Müşteri Analizi - Aktifbank

[![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)

> Aktifbank müşteri verisi üzerinde gerçekleştirilen kapsamlı Excel analiz projesi


## 🎯 Proje Hakkında

Bu proje, Aktifbank'a ait gerçek kredi kartı müşteri verisi kullanılarak hazırlanmış kapsamlı bir Excel analiz çalışmasıdır. Proje kapsamında:

- Müşteri segmentasyonu ve profilleme
- Churn (müşteri kaybı) analizi
- Gelir ve harcama davranış analizleri
- İnteraktif dashboard ve senaryo planlaması

gerçekleştirilmiştir.


## 📊 Veri Seti

| Özellik | Değer |
|---------|-------|
| **Kaynak** | Aktifbank (Gerçek Veri) |
| **Müşteri Sayısı** | 10,127 |
| **Sütun Sayısı** | 23 |
| **Veri Tipi** | CSV |

### Veri Yapısı

Veri seti aşağıdaki ana kategorileri içermektedir:

- **Demografik Bilgiler**: Yaş, cinsiyet, eğitim seviyesi, medeni durum
- **Finansal Bilgiler**: Gelir kategorisi, kredi limiti, kullanılabilir limit
- **Davranışsal Bilgiler**: İşlem sayısı, işlem tutarı, aylık ortalama harcama
- **İlişki Bilgileri**: Müşteri kıdemi, kart kategorisi, ilişki sayısı
- **Churn Flag**: Existing Customer (Mevcut) / Attrited Customer (Ayrılan)

## 🔍 Analiz Adımları

### 1️⃣ Veri Hazırlama ve Temizleme


Kullanılan Teknikler:
- TRIM, CLEAN, PROPER ile veri standartlaştırma
- Null değer kontrolü ve doldurma
- Duplicate kayıt temizleme
- Veri tipi düzenleme


### 2️⃣ Veri Dönüştürme

- **Yaş Grupları**: 25-35, 36-45, 46-65, 56+
- **Müşteri Kıdem Kategorisi**: 0-2 yıl, 2-4 yıl, 4+ yıl
- **Kredi Kullanım Seviyesi**: Düşük, Orta, Yüksek
- **Gelir Kategorisi**: <40K, 40K-60K, 60K-80K, 80K-120K, 120K+

### 3️⃣ Pivot Tablo Analizleri

- Gelir kategorisine göre ortalama kredi limiti
- Yaş ve cinsiyet bazında müşteri dağılımı
- Eğitim seviyesi vs. Gelir karşılaştırması
- Top 10 en yüksek harcama yapan müşteriler
- Müşteri segmenti bazında işlem tutarı analizi

### 3️⃣ Müşteri Segmentasyon Metodolojisi

Müşteriler, iki temel boyut üzerinden altı farklı segmente ayrılmıştır:

#### 📊 Segmentasyon Matrisi

| Harcama Seviyesi ↓ | Kullanım Oranı → | Düşük/Orta | Yüksek |
|-------------------|------------------|------------|---------|
| **Yüksek** | | Değerli - Sağlıklı | Değerli - Riskli |
| **Orta** | | Orta Değer | Orta - Riskli |
| **Düşük** | | Düşük Değer | Düşük - Potansiyel Risk |

#### 🎯 Segmentasyon Kriterleri

**Boyut 1: Aylık Ortalama Harcama Seviyesi (Monthly_Avg_Spend_Level)**
- **Yüksek**: Aylık harcama > 1000
- **Orta**:  Aylık harcama 500-1000 arası
- **Düşük**: Aylık harcama < 500

**Boyut 2: Kullanım Oranı (Avg_Utilization_Level)**
- **Düşük/Orta**: Kredi kullanım oranı düşük (sağlıklı kullanım)
- **Yüksek**: Kredi limitinin büyük kısmı kullanılıyor (potansiyel risk)


### 4️⃣ Senaryo Analizleri

| Araç | Kullanım Alanı |
|------|----------------|
| **Goal Seek** | Hedef gelir için gerekli müşteri sayısı |
| **Solver** | Kampanya bütçesi optimizasyonu |
| **Scenario Manager** | İyimser/Kötümser/Baz senaryo karşılaştırması |
| **Data Table** | Limit artışının işlem hacmine etkisi |

## 📈 Dashboard Özellikleri

### Temel Metrikler (KPI)

-  Toplam Müşteri Sayısı: **10,127**
-  Toplam İşlem Hacmi: **₺44.6M**
-  Churn Oranı: **16.07%**
-  Ortalama Kredi Limiti: **₺8,618**
-  Ortalama Kullanım Oranı: **27.5%**

### İnteraktif Özellikler

- Slicer ile dinamik filtreleme (Cinsiyet, Yaş Grubu, Gelir Kategorisi)
- Dinamik grafik başlıkları
- Conditional formatting ile KPI takibi

### Görselleştirmeler

- Waterfall Chart: Müşteri segmenti dağılımı
- Combo Chart: İşlem sayısı vs. Tutar
- Funnel Chart: Gelir kategorisi hiyerarşisi
- Line Chart: Limit artış senaryosu etkisi


## 💡 Temel Bulgular

### Müşteri Segmentasyonu

| Segment | Müşteri Sayısı | Toplam Hacim | Avg. İşlem |
|---------|----------------|--------------|------------|
| Değerli - Sağlıklı | 735 | ₺10.8M | ₺62,61 |
| Değerli - Riskli | 11 | ₺158K | ₺3,232 |
| Orta Değer | 686 | ₺5.5M | ₺15,001 |
| Orta - Riskli | 18 | ₺141K | ₺2,562 |
| Düşük Değer | 5,086 | ₺15.6M | ₺10,319 |
| Düşük - Potansiyel Risk | 3,591 | ₺12.4M | ₺3,119 |

### Churn Analizi

- **Genel Churn Oranı**: %16.07 (1,627 müşteri)
- **En Yüksek Risk Grubu**: Orta Gelir % 32.80
- **En Sadık Grup**: Değerli - Sağlıklı, Değerli - Riskli, Orta - Riskli


---

## 🙏 Teşekkürler

- Aktifbank'a veri seti için
- Ahmet Çalık Vakfı: Eğitim programı için

