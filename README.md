# SIMAK SMANTANG v50.1 — GitHub + Vercel

Sistem Informasi Manajemen Akademik dan Kurikulum  
SMA Negeri 1 Mantang

## Isi Paket

- `index.html` — aplikasi SIMAK SMANTANG
- `vercel.json` — konfigurasi deployment statis Vercel
- `firestore.rules` — template awal Security Rules Cloud Firestore
- `storage.rules` — template awal Security Rules Firebase Storage
- `README.md` — panduan deployment

## 1. Upload ke GitHub

1. Buat repository baru, misalnya `simak-smantang`.
2. Upload seluruh file dalam folder ini ke root repository.
3. Commit perubahan.

Struktur repository:

```text
simak-smantang/
├── index.html
├── vercel.json
├── firestore.rules
├── storage.rules
└── README.md
```

## 2. Deploy ke Vercel

1. Masuk ke Vercel.
2. Pilih **Add New → Project**.
3. Import repository GitHub `simak-smantang`.
4. Framework Preset: **Other**.
5. Root Directory: default/root repository.
6. Build Command: kosong.
7. Output Directory: kosong.
8. Install Command: kosong.
9. Klik **Deploy**.

Setelah deployment selesai, Vercel akan memberikan domain HTTPS.

## 3. Firebase

Pada Firebase Console:

1. Buat atau gunakan Firebase Project.
2. Tambahkan **Web App**.
3. Aktifkan **Authentication → Email/Password**.
4. Buat **Cloud Firestore**.
5. Aktifkan **Firebase Storage**.
6. Salin konfigurasi Firebase Web App.
7. Di SIMAK buka:
   **Administrasi & Laporan → Firebase Production**
8. Masukkan:
   - `apiKey`
   - `authDomain`
   - `projectId`
   - `storageBucket`
   - `messagingSenderId`
   - `appId`
9. Klik **Simpan Config** lalu **Uji & Inisialisasi Firebase**.

## 4. Authorized Domains

Di Firebase Authentication → Settings → Authorized domains, tambahkan domain Vercel yang digunakan, misalnya:

```text
simak-smantang.vercel.app
```

Jika nanti memakai domain sekolah sendiri, tambahkan domain tersebut juga.

## 5. Security Rules

Gunakan `firestore.rules` dan `storage.rules` sebagai **template awal**. Jangan langsung menganggap template ini final untuk produksi. Uji setiap role di Firebase Emulator atau Rules Playground sebelum migrasi data.

## 6. Status v50.1

v50.1 adalah **Firebase Production Foundation**, tetapi belum melakukan migrasi penuh data lokal ke Firestore. `localStorage` masih menjadi sumber utama data aplikasi.

Tahap berikutnya adalah v51:
- pembuatan akun Firebase Authentication;
- pemetaan UID ke role;
- migrasi data Firestore;
- migrasi konfigurasi sistem;
- sinkronisasi multi-perangkat;
- validasi Security Rules;
- transisi bertahap dari localStorage ke Firestore.

## Catatan Keamanan

Firebase Web Config bukan rahasia server. Jangan simpan:
- service-account JSON,
- private key,
- password admin,
- credential server,
- token rahasia

di repository GitHub atau `index.html`.

Untuk keamanan produksi, gunakan Firebase Authentication dan Security Rules yang ketat.
