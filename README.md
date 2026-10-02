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
/kurulum
```

ChatGPT'ye **`/kurulum`** yazın. Bu, kurulum sihirbazını başlatır ve size adım adım sorular
sorar:

1. Elinizde kaç video var, hangi formatta
2. Videoları hangi klasörden okuyacak
3. Gerekli araçlar hazır mı (Python, Node, FFmpeg)
4. Montaj motoru kurulumu
5. Araç kontrolü
6. Gerekli API anahtarları (hangi, ne kadar)
7. Çıktılar nereye gidecek
8. İlk deneme montajı

**Her adımda onayınızı ister. Varsayılan dayatmaz.**

> Codex'te beceri adıyla çağrılır: `/kurulum` ya da `$kurulum`.

Kurulum bittikten sonra **montaj istekleri** için normal cümlelerle yazabilirsiniz:

```
~/Videolarim/2026-shoot içindeki kliblerden 45 saniyelik bir tanıtım videosu yap.
Açılışta şehir silueti, ortada ürün, sonda marka logosu olsun.
```

Ajan `montaj-rehberi` becerisini kullanır, klipleri analiz eder ve size seçenekleri sunar.

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

| Araç | Sürüm |
|---|---|
| **ChatGPT masaüstü uygulaması** | Plus hesabı yeterli |
| **Python** | **3.10+** |
| **Node.js** | **18+** |
| **FFmpeg** | Güncel |

**macOS'ta `python3` genellikle eski sürüm gösterir (3.9 gibi).** Bu normaldir ama
OpenMontage 3.10+ istiyor — ajan kontrol edip hangi sürümü kullanacağını söyler.

Ayrıntılı liste, kurulum komutları ve doğrulama: [GEREKSINIMLER.md](GEREKSINIMLER.md)

API anahtarları gerekmez — montajın büyük kısmı tamamen yereldir. Anahtar gereken durumlar
için [ANAHTAR-TABLOSU.md](ANAHTAR-TABLOSU.md).

---

## Belgelendirme

| Dosya | İçerik |
|---|---|
| `KURULUM.md` | Adım adım kurulum kılavuzu |
| `GEREKSINIMLER.md` | Hangi araç, hangi sürüm, nasıl kurulur |
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