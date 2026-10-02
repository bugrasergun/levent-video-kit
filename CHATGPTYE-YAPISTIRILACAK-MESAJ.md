# ChatGPT'ye Yapıştırılacak Mesaj

Bu dosya, kurulumu başlatmak için kullanılacak **hazır mesajı** içerir.

---

## Adım 1 — Bu mesajı ChatGPT'ye yapıştırın

ChatGPT masaüstü uygulamasında yeni bir sohbet açın ve aşağıdaki metni olduğu gibi
yapıştırın:

---

> Seni bir video montaj sistemiyle çalıştıracağım.
>
> Adres: https://github.com/bugrasergun/levent-video-kit
>
> Bu depoyu incele ve montaj sistemimi kur. Kendi videolarımı montajlamak istiyorum.
>
> Şunları yap:
> 1. Depoyu klonla ve içindeki `README.md` ile `KURULUM.md` dosyalarını oku
> 2. `.agents/skills/` altındaki becerileri `~/.agents/skills/` klasörüne kopyala
> 3. Bana tek tek sorular sor — hiçbir şeyi varsayma. Özellikle:
>    - Elimde kaç video var, hangi formatta, hangi klasörde?
>    - Hangi çıktı klasörünü istiyorum?
>    - Gerekli araçlar (Python 3.10+, Node.js 18+, FFmpeg) bende kurulu mu, değilse
>      hangilerini kurmam gerekiyor?
> 4. Her adımda benim onayımı bekle
>
> Teknik bilgim sınırlı. Bir şeyi anlamadığımda veya iki seçenek arasında kaldığımda bana
> açıkça sor — kararı ben vereceğim.

---

## Adım 2 — Beklenen akış

Yapıştırdıktan sonra ajan sırayla ilerler:

```
1. Depoyu okur, ne yaptığını özetler
2. Becerileri ~/.agents/skills/ altına kopyalar
3. Sorar: kaç video var, hangi formatta?
4. Sorar: videolar hangi klasörde?
5. Kontrol eder: Python 3.10+, Node 18+, FFmpeg var mı?
   → Eksikse hangisini kurmanız gerektiğini söyler, onayınızı ister
6. Montaj motorunu kurar (make setup)
7. Sorar: çıktılar nereye gidecek?
8. API anahtarlarını sorar (çoğu montaj için gerekmez)
9. Küçük bir test montajı yapar
```

**Her adımda onayınızı ister.** Acele etmeyin — özellikle adım 5 ve 6 büyük indirme yapar.

---

## Adım 3 — Kurulumdan sonra

ChatGPT'ye normal cümlelerle yazabilirsiniz:

```
~/Videolarim/2026-shoot içindeki kliblerden 45 saniyelik bir tanıtım videosu yap.
Açılışta şehir silueti, ortada ürün, sonda marka logosu olsun.
```

---

## Not

`/kurulum` komutu **Codex'te** çalışır. ChatGPT masaüstü uygulamasında beceriyi bu
şekilde adıyla çağırmak yerine yukarıdaki mesajı yapıştırın — ajan depoyu okuyup
kurulumu kendisi başlatır.

---

## Takılmak için

| Belirti | Yapılacak |
|---|---|
| Beceriler görünmüyor | ChatGPT'yi kapatıp yeniden açın |
| "Bu depoyu bulamıyorum" derse | Depoyu elle klonlayın: `git clone https://github.com/bugrasergun/levent-video-kit.git ~/levent-video-kit` |
| Python sürümü eski derse | `brew install python@3.12` sonra ajana "3.12 kuruldu" deyin |
| Ajan çok hızlı ilerliyor | "Dur, adım 3'e dön" deyin |