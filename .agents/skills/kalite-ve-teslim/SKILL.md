---
name: kalite-ve-teslim
description: Use when reviewing, verifying or delivering a finished video. QA gates, technical checks, deliverable packaging.
tags: [video-production, qa, delivery, ffmpeg, accessibility]
related_skills: [montaj-rehberi]
---

# Video QA & Teslim

Bir render teslimat değildir. QA bir **kapıdır**, nezaketsizlik değil. Render edilen dosyada
aşağıdaki kontrollerin **hepsi gerçekten çalıştırılmadan** bir video "bitti" ilan edilmez.

> **Çalışma dizini:** bu pakette tanımlı değildir; kurulumda belirlenir. Aşağıdaki komutlar
> `renders/final.mp4` yolunu örnek olarak kullanır — kendi proje klasörünüzde çalıştırın.

**Önce oku:** çalışma alanındaki `skills/meta/reviewer.md` — kendi kendini gözden geçirme
protokolü. Bu dosya somut kontrol listesidir.

---

## Değişmez kurallar

1. **Dosyanın kendisini doğrula.** Başarılı bir render komutu kanıt değildir. Çıktıya
   `ffprobe` çalıştırıp gerçek değerleri oku.
2. **Atladığın kontrolde PASS yazma.** Eksik, kısmi, sahte veya başarısız kontrol **böyle
   raporlanır** — PASS olarak değil.
3. **Teslimden önce maliyet kaydedilir.** Üretim maliyeti, sağlayıcı, model ve
   çağrı/token sayıları teslim raporuna girer.
4. **Yayınlamadan önce insan onayı.** Bir yere yüklemek veya paylaşmak, render'ı
   onaylamaktan **ayrı** bir onaydır.

---

## Aşama 1 — Teknik doğrulama (ffprobe)

```bash
ffprobe -v error -show_format -show_streams -of json renders/final.mp4
```

Doğrulanıp kaydedilecek gerçek değerler:

| Alan | Nerede | Gereksinim |
|---|---|---|
| Süre | format/streams | Brief'in hedefiyle eşleşir (± öneride anlaşılan tolerans) |
| Çözünürlük | stream.width × height | Platform ayarıyla **tam** eşleşir |
| Kare hızı | stream.r_frame_rate | Tutarlı; onaylanmadıysa karışık/değişken yok |
| Video codec | stream.codec_name | H.264 veya onaylı alternatif |
| Ses codec | stream.codec_name | AAC |
| Ses kanalı | stream.channels | 2 (stereo), onaylanmadıysa mono değil |
| Bit hızı | format.bit_rate | Hedef aralıkta |
| Dosya boyutu | format.size | Platform sınırı içinde |

**Süre kayması** en sık görülen sessiz hatadır. Gerçek değer onaylı toleransın dışındaysa
blokerdir — "montajda düzeltirim" deyip raporlamadan geçmeyin.

---

## Aşama 2 — Ses doğrulama

```bash
ffmpeg -i renders/final.mp4 -af "ebur128=peak=true" -f null - 2>&1 | tail -20
```

| Ölçüt | Hedef | Neden |
|---|---|---|
| Entegre ses yüksekliği | **-14 LUFS** (stereo sosyal) | Platform normalizasyon hedefi |
| Gerçek tepe | **≤ -1.0 dBTP** | Platform kodlaması sonrası kırpılmayı önler |
| LRA | 4-12 LU | Aşırı sıkıştırma cansız; fazla geniş yorucu |

`per-lufs-stereo` güncel referanstır; -23 LUFS eski EBU R128 yayın değeridir. Alışkanlığa
değil, platformun hedefine uyun.

---

## Aşama 3 — Görsel QA

Encode'in temiz olduğunu varsaymayın; aralıklarla kare render edip **inceleyin**:

```bash
ffmpeg -i renders/final.mp4 -vf "fps=1/3,scale=640:-1" -q:v 3 qa_frames/frame_%04d.jpg
```

Her kare için kontrol edin:

- **Metin okunabilirliği** — ekrandaki en küçük metin telefon boyutunda okunuyor mu
- **Güvenli alanlar** — kritik içerik platform arayüzü içinde değil (üst bant, alt altyazı
  şeridi, Shorts/Reels/TikTok sağ aksiyon rayı)
- **Artefakt taraması** — bantlama, bloklama, metin çevresinde halkalanma, renk kayması
- **Siyah/boş kareler** — özellikle geçişlerde
- **Flaş kareleri** — saf beyaz/siyah, 1-2 karelik strob
- **Altyazı çakışması** — altyazılar grafiklerle veya konuşanla çakışıyor mu
- **Marka tutarlılığı** — renkler, tipografi, logo yerleşimi

Hareketli işlerde yalnız durağan aralıklar değil, **geçiş kareleri de** örnekleyin.

---

## Aşama 4 — Altyazı ve erişilebilirlik QA

- Brief vaat ettiyse altyazı var mı
- **Kelime düzeyinde** zamanlama konuşmadan görünür şekilde kaymıyor mu
- Satır sonu kelime ortasında değil, ifade sınırında mı
- Ekranda en fazla 2 satır, satır başına ~42 karakter
- Okuma hızı 160-180 kelime/dakika aralığında mı
- Arka plana karşı kontrast yeterli mi
- **Yazım hatası yok** — dosyanın varlığını kontrol etmek değil, **okuyun**

```bash
ffprobe -v error -select_streams s -show_entries stream=codec_name renders/final.mp4
ffmpeg -i renders/final.mp4 -map 0:s:0 -f srt - | head -40   # metni gözden geçir
```

---

## Aşama 5 — Brief'e karşı içerik QA

Onaylanmış öneri paketini ve son scripti yeniden okuyun. Doğrulayın:

- `scene_plan`deki **her sahne gerçekten üretildi mi**
- Maliyetten tasarruf için **sessizce düşürülen sahne var mı**
- Anlatım onaylı script yönüyle uyuşuyor mu
- Müzik ve efektler onaylandığı gibi var mı
- Brief'teki teslim vaadi **kesimle gerçekten karşılanıyor mu**
- Platform çerçevesi uyuyor mu (dikey 9:16 klipler, yatay bir render'dan onaysız
  pillarbox yapılmamalı)

---

## Aşama 6 — Teslim paketleme

```
deliverables/
├── final.mp4              # ana dosya
├── final-<platform>.mp4   # platform varyantları
├── subtitles.srt
├── thumbnail.jpg          # kapsam dahilse
├── production-report.md   # ne yapıldı, nasıl, ne kadar maliyetle
└── decision-log.json      # OpenMontage'den, salt-eklenen
```

**Üretim raporu** şunları belirtmelidir:

- Kullanılan pipeline ve nedeni
- Çağrılan her sağlayıcı/model, çağrı sayılarıyla
- Toplam maliyet ve hangi tahmine göre kontrol edildiği
- Alınan insan onayları, zaman damgalarıyla
- Seçilen motor (Remotion / HyperFrames / FFmpeg) ve reddedilen alternatifler
- Kabul edilen kısıtlamalar ve kimi kabul ettiği
- Teslim edilen dosyanın bilinen sınırları

---

## Blok raporlama

Bir kontrol başarısız olduğunda, sessizce düzeltip geçmeyin — şu yapıyla raporlayın:

1. Hangi kontrol başarısız, **ölçülen gerçek değerle**
2. Ne bekleniyordu ve bu beklenti **nereden geliyordu**
3. İçerik sorunu mu, kodlama sorunu mu
4. Seçenekler: düzelt, yeniden render, yeniden kodla, ya da belgelenmiş notla kabul et
5. Öneriniz

**Dürüstçe raporlanan, çözülmemiş bir QA hatası, sessizce brief'i ihlal eden "bitmiş"
bir videodan daha iyi bir sonuçtur.**

---

## Non-Negotiables

1. **Verify the actual file.** A successful render command is not evidence. Run
   `ffprobe` on the output and read real values.
2. **Never report PASS on a check you skipped.** Absent, partial, mocked or
   failed checks are reported as such — never as pass.
3. **Cost is recorded before delivery.** Production cost, provider, model and
   token/call counts go into the delivery report.
4. **Human approval precedes publish.** Uploading or posting anywhere is a
   separate approval from approving the render.

---

## Stage 1 — Technical verification (ffprobe)

```bash
ffprobe -v error -show_format -show_streams -of json renders/final.mp4
```

Verify and record actual values:

| Field | Where | Requirement |
|---|---|---|
| Duration | format/streams | Matches the brief's target (± tolerance agreed in proposal) |
| Resolution | stream.width × height | Matches the platform preset exactly |
| Frame rate | stream.r_frame_rate | Consistent; no mixed/variable rates unless approved |
| Video codec | stream.codec_name | H.264 or approved alternative |
| Audio codec | stream.codec_name | AAC |
| Audio channels | stream.channels | 2 (stereo) unless mono approved |
| Bitrate | format.bit_rate | Within the target range |
| File size | format.size | Within platform limit |

**Duration drift** is the most common silent failure. If actual is outside the
approved tolerance, it is a blocker — do not "fix it in the edit" without
reporting.

---

## Stage 2 — Audio verification

```bash
ffmpeg -i renders/final.mp4 -af "ebur128=peak=true" -f null - 2>&1 | tail -20
```

| Metric | Target | Why |
|---|---|---|
| Integrated loudness | **-14 LUFS** (stereo social) | Platform normalization target |
| True peak | **≤ -1.0 dBTP** | Prevents clipping after platform encode |
| LRA | 4-12 LU | Over-compression sounds lifeless; too wide is fatiguing |

Per-lufs-stereo is the modern reference; -23 LUFS is the older EBU R128
broadcast figure. Match the platform's target, not a habit.

---

## Stage 3 — Visual QA

Render frames at intervals and inspect them — do not assume the encode is clean:

```bash
ffmpeg -i renders/final.mp4 -vf "fps=1/3,scale=640:-1" -q:v 3 qa_frames/frame_%04d.jpg
```

Check each frame for:

- **Text legibility** — smallest on-screen text readable at phone size
- **Safe zones** — nothing critical within platform UI chrome (top bars, bottom
  caption strip, right-side action rail for Shorts/Reels/TikTok)
- **Artifact scan** — banding, blocking, ringing around text, color shift
- **Black/blank frames** — especially at transitions
- **Flash frames** — pure white/black frames, 1-2 frame strobes
- **Subtitle collision** — captions overlapping graphics or the speaker
- **Brand consistency** — colors, type, logo placement per the design system

For motion work, also sample mid-transition frames, not just static intervals.

---

## Stage 4 — Subtitle & accessibility QA

- Subtitles present when the brief promised them
- **Word-level timing** does not drift visibly from speech
- Line breaks at phrase boundaries, not mid-word
- Max 2 lines on screen, ~42 characters per line
- Reading speed within 160-180 WPM
- Contrast ratio sufficient against the background
- No typos — read them, do not just check the file exists

```bash
ffprobe -v error -select_streams s -show_entries stream=codec_name renders/final.mp4
ffmpeg -i renders/final.mp4 -map 0:s:0 -f srt - | head -40   # spot-read the text
```

---

## Stage 5 — Content QA against the brief

Re-read the approved `proposal_packet` and the final script. Verify:

- Every scene in the `scene_plan` was actually produced
- No scene silently dropped to save cost
- Narration matches the approved script direction
- Music and SFX present as approved
- The delivery promise in the brief is met by the actual cut
- Platform framing matches (vertical 9:16 clips must not be pillarboxed from a
  horizontal render without approval)

---

## Stage 6 — Delivery packaging

```
deliverables/
├── final.mp4              # the master
├── final-<platform>.mp4   # per-platform variants if required
├── subtitles.srt
├── thumbnail.jpg          # if in scope
├── production-report.md   # what was made, how, at what cost
└── decision-log.json      # append-only, from OpenMontage
```

The **production report** must state:

- Pipeline used and why
- Every provider/model called, with call counts
- Total cost, and the estimate it was checked against
- Human approvals obtained, with timestamps
- Runtime chosen (Remotion / HyperFrames / FFmpeg) and the rejected alternatives
- Any degradation accepted, and who accepted it
- Known limits of the delivered file

---

## Blocker reporting

When a check fails, report it in this structure — never silently fix and move on:

1. What check failed, with the actual measured value
2. What was expected, and where that expectation came from
3. Whether it is a content problem or an encoding problem
4. Options: fix, re-render, re-encode, or accept with a documented note
5. Your recommendation

An unfixed QA failure that gets reported honestly is a better outcome than a
"finished" video that silently violates the brief.
