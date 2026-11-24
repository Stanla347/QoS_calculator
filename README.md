# QoS Calculator

Website kalkulator **Quality of Service** jaringan: Throughput, Packet Loss, Delay, Jitter, dan indeks rata-rata standar TIPHON. Satu file (`index.html`), tanpa build, tanpa dependensi — langsung jalan di GitHub Pages.

## Fitur
- Kalkulator 4 parameter dengan hasil langsung dan substitusi rumus (sama seperti perhitungan manual/Excel).
- Impor CSV (format Excel Anda: pemisah `;`, desimal koma) — otomatis menghitung Total Delay, Total Jitter, dan Jumlah Paket, lengkap dengan grafik.
- Pilihan mode jitter: **bertanda** (persis Excel) atau **absolut**.
- Indeks TIPHON per parameter + indeks rata-rata + kategori.
- Halaman Fungsi & Rumus, Cara Konvensional (Wireshark + Excel), Tabel Indeks, dan Riwayat (disimpan di browser, bisa ekspor CSV).
- Salin hasil, cetak/PDF.

## Rumus
| Parameter | Rumus |
|---|---|
| Throughput | `(Jumlah Bytes ÷ Timespan) × 8` → bit/s |
| Packet Loss | `((Dikirim − Diterima) ÷ Dikirim) × 100` → % |
| Delay | `(Total Delay ÷ Jumlah Paket) × 1000` → ms (delay paket = `time 2 − time 1`) |
| Jitter | `(Total Jitter ÷ Jumlah Paket) × 1000` → ms (jitter paket = `delay 2 − delay 1`) |
| Indeks rata-rata | `(I_throughput + I_loss + I_delay + I_jitter) ÷ 4` |

## Format CSV
Header (baris pertama):

```
No.;Time;;time 1;time 2;delay;;delay 1';delay 2;jitter
```

- Baris data harus diawali nomor di kolom `No.`; baris ringkasan (Total/Rata) otomatis diabaikan.
- Jumlah paket = banyaknya baris bernomor (sama seperti Excel).
- Kolom `delay` dan `jitter` dipakai apa adanya; bila kosong, dihitung dari `time 2 − time 1` dan `delay 2 − delay 1`.
- Tombol **Unduh contoh format CSV** di halaman Impor CSV memberi file contoh.

## Deploy ke GitHub Pages
1. Buat repository baru di GitHub (mis. `qos-calculator`).
2. Unggah `index.html` dan `README.md` ke root repository (tombol **Add file → Upload files**), lalu **Commit changes**.
3. Buka **Settings → Pages**.
4. Pada **Build and deployment**, pilih **Source: Deploy from a branch**, branch **main**, folder **/ (root)**, lalu **Save**.
5. Tunggu ±1 menit. Situs aktif di `https://<username>.github.io/qos-calculator/`.

Alternatif lewat terminal:

```bash
git init
git add index.html README.md
git commit -m "QoS Calculator"
git branch -M main
git remote add origin https://github.com/<username>/qos-calculator.git
git push -u origin main
```

## Mengubah ambang indeks
Buka `index.html`, cari objek `TIPHON` di awal blok `<script>`. Tiap baris berisi indeks (`i`), teks rentang, dan fungsi `test`. Tabel di halaman otomatis mengikuti.

## Catatan
- Indeks Throughput memakai persentase terhadap bandwidth, jadi isi kolom **Bandwidth** bila ingin indeks tersebut ikut dihitung. Bila kosong, indeks rata-rata dihitung dari parameter yang tersedia.
- Semua perhitungan berjalan di browser; file CSV tidak diunggah ke server mana pun.
- Font memakai Google Fonts; bila offline, otomatis memakai font sistem.
