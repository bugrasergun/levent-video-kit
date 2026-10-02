---
name: kesif
description: Use when you need OpenMontage knowledge and do not know which file holds it. Locates the right pipeline, stage director, core or Layer 3 skill.
tags: [openmontage, discovery, skill-search, navigation]
related_skills: [montaj-rehberi]
---

# OpenMontage Keşif

Çalışma alanında **295'ten fazla bilgi dosyası** var ve bunların doğrudan bir dizinini
almadınız. Doğru dosyayı bulmanın yolu budur.

> **Ne zaman kullanılır:** ne yapmak istediğinizi biliyorsunuz ama bunu **hangi dosyanın
> anlattığını** bilmiyorsunuz. (Bir istatistik kartı nasıl yapılır, hangi sağlayıcıyı seçmeliyim,
> sinematik bir sahne nasıl planlanır.) Tam yolunu biliyorsanız atlayın ve doğrudan okuyun.

**Çalışma alanı** kurulumda belirlenir (varsayılan: `~/openmontage-workspace/repo`).
Aşağıdaki komutlarda `<workspace>` yazısı yerine bu yolu kullanın; yol hiçbir komutta elle
yazılmaz, ortam değişkeni olarak okunur.

Kendi yolunuz farklıysa `<workspace>` yazısını değiştirin — ama komutun başındaki `cd`
satırını güncellemezseniz yanlış dizinde çalışır.

---

## Üç katman

```
Katman 1  tools/tool_registry.py     "hangi araçlar var, ne işe yararlar"
             registry.list_all() ile döner.
             ↓  araç.agent_skills[] şuraya işaret eder ↓
Katman 3  .agents/skills/<ad>/SKILL.md   "teknoloji nasıl çalışır"
             API bilgisi, sağlayıcı istemlendirmesi, parametreler.

Katman 2  skills/                    "OpenMontage bu araçları nasıl kullanır"
     core/     ffmpeg, remotion, hyperframes, whisperx,
               subtitle-sync, color-grading
     creative/ editleme, ses, anlatı, istemlendirme
     meta/     reviewer, checkpoint, taste-direction,
               bespoke-composition, onboarding
     pipelines/<ad>/  *-director.md dosyaları
```

Çalışma alanı kökündeki `skills/INDEX.md` Katman 2 için **kanonik dizindir** — her skill'i
tetikleyicisi ve Katman 3 bağımlılıklarıyla eşler. Yönelmek istediğinizde okuyun. Uzundur;
**boşaltmayın, grep'leyin.**

---

## Karar tablosu — önce buraya bakın

| Ne yapmak istiyorsunuz | Git |
|---|---|
| Bir üretim çalıştırmak | `pipeline_defs/<pipeline>.yaml` + `skills/pipelines/<pipeline>/` |
| Bir aşamanın ne yaptığını öğrenmek | `skills/pipelines/<pipeline>/<stage>-director.md` |
| FFmpeg / Remotion / HyperFrames seçmek | `skills/core/hyperframes.md` (karar matrisi) |
| React sahnesi kurmak | `skills/core/remotion.md` → `.agents/skills/remotion-best-practices/` |
| Video istemi yazmak | `skills/creative/video-gen-prompting.md` (5 boyutlu kanonik şema) |
| Seslendirme / anlatım | `skills/creative/sound-design.md` |
| Müzik / efekt | `skills/creative/music-gen-usage.md`, `sound-design.md` |
| Altyazı | `skills/core/subtitle-sync.md` |
| Hikâye / ritim / kanca | `skills/creative/storytelling.md` |
| Kendi işini gözden geçirme | `skills/meta/reviewer.md` |
| Onay + checkpoint | `skills/meta/checkpoint-protocol.md` |
| Kahraman işi için tasarım oku | `skills/meta/taste-direction.md` |
| Jenerik görünümü reddetme | `skills/meta/bespoke-composition.md` |
| **Kendi çektiğiniz videoyu analiz etmek** | `skills/meta/video-reference-analyst.md` |
| Dikey / kısa format | `skills/creative/short-form.md` |
| Uzun format / YouTube | `skills/creative/long-form.md` |
| Ekran kaydı | `skills/creative/screen-recording.md` |
| Montaj ve kurgu | `skills/creative/` (editleme dosyaları) |

---

## Arama komutları

**Katman 2'de anahtar kelimeyle skill bul:**

```bash
cd <workspace> && grep -ril "anahtar kelime" skills/ --include="*.md" | head -20
```

**Katman 3'te ada veya yeteneğe göre skill bul:**

```bash
cd <workspace> && ls .agents/skills/ | grep -i "anahtar kelime"
```

**İki katmanda tam metin araması:**

```bash
cd <workspace> && grep -ril "anahtar kelime" skills/ .agents/skills/ --include="*.md" | head -20
```

**Bir pipeline'ın içinde ne olduğunu listele:**

```bash
cd <workspace> && ls skills/pipelines/<pipeline>/
```

**Hangi araçlar Katman 3 skill'i bildiriyor:**

```bash
cd <workspace> && grep -rl "agent_skills" tools/ --include="*.py" | head
```

---

## Neden sayı önemli

Bu çalışma alanı 295+ bilgi dosyası içeriyor. Hepsini okumaya çalışmak yerine:

- **Ne istediğinizi bilin** → karar tablosuna bakın
- **Nereye bakacağınızı bilin** → pipeline dizinlerini listeleyin
- **Araç davranışını anlamak istiyorsanız** → registry'den `agent_skills[]` alanını okuyun

Sayılar kurulumda doğrulanmalı; hardcode değildir. Şunları doğrulayın:
`ls .agents/skills | wc -l` · `find skills -name "*.md" | wc -l` ·
`registry.list_all()` uzunluğu

**Tuzak — pipeline dizin adı ≠ manifest adı olabilir.** `pipeline_defs/` içindeki ad ile
`skills/pipelines/` dizin adı her zaman aynı değildir. Örneğin manifest
`animated-explainer.yaml` adını taşır ama aşama yönergeleri `skills/pipelines/explainer/`
içindedir. Aşama yönergesi aramadan önce **önce `ls pipeline_defs/` yapın**, sonra manifest
adını dizin adıyla eşleştirin.

Çalışan sayma komutları:

```bash
cd <workspace>
find skills -name "*.md" | wc -l                      # Katman 2
find .agents/skills -maxdepth 1 -type d | wc -l       # Katman 3 dizinleri
find skills/pipelines -name "*-director.md" | wc -l    # aşama yönergeleri
ls pipeline_defs/*.yaml | wc -l                        # manifestler
```

> Rakamlar kurulumda doğrulanmalı; kaynak ağaçta değişebilir.

---

## Reading discipline

1. **Read the stage director before the stage.** Every pipeline stage has one.
   Skipping it is the single most common way to produce generic output.
2. **Read the Layer 3 skill before calling a tool.** A tool's `agent_skills[]`
   field names it. These carry the prompting guidance and parameter tuning that
   separate good output from generic.
3. **Read the manifest before the pipeline.** `pipeline_defs/<name>.yaml` holds
   `required_tools`, quality gates and `human_approval_default`.
4. **Read `skills/INDEX.md` when lost.** It maps trigger → skill → Layer 3 deps.

Do not guess a file path. If a search returns nothing, list the directory
instead. If the content genuinely is not there, escalate to the user rather than
inventing a technique — say what you searched and what you expected to find.
