# Gereksinimler

Sistemin çalışması için gerekenler. **Kurulumdan önce bu listeyi tamamlayın.**

---

## Zorunlu

| Gereksinim | Sürüm | Nasıl kurulur | Nasıl kontrol edilir |
|---|---|---|---|
| **Python** | **3.10 veya üzeri** | python.org'dan kurun, ya da Homebrew ile `brew install python@3.12` | `python3 --version` |
| **FFmpeg** | Güncel | `brew install ffmpeg` | `ffmpeg -version` |
| **Node.js** | **18 veya üzeri** | nodejs.org ya da `brew install node` | `node --version` |
| **Git** | Güncel | Xcode araçları ya da `brew install git` | `git --version` |
| **Homebrew** | — | [brew.sh](https://brew.sh) | `brew --version` |

**Yeni nesil Mac uyarısı:** macOS'ta `python3` komutu genellikle eski Python'ı gösterir
(3.9 gibi). Bu **normaldir** ve çoğu programı etkilemez — ama OpenMontage 3.10+ istiyor.
Eğer `python3 --version` 3.10'dan küçükse Homebrew ile güncel Python kurun ve o sürümü
kullanın.

Kurulumdaki ajan bu kontrolü yapar ve hangi sürümü kullanacağını söyler.

---

## Montaj motoru kurulumu

Gereksinimler tamam olduktan sonra:

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
> yarım bir kurulum bırakır. `make setup` hepsini sırayla yapar.

**Kurulum biraz sürebilir** (birkaç dakika) ve çok indirme yapar. Acele etmeyin.

---

## Toplam indirme

İlk kurulumda yaklaşık **1–2 GB** indirilir:

| Ne | Yaklaşık |
|---|---|
| Python bağımlılıkları | ~200 MB |
| Node paketleri (Remotion) | ~280 MB |
| Piper konuşma sentezi | ~150 MB |
| HyperFrames ön ısıtma | ~20 MB |

Diskte rahat yer olsun.

---

## Kurulum sonrası doğrulama

```bash
cd ~/openmontage-workspace/repo

# Sanal ortam doğru mu?
./venv/bin/python --version          # 3.10+ olmalı

# Araçlar hazır mı?
./venv/bin/python -c "from tools.tool_registry import registry; registry.discover(); print(len(registry.list_all()), 'araç')"

# Üç kurgu motoru var mı?
./venv/bin/python -c "
import shutil, subprocess
print('ffmpeg:', bool(shutil.which('ffmpeg')))
"
```

**Beklenen:** sanal ortam Python 3.10+, araç listesi boş değil, ffmpeg bulunuyor.

Ajan kurulumda bu kontrolleri sizinle birlikte çalıştırır.

---

## API anahtarları

**Montajın büyük kısmı anahtar istemez.** Kesme, birleştirme, altyazı, ses karışımı,
renk düzeltme — hepsi yereldir.

Anahtar gerektiren şey genelde yapay zekâ destekli görsel/video üretimi ve gelişmiş
konuşma sentezidir. Ayrıntı: [ANAHTAR-TABLOSU.md](ANAHTAR-TABLOSU.md)

---

## Sorun giderme

| Belirti | Çözüm |
|---|---|
| `python3 --version` 3.9 gösteriyor | Homebrew ile Python 3.12 kurun; `make setup` doğru sürümü kullanır |
| `make: command not found` | Xcode araçları yüklü değil; `xcode-select --install` |
| `brew: command not found` | [brew.sh](https://brew.sh) adresinden kurun |
| `node: command not found` | `brew install node` |
| Kurulum yarıda kesildi | `make setup` tekrar çalıştırılabilir; baştan başlatmaz |
| FFmpeg hatası | `brew install ffmpeg`, sonra `ffmpeg -version` ile doğrulayın |
| Node 18'den eski | `brew install node` sonra yeni terminal açın |

---

## Ne gerekmez

Bu pakette **gerekmez**:

- Ücretli API anahtarı (montaj için)
- Docker veya Podman
- Python paket yöneticisi olarak `pipx`, `poetry`, `conda`
- Harici veritabanı

Sadece yukarıdaki dört araç yeterli.