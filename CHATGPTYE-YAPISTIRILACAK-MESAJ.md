# ChatGPT'ye Yapıştırılacak Mesaj

Bu dosya, kurulumu başlatmak için kullanılacak **hazır mesajı** içerir.

---

## Adım 1 — Bu mesajı ChatGPT'ye yapıştırın

ChatGPT masaüstü uygulamasında yeni bir sohbet açın ve aşağıdaki metni olduğu gibi
yapıştırın:

---

> Sana yeni bir montaj kabiliyeti kazandıracağım.
>
> Adres: https://github.com/bugrasergun/levent-video-kit
>
> Bu depoyu incele ve montaj sistemimi kur. Kendi videolarımı montajlamak istiyorum.
>
> Şunları yap:
>
> 1. Depoyu klonla ve içindeki README.md ile KURULUM.md dosyalarını oku
> 2. .agents/skills/ altındaki becerileri kendi sistemine kopyala
> 3. Bana tek tek sorular sor — hiçbir şeyi varsayma. Özellikle:
>    - Elimde kaç video var, hangi formatta, hangi klasörde?
>    - Hangi çıktı klasörünü istiyorum?
>
>    Sonra şu üç şeyi kontrol et ve bana durumu bildir:
>    - Python 3.10+ kurulu mu?
>    - Node.js 18+ kurulu mu?
>    - FFmpeg kurulu mu?
>
>    Hangisi eksikse ne yapması gerektiğini ve neden gerekli olduğini açıkla, sonra kurma.
> 4. Her adımda benim onayımı bekle
>
> Teknik bilgim sınırlı. Bir şeyi anlamadığımda veya iki seçenek arasında kaldığımda bana
> net ve somut örneklerle benim anlayabileceğim şekilde açıkla — kararı ben vereceğim.

---

## Adım 1b — Becerileri ajanın kendi sistemine tanıtın

Ajan, becerileri **kendi ortamında geçerli olan skill dizinine** kopyalar. `KURULUM.md`
içinde `~/.agents/skills/` diye bir yol geçiyor ama bu bir varsayımdır — ajan kendi ortamını
araştırıp doğru dizini kendisi belirler.

Kopyaladıktan sonra ajana şunu sorun:

> Becerileri nereye kopyaladın, kaç tane oldu, yeniden başlatma gerekiyor mu?

Beceriler listede görünmüyorsa ajanı yeniden başlatın.

---

## Adım 2 — Beklenen akış

Yapıştırdıktan sonra ajan sırayla ilerler:

```
1. Depoyu okur, ne yaptığını özetler
2. Becerileri kendi skill dizinine kopyalar
3. Sorar: kaç video var, hangi formatta, hangi klasörde?
4. Sorar: çıktılar nereye gidecek?
5. Kontrol eder: Python 3.10+, Node.js 18+, FFmpeg
   → Eksik olanı ve neden gerekli olduğunu açıklar, onay ister
6. Montaj motorunu kurar (make setup)
7. API anahtarlarını sorar (çoğu montaj için gerekmez)
8. Küçük bir test montajı yapar
```

**Her adımda onay ister.** Acele etmeyin — 5. ve 6. adımlar büyük indirme yapar.

---

## Adım 3 — Kurulumdan sonra

ChatGPT'ye normal cümlelerle yazabilirsiniz:

```
~/Videolarim/2026-shoot içindeki kliblerden 45 saniyelik bir tanıtım videosu yap.
Açılışta şehir silueti, ortada ürün, sonda marka logosu olsun.
```

---

## Not

Bu mesaj **ChatGPT masaüstü uygulaması** içindir. Codex kullanıyorsanız beceriyi
`/kurulum` ya da `$kurulum` ile çağırabilirsiniz.

---

## Takılmak için

| Belirti | Yapılacak |
|---|---|
| Beceriler görünmüyor | ChatGPT'yi kapatıp yeniden açın |
| "Bu depoyu bulamıyorum" derse | Depoyu elle klonlayın: `git clone https://github.com/bugrasergun/levent-video-kit.git ~/levent-video-kit` |
| Python sürümü eski derse | `brew install python@3.12` sonra ajana "3.12 kuruldu" deyin |
| Ajan çok hızlı ilerliyor | "Dur, bir adım geri git" deyin |