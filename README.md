# Spotify Ses Özellikleri ile Şarkı Popülerliği Analizi ve Tahmini

Bu depo, Araştırma Yöntem ve Teknikleri dersi dönem projesi kapsamında oluşturulmuştur.

## 1. Proje Konusu ve Problem
Dijital müzik platformlarında her gün binlerce şarkı yayımlanmaktadır. Bir şarkının teknik ses özelliklerinin (enerji, dans edilebilirlik, ses yüksekliği, tempo, akustiklik vb.) dinleyiciler tarafından beğenilmesini ve popülerlik puanını (0-100) ne kadar etkilediğini incelemek amacıyla bu proje konusu seçilmiştir.

## 2. Araştırma Sorusu ve Hipotez
- **Araştırma Sorusu:** Spotify'daki şarkıların teknik ses özellikleri ile popülerlik puanı (0–100) arasında anlamlı bir ilişki var mıdır ve bu özelliklerle popülerlik tahmin edilebilir mi?
- **Hipotez (H1):** Şarkıların dans edilebilirlik, enerji ve ses yüksekliği değerleri arttıkça popülerlik puanı da artar.
- **Sıfır Hipotezi (H0):** Şarkıların ses özellikleri ile popülerlik puanı arasında anlamlı bir ilişki yoktur.

## 3. İncelenen Akademik Kaynaklar (Ön Literatür)
1. **Qiu vd. (2026)** - *Bayesian-Optimized Ensemble Learning for Music Popularity Prediction with Shapley-Based Interpretability*, Mathematics, 14(6), 946. (https://doi.org/10.3390/math14060946)
2. **Li, K. (2024)** - *Predicting song popularity in the digital age through Spotify's data*, Theoretical and Natural Science, 39(1), 68–75. (https://doi.org/10.54254/2753-8818/39/20240600)
3. **Gulmatico vd. (2022)** - *SpotiPred: A Machine Learning Approach Prediction of Spotify Music Popularity by Audio Features*, IEEE ICPC2T 2022. (https://doi.org/10.1109/ICPC2T53885.2022.9776765)

## 4. Kullanılacak Veri Seti
- **Veri Seti:** Spotify Tracks Dataset (Maharshi Pandya - Kaggle)
- **Bağlantı:** https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset
- **Açıklama:** Spotify Web API üzerinden alınan 114.000 şarkının popülerlik puanını ve ses özelliklerini içeren açık erişimli veri seti.

## 5. Kullanılacak Yöntem
Nicel araştırma ve ikincil veri analizi yöntemi kullanılacaktır. Veriler Python (Google Colab) ortamında incelenecek, betimsel istatistik ve korelasyon analizi yapılacak, popülerlik tahmini için Çoklu Doğrusal Regresyon ve Random Forest modelleri kullanılacaktır.
