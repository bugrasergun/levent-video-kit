---
name: yonetmenlik
description: Use when planning a video's story, shots, pacing or motion. Load BEFORE writing a script or building a scene. Prevents generic output.
version: 1.0.0
author: Assembled from smixs/visual-skills (CC BY 4.0) + LottieFiles/motion-design-skill (MIT)
license: "CC-BY-4.0 (dramaturgy refs) + MIT (motion-design refs) — see LICENSE files"
triggers:
  - senaryo yaz
  - storyboard
  - sahne tasarla
  - video planla
  - ne çekilir
  - nasıl anlatılır
  - pacing
  - ritim
  - motion design
  - timing
  - easing
  - animasyon kalitesi
  - cinematic
  - sinematik
  - yönetmenlik
trigger_keywords:
  - script
  - screenplay
  - narrative
  - story arc
  - beat sheet
  - shot list
  - storyboard
  - blocking
  - montage
  - pacing
  - rhythm
  - timing
  - easing
  - spring
  - interpolation
  - keyframe
  - animation
  - motion
  - transition
  - choreography
  - camera
  - lighting
  - composition
  - visual direction
  - creative direction
  - tone
  - art direction
metadata:
  hermes:
    tags: [video, directing, dramaturgy, motion-design, narrative, pacing, cinematography]
    attribution: "smixs/visual-skills (Serge Shima) — CC BY 4.0; LottieFiles/motion-design-skill — MIT"
---

# Directing Craft

> **Load this BEFORE writing a script, storyboard, scene plan, or animation.**
> Loaded after the fact it is a checklist, not a method.
>
> **Why it exists:** verified 2026-09-27 across two pilots. A technical brief
> produced a technically clean, creatively empty video. A brief that specified
> the direction produced work the user approved. The difference was not skill
> or tooling — it was whether the craft was applied before the render, not after.

**Sources and licensing**

| Part | Source | License |
|---|---|---|
| `references/*.md` (dramaturgy) | [smixs/visual-skills](https://github.com/smixs/visual-skills) — Serge Shima | **CC BY 4.0 — attribution required** |
| `references/motion-design/**` | [LottieFiles/motion-design-skill](https://github.com/LottieFiles/motion-design-skill) | MIT |

Both licences are in this skill's directory as `LICENSE-*.txt`.

**Full coverage.** All upstream reference files are included, including the
provider-specific ones (`seedance.md`, `seedance-25.md`, `kling.md`, `veo.md`)
and `race-and-speed.md`. Some of them describe AI video generators that are not
currently configured (0/26 providers) — that is a *runtime state*, not a reason
to drop the knowledge. If a provider key is added later, the guidance is already
here. Do not go looking for it then.

---

## Mandatory reading order

Do not skip steps. Skipping one silently degrades the result — you cannot tell
a wallpaper frame from a directed one by looking at it.

### Step 1 — `references/dramaturgy.md` (always)

**The scene formula:**

```text
Scene = hero's desire + obstacle + space geometry + controlled gaze + editing rhythm
```

> *"If any element is missing, the scene collapses into decoration."*

Before writing a scene, name all five in one sentence each. If you cannot, the
scene is not ready.

Contains: Murch Rule of Six, the three-jobs rule, blocking as choreography of
desire, the three-detail rule, 14-field shot card, rhythm ladder, three-layer
storyboard, and the dramaturgy check.

### Step 2 — `references/universal-rules.md` (always)

Rules that apply to any video regardless of tool: prompt skeleton, show-don't-
tell, lens language, character anchoring, duration discipline, the final-image
rule, the three-detail check.

### Step 3 — `references/role-modes.md` (when writing, not just rendering)

Decides whether you are operating as **Director**, **Screenwriter** or
**Editor** for this turn. Writing a script and building a shot list are
different jobs with different rules.

### Step 4 — pick by task

| The task | Read |
|---|---|
| Genre or story shape not settled yet | `references/patterns-and-genres.md` |
| Need lens / camera / light / sound vocabulary | `references/camera-lighting-vocabulary.md` |
| Still panels or keyframes to pitch a sequence | `references/animatic-keyframes.md` |
| A prompt or continuity is broken | `references/fixes-and-skeletons.md` |
| Race, drift, drag, chase, speed, kinetic montage | `references/race-and-speed.md` |
| Seedance, ByteDance, Doubao, Jimeng, multi-shot, Ultra Long | `references/seedance.md`, `references/seedance-25.md` |
| Kling, Kuaishou, Motion Brush, `[Character A: ...]`, 3.0 Omni/4K | `references/kling.md` |
| Veo, Google, dialogue/lip-sync, JSON prompts, synchronized SFX | `references/veo.md` |

Provider files are only useful once a matching API key exists. Check the live
registry first — do not write provider-specific syntax for a provider that is
not configured.

### Step 5 — before rendering, run the checks

- **Dramaturgy check** from `references/dramaturgy.md`
- **Three-detail check** — every shot owns one environmental pressure, one
  physical micro-action, one sound or visual motif
- **Motion quality checklist** from
  `references/motion-design/reference/quality-checklist.md`

---

## Motion design (applies to every animated element)

Read `references/motion-design/SKILL.md` when timing, easing or choreography is
involved. The short version, because these are the mistakes that make motion
look cheap:

**Never use linear easing on spatial movement.** That single rule is most of
what separates amateur motion from professional motion.

| Element | Duration |
|---|---|
| Micro-feedback | 80–120 ms |
| Button / toggle | 120–180 ms |
| Icon transition | 150–250 ms |
| Card enter / exit | 200–350 ms |
| Modal / dialog | 300–400 ms |
| Page transition | 400–600 ms |
| Dramatic reveal | 600–1200 ms |

- **Distance scales duration**: 100 px = 1.0×, 200 px = 1.3×, 400 px = 1.6×
- **Exit is 65–75% of entrance** — things leave faster than they arrive
- **Stagger total stays under 500 ms** or it reads as lag
- **Ease out on entrances, ease in on exits**
- **No unbroken motion longer than 1/3 of the container** (the 1/3 rule)

Full tables, the 12 adapted Disney principles, emotion→motion mapping, motion
personalities, and multi-element choreography are in
`references/motion-design/`.

---

## Bu paket içinde nerede duruyor

| Konu | Nerede |
|---|---|
| Hangi pipeline, hangi motor, sağlayıcı mevcut mu | `montaj-rehberi` |
| Doğru üst dosyayı bulmak | `kesif` |
| **Hikâye, çekim, ritim, hareket kalitesi** | **bu skill** |
| Teknik QA ve teslim | `kalite-ve-teslim` |
| Kurulum ve ilk iş | `kurulum` |

OpenMontage'ın kendi `skills/creative/storytelling.md` ve `skills/meta/taste-direction.md`
dosyaları da var. Geçerli olduklarında onları da okuyun — marka ve zevk katmanı onlarda.
Bu skill **zanaat** katmanını taşır: dramaturgi, kamera, ritim, hareket.

---

## The one question to ask before you render

> **Could this be any other company's video?**

If the honest answer is yes, the direction is not decided yet. Go back to the
proposal stage and present two or three distinct visual directions with
tradeoffs. Do not render a plausible-looking video built on a direction nobody
chose.
