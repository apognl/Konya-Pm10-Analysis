# Konya-Pm10-Analysis

Bu proje, 2021–2025 tarihleri arasında Konya şehir merkezindeki günlük PM10 ölçümlerini inceleyen,
mevsimsel ve trend bileşenlerini SARIMA modeli ile analiz eden; 
uç değerleri log dönüşümü ve Huber regresyonu ile değerlendirip RMSE/MAE karşılaştırması yapan
ve kısa vadeli hava kirliliği tahminleri sunan bir zaman serisi analiz çalışmasıdır.
---


## 📋 İçindekiler

1. [Proje Hakkında](#proje-hakkında)  
2. [Veri Seti](#veri-seti)  
3. [Kurulum & Gereksinimler](#kurulum-&-gereksinimler)  
4. [Çalıştırma & Kullanım](#çalıştırma-&-kullanım)  
5. [Dosya ve Klasör Yapısı](#dosya-ve-klasör-yapısı)  
6. [Ana Analiz Aşamaları](#ana-analiz-aşamaları)  
7. [Önemli Sonuçlar](#önemli-sonuçlar)    
8. [Lisans](#lisans)  

---

## 🔍 Proje Hakkında

Bu proje, Konya il merkezinde 2021–2025 yılları arasında toplanmış **günlük PM10 (ince toz parçacığı)** ölçümlerini kullanarak:

- **Mevsimsel ve trend bileşenlerini** görselleştiren bir veri keşfi (EDA)  
- **Aykırı değerlerin** (uç PM10 piklerinin) tespit edilmesi ve bunların doğrudan silinmeden “robust” yöntemlerle (log dönüşümü, Huber) nasıl ele alınabileceği  
- **Durağanlık testleri** (ADF, KPSS)  
- **Log dönüşümü** ile hata dağılımının normalleşmesi  
- **SARIMA (1,1,2)(0,1,1,12)** modeli ile mevsimsel zaman serisi tahmini  
- **Artık (residual) analizi** (ACF, normal dağılım kontrolü, heteroskedastisite testi)  
- **Performans karşılaştırması**: SARIMA vs. OLS (tarih + ay dummy) vs. HuberRegressor  
- **365 günlük hava kirliliği tahmini** ve %95 güven aralığı hesaplama

adımlarını kapsar. Amaç, Konya’nın hava kalitesi planlamasında kullanılabilecek kısa vadeli tahminler üretmek ve kirlilik dinamiklerini bilimsel olarak ortaya koymaktır.

---

## 📊 Veri Seti

- **Kaynak:** Projede kullanılan günlük PM10 verisi, Konya Çevre ve Şehircilik İl Müdürlüğü tarafından sağlanan Konya'nın farklı 5 noktasından alınan ( Bonsa, Karatay, Meram, Trafik) 25/04/2021-01/01/2025 tarihleri arasındaki günlük verilerin ortalamaları oluşturularak elde edilmiş veri tesi dosyasıdır.  
- **Dosya Adı:** `data/Pm10-KONYA.xlsx`  
- **Değişkenler:**  
  - `Date` (YYYY-MM-DD)  
  - `Mean` (günlük ortalama PM10 değeri, µg/m³)  
---

## 🛠️ Kurulum & Gereksinimler

1. **Python 3.8+** veya üzeri yüklü olmalıdır.  
2. Tercihen bir **sanal ortam (venv, conda)** oluşturun ve etkinleştirin:
   ```bash
   python3 -m venv venv
   source venv/bin/activate    # Windows için: venv\Scripts\activate
3. Gerekli Kütüphaneleri Kurma:
   '''bash
   pip install -r requirements.txt
4. Jupyter Notebook (Opsiyonel):
    pip install jupyterlab
    jupyter lab

### Neden?
- “Projeyi çalıştırmak isteyen” herkesin ilk önce hangi Python sürümü ve kütüphaneye ihtiyaç olduğunu bilmesi gerekir.  
- Sanal ortam tavsiyesi, “farklı projelere ait kütüphane sürümlerinin çakışmasını” engeller.  
- `requirements.txt`’i `pip install -r` ile bir defada kurmak hem sizin yaptığınız ortamı yeniden oluşturmayı hem de başkalarının hata almasını engeller.

---

## Çalıştırma & Kullanım (Run & Usage)

### Ne yapmalı?
“README’deki bu adımları takip ettiğinizde gerçekten nasıl çalıştırırsınız?” kısmını yazın:

## ▶️ Çalıştırma & Kullanım

1. Depoyu klonlayın:  
   ```bash
   git clone https://github.com/apognl/Konya-Pm10-Analysis.git
   cd Konya-Pm10-Analysis

2. Sanal ortamı etkinleştirin (eğer oluşturduysanız):
   ```
    source venv/bin/activate   # Windows: venv\Scripts\activate

4.  Gerekli kütüphaneleri kurun:
    ```
    pip install -r requirements.txt

5.  Jupyter Notebook’u başlatın:
    ```
    jupyter lab

6.  notebooks/PM10_KONYA_EDA.ipynb

7.  Ardından notebooks/PM10_KONYA_Modeling.ipynb ile SARIMA ve diğer modelleri çalıştırın.

8.  notebooks/PM10_KONYA_Forecast.ipynb ile 365 günlük tahmini ve grafiklerini görüntüleyin.
---

##7. Dosya ve Klasör Yapısı

## 📂 Dosya ve Klasör Yapısı
Konya-Pm10-Analysis/
├── data/ # Ham veri dosyaları
│ └── Pm10-KONYA.xlsx # Günlük PM10 ölçümleri
│
├── notebooks/ # Jupyter Notebook dosyaları
│ ├── PM10_KONYA_EDA.ipynb # Keşifsel veri analizi (EDA)
│ ├── PM10_KONYA_Modeling.ipynb # SARIMA ve model karşılaştırmaları
│ └── PM10_KONYA_Forecast.ipynb # 30 günlük tahmin ve grafikler
│
├── src/ # Python script ve modülleri
│ ├── load_data.py # Veri yükleme ve ön işlem fonksiyonları
│ ├── eda_utils.py # Grafik çizim fonksiyonları
│ ├── stationarity_tests.py # ADF/KPSS testleri
│ ├── model_utils.py # SARIMA/GARCH/OLS/Huber fonksiyonları
│ └── evaluation.py # RMSE/MAE ve Breusch-Pagan testi fonksiyonları
│
├── .gitignore # Git’in izlemeyeceği dosyalar (örneğin data/, pycache)
├── LICENSE # MIT lisansı
├── README.md # Proje açıklama dosyası (bu dosya)
└── requirements.txt # Python kütüphanelerinin listesi

## 🛠️ Ana Analiz Aşamaları

1. **Veri Yükleme & Ön İşlem**  
   - `load_data.py` kullanarak Excel/CSV dosyasını okuma, `Date` sütununu datetime’a çevirme  
   - Eksik/aykırı değer kontrolü, IQR yöntemiyle aykırılığın tespiti (`detect_outliers_iqr`)

2. **Keşifsel Veri Analizi (EDA)**  
   - Zaman serisi grafiği (`plot_time_series`)  
   - Aylık boxplot (`plot_monthly_boxplot`)  
   - Aylık ortalama trend grafiği (`plot_monthly_mean_trend`)

3. **Durağanlık Testleri**  
   - ACF/PACF grafikleri (`plot_acf_pacf`)  
   - ADF ve KPSS testleri (`run_stationarity_tests`)  
   - Orijinal ve log dönüşümlü seri için durağanlık kontrolü

4. **Modelleme**  
   - **SARIMA** parametre taraması (`itertools.product` ile `pdq` ve `seasonal_pdq`)  
   - En uygun parametreleri seçme (AIC’ya göre)  
   - Final SARIMA(1,1,2)(0,1,1,12) modelini fit etme  
   - Artık analizi (ACF, histogram, heteroskedastisite testi)

5. **Alternatif Modeller**  
   - **OLS** (tarih + ay dummy)  
   - **HuberRegressor** (robust regresyon)  
   - RMSE/MAE karşılaştırması

6. **Tahmin**  
   - Son 100 günü çizerek model tahminini görselleştirme  
   - 365 günlük ileriye dönük tahmin (`get_forecast`) ve %95 güven aralığı  


## 📈 Önemli Sonuçlar

- **Mevsimsel Dalgalanma:** Yaz aylarında PM10 (ortalama ~25 µg/m³), kış aylarında ise PM10 (ortalama ~80 µg/m³) olarak tavan yapıyor.  
- **Aykırı Değerlerin Oranı:** Veride yaklaşık %7.8 oranında “uç kirlenme günleri” var (150–300 µg/m³ aralığı). Bu, halk sağlığı riskinin kış aylarında ciddi boyutta olduğunu gösteriyor.  
- **Model Performansı:**  
  - **SARIMA (Log Ölçek):** RMSE ≈ 22.63, MAE ≈ 15.78  
  - **OLS:** RMSE ≈ 37.32, MAE ≈ 22.74  
  - **HuberRegressor:** RMSE ≈ 39.01, MAE ≈ 22.17  
  SARIMA, “mevsim ve trend + otokorelasyon” kombinasyonu sayesinde en düşük hata oranına ulaştı.  
- **Artıklarda Heteroskedastisite:** Breusch–Pagan testi p ≈ 0.0109 (< 0.05), “artık varyansının sabit olmadığı” anlamına geliyor. Bu, kış aylarında model belirsizliğinin (tahmin aralıklarının) artığına işaret ediyor.  
- **Sonuç:** Konya’da toz yoğunluğunu dört yıl boyunca izlediğimizde, yaz aylarının çoğunlukla temiz hava sunduğunu, kış aylarında ise birdenbire çok kirli günlerin yaşandığını gördük. Geliştirdiğimiz tahmin yöntemi, geçmiş verilerin ve mevsimsel döngünün yardımıyla günlük toz seviyelerini ortalama 15–20 birim hata ile öngörebiliyor. Bu da belediyenin ve halkın "yaklaşan kirli havaya" karşı birkaç gün önceden önlem almasını sağlıyor. Aynı zamanda kış aylarında hava kalitesinin değişkenliği hâlâ fazla olduğu için, ileride bu dalgalanmayı daha da azaltacak ek adımlar atmamız gerektiğini öğrendik. Bu çalışma sayesinde artık Konya’da hangi aylarda ve hangi koşullarda daha çok önlem alınması gerektiğini net olarak biliyoruz.

📜 Lisans
Bu proje MIT Lisansı ile lisanslanmıştır.
Detaylar için LICENSE dosyasına bakabilirsiniz.
