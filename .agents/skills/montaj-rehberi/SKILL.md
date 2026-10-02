---
name: montaj-rehberi
description: Use when editing or assembling video from footage you already have — choosing the right pipeline, planning the cut, and presenting decisions for approval. Load when the user brings their own recordings.
tags: [montaj, video-editing, pipeline, openmontage, kes]
---

# Montaj Rehberi

Elinizde **kendi çektiğiniz videolar** var ve bunlardan bir iş çıkarmak istiyorsunuz. Bu rehber o işin ana akışıdır.

> **Bu paket montaja odaklanır.** Görsel üretmek önceliği değildir. Elinizdeki görüntü
> elinizdeki görüntüyle iş yapmak esastır; destek görseli sadece ihtiyaç olursa üretilir.

---

## Değişmez kurallar

1. **Her iş bir pipeline ile yapılır.** Rastgele komut dizileri, pipeline sistemini atlayan
   doğrudan API çağrıları yok.
2. **Registry gerçek kaynaktır.** Sağlayıcı adlarını, anahtar adlarını, araç listesini
   hafızadan yazma — çalışma anında sor.
3. **İşe başlamadan önce ön kontrol.** Neyi yapabileceğinizi ölç, menüyü göster, anlaşılmasını sağla.
4. **İki kurgu motoru varsa ikisini de sun.** Sessizce birini seçmek hatadır.
5. **Ücretli toplu iş için onay al.** Tahmin → sun → onayla → çalıştır.
6. **Tek taraflı ikame yok.** Sağlayıcı değişimi, model değişimi, motor değişimi, sabit
   görsele düşürme — hepsi önceden onay ister.
7. **Her aşamadan önce o aşamanın yönergesini oku.** Bilgi dosyalarında, doğaçlamada değil.

---

## Adım 1 — Ne yapabiliyoruz? (zorunlu ön kontrol)

Kullanıcıya ham bir liste vermeyin. Yetenekleri **ne işe yaradığına göre** gruplayın ve
oranı gösterin: "X / Y hazır".

Registry'nin özet çıktısı şu dört alanı verir:

- `composition_runtimes` — `ffmpeg` / `remotion` / `hyperframes` hazır mı. **İki motor
  kuralının kaynağı budur.**
- `capabilities[]` — yetenek ailesi başına `yapılandırılmış / toplam` ve sağlayıcı listesi.
- `setup_offers[]` — eksik araçlar, tek bir ortam değişkeniyle açılabilenler.
- `runtime_warnings[]` — kullanıcıya **kelimesi kelimesine** iletin.

Örnek biçim:

```
SİZİN İMKÂNLARINIZ
  Video Düzenleme:  9/9 hazır   ← her zaman yerel, FFmpeg ile
  Görsel Üretimi:   0/16 hazır
  Konuşma (TTS):   1/10 hazır
  Müzik:            0/5 hazır

  Şu anda kendi videolarınızı montajlayabilirsiniz: kesme, birleştirme,
  altyazı, ses karışımı, ekran kaydı.
```

Sonra seçilen pipeline'ın `required_tools` girdilerini registry'ye karşı kontrol edin ve
**`geçti` / `kısıtlı` / `bloke`** olarak raporlayın. Kullanıcı gerçek yetenek zarfını
anlamadan üretime başlamayın.

---

## Adım 2 — Pipeline seçimi

Montaj için uygun olanlar:

| Pipeline | En uygun olduğu iş | Durum |
|---|---|---|
| `hybrid` | Elinizdeki çekimler + destek görselleri | production |
| `screen-demo` | Ekran kaydı, ürün gezintisi, anlatım | production |
| `talking-head` | Konuşan kişi ağırlıklı | beta |
| `clip-factory` | Tek bir uzun kaynaktan çok klip | beta |
| `podcast-repurpose` | Podcast bölümleri ve türevleri | beta |
| `localization-dub` | Altyazı, dublaj, çeviri varyantları | beta |
| `cinematic` | Trailer, teaser, ruh hâli öncelikli | production |
| `documentary-montage` | Belgesel montajı | beta |

**Beta** olanlar denetlenmemiştir — çalışır ama köşeleri pürüzlüdür. Kullanıcı seçerse
bunu söyleyin.

Genel bir iş için en doğru seçim genelde `hybrid`'dir: elinizdeki görüntüyü temel alır,
gerektiğinde destek görseli ekler.

---

## Adım 3 — Aşama aşama yürütme

```
research → proposal → script → scene_plan → assets → edit → compose → publish
```

Her aşama için:

1. **Çalışmadan önce** o aşamanın yönergesini okuyun (`skills/pipelines/<pipeline>/<stage>-director.md`).
2. Her araç çağrısından önce `agent_skills[]` alanını kontrol edip ilgili referansı okuyun —
   sağlayıcıya özel yönlendirme burada durur; iyi çıktı ile jenerik çıktıyı fark eden şey budur.
3. Kendi işinizi gözden geçirin (`skills/meta/reviewer.md`).
4. Onay noktasına geldiyseniz durun ve onay isteyin.

**Montaj için özel:** `assets` aşamasında elinizdeki videolar envanterlenir. Her klip için
süre, çözünürlük, kare hızı, kamerası ve konusu not edilir. Bu envanter montaj kararlarının
dayandığı veridir — klipleri tanımadan kesme yapılırsa sonradan düzeltilemez.

---

## Yaratıcı yön kuralı

> **Siz yürütücüsünüz, yaratıcı yönetmen değil.**

Brief'te yaratıcı yön yoksa (izleyici ne **hissetmeli**, hangi görsel dil, hangi ritim,
hangi tipografi?), o yön **eksiktir** ve sizden uydurulmamalıdır.

1. **Eksikliği tespit edin.** Brief bunu söylüyor mu?
2. **Öneri aşamasında durun.** 2–3 ayrı konsept üretin: her biri adlandırılmış görsel yön,
   referans duygu ve dürüst bir ödünleme ile.
3. **Kullanıcı seçsin.** Bu diğer onaylardan farklı değildir. Sormak hata değildir —
   doğru davranıştır.
4. **Sonra yürütün.** Yön seçildikten sonra yeniden açmayın.

Şunları reddedin:

- Köşeye bırakılmış, altında süsleme çizgisi olan metin
- Gerekçesi olmayan varsayılan şablon renkleri
- Ayrıksınlık denetlenmeden yığılmış stok sahne tipleri
- Süreyi doldurmak için yazılmış, noktaya varan script

Render öncesi soru: **"Bu herhangi bir şirketin videosu olabilir mi?"** Evet ise öneri
aşamasına dönün.

---

## Kurgu motoru kararı (SERT KURAL)

Üç motor vardır, hepsi birbirinin yerine geçmez:

| Motor | Ne için | Gereksinim |
|---|---|---|
| **FFmpeg** | Yalnız video kesme, birleştirme, kırpma, altyazı yakma | `ffmpeg` (her zaman var) |
| **Remotion** | React kompozisyonu: görsel → animasyonlu video, metin/kart, grafik, kelime düzeyinde altyazı | Node.js + `remotion-composer/` |
| **HyperFrames** | HTML/CSS/GSAP: hareketli tipografi, ürün tanıtımı, tanıtım filmi, web sitesinden videoya | Node.js >= 22 + FFmpeg + `npx hyperframes` |

`render_runtime` **öneri aşamasında kilitlenir** ve değişmeden taşınır. Sessiz ikame yasaktır.

Her motor için şunları sunun:
1. Bu brief için **ne iyi** olduğu
2. **Bir dürüst ödünleme**
3. Brief'in vaadine bağlı öneriniz

Kısa listeyi (üçü + ffmpeg) `render_runtime_selection` kararına `options_considered`
olarak yazın. İkisi de varken tek motoru kaydetmek **kritik** bir bulgudur.

**Tek motor varsa** onunla devam edin ama eksik olanı `rejected_because: "bu makinede
mevcut değil"` olarak yazın.

**Hareket zorunlu isteklerde** (trailer, sinematik teaser, avatar, hype edit):
- Sabit görsele düşmek **yasaktır** — sessiz Ken Burns/animatic küçültme yok.
- Kilitli motor kullanılamıyorsa **yükseltin**, başka yola yönlendirmeyin.

---

## Nereye yazılır?

Bu paket bir klasör yapısı varsayar; kurulumda belirlenir:

```
<proje-klasörü>/
├── <video-id>/
│   ├── index.md              ← brief, pipeline, seçilen motor, maliyet, onay, durum
│   ├── production-report.md  ← sağlayıcılar, modeller, çağrı sayıları, maliyet, QA
│   ├── decision-log.json     ← OpenMontage'den, salt-eklenir
│   ├── final.mp4
│   ├── final-<platform>.mp4
│   ├── subtitles.srt
│   ├── thumbnail.jpg
│   └── assets/{images,video,audio,music}/
```

- `<video-id>` videonun başlığından türetilmiş **kebab-case** ve **sabit** olmalı.
- `index.md` ve `production-report.md` dosyalarını **siz** oluşturursunuz; pipeline
  otomatik oluşturmaz.
- Ara adımlar, probe çıktıları `/tmp`'ye gider. Teslim paketi kalıcı olan tek şeydir.

**Büyük dosyalar:** bir 4K stok klip 130 MB'tır; git'in yeri değildir. Belgeleri tutun,
büyük medyayı yanına koyup göreli yolla bağlayın. Her varlık için `source_url`, `creator`
ve `license` kaydedin — bu teslimatın ihtiyaç duyduğu kökendir.

---

## Karar iletişim sözleşmesi

**Çalıştırmadan önce duyur** — ücretli veya sonuç doğuran her çağrıdan önce: araç adı,
sağlayıcı, model/varyant, neden seçildi, örnek mi toplu mu.

**Büyük değişikliklerden önce sor** — sağlayıcı değişimi, model ailesi değişimi, video
odaklıdan sabit görsel odaklıya, kurgu motoru değişimi, anlatım/müzik çıkarma, örnekten
topluya geçiş.

Onaylanmış yol içindeki küçük prompt düzeltmeleri ayrı onay gerektirmez.

**Değişen kararları yeniden yaz** — `decision_log` salt-eklenen geçmiş. Orta bir yerde
değişen bir seçimde **aynı `category` ve aynı `subject`** ile yeni bir kayıt ekleyin,
geçersiz olanı `options_considered` içine taşıyın, `rejected_because` yazın. Eski kaydı
sessizce değiştirmeyin.

---

## Tıkandığınızda

Her blok raporu beş parçalıdır:

1. Ne denendi
2. Ne başarısız oldu
3. Kimlik/erişim mi, sağlayıcı erişimi mi, araç hatası mı, yoksa istem/tasarım kalitesi mi
4. Hangi seçenekler var
5. Hangisini öneriyorsunuz ve neden

**Onaylanmadan ikame bir yola devam etmeyin.**

### Tıkanınca ne yapmalı

Kullanıcıya üç seçenek sunun ve kararı ona bırakın:

- **(a) Dur** — şimdilik bırak
- **(b) Geçici çözümle devam** — kısıtı kabul ederek ilerle, kayda geç
- **(c) Alternatife geç** — hangisi önerildiğini gerekçesiyle yaz

Teknik bilginiz yoksa dürüstçe **"bilmiyorum"** deyin — bu normaldir ve (b) önerilir.

**Bu pakette kararı siz verirsiniz.** Ajan önerir, siz seçersiniz.

---

## Stok görüntü — anahtarsız çalışan yol

Stok görüntü, ek anahtar istemeden bugün çalışan tek varlık kaynağıdır. Arka plan, açılış ve
B-roll için kullanın.

`direct_clip_search` **arama** aracıdır:

```python
registry._tools['direct_clip_search'].execute({
    "output_dir": "/path/to/project/assets",
    "queries": [{"query": "sunset city skyline timelapse", "orientation": "landscape"}],
    "sources": ["pexels"],
    "clips_per_query": 2,
    "extract_thumbnails": True,
    "timeout_seconds": 90,
})
```

Her klip için döner: `clip_id`, `source_url`, `path`, `thumbnail`, `duration`, `width`,
`height`, `creator`, `license`.

**Sağlayıcı adları tahmin edilemez.** `pixabay` yanlıştır; kayıtlı ad `pixabay_video`'dur.
Emin değilseniz hata mesajındaki geçerli listeyi okuyun.

Arama yapmak için `pexels_video` / `pixabay_video` araçlarını **kullanmayın** — onlar
belirli bir varlığı edinir. Arama sorgusuyla çağrılırlarsa `success: true` döner ve boş
sonuç verir: **sessiz başarısızlık.**

Pexels ve Pixabay lisansları: **ücretsiz, atıf gerekmez.** Yine de her klip için `creator`,
`license` ve `source_url` kaydedin.

---

## Elinizdeki videoyla çalışma notları

- **Kaynak videoları hiçbir zaman değiştirmeyin.** Montaj kopyalar üzerinde yapılır.
- Klip envanteri montaj kararlarının dayandığı veridir: süre, çözünürlük, kare hızı, kamera
  açısı, konu. Tanımadan kesme yapmayın.
- Kaynak dosya adları klibi tanımlar — yeniden adlandırmayın, kopyalayın.
- Altyazı kliplerin konuşma içeriğinden üretilir; zamanlama kayması en sık görülen
  başarısızlıktır, `kalite-ve-teslim` becerisi bunu kontrol eder.

---

## Dosya yolları

Workspace yolu kurulumda belirlenir ve `kesif` becerisi tarafından kullanılır. Hiçbir
komutta yol **elle yazılmaz** — ortam değişkeni olarak okunur.

`lib/paths.py` ve `lib.checkpoint.PROJECTS_DIR` bu değişkeni okur; tüm checkpoint, olay,
karar günlüğü ve çıktı klasörü oraya gider. Bu, `git pull` ve tam yeniden klonlamadan
sağ çıkar: repo kendi `.env` dosyasını taşımaz.