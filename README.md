# Güneş Döngüleri 23–25: Güneş Patlamaları, Güneş Lekeleri ve Jeomanyetik Etkiler

**Lisans tezi · Tunahan İnci · 2026**

2000–2025 döneminde güneş aktivitesinin nasıl değiştiğini ve bu aktivitenin Dünya'daki jeomanyetik fırtınalara nasıl yansıdığını GOES X-ışını, SILSO güneş lekesi ve NASA OMNI2 verileriyle inceleyen zaman serisi analizi.

- **Tez sitesi:** https://tunahandv.github.io/gunes-tezi/
- **Proje defteri** (kararlar, bulgular, yol haritası): https://tunahandv.github.io/gunes-tezi/proje-defteri.html

## Araştırma soruları

| | Soru | Durum |
|---|---|---|
| S1 | Patlama sayısı ve şiddeti döngüden döngüye nasıl değişiyor? | Sonuç var |
| S2 | Leke sayısıyla patlamalar ve fırtınalar arasında gecikme var mı? | Ön çalışma |
| S3 | Patlama büyüklükleri güç yasasına uyuyor mu? | Sırada |
| S4 | SARIMA, Prophet ve LSTM basit referans modelleri geçebiliyor mu? | Sırada |
| S5 | Büyük patlamalardan sonra fırtına olasılığı ne kadar artıyor? | Sonuç var |

## Öne çıkan bulgular

1. **Veri homojenleştirme sonucu değiştiriyor.** NOAA operasyonel listesindeki 0,7 ölçek çarpanı ve uydular arası kalibrasyon farkları düzeltilmeseydi Döngü 25 / Döngü 24 oranı 2,39 olarak raporlanacaktı. Düzeltilmiş değer 1,40. GOES-16 / GOES-15 oranı (1,08) Hudson ve ark. (2023) ile uyumlu.
2. **Döngü 24 leke başına en az patlama üretti.** 1000 leke başına M+X patlama: Döngü 23 → 325,6, Döngü 24 → 215,8, Döngü 25 → 302,7. Döngü 25 / 24 = 1,40, tüm duyarlılık testlerinde sabit.
3. **Büyük patlama fırtına olasılığını artırıyor.** Patlamadan sonraki 12–96 saatte şiddetli fırtına (Dst ≤ −100 nT) olasılığı, rastgele zamanlara göre: M1–M5 1,43×, M5–X1 1,69×, ≥X1 2,60×.
4. **Fırtınanın büyüklüğünü patlamanın büyüklüğü belirlemiyor.** Analiz penceresindeki en güçlü fırtınadan (2003-11-20, Dst −422 nT) önceki 4 günün en büyük patlaması M7.9. Kayıtlı en büyük patlamanın (2003-11-04, batı kenarı) ardından Dst yalnızca −29 nT.

## Depo yapısı

```
notebooks/   Google Colab defterleri, çalıştırma sırasıyla
docs/        Tez sitesi (index.html) ve proje defteri; GitHub Pages buradan yayınlanır
data/        tez_verisi.json: sitedeki tüm grafik ve sayıların kaynağı (07 defterinin çıktısı)
```

| Defter | İçerik |
|---|---|
| `01_veri_cekme` | SILSO leke sayıları, 2000–2025 OMNI2 saatlik veri, HEK flare listesi |
| `02_flare_homojen_A` | HEK listesinin teşhisi, NCEI bilimsel kalite flare özetlerinin indirilmesi |
| `02_flare_homojen_B` | 12 GOES uydusunun birleştirilmesi, ölçek farkının ölçülmesi, doymuş patlamalar |
| `03_capraz_kalibrasyon` | Uydular arası kalibrasyon (ağırlıklı en küçük kareler + bootstrap) |
| `04_kopru_tarama` | 1 dakikalık veride eski–yeni uydu çakışmalarının taranması |
| `05_kopru_senaryolar` | 2009 köprüsü, M sınıfı duyarlılık analizi, Döngü 23 senaryoları |
| `06_dunyaya_etki` | Nihai liste (S4), üst üste bindirilmiş olay analizi, fırtına olasılığı, gecikme, vakalar |
| `07_web_verisi` | Site için `tez_verisi.json` dosyasının üretilmesi |
| `08_anlamlilik` | Blok bootstrap, faz rastgeleleştirilmiş yapay seriler, rastgele küme ve permütasyon testleri |

## Çalıştırma

Defterler Google Colab için yazıldı ve verileri Google Drive'da `gunes_tezi/` klasörüne kaydeder. Sırayla çalıştırılmalıdır (01 → 07). Ham veriler depoya eklenmedi; 01 ve 02A defterleri onları resmi kaynaklardan yeniden indirir ve her dosyanın adresini, indirme zamanını ve SHA-256 özetini `data/indirme_kaydi.json` dosyasına yazar.

Kullanılan başlıca kütüphaneler: `pandas`, `numpy`, `matplotlib`, `xarray`, `scipy`, `requests`, `sunpy[net]`.

## Veri kaynakları

- **SILSO**, Belçika Kraliyet Gözlemevi: güneş lekesi sayısı, sürüm 2.0 — https://www.sidc.be/SILSO/
- **NASA SPDF OMNI2**: saatlik Dst, Kp, güneş rüzgârı — https://spdf.gsfc.nasa.gov/
- **NOAA NCEI**: GOES XRS bilimsel kalite flare özetleri (GOES 8–19) — https://www.ncei.noaa.gov/products/goes-r-extreme-ultraviolet-xray-irradiance
- **HEK**: NOAA SWPC operasyonel flare olayları (karşılaştırma için)

## Kaynakça

- Hudson, H. S., Cliver, E. W., White, S. M., Machol, J. ve ark. (2023). *The greatest GOES soft X-ray flares: Saturation and recalibration over two Hale cycles.* arXiv:2310.11457.

## Sıradaki adımlar

1. ~~Danışmana sunum ve konu onayı~~ (onaylandı)
2. Anlamlılık testleri (08 defteri)
3. S3: döngü bazında güç yasası üssü (arka planı çıkarılmış akılarla)
4. S4: SARIMA, Prophet ve LSTM; zamana göre ayrılmış test, basit referans modellerle karşılaştırma
5. SOHO/LASCO CME kataloğunun eklenmesi ve S5'in CME üzerinden tekrarı
