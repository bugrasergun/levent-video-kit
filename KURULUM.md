# Kurulum Kılavuzu

Bu paketi ilk kez kuruyorsanız. **Kurulum** becerisini ajanınıza çağırmasını söyleyin
(`/kurulum`) — sizi adım adım yönlendirir ve her adımda onayınızı ister.

Bu dosya aynı sürecin yazılı hâlidir; ajanın sorularını önceden görmek isterseniz
okuyabilirsiniz.

---

## Adım 1 — Paketi kurun

### 1a. Depoyu indirin

```bash
git clone https://github.com/bugrasergun/levent-video-kit.git ~/levent-video-kit
```

### 1b. Becerileri Codex'e tanıtın

Codex becerileri `~/.agents/skills/` altından okur. Paketin beceri klasörünü kopyalayın:

```bash
mkdir -p ~/.agents/skills
cp -R ~/levent-video-kit/.agents/skills/* ~/.agents/skills/
```

Kontrol:

```bash
ls ~/.agents/skills/
```

Beş beceri görünmeli: `kurulum`, `montaj-rehberi`, `yonetmenlik`, `kalite-ve-teslim`, `kesif`.

Codex yeni becerileri kendi algılar. Bir beceri görünmezse Codex'u yeniden başlatın.

---

## Adım 2 — Motorda ihtiyaç duyulan üç şey

| Gereksinim | Neden | Ücretsiz mi |
|---|---|---|
| **ChatGPT masaüstü uygulaması** | Codex becerileri burada çalışır | Plus hesabı yeterli |
| **FFmpeg** | Kesme, birleştirme, altyazı, ses | Evet |
| **Node.js 22+** | Remotion / HyperFrames montaj stilleri | Evet |

FFmpeg kurulumu (Homebrew ile):

```bash
brew install ffmpeg
```

Node.js kontrolü:

```bash
node --version      # v22 veya üzeri olmalı
ffmpeg -version     # kurulu olduğunu doğrulayın
```

---

## Adım 3 — Montaj motorunu kurun

Paket, montaj motorunu **kendi kaynağından** kurmanızı sağlar.

```bash
git clone https://github.com/calesthio/OpenMontage.git ~/openmontage-workspace/repo
cd ~/openmontage-workspace/repo
python3 -m venv venv
```

**Bu klasörü değiştirmeyin.** Salt-okunur çalışma malzemesidir.

### Çıktı yönlendirmesi — bu adım kritik

Varsayılan olarak motor çıktıları repo içine yazar. Bu istemezsiniz: sonra `git pull`
veya yeniden klonlama çıktıları siler. Kendi klasörünüzü gösterin:

```bash
# ~/.zshrc dosyasına ekleyin
export OPENMONTAGE_PROJECTS_DIR=/kendi/proje/klasörünüz
```

Bu ayar `git pull`, `reset --hard` ve tam yeniden klonlamadan sağ çıkar.

**Doğrulama:** İlk işi başlatın, klasör yapısı **sizin** klasörünüzde oluşuyor mu? Depoda
değilse doğru yapılandırılmıştır.

---

## Adım 4 — API anahtarları (isteğe bağlı)

Montajın büyük kısmı anahtar istemez. Anahtarlar gerektiren şey genelde görsel/video
üretimi ve gelişmiş seslendirmedir.

Detay: [ANAHTAR-TABLOSU.md](ANAHTAR-TABLOSU.md)

Kurulum sırasında ajan her anahtar için ne işe yaradığını ve maliyetini söyleyip **kararı
size bırakacaktır.**

---

## Adım 5 — İlk iş denemesi

Kurulumun çalıştığını kanıtlamak için küçük bir iş yapın:

> "Kaynak klasördeki videolardan 10 saniyelik bir test montajı yap. En güçlü birkaç klibi
> sırala, aralarına basit bir geçiş koy. Altyazı ekleme. Müzik önerme."

İzleyin:

1. Ajan klipleri gerçekten analiz ediyor mu
2. Çıktı **belirlediğiniz klasöre** yazıldı mı (depoya değil)
3. Eksik olanı söyledi mi

---

## Sorun giderme

| Belirti | Çözüm |
|---|---|
| Codex becerileri görmüyor | `ls ~/.agents/skills/` — kopyalama yapıldı mı? Codex'u yeniden başlatın. |
| `ffmpeg: command not found` | `brew install ffmpeg` |
| Node sürümü çok eski | `node --version` → 22+ olmalı |
| Çıktı depoda oluşuyor | `OPENMONTAGE_PROJECTS_DIR` ayarlanmamış — Adım 3'e dönün |
| Python sürüm hatası | Motorun kendi `venv`'ini kullanın, sistem Python'u değil |
| Ajan "bilmiyorum" diyor | Beklenen davranış. `montaj-rehberi` içindeki kurallara göre seçenekleri sunması gerekir. |

---

## Belgelendirme

| Dosya | İçerik |
|---|---|
| [README.md](README.md) | Pakete genel bakış |
| [ANAHTAR-TABLOSU.md](ANAHTAR-TABLOSU.md) | Anahtarlar ve maliyetler |
| [KAYNAKLAR-LISANS.md](KAYNAKLAR-LISANS.md) | Kaynaklar ve lisanslar |