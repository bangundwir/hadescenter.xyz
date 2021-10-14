---
title: Cara Clone Sebuah Repository id Github
date: 2021-10-14
author: Anonymouse
summary: Cara Clone Sebuah Repository
tags:
  - Tips

---

Selamat hari senin, semoga hari kalian menyenangkan ya dengan cuaca yang sedikit tidak menentu ini >.<

Kali ini saya akan membagikan sedikit cara untuk proses clone sebuah repository di github. Clone disini dimaksudkan untuk menduplikat sebuah repository, dan kali ini akan saya contohkan dengan menggunakan Github. Proses clone ini biasanya digunakan oleh para developer untuk berkolaborasi di dalam sebuah project, jadi sebuah project dikerjakan oleh lebih dari 1 orang dan project tersebut disimpan di 1 repository saja.

Langsung saja, berikut adalah langkah-langkahnya

Langkah pertama anda harus mengakses link repository yang ingin anda clone, anda bisa coba akses salah satu repository saya yang ada di Github pada link [ini](https://github.com/saraswatisc/bali-gophers-workshop).

Kemudian anda akan melihat gambar seperti dibawah ini

![img](https://miro.medium.com/max/1400/1*96jHjRM3ZIDPXg4RqAUKtg.png)

Arahkan kursor ke bagian tombol **Clone or download.** Pada gambar diatas anda akan diberikan pilihan clone, yaitu **Clone with SSH** atau **Clone use HTTPS.** Karena di git saya sudah setup SSH maka saya memilih link clone dengan menggunakan SSH, jika anda belum setting SSH anda dapat gunakan link clone dengan menggunakan HTTPS. Sejauh ini perbedaan yang saya alami adalah saya tidak perlu menginputkan password setiap melakukan perintah git jika menggunakan SSH. Untuk setting SSH akan saya jelaskan pada kesempatan lain.

Selanjutnya anda copy link yang diberikan dengan klik tombol yang sudah saya tandai dengan kotak merah.

Kini saatnya anda membuka terminal anda dan arahkan di directory mana akan anda simpan clone dari repository di github.

Saya meletakkan di directory **C:\Users\saras\icebox.** Selanjutnya anda dapat menjalankan perintah **git clone** dengan menyertakan link yang sudah anda copy sebelumnya seperti gambar dibawah ini

![img](https://miro.medium.com/max/60/1*lKGHiCwj8CnkVmOrdUntgg.png?q=20)

![img](https://miro.medium.com/max/666/1*lKGHiCwj8CnkVmOrdUntgg.png)

Proses clone ini memerlukan koneksi internet, jadi pastikan jaringan internet yang anda gunakan dalam kondisi stabil. Jika proses clone berhasil, maka akan tampil seperti gambar di bawah ini

![img](https://miro.medium.com/max/60/1*7a0FmjG0wgDRTXZXyB4Z0Q.png?q=20)

![img](https://miro.medium.com/max/676/1*7a0FmjG0wgDRTXZXyB4Z0Q.png)

Anda dapat mengecek project yang sudah anda clone di directory yang anda pilih tadi.

Sekian tutorial clone sebuah repository dari github yang dapat saya bagikan kali ini, sampai bertemu kembali di tutorial selanjutnya.

Terima kasih, happy coding :)