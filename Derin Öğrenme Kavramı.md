# Derin Öğrenme Kavramı

#derin-öğrenme #temel-kavramlar

## Derin Öğrenme Nedir?
Derin öğrenme, bilgisayarlara verileri **insan beyninin çalışma şeklinden esinlenerek** analiz etmeyi öğreten bir yapay zekâ yöntemi.

Resim, metin, ses gibi verilerdeki **karmaşık desenleri tanıyıp** bunlara göre tahmin yapabiliyor. Bu yüzden normalde insan zekâsı gerektiren işleri otomatikleştirmek için kullanılıyor. Derste verilen örnekler:
- **Görüntü tanıma:** Bir görüntüde ne olduğunu söylemek
- **Sesli veri işleme:** Ses kaydını yazıya çevirmek

Slayttaki örnek şuydu: Bir araba resmi ağa veriliyor, ağ resmi işliyor ve sonunda "bu bir **araba**" ya da "**araba değil**" diyor.

## Derin Öğrenme Nasıl Çalışır?
Derin öğrenme algoritmaları, **insan beyninden esinlenerek modellenmiş sinir ağları**.

İnsan beyninde bilgiyi öğrenmek ve işlemek için birlikte çalışan, birbirine bağlı milyonlarca nöron var. Yapay sinir ağları da buna benziyor: bilgisayarın içinde birlikte çalışan **birçok yapay nöron katmanından** oluşuyorlar.

Yapay nöronlara **düğüm (node)** da deniyor. Aslında bunlar veriyi işlemek için **matematiksel hesaplama yapan küçük yazılım parçaları**.

## Derin Öğrenme Ağının Bileşenleri

![[Bileşenleri (işaretli).png]]

Bir derin öğrenme ağı 3 kısımdan oluşuyor:
- **Girdi katmanı (input layer):** Verinin ağa girdiği yer.
- **Gizli katmanlar (hidden layers):** Girdi ile çıktı arasındaki katmanlar. Görseldeki ağda iki tane var.
- **Çıktı katmanı (output layer):** Ağın sonucunu verdiği yer.

Hocanın şema üzerinde gösterdikleri:
- **Çıktı bir olasılık:** Çıktı katmanı kesin bir cevap yerine olasılık veriyor. Örneğin **0.8** çıkarsa sonuç **K**, yani %80 ihtimalle "K sınıfı". Geriye kalan **0.2** de **K değil (K̄)** ihtimali. Arabalı örnekteki "araba / araba değil" ayrımı da böyle çalışıyor.
- **Öğrenme gizli katmanlarda oluyor:** Hoca iki gizli katmanı işaretleyip "öğrenme?" diye sordu. Ağın öğrendiği şeyler bu katmanlarda. Nasıl öğrendiği bir sonraki başlığın konusu.

## Derin Öğrenme Nasıl Öğrenir?

![[Nasıl Öğrenir (işaretli).png]]

Hocanın cevabı: **parametrelerin güncellenmesiyle.** Parametreler ağırlıklar ($w$) ve bias'lar ($b$). Bu güncelleme işine **gradient descent** deniyor.

Şemadaki parçalar:
- **Girdiler ($x_1$, $x_2$):** Ağa giren veri (input).
- **Gri "1" daireleri:** Her katmanın **bias**'ı.
- **Oklar:** Her bağlantının bir **ağırlığı ($w$)** var.
- **Nöronlardaki "z | f":** Her nöron önce ağırlıklı toplamı hesaplıyor, sonra sonucu **aktivasyon fonksiyonundan ($f$)** geçiriyor. Hoca aktivasyon fonksiyonu için **"nöronun çekirdeği"** dedi.

### Forward propagation (ileri yayılım)
Veri soldan sağa ilerliyor. Hoca tahtaya katman katman şöyle yazdı:

| Katman | Önce | Sonra (aktivasyon) |
|---|---|---|
| 1. gizli katman ($h_1$) | $xw + b = h_1$ | $f(h_1) = z_1$ |
| 2. gizli katman ($h_2$) | $z_1w + b = h_2$ | $f(h_2) = z_2$ |
| Çıktı (out) | $z_2w + b = z_3$ | $f(z_3) = y'$ |

Her katmanın çıktısı bir sonrakinin girdisi oluyor. En sonda çıkan **$y'$ bizim tahminimiz (prediction).**

### Loss (hata)
Tahmin ($y'$) ile gerçek değer ($y$, true value) **loss fonksiyonuna** veriliyor. Loss fonksiyonu ikisi arasındaki farkı ölçüyor. **Hata = loss.** Çıkan sayıya **loss score** deniyor.

### Backward propagation (geri yayılım)
Loss score bu sefer sağdan sola, geriye doğru gidiyor. **Optimizer** bu değere bakıp ağırlıkları güncelliyor (**weight update**).

### Döngü
Ağırlıklar güncellendikten sonra her şey baştan tekrar ediyor. Şemadaki mavi oklar da bunu anlatıyor: bu süreç **loss en aza inene kadar** devam ediyor.

> 💡 **Kendime örnek:** $x=2$, gerçek değer $y=3$, başta $w=0.5$, $b=1$ olsun.
> - Tahmin: $2 \cdot 0.5 + 1 = 2$, yani 1 eksik.
> - Gradient descent $w$ ve $b$'yi biraz artırıyor: $w=0.9$, $b=1.2$
> - Yeni tahmin: $2 \cdot 0.9 + 1.2 = 3$ ✅ Hata kapandı.

## Derin Öğrenme Donanım Gereksinimleri
Derin öğrenme **çok büyük hesaplama gücü** istiyor.

- **GPU (grafik işlemci) ideal**, çünkü çok çekirdekli. Aynı anda birçok hesaplamayı büyük bir bellekle yapabiliyor.
- **Bulutta çalışmanın avantajları** da var:
  - **Hız**
  - **Ölçeklenebilirlik:** İhtiyaç arttıkça daha fazla güç kullanabilmek

## Derin Öğrenmenin Zorlukları
- **Büyük miktarda yüksek kaliteli veri:** Ağın iyi öğrenmesi için hem çok hem de düzgün veri lazım.
- **Büyük işlem gücü:** Güçlü donanım gerekiyor.
- **Yorumlanabilirlik:** Modelin bir kararı neden verdiğini anlamak zor.
- **Aşırı öğrenme (overfitting):** Model eğitim verisini ezberleyebiliyor, yeni veride kötü sonuç veriyor.
- **Zaman:** Eğitim uzun sürebiliyor.

## Derin Öğrenme Yöntemleri
Derste şu yöntemlerin listesi verildi. İşledikçe notlarını ekleyeceğim:

- [[Yapay Sinir Ağları (ANN)]]
- Evrişimsel Sinir Ağları (CNN)
- Yinelemeli Sinir Ağları (RNN)
- Uzun Kısa Süreli Bellek (LSTM)
- Çekişmeli Üretici Ağlar (GANs)
- Radyal Temelli Fonksiyon Ağları (RBFNs)
- Kendini Düzenleyen Haritalar (SOMs)
- Derin İnanç Ağları (DBNs)
- Otomatik Kodlayıcılar (Autoencoders)
- Transfer Öğrenimi (Transfer Learning)
- Artık Ağlar (ResNets)
- Derin Pekiştirmeli Öğrenme
- Transformers

---
🏠 [[Giriş]] | Sonraki → [[ANN, CNN, RNN, LSTM]]
