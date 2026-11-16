# Evrişimsel Sinir Ağları (CNN)

#derin-öğrenme #yöntemler

## Tanım
Evrişimsel sinir ağları (Convolutional Neural Networks – CNN), özellikle **görüntü işleme ve görüntü tanıma** işlerinde çok başarılı olan derin öğrenme modelleri.

- **Kullanım alanları:** Görsel veri analizi, yüz tanıma, otonom araçlar, tıbbi görüntüleme
- **Örnek:** Güvenlik kamerası kayıtlarındaki nesneleri tanımak ve sınıflandırmak

Slayttaki örnekte el yazısıyla yazılmış bir "2" rakamı CNN'e veriliyor. Görüntü evrişim (convolution) ve havuzlama (max-pooling) katmanlarından geçiyor, sonra tam bağlantılı katmanlara giriyor. En sonda ağ bunun 0–9 arasındaki rakamlardan hangisi olduğunu söylüyor.

## Öğrenme

![[CNN Öğrenme (işaretli).png]]

Hocanın ilk vurguladığı şey: **CNN'de öğrenme ANN'e benziyor.** Yine forward → loss → backward → güncelleme döngüsü var. Fark, ANN'in önüne **convolution + pooling** katmanlarının eklenmesi. CNN'de öğrenilen şey de **filtreler**, yani filtrelerin içindeki $w$ ve $b$ değerleri.

Şema iki büyük parçadan oluşuyor:
- **Feature learning (özellik öğrenme):** Görüntüden özellikleri çıkaran kısım. Convolution, ReLU, pooling burada. Slaytta "Future learning" yazıyor ama doğrusu "feature learning".
- **Classification (sınıflandırma):** Çıkan özelliklere bakıp karar veren kısım. Hoca bunun için **"burası ANN"** dedi.

### Input (girdi)
Girdi bir görüntü. Görüntüler iki çeşit olabiliyor:
- **2B:** Siyah-beyaz görüntü, tek kanal.
- **3B:** Renkli görüntü. **w** (genişlik), **h** (yükseklik) ve **c** (kanal) olarak üç boyutu var. Renkli görüntüde 3 kanal bulunuyor: **R, G, B** (kırmızı, yeşil, mavi).

### Convolution (evrişim)
Görüntünün üzerinde küçük bir **filtre (kernel)** gezdiriliyor. Filtre görüntüdeki desenleri yakalıyor ve sonuçta **feature map (özellik haritası)** oluşuyor. Ağın öğrendiği şey bu filtreler.

### ReLU
Convolution'dan sonra **ReLU** aktivasyon fonksiyonu uygulanıyor. Hocanın çizdiği grafik:

![[ReLU.png]]

Negatif değerleri 0 yapıyor, pozitif değerleri olduğu gibi bırakıyor.

### Pooling (havuzlama)
Feature map'lerin boyutunu küçültüyor. Hocanın yazdığına göre iki faydası var:
- **Maliyeti azaltıyor:** Daha az hesaplama.
- **Overfitting'i azaltıyor.**

Convolution + ReLU + pooling birkaç kez arka arkaya tekrar edebiliyor.

### Flatten (düzleştirme)
Buraya kadar veri 2 ya da 3 boyutlu. ANN kısmına girebilmesi için **tek boyuta (bir vektöre)** çevriliyor. Hoca bunu **"2, 3 → 1"** diye yazdı.

### Fully connected (tam bağlantılı katman)
Burası artık ANN. Nöronlar arasında yine **$w$ ve $b$** var.

### Çıktı
Çıktı katmanında problemin türüne göre farklı bir aktivasyon fonksiyonu kullanılıyor:
- **Sınıflandırma** (araba mı, kamyon mu, bisiklet mi?) → **softmax** ya da **sigmoid**
- **Regresyon** (bir sayı tahmini) → **linear**

## Gerçek Hayat Problemi: Otonom Araçlarda Yaya Tespiti

![[CNN Yaya Tespiti (işaretli).png]]

Amaç, otonom aracın kamerasından gelen görüntüde **yayayı tespit etmek.**

Yapı yine iki parça:
- **Feature extraction (özellik çıkarımı):** Convolution → maxout → pooling → convolution → maxout → pooling
- **Classification (sınıflandırma):** Fully connected katman → çıktı katmanı

Hocanın kenara yazdıkları:
- **Etiketleme:** Eğitim için görüntülerdeki yayaların yeri işaretleniyor. Yayanın etrafına bir kutu çiziliyor ve bu kutu 4 sayıyla tanımlanıyor: **x, y** (kutunun konumu), **w** (genişliği), **h** (yüksekliği). Hocanın örneği: **(5, 10, 50, 250)**.
- **Veri ön işleme: data augmentation (veri artırma):** Elimizdeki görüntülerden yeni eğitim örnekleri türetilerek veri çoğaltılıyor.

---
← [[Yapay Sinir Ağları (ANN)]] | 🏠 [[Giriş]]
