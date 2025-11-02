# Cara Kerja Platform Try Out TKA SD Kelas VI

## Ringkasan Sistem

Platform Try Out TKA SD Kelas VI adalah aplikasi web berbasis HTML, CSS (Tailwind), dan JavaScript (React) yang dirancang untuk membantu siswa kelas 6 SD berlatih menghadapi ujian Tes Kemampuan Akademik.

---

## Struktur Direktori

```
tryout-tka-sd-2025/
├── index.html                          # Halaman utama (landing page)
└── matematika/
    ├── index.html                      # Dashboard matematika
    ├── ringkasan-rumus.html            # Kumpulan rumus matematika
    ├── umum/                           # Kategori Umum
    │   ├── sesi-1.html                 # 25 soal dasar
    │   ├── sesi-2.html                 # 25 soal pengembangan
    │   ├── sesi-3.html                 # 50 soal pendalaman
    │   ├── sesi-4.html                 # (dalam pengembangan)
    │   └── sesi-5.html                 # (dalam pengembangan)
    └── khusus/                         # Kategori Khusus
        └── operasi-bilangan-sesi-1.html # 25 soal operasi bilangan
```

---

## Alur Kerja Platform

### 1. **Halaman Utama (index.html)**

**Fungsi:**
- Landing page yang menampilkan 4 mata pelajaran: Matematika, Bahasa Indonesia, IPA, dan PKN
- Saat ini hanya Matematika yang aktif, mata pelajaran lain dalam pengembangan

**Fitur:**
- Design gradien modern dengan Tailwind CSS
- Card hover effects untuk interaksi visual
- Badge status "Tersedia" vs "Segera Hadir"
- Informasi panduan penggunaan platform

**Teknologi:**
- HTML5 dengan semantic markup
- Tailwind CSS (via CDN) untuk styling
- CSS custom untuk animasi dan gradient

---

### 2. **Dashboard Matematika (matematika/index.html)**

**Fungsi:**
- Hub utama untuk materi matematika
- Menampilkan 2 kategori pembelajaran berbeda

**Kategori Pembelajaran:**

#### A. **KATEGORI UMUM** (5 Sesi)
Sesi fundamental yang disusun sistematis:
- **Sesi 1**: Pengenalan Dasar (25 soal) - Operasi Bilangan Bulat, Pecahan & Desimal ✓ Aktif
- **Sesi 2**: Pengembangan (25 soal) - Geometri, Pengukuran, Statistika ✓ Aktif
- **Sesi 3**: Pendalaman (50 soal) - Perbandingan, Skala, Debit, Kecepatan ✓ Aktif
- **Sesi 4**: Latihan Intensif (50 soal) - Segera Hadir
- **Sesi OSN**: Olimpiade (60 soal) - Segera Hadir

#### B. **KATEGORI KHUSUS** (Pendalaman Topik Spesifik)
Dirancang untuk pendalaman topik tertentu dengan multiple sesi bertingkat:
- **Operasi Bilangan**: 4 sesi (Sesi 1 aktif, 2-4 dalam pengembangan)
  - Tingkatan: Awal ★★☆☆ → Menengah ★★★☆ → Lanjutan ★★★★ → OSN ★★★★★
- **Geometri & Pengukuran**: Segera Hadir
- **Statistika & Peluang**: Segera Hadir

#### C. **RINGKASAN RUMUS**
- Kompendium rumus matematika lengkap
- 10 kategori khusus dengan tabel dan tips praktis

**Fitur UI:**
- Progress bar untuk tracking materi
- Badge status (Aktif/Segera Hadir)
- Stats cards (jumlah sesi, total soal, konten tersedia)
- Breadcrumb navigation
- Hover effects dengan animasi lift

---

### 3. **Sistem Kuis Interaktif (File Sesi)**

**Teknologi Stack:**
- **React 18.2.0** (via CDN) - Framework UI interaktif
- **Babel** (in-browser transpiler) - Untuk JSX transformation
- **Tailwind CSS** - Styling responsif
- **SVG** - Visualisasi diagram dan ilustrasi

#### Komponen Utama React

**A. State Management (useState)**
```javascript
const [currentQuestion, setCurrentQuestion] = useState(0)
const [userAnswers, setUserAnswers] = useState({})
const [showResults, setShowResults] = useState(false)
const [expandedExplanations, setExpandedExplanations] = useState({})
```

**State yang dikelola:**
- `currentQuestion`: Nomor soal yang sedang ditampilkan (0-based index)
- `userAnswers`: Object berisi jawaban user {nomorSoal: 'A/B/C/D'}
- `showResults`: Boolean untuk toggle mode latihan/hasil
- `expandedExplanations`: Object untuk track pembahasan yang dibuka

#### Alur Kerja Kuis

**1. Mode Latihan (showResults = false)**

```
[Soal ke-X]
├── Nomor soal
├── Pertanyaan soal
├── [Visual/Diagram] (jika ada)
├── 4 Pilihan Jawaban (A, B, C, D)
├── Tombol navigasi
│   ├── ← Soal Sebelumnya
│   └── Soal Berikutnya →
└── Progress: "X dari 25 soal terjawab"
```

**Fitur:**
- User bisa memilih jawaban (A/B/C/D)
- Jawaban tersimpan di state `userAnswers`
- User bisa navigasi bebas antar soal
- Tombol "Lihat Hasil" muncul setelah semua soal dijawab
- Tombol Print/Download untuk menyimpan soal

**2. Mode Hasil (showResults = true)**

```
[Ringkasan Hasil]
├── Score: "XX dari 25 benar (XX%)"
├── Status: "Sangat Baik / Baik / Cukup / Perlu Belajar Lagi"
├── Daftar Semua Soal
    └── Setiap Soal:
        ├── Nomor & Pertanyaan
        ├── [Visual/Diagram] (jika ada)
        ├── Pilihan Jawaban dengan indikator:
        │   ├── ✓ Hijau = Jawaban benar
        │   ├── ✗ Merah = Jawaban user yang salah
        │   └── Gray = Pilihan lain
        ├── Badge: "Benar" (hijau) atau "Salah" (merah)
        └── [Pembahasan] (dapat dibuka/tutup)
            └── Penjelasan detail cara penyelesaian
```

**Fitur:**
- Automatic grading system
- Color-coded feedback (hijau=benar, merah=salah)
- Expandable explanations (accordion)
- Tombol "Kembali ke Beranda"
- Tombol "Ulangi Latihan" untuk reset

#### Sistem Visualisasi

**8 Tipe Diagram SVG Interaktif:**

1. **DiagramBatang** - Visualisasi data hasil panen
2. **TamanKolam** - Ilustrasi geometri (persegi + lingkaran)
3. **DiagramLingkaran** - Pie chart distribusi hobi
4. **BangunGabungan** - Persegi panjang + segitiga
5. **PrismaSegitiga** - Bangun ruang 3D
6. **KoordinatKartesius** - Sistem koordinat dengan grid
7. **KubusLimas** - Bangun ruang gabungan
8. **LimasSegiempat** - Limas dengan alas segiempat
9. **PerjalananKecepatan** - Ilustrasi soal cerita kecepatan

**Karakteristik Visualisasi:**
- Dibuat dengan SVG native (scalable, tidak pixelated)
- Responsive dengan `viewBox`
- Interactive hover states
- Color-coded untuk memudahkan pemahaman
- Dilengkapi label, dimensi, dan keterangan

---

## Data Soal

**Format Data:**
```javascript
{
  no: 1,                                    // Nomor soal
  soal: 'Pertanyaan...',                    // Teks soal
  pilihan: ['A. ...', 'B. ...', ...],       // Array pilihan jawaban
  jawaban: 'A',                             // Kunci jawaban
  pembahasan: 'Penjelasan lengkap...',      // Pembahasan
  visual: <KomponenVisualisasi />           // (Optional) Komponen React
}
```

**Karakteristik Soal:**
- Soal bersifat kontekstual (real-world problems)
- Tingkat kesulitan progresif
- Mencakup semua topik matematika SD kelas VI
- Dilengkapi pembahasan detail step-by-step

---

## Fitur-Fitur Khusus

### 1. **Sistem Penilaian Otomatis**
```javascript
const correctCount = soalData.filter(
  (q, idx) => userAnswers[idx] === q.jawaban
).length
```

### 2. **Progress Tracking**
- Jumlah soal terjawab
- Persentase penyelesaian
- Visual progress bar

### 3. **Print/Download Function**
- Tombol print untuk menyimpan soal ke PDF
- Function: `window.print()`

### 4. **Navigation System**
- Breadcrumb navigation
- Back to home button
- Sequential question navigation

### 5. **Responsive Design**
- Mobile-first approach
- Grid system dengan Tailwind
- Breakpoints: sm, md, lg, xl

---

## Teknologi yang Digunakan

| Teknologi | Versi | Fungsi |
|-----------|-------|--------|
| React | 18.2.0 | UI Framework & State Management |
| React DOM | 18.2.0 | Rendering ke DOM |
| Tailwind CSS | Latest (CDN) | Utility-first CSS Framework |
| Babel Standalone | Latest | In-browser JSX transformation |
| HTML5 | - | Struktur markup |
| SVG | - | Visualisasi diagram |

**CDN Links:**
- React: `cdnjs.cloudflare.com/ajax/libs/react/18.2.0/`
- Tailwind: `cdn.tailwindcss.com`
- Babel: Implicitly loaded for JSX

---

## Alur User Journey

```
1. User mengakses index.html
   ↓
2. Klik card "Matematika"
   ↓
3. Masuk ke dashboard matematika/index.html
   ↓
4. Pilih sesi (Kategori Umum atau Khusus)
   ↓
5. Kerjakan soal satu per satu
   - Pilih jawaban A/B/C/D
   - Navigasi antar soal
   ↓
6. Setelah semua dijawab, klik "Lihat Hasil"
   ↓
7. Review hasil:
   - Lihat score
   - Review jawaban benar/salah
   - Baca pembahasan
   ↓
8. Pilihan:
   - Ulangi latihan (reset)
   - Kembali ke dashboard
   - Pilih sesi lain
```

---

## Keunggulan Sistem

1. **Pure Frontend** - Tidak memerlukan backend/database, dapat dihost statis
2. **Offline-capable** - Setelah load pertama, bisa berjalan tanpa internet (kecuali CDN)
3. **Lightweight** - Hanya HTML + React (no heavy frameworks)
4. **Interactive** - Real-time feedback dan visualisasi
5. **Educational** - Fokus pada pemahaman dengan pembahasan detail
6. **Scalable** - Mudah menambah mata pelajaran/sesi baru
7. **Responsive** - Berjalan optimal di desktop, tablet, dan mobile
8. **Modern UI** - Design gradien, animasi smooth, user-friendly

---

## Limitasi & Future Development

**Limitasi Saat Ini:**
- Data soal hardcoded (tidak menggunakan JSON eksternal)
- Tidak ada persistensi data (refresh = reset)
- Hanya Matematika yang aktif
- Beberapa sesi masih dalam pengembangan

**Rencana Pengembangan:**
- Tambahan mata pelajaran: Bahasa Indonesia, IPA, PKN
- Sistem login & tracking progress user
- Leaderboard & gamification
- Export hasil ke PDF
- Timer untuk latihan
- Randomize soal
- Bank soal lebih besar

---

## Cara Menjalankan

### Option 1: Local Development
```bash
# Langsung buka file di browser
open index.html
# atau
python -m http.server 8000
# Akses: http://localhost:8000
```

### Option 2: Deploy ke Hosting Statis
- **GitHub Pages**: Push ke repo, enable GitHub Pages
- **Netlify**: Drag & drop folder
- **Vercel**: Import Git repository
- **Cloudflare Pages**: Connect Git repo

**Tidak memerlukan:**
- Node.js server
- Database setup
- Build process
- Environment variables

---

## Kesimpulan

Platform Try Out TKA SD Kelas VI adalah sistem pembelajaran interaktif berbasis web yang:
1. Menggunakan React untuk interaktivitas
2. Menyediakan visualisasi SVG untuk pemahaman konsep
3. Memberikan feedback real-time dengan sistem penilaian otomatis
4. Menyajikan pembahasan detail untuk setiap soal
5. Mudah di-maintain dan dikembangkan lebih lanjut

Sistem ini efektif untuk self-paced learning dengan fokus pada pemahaman konsep, bukan sekedar hafalan.
