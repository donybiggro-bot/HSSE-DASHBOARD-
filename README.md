# 🛡️ Dashboard HSSE Bulanan — Pertamina Gas

Dashboard pelaporan HSSE (Health, Safety, Security & Environment) berbasis web untuk laporan bulanan Pertamina Gas. Tidak perlu instalasi — cukup buka di browser.

**🔗 Live demo:** `https://<username>.github.io/hsse-dashboard/`

---

## 📋 Fitur

| Item | Keterangan |
|------|------------|
| ⏱️ Jam Kerja Selamat | Total jam kerja, jam selamat, tenaga kerja, YTD |
| 🚨 Laporan Insiden | FAT, LTI, RWC, MTC, FAC, Near Miss, PD + LTIFR otomatis |
| 👁️ Laporan PEKA | Target vs realisasi observasi, safe/at-risk behavior |
| 🌿 Laporan Lingkungan | Limbah B3, konsumsi air, emisi GRK, tumpahan |
| 🦺 Safety Program | Safety talk, inspection, training, drill, close-out temuan |

- ✅ Infografis langsung dari form input
- ✅ LTIFR dihitung otomatis
- ✅ Warna status otomatis (hijau / kuning / merah)
- ✅ Dark mode support
- ✅ Bisa dicetak / print
- ✅ Tidak butuh internet / backend

---

## 🚀 Deploy ke GitHub Pages (5 menit)

### 1. Fork / Upload repo ini

```bash
# Clone repo ini
git clone https://github.com/<username>/hsse-dashboard.git
cd hsse-dashboard
```

### 2. Push ke GitHub

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### 3. Aktifkan GitHub Pages

1. Buka repo di GitHub → **Settings**
2. Klik **Pages** di sidebar kiri
3. Source: pilih **Deploy from a branch**
4. Branch: **main** → folder **/ (root)**
5. Klik **Save**

Dalam 1–2 menit, dashboard live di:
```
https://<username>.github.io/hsse-dashboard/
```

---

## 📁 Struktur File

```
hsse-dashboard/
├── index.html        # Halaman utama
├── css/
│   └── style.css     # Semua styling
├── js/
│   └── app.js        # Logic form & generate infografis
└── README.md
```

---

## 🔄 Update Laporan Bulanan

1. Buka link GitHub Pages Anda
2. Isi form input dengan data bulan terbaru
3. Klik **Generate Infografis**
4. Gunakan tombol **🖨️ Cetak** untuk mencetak / export PDF

---

## 🛠️ Teknologi

- Pure HTML5 + CSS3 + Vanilla JavaScript
- Tanpa framework, tanpa dependency
- Responsive (mobile & desktop)
- Dark mode otomatis

---

## 📄 Lisensi

Internal use — Pertamina Gas HSSE Department.
