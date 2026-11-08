# Spotify Ses Özellikleri ile Şarkı Popülerliği Analizi ve Tahmini

Bu depo, **Araştırma Yöntem ve Teknikleri** dersi dönem projesi kapsamında oluşturulmuştur.

- **Proje Adı:** Spotify Ses Özellikleri ile Şarkı Popülerliği Analizi ve Tahmini

## 1. Proje Konusu ve Problem
Dijital müzik platformlarında her gün binlerce şarkı yayımlanmaktadır. Bir şarkının teknik ses özelliklerinin (enerji, dans edilebilirlik, ses yüksekliği, tempo, akustiklik vb.) dinleyiciler tarafından beğenilmesini ve popülerlik puanını (0–100) ne kadar etkilediğini incelemek amacıyla bu proje konusu seçilmiştir.

## 2. Araştırma Sorusu ve Hipotezler
- **Araştırma Sorusu:** Spotify'daki şarkıların teknik ses özellikleri ile popülerlik puanı (0–100) arasında anlamlı bir ilişki var mıdır ve bu özelliklerle popülerlik tahmin edilebilir mi?
- **Hipotez (H1):** Şarkıların dans edilebilirlik, enerji ve ses yüksekliği değerleri arttıkça popülerlik puanı da artar; Random Forest modeli doğrusal regresyona göre popülerliği daha düşük hatayla tahmin eder.
- **Sıfır Hipotezi (H0):** Şarkıların ses özellikleri ile popülerlik puanı arasında anlamlı bir ilişki yoktur.

## 3. İncelenen Akademik Kaynaklar (Ön Literatür)
1. **Qiu vd. (2026)** - *Bayesian-Optimized Ensemble Learning for Music Popularity Prediction with Shapley-Based Interpretability*, Mathematics, 14(6), 946. ([DOI: 10.3390/math14060946](https://doi.org/10.3390/math14060946))
2. **Li, K. (2024)** - *Predicting song popularity in the digital age through Spotify's data*, Theoretical and Natural Science, 39(1), 68–75. ([DOI: 10.54254/2753-8818/39/20240600](https://doi.org/10.54254/2753-8818/39/20240600))
3. **Gulmatico vd. (2022)** - *SpotiPred: A Machine Learning Approach Prediction of Spotify Music Popularity by Audio Features*, IEEE ICPC2T 2022. ([DOI: 10.1109/ICPC2T53885.2022.9776765](https://doi.org/10.1109/ICPC2T53885.2022.9776765))

## 4. Kullanılacak Veri Seti ve Yöntem
- **Veri Seti:** Spotify Tracks Dataset (Maharshi Pandya - Kaggle / Hugging Face). 114.000 şarkı ve 20 sütun içermektedir. ([Veri Seti Linki](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset))
- **Yöntem:** Nicel araştırma ve ikincil veri analizi. Python (Google Colab) ortamında betimsel istatistik, korelasyon analizi ve Çoklu Doğrusal Regresyon ile Random Forest Regressor modelleri karşılaştırılacaktır.

---

## 5. UML Diyagramları ve Sistem Modellemesi (Ödev 3)

Kodlama aşamasına geçmeden önce sistemin aktörlerini, işleyiş akışını ve nesne yönelimli mimarisini planlamak amacıyla 3 temel UML diyagramı hazırlanmıştır:

### 5.1. Use Case Diagram (Kullanım Durumu Diyagramı)
Sistem sınırlarını, sistemle etkileşime giren aktörleri (Araştırmacı, Kullanıcı/Müzisyen, Dış Sistem: Kaggle/Spotify API) ve temel kullanım durumlarını gösterir.

[use_case_diagram.png]

- **Temel Aktörler:**
  - *Araştırmacı / Veri Bilimci (Öğrenci):* Veri yükleme, temizleme, model eğitimi ve değerlendirme adımlarını yürütür.
  - *Kullanıcı / Müzisyen:* Yeni şarkı ses özelliklerini sisteme girerek popülerlik tahmini alır ve özelliklerin önem düzeylerini görüntüler.
  - *Spotify Web API / Kaggle:* Ham veri setini sağlayan dış sistemdir.
- **İlişkiler:** Model Eğitimi (UC-4), Veri Ön İşlemeyi (UC-2) zorunlu olarak içerir (`<<include>>`). Tahmin Etme (UC-6) adımı ise isteğe bağlı olarak Özellik Önem Düzeylerini Görüntüleme (UC-7) ile genişletilebilir (`<<extend>>`).

---

### 5.2. Activity Diagram (Etkinlik Diyagramı)
Verinin ham halden yüklenip temizlenmesi, özellik ölçekleme, modellerin eğitilmesi, metrik hesaplama ve başarı durumuna göre hiperparametre iyileştirme döngüsünü içeren uçtan uca veri analizi iş akışını modeller.

[activity_diagram.png]

- **Akış ve Karar Noktaları:**
  - *1. Karar:* Veride eksik veya mükerrer satır var mı? Evet ise temizlenir, hayır ise özellik mühendisliğine geçilir.
  - *Fork & Join (Çatallanma ve Birleşme):* Doğrusal Regresyon ve Random Forest modelleri aynı eğitim verisinde paralel olarak eğitilir.
  - *2. Karar:* Test verisinde $R^2 \ge 0.60$ başarı eşiği sağlandı mı? Başarılıysa grafik ve rapor üretilerek süreç tamamlanır; yetersizse hiperparametreler güncellenerek eğitime geri dönülür.

---

### 5.3. Class Diagram (Sınıf Diyagramı)
Projenin nesne yönelimli (OOP) yazılım yapısını, sınıfların alanlarını (attributes), metotlarını (methods) ve sınıflar arası kalıtım, bileşim ve bağımlılık ilişkilerini gösterir.

[class_diagram.png]

- **Temel Sınıflar:**
  - `Sarki` ve `SesOzellikleri`: Şarkı ve ona ait 9 temel akustik ölçümü temsil eden varlık sınıflarıdır (Bileşim - Composition: 1'e 1).
  - `VeriYukleyici`: Veriyi okuyan, eksik değerleri temizleyen ve ölçekleyen yardımcı sınıftır.
  - `MLModel` (Soyut Sınıf): Tüm modeller için ortak `egit()`, `tahmin_et()`, `degerlendir()` arayüzünü belirler.
  - `DogrusalRegresyonModeli` ve `RandomForestModeli`: `MLModel` taban sınıfından kalıtım (`generalization/inheritance`) alan somut model sınıflarıdır.
  - `DegerlendirmeVeGorsellestirme`: Korelasyon haritası, hata dağılımı ve model karşılaştırma raporu üreten servis sınıfıdır.


---

## 6. Veri Analizi, Betimsel İstatistikler ve Görselleştirme (Hafta 6)

6. hafta Google Colab ve Veri Analizi çalışması kapsamında, projeye ait açık veri setinden (Kaggle Spotify Tracks Dataset) seçilen örneklem üzerinde uçtan uca veri analizi, tanımlayıcı istatistik hesaplamaları ve görselleştirmeler yapılmıştır.

### 6.1. Proje Dosya ve Klasör Düzeni
Dönem projesi standart dosya mimarisi şu şekildedir:

```text
spotify-sarki-populerlik-analizi/
├── README.md                          # Proje ana tanıtımı ve dokümantasyon
├── activity_diagram.png               # Sistem aktivite diyagramı
├── class_diagram.png                  # Nesne yönelimli sınıf diyagramı
├── use_case_diagram.png               # Kullanım senaryosu diyagramı
├── data/
│   ├── spotify_populerlik_verisi.csv       # Şarkı öznitelikleri CSV veri tablosu
│   └── spotify_populerlik_verisi.json      # Şarkı öznitelikleri JSON veri dosyası
├── notebooks/
│   └── spotify_veri_analizi_hafta6.ipynb   # Çalışır Google Colab analiz defteri
├── outputs/
│   ├── ozet.csv                            # Tanımlayıcı istatistik tablosu (CSV)
│   ├── ozet.json                           # Tanımlayıcı istatistik tablosu (JSON)
│   ├── populerlik_karsilastirma_sutun.png  # Şarkı popülerlikleri sütun grafiği
│   └── ses_ozellikleri_degisim_cizgi.png   # Ses öznitelikleri değişim çizgi grafiği
└── docs/
    └── haftalik_rapor_hafta6.md            # 6. hafta akademik ilerleme raporu
```
### 6.2. Hesaplanan Temel İstatistiksel Bulgular
İncelenen Şarkı Sayısı (Gözlem): 10 adet

Toplam Popülerlik Puanı: 830 puan

Ortalama Popülerlik: 83.00 puan (En düşük: 76, En yüksek: 92, Standart Sapma: 5.48)

Ortalama Dans Edilebilirlik: 0.656 (0.0 – 1.0 normalize indeks)

Ortalama Enerji Seviyesi: 0.641 (0.0 – 1.0 normalize indeks)

Ortalama Ses Gürlüğü (Loudness): -6.89 dB

Ortalama Tempo: 119.82 BPM

### 6.3. Üretilen Grafikler
Sütun Grafiği (Bar Chart): Şarkıların popülerlik puanlarının (0–100) karşılaştırılması ve ortalama referans çizgisi (outputs/populerlik_karsilastirma_sutun.png).

Çizgi Grafiği (Line Chart): Popülerlik sıralamasına göre enerji, dans edilebilirlik ve pozitiflik (valence) değişim trendi (outputs/ses_ozellikleri_degisim_cizgi.png).

### 6.4. Akademik Yorum ve Sınırlılıklar
Temel Bulgu: İncelenen örneklemde en yüksek popülerliğe sahip parçaların genel olarak yüksek enerji (>0.70) ve orta-yüksek dans edilebilirlik (>0.50) bileşimine sahip olduğu görülmüştür.

Sınırlılıklar: Popülerlik sadece ses dalgası ve akustik sinyal parametrelerine bağlı değildir; sanatçı popülaritesi, plak şirketi pazarlama bütçesi, Spotify başyazı (editorial) çalma listelerine giriş başarısı ve viral sosyal medya trendleri gibi dışsal değişkenler bu veri setinde yer almamaktadır.

Nedensellik Uyarısı: Ses nitelikleri ile popülerlik arasındaki istatistiksel ilişki tek başına neden-sonuç (illiyet) ilişkisini kanıtlamaz; yalnızca popüler parçalarda sıkça rastlanan ortak akustik eğilimleri betimler.
