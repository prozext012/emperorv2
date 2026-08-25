# dixzSTORE — Panel Admin

**Dashboard pengelolaan toko real-time, dengan login aman & analitik pengunjung**

Kelola produk, testimoni, status, chat pelanggan, dan pantau statistik kunjungan — semua tersinkron langsung ke web utama tanpa perlu deploy ulang.

![Firebase](https://img.shields.io/badge/Firebase-Firestore%20%7C%20Auth-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)
![Cloudinary](https://img.shields.io/badge/Media-Cloudinary-3448C5?style=for-the-badge&logo=cloudinary&logoColor=white)
![Chart.js](https://img.shields.io/badge/Charts-Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)
![Vercel](https://img.shields.io/badge/Deploy-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)

---

## Daftar Isi

- [Tentang Proyek](#tentang-proyek)
- [Fitur](#fitur)
- [Struktur Folder](#struktur-folder)
- [Tumpukan Teknologi](#tumpukan-teknologi)
- [Instalasi & Setup](#instalasi--setup)
- [Konfigurasi Firebase Authentication](#konfigurasi-firebase-authentication)
- [Keamanan](#keamanan)
- [Repo Terkait](#repo-terkait)

---

## Tentang Proyek

Repo ini adalah **dashboard admin dixzSTORE** — akses privat untuk mengelola seluruh konten yang tampil di web utama (`kaisarv1`). Dilindungi login Firebase Authentication, hanya satu akun admin yang diizinkan mengakses.

Setiap perubahan di sini (produk baru, testimoni, status, dll) langsung muncul di web utama secara real-time berkat `onSnapshot` Firestore.

---

## Fitur

| Fitur | Deskripsi |
|---|---|
| **Login aman** | Email & Password lewat Firebase Authentication, dibatasi 1 akun |
| **Manajemen produk** | Tambah, edit, hapus produk beserta gambar |
| **Kelola testimoni & notifikasi** | Atur konten yang tampil di web utama |
| **Kelola status/story** | Upload gambar/video, kedaluwarsa otomatis |
| **Edit profil toko** | Foto, banner, bio, nomor WhatsApp |
| **Inbox pesan masuk** | Baca chat dari pengunjung web utama |
| **Dashboard analitik** | Sesi pengunjung aktif & halaman terpopuler |
| **Pembersihan otomatis terjadwal** | Bersihkan data lama (status, chat, log) otomatis |

---

## Struktur Folder

- `admin.html` — Dashboard admin (single-page app)
- `firestore.rules` — Aturan keamanan database (dikelola bersama `kaisarv1`)

---

## Tumpukan Teknologi

| Kategori | Teknologi |
|---|---|
| **Frontend** | HTML5, CSS3, Vanilla JavaScript (ES Modules) |
| **Database** | Firebase Firestore (real-time) |
| **Autentikasi** | Firebase Authentication (Email/Password) |
| **Media** | Cloudinary (gambar & video) |
| **Visualisasi Data** | Chart.js |
| **Hosting** | Vercel |

---

## Instalasi & Setup

**1. Clone repository**
```bash
git clone <url-repo-kaisarv2>
cd kaisarv2
```

**2. Konfigurasi Firebase**

Salin config project Firebase (sama dengan yang dipakai di `kaisarv1`) ke `admin.html`:

```js
const firebaseConfig = {
  apiKey: "xxxxxxxxxxxxxxxxxxxxxxxx",
  authDomain: "xxxxxxxxxxx.firebaseapp.com",
  projectId: "xxxxxxxxxxx",
  storageBucket: "xxxxxxxxxxx.firebasestorage.app",
  messagingSenderId: "xxxxxxxxxxx",
  appId: "xxxxxxxxxxx"
};
```

**3. Konfigurasi Cloudinary**

Sesuaikan `CLOUDINARY_CLOUD_NAME` dan `CLOUDINARY_UPLOAD_PRESET` di `admin.html`.

**4. Jalankan secara lokal**
```bash
npx serve .
```

**5. Deploy**

Deploy folder ini sebagai project Vercel terpisah, arahkan ke domain:
`notifikasi-dixzvip.vercel.app`

---

## Konfigurasi Firebase Authentication

1. Di **Firebase Console → Authentication → Sign-in method**, aktifkan provider **Email/Password**
2. Di tab **Users**, tambahkan akun admin secara manual
3. Di **Authentication → Settings → Authorized domains**, tambahkan domain panel admin
4. Di **Google Cloud Console → Credentials**, pastikan API key dibatasi (*HTTP referrer restriction*) hanya untuk domain resmi

---

## Keamanan

Panel ini dilindungi berlapis:

| Lapisan | Fungsi |
|---|---|
| **Login wajib** | Halaman dashboard tersembunyi total sebelum login berhasil |
| **Validasi email ketat** | Hanya 1 alamat email yang diizinkan mengakses, dicek ulang tiap sesi |
| **Firestore Rules** | Validasi ulang di sisi server — walau UI login "dibobol", database tetap terlindungi |
| **API Key Restriction** | Kunci Firebase dibatasi hanya bisa dipanggil dari domain resmi |

> Jangan pernah menaruh **password** di dalam kode — hanya alamat **email** admin yang boleh ditulis di source code (untuk validasi tampilan), karena email bukan data rahasia. Password admin **hanya** tersimpan di sistem Firebase Authentication.

---

## Repo Terkait

| Repo | Fungsi | Domain |
|---|---|---|
| `kaisarv1` | Web utama / etalase toko | `dixz-vip.vercel.app` |
| **`kaisarv2`** *(repo ini)* | Panel admin & dashboard | `notifikasi-dixzvip.vercel.app` |

Kedua repo berbagi satu database Firebase yang sama secara real-time.

---

<sub>Dibuat untuk **dixzSTORE**</sub>
