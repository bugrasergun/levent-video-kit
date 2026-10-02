# Levent Video Kit — Montaj Beceri Paketi

Kendi çektiğiniz videoları montajlamak için bir yapay zekâ ajanı kılavuzu. Kod bilgisi gerekmez.

---

## Ne işe yarar

Elinizde kaç yüz dakikalık çekim var, müzik var, belli bir süre veya platform hedefi var. Bunlardan **izlenmeye değer bir video** çıkarmak istiyorsunuz. Bu paket, ajanınıza şunu öğretir:

- Hangi montaj yöntemi (pipeline) senin işine uygun
- Ajanın **gerçekten ne yapabildiğini** nasıl anlar (bilerek abartmadan)
- Ne zaman durup **sana sorması** gerektiği
- Biten videonun **gerçekten teslimata uygun olup olmadığını** nasıl kontrol edeceği
- Teslim paketini nasıl hazırlayacağı

## Hızlı başlangıç

```
Bu videoyu izledim, ne yapabiliyorsun?
```

Ajandan bu soruyu sorun. O, **kurulum sihirbazını** çalıştırır ve size adım adım sorular sorar:

1. Elinizde kaç video var, hangi formatta
2. Videoları hangi klasörden okuyacak
3. OpenMontage kurulumu
4. Araç kontrolü
5. Gerekli API anahtarları (hangi, ne kadar)
6. Çıktılar nereye gidecek
7. İlk deneme montajı

**Her adımda onayınızı ister. Varsayılan dayatmaz.**

---

## Beceriler

| Beceri | Ne zaman devreye girer |
|---|---|
| `kurulum` | İlk seferinde, adım adım kurulum |
| `montaj-rehberi` | Her montaj işinde — ana akış |
| `yonetmenlik` | **Hikâye, ritim, geçiş kararı vermeden önce** |
| `kalite-ve-teslim` | Video bittiğinde — teslimata uygun mu diye kontrol |
| `kesif` | "Ne yapmak istiyorum ama hangi dosya bunu anlatıyor bilmiyorum" |

---

## Önemli bir kural

**Montajı ajana yaptırın, ama yaratıcı kararı siz verin.**

Ajan "şunu yaptım" dediğinde, o teknik olarak doğru bir iş çıkarabilir ama **siz istediğiniz şey olmayabilir.** Bu pakette ajanın size üç seçenek sunup onaylamanızı isteyen kapılar var. O noktaları atlamayın — montajın farkı orada oluşur.

---

## Kurulum gereksinimleri

- **Mac** (macOS)
- **ChatGPT masaüstü uygulaması** (Plus hesabı yeterli)
- **FFmpeg** — video işleme, ücretsiz
- **Node.js 22+** — bazı montaj stilleri için

Ajan bunları adım adım kontrol eder ve ne eksekse söyler.

---

## API anahtarları

Bazı işlemler için anahtar gerekir. **Ücretsiz olanlarla başlayabilirsiniz.** Her anahtarın ne işe yaradığı ve ücretli olup olmadığı `ANAHTAR-TABLOSU.md` dosyasında yazılıdır. Ajan kurulumda bunları sırayla sorar ve **her biri için maliyetini söyleyerek kararınıza bırakır.**

---

## Belgelendirme

| Dosya | İçerik |
|---|---|
| `KURULUM.md` | Adım adım kurulum kılavuzu |
| `ANAHTAR-TABLOSU.md` | Hangi anahtar, ne için, ne kadar |
| `KAYNAKLAR-LISANS.md` | Kullanılan açık kaynak materyaller ve lisansları |

---

## Bilinen sınırlar

- Paket **montaja** odaklanır; görsel üretmek önceliği değildir
- İlk işte beklenmedik bir şey çıkabilir — ajanı tanıma süreci
- Kalite kapıları profesyonel teslimat standartlarını uygular; bazıları alışkanlık gerektirir

---

## Kaynaklar

Bu paket açık kaynak materyallerden derlendi. Kaynaklar ve lisanslar
[KAYNAKLAR-LISANS.md](KAYNAKLAR-LISANS.md) dosyasında açıkça belirtilmiştir.