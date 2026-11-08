# 6. Hafta İlerleme Raporu: Veri Analizi ve Görselleştirme

**Ders:** Araştırma Yöntem ve Teknikleri  
**Proje:** Spotify Şarkı Popülerlik Analizi  
**Öğrenci Adı:** Yılmaz Kaan Çebi

---

## 1. Bu Hafta Yapılan İşlemler
1. **Veri Seti Uçtan Uca Yapılandırıldı:** Kaggle Spotify Tracks Dataset kaynaklı gerçek akustik nitelikler kullanılarak 10 parçalık analiz veri seti hem CSV (`data/spotify_populerlik_verisi.csv`) hem de JSON (`data/spotify_populerlik_verisi.json`) formatında oluşturuldu.
2. **Pandas ile Tanımlayıcı İstatistikler Hesaplandı:** Veri setinin eksik değer içermediği (`isna().sum() == 0`) doğrulandı. Popülerlik puanı ortalaması 83.00, standart sapması 5.48, dans edilebilirlik ortalaması 0.656, enerji ortalaması 0.641 ve ortalama tempo 119.82 BPM olarak hesaplandı.
3. **Matplotlib ile Çift Grafik Üretildi:**
   - **Sütun Grafiği:** Şarkıların popülerlik puanlarının karşılaştırılması (`outputs/populerlik_karsilastirma_sutun.png`).
   - **Çizgi Grafiği:** Popülerlik seviyesine göre enerji, dans edilebilirlik ve pozitiflik (valence) değişim eğilimi (`outputs/ses_ozellikleri_degisim_cizgi.png`).
4. **Çıktılar Saklandı:** `outputs/ozet.csv` ve `outputs/ozet.json` oluşturuldu.
5. **Jupyter Notebook Hazırlandı:** `notebooks/spotify_veri_analizi_hafta6.ipynb`.

---

## 2. Akademik Değerlendirme ve Sınırlılıklar
- **Temel Bulgu:** En popüler şarkılarda yüksek enerji (>0.70) ve orta-üstü dans edilebilirlik (>0.50) gözlenmektedir.
- **Sınırlılık:** Popülerlik yalnızca ses sinyal özellikleriyle açıklanamaz; sanatçı bilinirliği, pazarlama ve Spotify editör listeleri gibi dışsal faktörler bu veri setinde yer almamaktadır.
- **Nedensellik Uyarısı:** Ses özellikleri ile popülerlik arasındaki korelasyon kesin bir sebep-sonuç ilişkisi anlamına gelmez.