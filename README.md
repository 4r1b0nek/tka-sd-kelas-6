# TKA SD Kelas 6 — Latihan Online

Aplikasi latihan **Tes Kemampuan Akademik (TKA) SD Kelas 6** berupa aplikasi web satu halaman (HTML + PWA). Berisi **400 soal** (100 soal per mapel: Matematika, Bahasa Indonesia, IPA, dan Bahasa Inggris). Setiap sesi menampilkan 20 soal acak dengan pembahasan detail, analisis per topik, riwayat percobaan, dan laporan hasil yang bisa dicetak atau disimpan sebagai PDF.

## Fitur

| Fitur | Keterangan |
|---|---|
| 4 mata pelajaran | Matematika, Bahasa Indonesia, IPA, Bahasa Inggris |
| Bank soal | 100 soal per mapel (400 soal); **20 soal acak per sesi**, pilihan ganda A–D |
| Pembahasan detail | Kunci jawaban + alasan benar/salah untuk setiap soal |
| Dua mode | **Mode Ujian** (20 soal acak, 30 menit, pembahasan di akhir) dan **Mode Latihan** (tanpa batas waktu, pembahasan langsung) |
| Pemanasan | Maskot lucu + pesan semangat, pilihan **Asiap / Belum siap**, lalu hitung mundur **5 detik** sebelum sesi dimulai |
| Perayaan | Setelah menekan tombol selesai: layar **“Kamu hebat!”** dengan konfeti, pilihan **Cek lagi / Selesai**, lalu hitung mundur 5 detik sebelum hasil |
| Evaluasi | Skor 0–100, predikat, jumlah benar/salah/kosong, waktu pengerjaan |
| Analisis topik | Persentase penguasaan per topik + rekomendasi materi yang perlu diulang |
| Riwayat | 30 percobaan terakhir tersimpan di browser, bisa dibuka kembali |
| Laporan | Cetak / simpan PDF, sudah termasuk tabel hasil, analisis, pembahasan, dan kolom tanda tangan |
| Navigasi | Grid nomor soal, tanda ragu-ragu, dan pintasan keyboard `1`–`4`, `←`, `→` |
| Responsif | Nyaman dipakai di laptop, tablet, maupun ponsel |
| PWA / Android | Bisa dipasang di layar utama, terbuka tanpa address bar, offline, dan punya shortcut per mapel |

## Sebaran bank soal

- **Matematika (100 soal):** operasi bilangan & pecahan, FPB & KPK, perbandingan/skala/persen, pengukuran & debit, geometri & bangun ruang, statistika & pola.
- **Bahasa Indonesia (100 soal):** gagasan pokok & paragraf, kosakata & ungkapan, kata baku/ejaan/imbuhan, kalimat efektif & tanda baca, jenis teks & sastra, surat/pidato/wawancara/iklan.
- **IPA (100 soal):** ciri & klasifikasi makhluk hidup, ekosistem & simbiosis, perkembangbiakan, tubuh manusia, benda/gaya/energi, listrik/magnet/cahaya/bunyi, tata surya.
- **Bahasa Inggris (100 soal):** kosakata & ejaan, kata ganti & to be, present tense, preposisi/artikel/bilangan, membaca teks, percakapan & ungkapan.

## Cara membuka

1. Unduh folder ini.
2. Klik dua kali `index.html` — aplikasi langsung terbuka di browser.
3. Tidak perlu internet, instalasi, atau server.

> Data hasil disimpan di **localStorage** browser. Jika file dipindah, dibuka di browser lain, atau mode incognito, riwayat tidak ikut berpindah.

## Cara mempublikasikan (opsional)

Supaya bisa diakses lewat tautan (dan bisa dipasang di Android):

- **Netlify Drop** — buka <https://app.netlify.com/drop>, tarik **seluruh folder ini** ke halaman tersebut. Selesai.
- **GitHub Pages** — unggah semua file (`index.html`, `manifest.json`, `sw.js`, folder `icons/`) ke repositori, lalu aktifkan Pages (branch `main`, folder `/root`).
- **Vercel / Cloudflare Pages** — impor folder, tanpa build command.

Nama file `index.html` sengaja dipakai agar langsung menjadi halaman utama saat di-hosting. Unggah seluruh folder, bukan hanya `index.html`, agar manifest, ikon, dan service worker ikut berfungsi.

## Pasang di Android (shortcut layar utama)

Aplikasi ini sudah disiapkan sebagai **PWA**, sehingga bisa dipasang seperti aplikasi biasa.

1. Publikasikan folder ini (Netlify Drop / GitHub Pages / Vercel). PWA memerlukan **HTTPS** — membuka `file://` tidak bisa memasang service worker.
2. Buka tautannya di **Chrome Android**.
3. Setelah halaman terbuka, akan muncul kartu **“📲 Pasang di layar utama”** — tekan **Pasang**. Jika kartu tidak muncul, buka menu **⋮ → Instal aplikasi / Tambahkan ke Layar Utama**.
4. Ikon bintang TKA SD muncul di layar utama. Aplikasi terbuka tanpa address bar dan tetap bisa dipakai offline setelah sekali dibuka.
5. **Tekan lama ikon** untuk shortcut langsung ke Matematika, B. Indonesia, IPA, atau B. Inggris.

Catatan:

- Kalau hanya membuka `index.html` langsung dari penyimpanan HP (tanpa hosting), Chrome masih bisa membuat shortcut lewat menu “Tambahkan ke Layar Utama”, tetapi tidak dalam mode standalone/offline PWA.
- iPhone/iPad: Safari → **Bagikan** → **Tambahkan ke Layar Utama** (memakai `icons/icon-180.png`).
- Untuk memperbarui versi yang sudah dipasang, buka aplikasi saat online; service worker mengambil `index.html` terbaru.

### File PWA

- `manifest.json` — nama, ikon, warna, dan 4 shortcut mapel.
- `sw.js` — cache offline halaman + ikon.
- `icons/` — ikon 192/512, maskable, dan Apple 180.

## Struktur soal

Semua soal ada di dalam `index.html`, pada objek `BANK` di bagian awal `<script>`:

```js
{
  id: "M1",                          // unik, dipakai untuk riwayat & pembahasan
  topik: "Operasi bilangan & pecahan", // dasar analisis per topik
  level: "Sedang",                   // "Mudah" | "Sedang" | "Sulit"
  teks: "…",                         // opsional, untuk bacaan/pantun/cerita
  tanya: "Hasil dari … adalah ....",
  opsi: ["−33", "−45", "15", "27"],  // selalu 4 pilihan
  kunci: 0,                          // indeks jawaban benar (0 = A)
  bahas: "Kerjakan perkalian …\nBaris baru dipisah \\n."
}
```

Untuk menambah soal: tambahkan objek baru ke array `soal` pada mapel terkait. Jumlah soal yang ditampilkan tiap sesi diatur oleh `JUMLAH_TAMPIL` (default 20); grid navigasi menyesuaikan otomatis.

## Catatan teknis

- Inti aplikasi tetap satu `index.html` tanpa library eksternal (font sistem + emoji). File PWA (`manifest.json`, `sw.js`, `icons/`) hanya diperlukan untuk pemasangan dan mode offline.
- Shortcut mapel membuka `index.html?mapel=matematika` (atau `bahasa`, `ipa`, `inggris`) dan langsung menampilkan layar Asiap untuk mapel tersebut.
- Setiap sesi mengambil 20 soal secara acak dari bank, dengan satu soal per topik lebih dahulu agar semua topik terwakili. Urutan pilihan jawaban juga diacak per sesi.
- Sebelum sesi dimulai, muncul layar pemanasan (Asiap / Belum siap). Jika memilih Asiap, hitung mundur 5 detik berjalan; timer ujian baru dimulai setelah hitungan selesai.
- Analisis dan skor dihitung ulang dari jawaban, sehingga riwayat lama tetap bisa dibuka meskipun urutan soal diubah.
- Menutup tab saat sesi berjalan akan menyimpan progres; banner “Lanjutkan” muncul di halaman utama.
- Waktu habis pada Mode Ujian mengumpulkan jawaban secara otomatis.
- Cetak: gunakan tombol **Cetak / Simpan PDF**, lalu pilih *Save as PDF* pada dialog cetak.

## Lisensi

Bebas digunakan dan dimodifikasi untuk keperluan belajar mengajar di sekolah.
