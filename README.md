# 🛠️ Unified Recovery Builder

> Gabungan & optimalisasi dari **Action-TWRP-Builder** + **Custom-Recovery-Builder-twrp**  
> by YoruPrjkt

---

## ✨ Fitur

| Fitur | Keterangan |
|-------|-----------|
| 🔧 **Multi-Recovery** | TWRP · OrangeFox · PBRP · TWRP Legacy |
| 📱 **Universal Device** | Semua device Android (Qualcomm, MTK, Exynos, dll) |
| 🌿 **Multi-Branch** | twrp-7.1 ~ twrp-12.1, ofox 11/12.1, PBRP 11/12.1 |
| 🎯 **Multi-Target** | recovery · boot · vendorboot |
| 🔗 **Common Tree** | Support optional common device tree |
| 📦 **Auto Deps** | Auto-detect & sync device dependencies |
| 📄 **Auto Makefile** | Auto-detect prefix: twrp\_ / omni\_ / pb\_ / recovery\_ |
| ⚡ **ccache** | Cache build artifacts (rebuild jauh lebih cepat) |
| 🔍 **LDCheck** | Optional blob dependency checker |
| 🔑 **SSH Keys** | Support private manifest/tree via SSH |
| 📢 **Telegram** | Notifikasi build sukses/gagal ke Telegram |
| 💾 **Swap 24GB** | Default 24GB swap untuk build stabil |
| 🇮🇩 **Auto Timezone** | Asia/Jakarta |

---

## 🚀 Setup

### 1. Secrets yang dibutuhkan

Pergi ke **Settings → Secrets and variables → Actions**, tambahkan:

| Secret | Wajib? | Keterangan |
|--------|--------|-----------|
| `GITHUB_TOKEN` | ✅ Auto | Sudah otomatis tersedia |
| `SSH_PRIVATE_KEY` | ❌ Opsional | Jika pakai manifest/tree private via SSH |
| `TELEGRAM_BOT_TOKEN` | ❌ Opsional | Bot token untuk notifikasi Telegram |
| `TELEGRAM_CHAT_ID` | ❌ Opsional | Chat ID tujuan notifikasi |

---

## 📋 Parameter Build

### Recovery Type
| Pilihan | Keterangan |
|---------|-----------|
| `TWRP` | TWRP modern (twrp-11, twrp-12.1) |
| `OrangeFox` | OrangeFox Recovery (11.0, 12.1) |
| `PBRP` | PitchBlack Recovery Project (android-11.0, android-12.1) |
| `TWRP-Legacy` | TWRP lama (twrp-7.1, twrp-8.1, twrp-9.0, omni-*) |

### Manifest Branch
```
TWRP       : twrp-12.1 | twrp-11 | twrp-9.0
OrangeFox  : 12.1 | 11.0
PBRP       : android-12.1 | android-11.0
Legacy     : twrp-7.1 | twrp-8.1 | twrp-9.0 | omni-7.1 | omni-8.1
```

### Manifest URL (opsional)
Kosongkan → auto-detect berdasarkan Recovery Type + Branch.  
Isi manual jika pakai fork/mirror:
```
https://github.com/fork-user/platform_manifest_twrp_aosp
git@github.com:user/manifest   ← jika SSH
```

### Build Target
| Target | Keterangan |
|--------|-----------|
| `recovery` | recovery.img (most common) |
| `boot` | boot.img (untuk device A/B tanpa recovery partition) |
| `vendorboot` | vendor_boot.img (GKI devices) |

---

## 📝 Contoh Konfigurasi

### Xiaomi Redmi 5 Plus (vince) — TWRP 12.1
```
Recovery Type  : TWRP
Manifest Branch: twrp-12.1
Device Tree    : https://github.com/rahmatsobrian/android_device_xiaomi_vince
Device Branch  : twrp-12.1
Device Path    : device/xiaomi/vince
Device Name    : vince
Build Target   : recovery
```

### Redmi Note 4 (mido) — OrangeFox
```
Recovery Type  : OrangeFox
Manifest Branch: 12.1
Device Tree    : https://github.com/user/android_device_xiaomi_mido
Device Branch  : ofox-12.1
Device Path    : device/xiaomi/mido
Device Name    : mido
Build Target   : recovery
```

### Legacy device — TWRP 9.0
```
Recovery Type  : TWRP-Legacy
Manifest Branch: twrp-9.0
Device Tree    : https://github.com/user/android_device_brand_codename
Device Branch  : twrp-9.0
Device Path    : device/brand/codename
Device Name    : codename
Build Target   : recovery
```

---

## 🔍 LDCheck

LDCheck berguna untuk debug missing library dependencies (decryption blobs).  
Set `LDCHECK_PATH` ke binary yang ingin dicek, contoh:
```
system/bin/qseecomd
vendor/bin/hw/android.hardware.keymaster@4.0-service
```
Kosongkan untuk skip LDCheck.

---

## ⚡ ccache

ccache otomatis di-cache antar runs via `actions/cache`.  
Cache key per device + recovery + branch → rebuild kedua jauh lebih cepat.

---

## 📁 Struktur Repo

```
.
├── .github/
│   └── workflows/
│       └── Recovery-Builder-Unified.yml   ← Workflow utama
├── scripts/
│   └── convert.sh                         ← Parser dependencies
├── tools/
│   ├── ldcheck                            ← LDCheck binary
│   └── libneeds                           ← LDCheck helper
└── README.md
```

---

## 🙏 Credits

- [Action-TWRP-Builder](https://github.com/azwhikaru/Action-TWRP-Builder) by azwhikaru
- [Custom-Recovery-Builder](https://github.com/Rangertabib/Custom-Recovery-Builder-twrp) 
- [TeamWin](https://github.com/TeamWin) — TWRP
- [OrangeFox Project](https://gitlab.com/OrangeFox)
- [PitchBlack Recovery Project](https://github.com/PitchBlackRecoveryProject)
- Unified & enhanced by **Yoru Prjkt** 🔥
