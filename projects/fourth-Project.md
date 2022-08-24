---
title: Membangun Aplikasi Catatan Menggunakan React
emoji: 🚀
metaDescription: This is a sample meta description. If one is not present in your page/project's front matter, the default metadata.desciption will be used instead.
date: 2022-24-08T00:00:00.000Z
summary: Aplikasi Catatan Menguanakn React
tags:
  - javascrip
  - Reactjs
  - WebDevelopment
---

![img](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/02lu6rv7a5aq14z6v1cr.png)

[My Personal Notes (dwirz.my.id)](https://note.dwirz.my.id/)

### Kriteria Utama 1: Mampu Menampilkan Daftar Catatan

- Aplikasi harus mampu menampilkan daftar catatan dengan data awal (initial data) yang telah kami sediakan.

- Memanfaatkan state component untuk menyimpan data catatan.

- Menggunakan teknik array map untuk menampilkan daftar catatan.

  

### Kriteria Utama 2: Mampu Menambahkan Catatan

- Aplikasi harus mampu menambahkan data catatan baru.

- Memanfaatkan controlled component dalam membuat form input.

- Data catatan disimpan cukup pada memori saja (akan hilang jika browser di-refresh).

- Data catatan yang disimpan merupakan objek JavaScript dengan struktur berikut

  ```jsx
  {
    id: number | string,
    title: string,
    body: string,
    archived: boolean, 
    createdAt: string,
  }
  ```

  Berikut contoh data riilnya:

  ```jsx
  {
      id: 1,
      title: "Babel",
      body: "Babel merupakan tools open-source yang digunakan untuk mengubah sintaks ECMAScript 2015+ menjadi sintaks yang didukung oleh JavaScript engine versi lama. Babel sering dipakai ketika kita menggunakan sintaks terbaru termasuk sintaks JSX.",
      archived: false,
      createdAt: '2022-04-14T04:27:34.572Z'
    },
  ```

  - **Catatan:**
    Untuk id pada tiap catatan yang disimpan haruslah unik. Tips dalam menetapkan nilai untuk adalah Anda bisa memanfaatkan nilai *timestamp*. Untuk mendapatkan nilai timestamp di JavaScript cukup mudah, cukup dengan menuliskan expressions +new Date().

    

  ### Kriteria Utama 3: Mampu Menghapus Catatan

  - Aplikasi harus menyediakan tombol **hapus** untuk menghapus data catatan yang disimpan.

  - Terdapat *conditional rendering* di mana bila tidak terdapat data catatan, maka UI menampilkan pesan **“Tidak ada catatan”** atau pesan apa pun yang mengindikasikan data catatan kosong.

    

  Selain kriteria utama, terdapat kriteria opsional yang yang dapat Anda penuhi agar mendapat nilai yang lebih tinggi.

  

  ### Kriteria Opsional 1: Terdapat Fitur Pencarian Catatan

  - Aplikasi memiliki fitur pencarian catatan berdasarkan kata kunci yang dimasukkan, dengan ketentuan:

    - Jika kolom pencarian tidak kosong, maka aplikasi **hanya menampilkan daftar catatan yang judulnya mengandung kata kunci yang dimasukkan.**
    - Jika kolom pencariannya kosong, maka aplikasi menampilkan seluruh catatan.

  - Memanfaatkan controlled component dalam membangun fitur catatan.

    

  ### Kriteria Opsional 2: Terdapat Limit Karakter pada Input Judul Catatan

  - Aplikasi dapat mencegah pengguna untuk memberikan judul catatan lebih dari 50 karakter.

  - Menggunakan state dalam melimitasi, bukan atribut *maxlength*.

  - Menampilkan jumlah karakter tersisa yang dapat digunakan oleh pengguna.

    

  ### Kriteria Opsional 3: Terdapat Fitur Arsip Catatan

  - Aplikasi memiliki fitur arsip catatan.
  - Aplikasi harus menyediakan tombol **arsipkan/pindahkan** untuk mengarsipkan atau memindahkan catatan dari arsip.
  - Daftar catatan yang diarsip harus ditampilkan pada tempat terpisah dari catatan yang tidak diarsip.

