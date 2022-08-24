---
title: Add Domain Vercel + Cloudflare Setup
date: 2022-08-24
author: Anonymouse
summary: Domain Vercel + Cloudfalre Setup
tags:
  - Pemrograman
  - Tips


---

![img](https://images.squarespace-cdn.com/content/v1/5cc22d6593a63233d214110c/1597710652025-QEY2UL92MLE1E2BX4WSJ/Vercel+%28Zeit%29.jpg?format=1000w)



Saya suka meng-host domain saya di Cloudflare. Ini memberi saya kemampuan untuk mengubah server saya dengan cepat selain CDN, SSL, dan manfaat keamanan gratis. Dan sebelum saya lupa, saya menyukai penawaran Analytics baru yang mereka miliki. Jauh lebih baik daripada solusi sisi klien.

## Siapkan Domain dengan Vercel & Cloudflare

Vercel (sebelumnya ZEIT) dan Cloudflare tidak selalu langsung membahas topik pengaturan domain karena keduanya menawarkan beberapa fitur yang menjadi berlebihan. Seperti CDN, SSL, dll.

Jadi, untuk referensi di masa mendatang, jika saya lupa, tulis posting ini tentang cara mengatur domain Vercel (sebelumnya ZEIT) dan Cloudflare menggunakan langkah-langkah berikut:

- Pastikan untuk mengganti referensi di bawah ini dengan nama domain Anda yang sebenarnya, misalnya ahmadawais.com akan menjadi file .`example.tld``example.tld`
- **Cloudflare**: Klik tombol [Add Record] (Tambah Catatan). Pilih jenis , nama adalah milik Anda , dan di area konten tempel `TXT``example.tld``cname.vercel-dns.com`
- **Cloudflare**: Sekali lagi pilih ketik , namanya adalah milik Anda , dan di pasta target `CNAME``example.tld``cname.vercel-dns.com`
- Jika belum selesai, maka alihkan CNAME dari Sekarang buka tab **SSL / TLS** dan pilih aktifkan opsi SSL **Penuh (Ketat)**
- Menyiapkan **Aturan Halaman** dengan pola kecocokan lalu pilih **PENGATURAN SSL** dan **matikan**`*example.tld/.well-known/*`
- Buka dasbor Vercel.com Anda, Anda harus sudah memiliki proyek di sana, pergi ke dan kemudian dan tambahkan domain Anda ke Vercel sebagai `Settings``Domains``example.tld`
- Dan akhirnya, tambahkan di pengaturan proyek Vercel Anda`<domain>`

### UNTUK MENGONFIRMASI[#](https://ahmadawais.com/vercel-cloudflare-domain-setup/#to-confirm)

- Jalankan (Perhatikan bahwa itu dan tidak) di terminal Anda. Ini harus mengembalikan konfigurasi mana yang paling cocok untuk Vercel. Jika Anda menjalankan perintah dan mendapatkan pengalihan sebagai gantinya, maka Cloudflare mencegah rute ini diakses. Vercel akan menandai domain sebagai tidak dikonfigurasi`curl http://example.tld/.well-known/acme-challenge -I``http``https``HTTP/1.1 404 Not Found …``curl``3XX`
- Jika Anda masih mendapatkan kesalahan, pastikan di [Aturan Halaman](https://support.cloudflare.com/hc/en-us/articles/218411427-Understanding-and-Configuring-Cloudflare-Page-Rules-Page-Rules-Tutorial-) — Anda telah menonaktifkan SSL untuk jalur tersebut `example.tld/.well-known/*`
- Jika masih tidak berfungsi, maka beberapa kali opsi Cloudflare yang disebut [Selalu gunakan HTTPS](https://support.cloudflare.com/hc/en-us/articles/204144518-SSL-FAQ) bisa menjadi masalah. Konfigurasi ini ada di bawah dan kemudian tab dan dapat mempengaruhi aturan halaman Anda. Silakan dan nonaktifkan yang ini. Saya harus melakukannya ketika saya pindah dari pengaturan Netlify ke pengaturan di Vercel`SSL/TLS``Edge Certificates``A``CNAME`

Itu saja. Vercel (sebelumnya ZEIT) akan mulai memproses sertifikat SSL untuk Anda. Untuk pengaturan ini, Anda akan terus menggunakan server nama Anda untuk Cloudflare dan bahkan tidak perlu khawatir tentang pengaturan ANAME atau apa pun.

Gunakan kode Anda untuk selamanya. !🥁