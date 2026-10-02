---
name: kurulum
description: Use when the user is setting up this video kit for the first time, or asks how to install it. Walks through source footage inventory, OpenMontage setup, API keys, and a first test edit — asking for approval at every step.
tags: [kurulum, setup, montaj, openmontage, video]
---

# Kurulum Sihirbazı

Bu paketi ilk kez kuruyorsanız veya "kurulum" derseniz bu akış çalışır.

**Kural: Her adımda onay isteyin.** Hiçbir adımı varsayılan olarak atlamayın, özellikle
klasör yollarını ve API anahtarlarını.

---

## Adım 1 — Bu paket ne işe yarar?

Önce ne yapacağınızı netleştirin. Kısaca anlatın:

- Elinizdeki videoları **montajlamak** (kesme, birleştirme, altyazı, ses, müzik, renk)
- Her iş bir **pipeline** ile yapılır; ajan klipleri analiz edip en uygun yöntemi önerir
- **Yaratıcı kararı siz verirsiniz**, ajan yürütür
- Biten video **teslimata uygun mu diye kontrol edilir**

Sonra sorun: **"Devam edelim mi?"**

---

## Adım 2 — Eldeki video envanteri

Montaj planı bu envantere dayanır. Şunları sorun, bilmiyorsanız birlikte bakın:

| Soru | Neden önemli |
|---|---|
| Kaç video var? | Süre ve iş yükü tahmini |
| Hangi format? (MOV/MP4/HEVC/ProRes) | Codec uyumluluğu |
| Toplam süre ne kadar? | Ne tür bir montaj çıkacağı |
| Ortalama klip süresi | Kesme temposu |
| Sesi var mı, kendi mi çektiniz? | Diyalog altyazısı, anlatım |
| Hepsi aynı çekim mi, farklı çekimler mi? | Anlatı çizgisi kurulabilir mi |
| Not aldığınız çekim bilgisi var mı? | Klipleri tanımlamayı kolaylaştırır |

Videoların olduğu klasörü de sorun. **Varsayılan önermeyin, ondan sorun.**

> Levent'in 40 klibi `~/Müzik/2026-shoot/` içinde gibi bir öneri yapabilirsiniz, ama
> kararı o versin.

---

## Adım 3 — Kaynak klasörünü belirleyin

Videoların **hangi klasörden** okunacağını sorun ve kaydedin. **Varsayılan önermeyin.**

Kullanıcı bir yol söyler; bu yol montaj boyunca kaynak medya olarak kullanılır. Sonraki
adımlarda bu yolu referans alın.

> Kullanıcı farklı bir yapı kurmak isterse (ör. müşteri başına klasör) bunu sorun ve not
> alın — kurulum bu yapıya göre devam eder.

Bu adım tek başına küçük ama atlanırsa tüm iş yanlış klasörde yapılır.

---

## Adım 4 — Gereksinim kontrolü

Montaj motorundan önce dört şeyin hazır olması gerekiyor:

| Gereksinim | Sürüm | Kontrol | Karşılığı |
|---|---|---|---|
| **Python** | **3.10+** | `python3 --version` | `brew install python@3.12` |
| **Node.js** | **18+** | `node --version` | `brew install node` |
| **FFmpeg** | güncel | `ffmpeg -version` | `brew install ffmpeg` |
| **Homebrew** | — | `brew --version` | [brew.sh](https://brew.sh) |

> **macOS tuzağı:** Sistem `python3` komutu genellikle **3.9** gibi eski bir sürüm gösterir.
> OpenMontage **3.10+** istiyor. Sürüm düşükse Homebrew ile güncel Python kurun ve kurulumda
> o sürümü kullanacağınızı söyleyin.

Tabloyu kullanıcıyla birlikte tek tek kontrol edin. Eksik olanı **önce onay alarak** kurun —
özellikle Node ve FFmpeg büyük indirmelerdir.

Ayrıntılı liste, indirme tahminleri ve doğrulama komutları:
`GEREKSINIMLER.md` (paketin kökünde). Kullanıcı teknik bilgisi yoksa buraya yönlendirin.

---

## Adım 5 — Montaj motorunu kurun

Gereksinimler (Adım 4) hazırsa motoru kurun. Kullanıcıdan tam yolu isteyin (varsayılan:
`~/openmontage-workspace/repo`):

```bash
git clone https://github.com/calesthio/OpenMontage.git ~/openmontage-workspace/repo
cd ~/openmontage-workspace/repo
make setup
```

**`make setup` ne yapar** — hepsini tek komutta kurar:

- Python sanal ortamını oluşturur (doğru sürümle)
- Python bağımlılıklarını kurar (`requirements.txt`)
- Remotion müzik kütüphanesini kurar (Node paketleri)
- Ücretsiz çevrimdışı konuşma sentezini (Piper) dener
- HyperFrames çalışma zamanını önden ısıtır (ilk render'da beklemek için)

> **Elle kurmayın.** `pip install` veya `npm install` komutlarını tek tek çalıştırmak
> **yarım bir kurulum** bırakır.

Kurulum birkaç dakika sürer ve **~1–2 GB** indirir. Kullanıcıyı bilgilendirin, acele
etmesin. Yarıda kesilirse `make setup` tekrar çalıştırılabilir — baştan başlatmaz.

**Bu depoyu değiştirmeyin.** Salt-okunur çalışma malzemesidir. İçinde düzenleme, commit, fork
veya yeniden dağıtım yapılmaz. Bir dosya yanlış görünürse kullanıcıya sorun — düzeltmeyin.

### Çıktı yönlendirmesi — bu, kurulumun en kritik adımıdır

Varsayılan olarak pipeline çıktıları repo içine yazar. Bu **istenmez**: sonra `git pull`
veya yeniden klonlama çıktıları siler. Bunun yerine kendi klasörünüzü gösterin:

```bash
# Bu değişkeni shell profiline ekleyin (~/.zshrc)
export OPENMONTAGE_PROJECTS_DIR=/kendi/proje/klasörünüz
```

Bu ayar `git pull`, `reset --hard` ve tam yeniden klonlamadan sağ çıkar — çünkü değişken
kendi kabuk ayarınızda durur ve depoda `.env` yoktur.

Doğrulayın: yeni bir iş başlatın, klasör yapısı **sizin** klasörünüzde oluşuyor mu? Depoda
değilse doğru yapılandırılmıştır. Depoda `projects/` görüyorsanız bu ayar eklenmemiş demektir —
geri dönüp ekleyin, çünkü sonraki `git pull` silecektir.

---

## Adım 6 — Araç ön kontrolü

Kurulumdan sonra üç kurgu motorundan hangilerinin hazır olduğunu ölçün, tahmin etmeyin:

```bash
cd ~/openmontage-workspace/repo
ffmpeg -version | head -1
node --version
./venv/bin/python --version
```

| Motor | Gereken |
|---|---|
| **FFmpeg** | `ffmpeg` kurulu olmalı |
| **Remotion** | `remotion-composer/node_modules` kurulmuş olmalı (`make setup` yapar) |
| **HyperFrames** | Node 18+ + FFmpeg + `npx hyperframes` erişilebilir |

Eksik olan varsa motoru yeniden `make setup` ile kurun — tekrarı güvenlidir.

Sonuçta ajan `ffmpeg`, `remotion`, `hyperframes` için hangilerinin hazır olduğunu bilmelidir.
**İkisi de hazırsa ikisi de sunulur** — hangisini seçeceğine kullanıcı karar verir.

---

## Adım 7 — API anahtarları

Her anahtar için şu dört şeyi söyleyin, sonra **kararı kullanıcıya bırakın**:

1. **Ne işe yarar**
2. **Ücretsiz mi, ücretli mi** (varsa aylık maliyet)
3. **Alınmadan ne yapılabiliyor** (genelde montajın büyük kısmı)
4. **Nereden alınır**

`ANAHTAR-TABLOSU.md` dosyasında tam liste var. Özet:

| Anahtar | İşe yarar | Ücret |
|---|---|---|
| *(kurulumda doldurulacak)* | | |

**Öncelik sırası:** Önce anahtarsız ne yapılabiliyorsa gösterin. Montajın büyük kısmı
yerel FFmpeg ile yapılır — kesme, birleştirme, altyazı, ses karışımı, renk düzeltme.
Anahtar gerektiren şey genelde yapay zekâ destekli görsel/video üretimi ve gelişmiş
konuşma sentezidir.

> Bir anahtarı **siz istemeyin.** "Anahtarınızı buraya yapıştırın" demeyin. Anahtarın
> nerede duracağını söyleyin (`~/openmontage-workspace/repo/.env`), kullanıcı kendisi
> oraya yazsın. Sır paylaşmak gerekmez.

Gerekli değilse anahtar istemeyin. Her anahtar günlük kullanım için ücret doğurabilir.

---

## Adım 8 — Çıktı klasörü

Çıktılar nereye yazılsın? Bir öneri sunun, kararı kullanıcı versin.

| Seçenek | Ne zaman |
|---|---|
| Mevcut bir proje klasörü | Her iş ayrı bir müşteri/çekim için ayrı klasör |
| Yeni bir klasör | Her iş için alt klasör açılır |

Klasör yapısı:

```
<çıktı-klasörü>/
├── <video-id>/
│   ├── index.md
│   ├── production-report.md
│   ├── decision-log.json
│   ├── final.mp4
│   ├── subtitles.srt
│   └── assets/
```

`<video-id>` videonun başlığından türetilmiş **kebab-case** ve **sabit** olmalı — başka
işler bu adı referans alır.

**Öneri sunun, kararı kullanıcı versin.** Onayınız olmadan klasör oluşturmayın.

---

## Adım 9 — İlk iş denemesi

Kurulum bittiğini kanıtlamak için küçük bir iş yapın. 10–15 saniyelik bir montaj yeterli.

Şunu deneyin:

> "Kaynak klasördeki videolardan 10 saniyelik bir test montajı yap. En güçlü birkaç klibi
> sırala, aralarına basit bir geçiş koy. Altyazı ekleme. Müzik önerme."

İzleyecekleriniz:

1. Ajan **klipleri gerçekten analiz ediyor mu**, yoksa uyduruyor mu
2. Süre ve geçişler makul mü
3. Çıktı **belirlediğiniz klasöre** yazıldı mı (depoya değil)
4. Ajan **eksik olanı söyledi mi** (ör. altyazı için araç gerekiyorsa)

Bu iş montajınızın işi değil, **sistemin sizinle çalışıp çalışmadığının** testidir.

---

## Adım 10 — Hazır

Kurulum bitti. Bundan sonra:

- Bir montaj isteyin: **"Şu klasördeki videolardan X için bir video yap"**
- İlk işte **yaratıcı yön siz verin.** Ajan "ne hissettirelim?" diye soracaktır —
   cevap vermeden geçmeyin, orası farkı yaratır.

Ajan neyi yapamıyorsa söyler. Sormadığınız şeyi de varsaydığınız sanmayın.

---

## Sorun giderme

| Belirti | Olası neden | Çözüm |
|---|---|---|
| Ajan "bulamadım" diyor | Workspace yolu yanlış | Ortam değişkenini kontrol edin |
| Çıktı depoda oluşuyor | `OPENMONTAGE_PROJECTS_DIR` ayarlanmamış | Adım 3'e dönün |
| Pipeline bloklu | Eksik araç | `setup_offers` çıktısına bakın, gerekli anahtarı ekleyin |
| Render uzun sürüyor | İki motor da hazır, hangisinin seçildiğine bakın | `render_runtime` kilitlidir, değişiklik yeni iş gerektirir |
| Python sürüm hatası | Yanlış yorumlayıcı | Pipeline'ın kendi `venv`'ini kullanın, sistem Python'u değil |