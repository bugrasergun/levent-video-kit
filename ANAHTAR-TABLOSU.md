# API Anahtarları — Ne İçin, Ne Kadar

Bu tablo kurulum sırasında ajan tarafından kullanılır. **Her anahtar sizin kararınızla
eklenir.**

---

## Önce önemli olan

**Montajın büyük kısmı anahtar istemez.** Şunlar tamamen yereldir:

- Kesme, birleştirme, kırpma
- Altyazı ekleme ve yakma
- Ses karışımı, müzik bindirme
- Renk düzeltme, geçişler
- Ekran kaydı
- Video kare hızı ve çözünürlük dönüşümü

Bunlar FFmpeg ile yapılır. Başlamak için **hiçbir anahtara ihtiyacınız olmayabilir.**

Anahtarlar gerektiren şey genelde **yapay zekâ destekli görsel veya video üretimi** ve
**gelişmiş konuşma sentezidir** — yani sizin elinizdeki görüntüyü işlemek için değil,
olmayan görüntüyü üretmek için.

---

## Anahtar tablosu

> Aşağıdaki tablo **OpenMontage kurulduktan sonra doldurulur.** Ajan kurulumda bu listeyi
> gerçek değerlerle ve güncel maliyetlerle doldurup size sunar.
>
> Neden ayrı bir tablo? Çünkü anahtarlar, sağlayıcılar ve fiyatlar değişir. Buradaki
> kalıplar sizin ne beklemeniz gerektiğini gösterir; **sayıları ajan size doğrulatır.**

| Anahtar | İşe yarar | Genelde ücretli mi | Onaysız yapılabilen |
|---|---|---|---|
| `FAL_KEY` | Çok sayıda video/görsel üretim sağlayıcısını tek anahtarla açar | Ücretli, kullanım bazlı | Hayır |
| `PEXELS_API_KEY` | Ücretsiz stok video | **Ücretsiz** | Kısmen |
| `PIXABAY_API_KEY` | Ücretsiz stok video | **Ücretsiz** | Kısmen |
| *(yapay zekâ TTS)* | Metni sese çevirir — seslendirme gerekiyorsa | Ücretli, kısa metinlerde düşük maliyet | Piper ile yerel olarak yapılabilir |
| *(müzik üretimi)* | Müzik üretir | Ücretli | Mevcut müziklerinizi kullanabilirsiniz |

---

## Kurulumda ajanın size soracağı format

Her anahtar için ajan şunları söyler, sonra **kararı size bırakır**:

1. **Ne işe yarar** — somut, bu işte neyi açar
2. **Maliyet** — ücretsiz mi; ücretliyse ne kadar (kullanım başına mı, aylık mı)
3. **Onaysız ne yapılabilir** — anahtarsız hangi işler yapılabiliyor
4. **Nereden alınır** — bağlantı
5. **Sorun** — "Almak istiyorum" / "Geçelim" / "Sonra bakarız"

---

## Kurallar

**1. Anahtarı sohbete yazmayın.** "Anahtarınızı buraya yapıştırın" denmez. Anahtar şu dosyaya
yazılır:

```
<openmontage-kurulum-dizini>/.env     # kurulumda belirlenen workspace yolu
```

2. **Anahtarları paylaşmayın.** Herkes kendi anahtarını kendi kullanır.
3. **Gereksiz anahtar istemeyin.** Montaj yapmak için gerekmiyorsa eklemeyin — sadece
   maliyet çıkar.
4. **Ücretsiz olanla başlayın.** Stok görüntü anahtarları ücretsizdir ve birçok iş için yeter.

---

## Maliyet kontrolü

Ajan ücretli bir aracı çağırmadan önce:

- **Önce tahmini maliyeti söyler**
- **Onayınızı ister**
- Onaylanmadan **toplu iş çalıştırmaz**

Bir klip üretirken tek bir görsel üretmekten 10 kat pahalı olabilir. Bu yüzden önce bir örnek
(tek klip) üretip sonra topluya geçmek genellikle daha ucuzdur.