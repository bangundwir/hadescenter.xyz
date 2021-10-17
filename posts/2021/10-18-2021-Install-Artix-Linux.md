---
title: Install Artix Linux 🐱‍👤
date: 2021-10-18
author: Anonymouse
summary: Install Artix Linux
tags:
  - Tips



---

![Cover image for ❗Install Artix Linux ](https://res.cloudinary.com/practicaldev/image/fetch/s--7N0gq-hL--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ueql52v6tcbhrvq5v0qh.png)

Salam, dalam artikel pertama saya ini, saya akan mencoba untuk menunjukkan cara menginstal Arch seperti distribusi Linux, [khususnya, Artix Linux](https://artixlinux.org/) alias dari awal. (i.e. from a base .iso image)
Saya akan mencoba menjelaskan segala sesuatu yang tidak sepele tanpa masuk ke banyak kedalaman. Untuk itu Anda selalu bisa mereferensikan [wiki Artix.](https://wiki.artixlinux.org/) `The Art Of Linux`

*Tujuan dari artikel ini adalah untuk membuat tangan Anda kotor, mencoba dan bereksperimen dengan menginstal Distribusi Linux dari awal dan dengan demikian mendapatkan pemahaman yang lebih baik tentang keindahan sistem operasi UNIX, khususnya Linux dan juga mendapatkan pemahaman yang lebih baik tentang bagaimana sistem operasi bekerja di belakang layar. (Kami tidak akan melakukan kursus ilmu komputer Sistem Operasi di sini dan tentu saja kami tidak akan menggunakan C untuk memodifikasi atau bahkan menulis kernel Linux di sini, tetapi Anda akan mendapatkan intinya nanti ...)*

Karena ini adalah instalasi Linux minimal, saya juga menjaga artikel ini tetap minim. (yaitu tanpa gambar (kecuali yang di bawah ini ^.-)). Alasan untuk itu adalah, bahwa Anda perlu menyelam, membaca dengan hati-hati apa yang terjadi dan bereksperimen di mesin Anda sendiri dan tidak hanya mengikuti slideshow gambar dan copy paste beberapa perintah. Jika Anda gagal instalasi pertama Anda, itu benar-benar sempurna. Semua orang gagal! Dapatkan tangan Anda kotor dan mencoba lagi, gagal lagi dan mencoba lagi. Begitulah cara itu akan menempel pada otak Anda dan dengan demikian Anda akan mendapatkan pengetahuan!

> Saya juga akan menampilkan di akhir artikel ini cara menginstal skrip bootstrapping bagi mereka yang menginginkan lingkungan grafis *siap pakai* setelah instalasi Linux minimal / basis.

![Teks Alt](https://res.cloudinary.com/practicaldev/image/fetch/s--mMnMUgXe--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6tjhaau67o7bxof2rttl.png)

## Dan perjalanan dimulai...

Jadi, hal pertama yang harus dilakukan adalah pergi ke halaman Download Artix Linux dan memilih instalasi dasar .iso gambar. (karena kita ingin membangunnya dari awal). ~ > [link](https://artixlinux.org/download.php)

Anda juga bisa memilih gambar dengan lingkungan desktop yang sudah diinstal, tapi kami tidak akan melakukannya di sini.

Ada 3 gambar dasar untuk diunduh:

1. openrc
2. runit
3. s6

Dan pada dasarnya itu adalah 3 sistem init yang berbeda dari distribusi Artix. (Anda dapat menemukan info lebih lanjut di wiki Artix)

Setelah kami mengunduh gambar, kami kemudian ingin memasukkannya ke drive usb dan membuatnya dapat di-boot.
Jika kita membuka tty (terminal) dan berjalan di:

```bash
$ lsblk
```



Kita harus melihat hard drive yang sudah kita miliki dalam sistem kita. Setelah kita dapat memasukkan ke komputer kita usb stick dan menjalankan lagi perintah yang sama untuk mengetahui bagaimana sistem kita melabeli usb stick. Biasanya itu seperti diikuti dengan huruf lain. Jadi misalnya, hard drive utama kami akan memiliki label dan ketika kami memasukkan ke dalam USB kami maka itu mungkin diberi nama. Jadi lokasi file kemudian harus: . Untuk memastikan kita juga dapat memeriksa kapasitas setiap drive. `sd``sda``sdb``/dev/sdb`

Sekarang, setelah kami memastikan bahwa kami telah mengenali mana drive usb kami, maka kami ingin membuatnya dapat di-boot dengan gambar .iso kami.
Untuk melakukan itu, pertama-tama kita membutuhkan hak istimewa sudo dan kemudian kita dapat menjalankan perintah berikut:

```bash
$ dd if=our_iso_image_here.iso of=output_file_to_write_the_image status='progress' #if we want to see a progress bar

# so an example of the above explanation: 

$ dd if=arix-base-runnit-20200214-x86_64.iso of=/dev/sdb status='progress'
```



Dan sekarang kami memiliki usb stick bootable dengan gambar runnit Artix dan kami dapat boot dari komputer kami dan memulai instalasi.

Pertama, kita harus login sebagai root dan kredensial untuk itu adalah

```bash
Username: root
Password: artix
```



Atau kita bisa login sebagai pengguna artix dan kemudian melakukan: `sudo su`

```bash
Username: artix
Password: artix
```



Jadi begitu kita melakukan itu, pertama-tama kita harus memastikan apakah komputer kita berjalan atau tidak.
Sebagian besar mesin baru akan memiliki uefi tetapi untuk membuat 100% yakin kita harus menjalankan perintah berikut:`UEFI``Legacy Boot`

```bash
$ ls /sys/firmware/efi/efivars
```



**Jika Anda MELIHAT hal-hal muncul maka komputer menggunakan UEFI**

**Jika Anda TIDAK melihat hal-hal muncul maka komputer menggunakan Legacy Boot**

Jadi jika Anda mendapatkan sesuatu seperti: ls: tidak dapat mengakses: Tidak ada file atau direktori tersebut, maka **ANDA TIDAK** menggunakan UEFI. `/sys/firmware/efi/efivars`

Pada titik ini kita perlu memastikan bahwa kita terhubung ke internet! Sangat disarankan untuk dihubungkan melalui kabel ethernet, tetapi jika Anda tidak memilikinya, Anda dapat menggunakan perintah: untuk terhubung ke jaringan wifi dan itu harus sudah diinstal sebelumnya pada gambar iso. `iwd`

Untuk memeriksa apakah Anda memiliki koneksi internet, Anda dapat melakukan ping situs web seperti:

```bash
$ ping artixlinux.org
```



dan itu harus mengembalikan tanggapan dan dengan demikian itu berarti anda terhubung ke internet.

Sekarang dengan menjalankan kita harus menemukan hard drive dari komputer yang kita ingin menginstal Artix Linux pada. Sekali lagi kita bisa mengenalinya dengan ukuran kapasitasnya. `lsblk`

Setelah kita menemukannya kita harus menjalankan perintah berikut untuk memulai partisi disk.

```bash
$ fdisk /dev/sda

# /dev/sda is the (example) disk that we want to install Artix on
```



Dalam panduan contoh kami di sini, kami akan menghapus SEMUANYA dari hard drive dan partisi semuanya dari awal, tetapi Anda bisa jika Anda ingin menyimpan partisi rumah Anda (jika Anda belum mendukungnya) dan hanya membuat di langkah selanjutnya root dan partisi boot.

Sekarang, setelah mengeksekusi perintah, prompt akan datang bertanya kepada kita partisi mana yang ingin kita hapus.
Jika kita hanya mengetik: , itu akan menghapus partisi default yang disebutkan dalam kurung dan kemudian kita harus mengetik 2 kali lagi untuk menghapus partisi yang tersisa juga. `fdisk``d``d`

Jika kita mengetik: pada waktu tertentu itu harus menampilkan partisi kita. Tentu saja jika kita menghapus semuanya, kita tidak akan memilikinya. `p`

Sekarang kita akan membuat partisi baru kita.

Ketik pertama: untuk mulai membuat partisi baru. `n`

Partisi pertama yang selalu ingin kita buat adalah partisi **boot.**
Pertama meminta nomor partisi ~ > **`hanya tekan enter tanpa mengetik apa-apa`**

Kemudian meminta sektor pertama ~ > **`lagi hanya menekan enter tanpa mengetik apa pun`**

Dan sekarang meminta sektor Terakhir dan seberapa besar Anda menginginkannya, biasanya di sini orang memberikan 512M tapi kita akan memberikan 1G, jadi kita hanya perlu mengetik: .`+1G`

Kemudian ia akan bertanya kepada kita apakah kita ingin menghapus tanda tangan. Jika disk yang Anda instal kosong dari awal hanya tekan tidak, tetapi jika berisi sesuatu sebelumnya dan Anda sedang mempartisi ulang, Anda harus mengetik: `Y`

Sekarang, jika kita menekan kita dapat melihat partisi yang baru saja kita buat. `p`

Selanjutnya, kita akan membuat 2 partisi lagi.

Yang berikutnya adalah partisi **root.**

Jadi, pertama-tama kita ketik untuk membuat partisi baru, kemudian pada nomor partisi dan sektor pertama kita cukup tekan enter tanpa mengetik apa pun dan pada sektor terakhir yang menanyakan ukuran partisi root, kita akan memberikan ~ > **`+40G.`**`n`

Sekarang, mungkin atau mungkin tidak meminta lagi untuk menghapus tanda tangan dan hal yang sama seperti yang disebutkan di atas berlaku.

Sekarang, kita akan membuat partisi ke-3 dan terakhir kita yang merupakan partisi rumah kita.

Jadi, sekali lagi ketik dan tekan 3 kali dan kemudian secara otomatis akan mengisi sisa ruang untuk partisi rumah dan pada titik ini jika kita menekan kita dapat melihat 3 partisi yang kita buat. `n``enter``p`

Dan sekarang kita dapat mengetik: **`w`** untuk menulis partisi yang baru dibuat dan sekarang kita memiliki hard drive kosong dengan 3 partisi yang kita buat dan kita harus kembali ke shell login sebagai root.

Sekarang, kita dapat mengetik dan melihat hard drive kita dan partisi yang kita format dengan ukuran masing-masing. `lsblk`

Hal berikutnya yang ingin kita lakukan adalah mulai menempatkan sistem file pada partisi ini sehingga kita dapat menempatkan file pada mereka. (Perhatikan bahwa semua yang ada di linux bekerja dengan file)

So now we will start by making our home partition and that should be: to be in ext4 file system format.
To do that, type in:`/dev/sda3`

```bash
$ mkfs.ext4 /dev/sda3
```



**Important note**: we're going to format everything in this particular guide in an ext4 file system format, BUT if you're using an UEFI system (you can find that out by the command we run above) then you want to format the BOOT partition in file system format and then the home, root partitions in ext4.
But in our case we're going to follow the Legacy boot system and we're going to format all the 3 partitions in ext4 file system format. `fat`

Alright, and now it will take a while and once finished then we can make the root partition to be in ext4 file system format by running:

```bash
$ mkfs.ext4 /dev/sda2
```



And once that is finished as well we're going to do the same for our boot partition by running:

```bash
$ mkfs.ext4 /dev/sda1
```



**!!** If you're using UEFI then to format your boot partition in fat file system format you can use:

```bash
$ mkfs.fat -F32 /dev/sda1
```



And now we're done creating our file systems on our partitions and we're ready to start adding files on them!

And so now basically we're going to mount our partitions the way we want them to be mounted and then install our operating system which is basically one command and after that we're going to make a couple of changes and we're done!

Now, we first want to take the partition and mount it to
To do that we run:`root``/mnt`

```bash
$ mount /dev/sda2 /mnt
```



And now we're going to make 2 directories inside /mnt, one for the home and on for the boot partitions.

```bash
$ mkdir /mnt/home
$ mkdir /mnt/boot
```



And now we can mount our other 2 partitions.

```bash
$ mount /dev/sda1 /mnt/boot
$ mount /dev/sda3 /mnt/home
```



And now we can run and we'll see our partitions mounted to where we mounted them. (basically where it's supposed to be mounted)`lsblk`

And now basically we're ready to install our operating system, and we will do that with the following command in which basically we're going to tell it where exactly to install the operating system and then we're going to tell it what exactly we want to install. (remember that you should be connected to the internet)
Note that the below command is for the runit init system of the Artix Linux. You will need to install different things for s6 or openrc. (Head to the installation guide on artix linux wiki to find out what should be done)

```bash
$ basestrap /mnt base base-devel runit elogind-runit linux linux-firmware vim curl gcc git # and basically whatever other program you want here to be installed.
```



And now once the above command is done, we basically have an operating system installed on our hard drive, but we can't boot to it because we haven't set yet a bootloader and a couple of other things, so we're going to first set a bootloader.

So basically when we reboot our computer it we need to tell it in what ourder our moun points should be. i.e. in simple manners the boot partition to the boot mounting point, the home partition to the home mounting point etc...

So, if we run:

```bash
$ fstabgen /mnt
```



We will see where everything should be mounted.
Now we want to give a couple of options to this command:

```bash
$ fstabgen -U /mnt >> /mnt/etc/fstab
```



What tells it it's that it should read the partitions based on their UUID and not on the sda,sdb,sdc letters because those might be different on different computers but their UUID's are unique and so we definetely want it to be like that, and then we append that to the fstab file in the /etc so each time we reboot the computer knows where everything is mounted when it boots again. `-U`

And now we need to run the following command, and basically we then should be inside the actual installed operating system and not on the bootable usb drive.

```bash
$ artix-chroot /mnt
```



Probably we'll get prompted to the default shell which is sh but if we run: we should get to the bash shell with all it's features etc...`bash`

Now, what we want to do is edit the mirrorlist file and basically what we want to do in that file is move on top of the file the mirrors which are closer to the country we live in. (simply for better pings and ms and so on...)
To do that:

```bash
$ vim /etc/pacman.d/mirrorlist
```



Sekarang kita mungkin ingin menetapkan zona waktu lokal kita.
Untuk melakukan itu, kami akan membuat simlink ke /etc/localtime dan perintah untuk itu adalah:

```bash
$ ln -sf /usr/share/zoneinfo/your_time_zone_here /etc/localtime
```



Dan sekarang jika kita berlari:

```bash
$ ls -l /etc/localtime
```



Ini akan menampilkan waktu lokal kita, sebenarnya di mana kita mengatur sistem kita untuk berada ...

Dan kita mungkin juga ingin memperbarui jam perangkat keras kita agar sinkron dengan apa yang kita tetapkan di atas.

```bash
$ hwclock --systohc
```



Dan sekarang kita akan membuka file berikut:

```bash
$ vim /etc/locale.gen
```



Untuk mengatur sistem dan bahasa utama keyboard kami.
Bagaimana?
Cukup uncomment salah satu yang sesuai dengan bahasa Anda, misalnya en_US (baik UTF-8 dan ISO)

Dan kemudian Anda menyimpan file dan menjalankan:

```bash
$ locale-gen
```



Dan kemudian kita akan membuat file baru:

```bash
$ vim /etc/locale.conf
```



Dan pada dasarnya Anda ingin mengetik: dan kemudian menyimpan file.`LANG=en_US.UTF-8`

Dan sekarang kita akan menginstal beberapa paket penting.

```
$ pacman -S networkmanager networkmanager-runit 
```



Sekarang kami ingin memberitahu Artix untuk memulai manajer jaringan setiap kali kami boot up. (Ini lagi akan berbeda untuk runit, s6, openrc)

Untuk melakukan itu:

```bash
$ ln -s /etc/runit/sv/NetworkManager /etc/runit/runsvdir/default/
```



Dan pada dasarnya itulah cara Anda memberi tahu runit untuk secara otomatis memulai layanan setiap kali Anda boot.
Juga, di dalam direktori ~ > Anda dapat menemukan semua layanan yang dapat Anda beri tahu runit untuk memulai secara otomatis di boot dan di situlah NetworkManager berada. `/etc/runit/sv/`

**Catatan penting** Sebenarnya satu-satunya saat Anda menautkan layanan adalah pada waktu instalasi pertama seperti yang kami lakukan sekarang. TAPI, Anda harus dari saat sistem diinstal dan ke layanan simlink hanya ke: **`/ run / runit / layanan`**!!! `/etc/runit/runsvdir/default/`

Sekarang, kami ingin mengedit yang berikut:

```bash
$ vim /etc/hostname
```



Dan pada dasarnya kita menambahkan pada baris pertama (file harus kosong) nama komputer yang kita inginkan. bekas: `desktop`

Simpan file lalu edit:

```bash
$ vim /etc/hosts
```



Dan tambahkan di sana
baris berikut: (Anda dapat menemukan info lebih lanjut tentang detail pada panduan instalasi wiki Artix)

```bash
127.0.0.1    localhost
::1          localhost
127.0.0.1    desktop.localdomain desktop # <~ desktop is the name we gave to our computer in the hostname file.
```



Simpan file.

Dan sekarang akhirnya kita akan membuat mesin kita bootable dengan menginstal bootloader.

yaitu grub dalam panduan khusus ini tetapi anda dapat memilih bootloader apa pun yang anda sukai.

```bash
$ pacman -S grub 

# note here that if you want to sometime do a dual boot on your machine you need to install the program: os-prober as well.
# also if you run UEFI instead of Legacy Boot you need to install as well: efibootmgr
```



Sekarang kita perlu mengatur grub (perintah ini akan kembali berbeda untuk UEFI vs Legacy Boot)

Untuk Legacy Boot:

```bash
$ grub-install --target=i386-pc /dev/sda # <~ your hard drive that you're installing the system, check with: lsblk
```



Untuk UEFI:

```bash
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
```



### Boot ganda dengan windows 10 (opsional)

> pada titik ini saya ingin menambahkan beberapa langkah jika Anda ingin dual boot instalasi artix (lengkungan) linux Anda dengan windows 10.

**Ini adalah prasyarat bahwa Anda telah menginstal windows 10 dalam partisi terpisah dari partisi Linux kami yang dibuat di atas sebelum memulai instalasi Linux.**

Jadi misalnya Anda bisa memiliki partisi / dev / sda4 dengan windows 10 diinstal di dalamnya.

> Ini adalah praktik terbaik ketika Anda ingin dual boot, untuk pertama menginstal Windows 10 pada disk drive kosong Anda dan kemudian mengalokasikan dari dalam jendela beberapa ruang kosong untuk instalasi Linux Anda.

Tapi, jika Anda sudah menginstal Linux, maka masih mungkin untuk melakukan boot ganda. Pertama backup direktori / home Anda ke hard disk drive eksternal dengan memberikan perintah berikut:

```bash
$ rsync -a --delete --quiet --progress /path/to/backup /location/of/backup
```



**a,**menunjukkan bahwa file harus diarsipkan, yang berarti bahwa sebagian besar karakteristik mereka dipertahankan (tetapi tidak ACLs, hard link atau atribut diperpanjang seperti kemampuan)

**--delete,**berarti file yang dihapus pada sumber harus dihapus pada cadangan juga

> Di sini, /path/to/backup harus diubah menjadi apa yang perlu dicadangkan (misalnya /home) dan /location/of/backup adalah tempat backup harus disimpan (misalnya /media/disk).

Dan setelah melakukannya Anda kemudian harus boot dengan usb stick artix bootable Anda dan menghapus partisi / rumah dengan sehingga Anda dapat membuat beberapa ruang kosong untuk instalasi windows 10 Anda. Setelah menghapus partisi / rumah, Anda harus memiliki beberapa ruang kosong dari beberapa GB dan Anda dapat membuat 2 partisi primer baru seperti yang kami lakukan di atas, 1 untuk direktori / rumah baru untuk Linux dan 1 lainnya untuk instalasi Windows. Jadi dengan asumsi bahwa partisi ke-4 diberi nama (Anda tahu sekarang cara menemukannya), Anda harus boot dari usb stick Windows 10 yang dapat di-boot dan menginstal Windows pada partisi tertentu. Setelah melakukannya, windows akan mengambil alih Grub sehingga Anda ingin dapat melihat instalasi Linux Anda dan komputer Anda akan secara otomatis boot ke windows, sekarang adalah waktu untuk menggunakan Linux Anda bootable usb stick lagi dan mengikuti prosedur instalasi Linux artikel ini dari awal (menghapus 1,2,3 partisi dan menciptakannya kembali tanpa menyentuh sama sekali partisi 4 (yang merupakan jendela satu) dan kemudian ikuti berikut 3 perintah terakhir dan Anda akan memiliki kedua sistem operasi pada mesin Anda). Kemudian Anda dapat menggunakan cadangan / rumah Anda untuk membawa semuanya kembali pada instalasi Linux Anda.`fdisk``/dev/sda4`

Seperti disebutkan di atas, jika Anda ingin dual boot distribusi lengkungan dengan sistem operasi lain, Anda memerlukan program: **os-prober.** Anda dapat menginstalnya baik sebelumnya ketika kami menginstal program dasar kami dengan basestrap atau bahkan pada titik ini kami sekarang dengan mengetik:

```bash
$ pacman -S os-prober
```



**!!!** PERHATIKAN, ada kasus bahwa os-prober mungkin tidak mendeteksi instalasi Windows 10 Anda secara otomatis (dalam langkah selanjutnya), jadi untuk melakukannya Anda perlu menginstal juga program berikut juga:

```bash
$ pacman -S ntfs-3g
```



Sekarang, pada titik ini jika kita menjalankan perintah

```bash
$ os-prober
```



Kita harus melihat bahwa itu mendeteksi instalasi Windows 10 kami pada partisi ke-4 Anda dan kemudian setelah menghasilkan file konfigurasi grub dengan perintah di bawah ini kita harus melihat bahwa itu berisi instalasi Linux kami dan instalasi Windows kami dan kami baik untuk pergi!

Jika kita reboot sekarang, kita harus melihat grub dengan Linux kami, instalasi Windows!

```bash
$ grub-mkconfig -o /boot/grub/grub.cfg
```



Dan hal terakhir yang harus dilakukan adalah membuat kata sandi!

```bash
$ passwd 
```



Dan pada titik ini kami sudah selesai dan Anda baru saja berhasil menginstal Artix linux dari awal, selamat!

Sekarang... setelah semua pekerjaan ini wajah Anda harus
seperti ~ > 😑 Karena Anda akan mengetahui bahwa Anda boot dan Anda hanya memiliki tty gelap polos (terminal).
Tapi! Itulah keajaiban menginstal sistem operasi linux tanpa lingkungan desktop pra-instal dan memiliki semua pengaturan yang kami lakukan di atas dibuat secara otomatis oleh gambar, hanya untuk mendapatkan pemahaman yang lebih baik tentang apa yang sebenarnya terjadi di belakang dan layar dan dengan demikian memiliki "koneksi" yang lebih baik dengan mesin Anda sendiri yang Anda bangun dari awal (yah tidak 100% dari awal, karena jelas Anda tidak menulis semua kode C dari semua perintah yang kami jalankan dan tentu saja kami sudah memiliki gambar distribusi Artix Linux yang siap dan dengan demikian kernel linux, sehingga seluruh Kernel ditulis oleh orang lain, tapi ya Anda mendapatkan intinya ...)

Dan sekarang apa? Apakah kita terjebak dengan tty polos?

Nah, tidak jika kita tidak mau. Kita sekarang dapat mulai menginstal lingkungan grafis atau manajer jendela kita sendiri dan shell yang lebih baik dan manajer tampilan (layar masuk) dan pada dasarnya program apa pun yang Anda inginkan atau bahkan lingkungan desktop dengan yang telah diinstal sebelumnya hanya untuk belajar cara bermain dengan mereka dan bagaimana mereka beroperasi dan untuk dapat mengkonfigurasi semuanya sendiri dan itulah keajaiban Linux!

Atau pada titik ini Anda bahkan dapat menjalankan skrip bootstrapping yang telah ditulis orang lain dan pada dasarnya apa ini, ini adalah skrip shell yang menginstal secara otomatis semua yang disebutkan dalam baris di atas + beberapa konfigurasi tambahan dari orang yang menulis skrip + dotfiles mereka dan seterusnya ...
Pada dasarnya ini akan membuat Anda bangun dan berjalan dengan lingkungan grafis yang lengkap, tetapi tentu saja dengan konfigurasi orang itu Anda harus belajar bagaimana menggunakan atau memodifikasinya sesuai keinginan Anda.

Saya akan memberikan di sini naskah yang saya pribadi sangat suka seperti yang dijanjikan di awal artikel ini, dan itu disebut LARBS dan ditulis oleh [Luke Smith.](https://lukesmith.xyz/)
Anda dapat menemukan informasi tentang instalasi dan lebih banyak lagi ~ > [di sini.](https://larbs.xyz/)

Pada dasarnya, setelah Anda selesai dengan instalasi Artix Anda cukup menjalankan perintah di bawah ini dan mengikuti UI dan Anda akan memiliki sistem operasi yang sepenuhnya bagus dan siap untuk pergi dengan semua fungsi dan konfigurasi dan program yang dimiliki Luke dalam skrip bootstrapping-nya! Tentu saja Anda bebas untuk mengubah segalanya (disarankan) sesuai keinginan Anda atau belajar menggunakan sistemnya jika Anda menyukainya dan menyimpannya apa adanya.

```bash
# should be run as root

$ curl -LO larbs.xyz/larbs.sh
$ bash larbs.sh
```



atau:

```bash
$ git clone https://github.com/LukeSmithxyz/LARBS.git
$ cd LARBS/ 
$ ./larbs.sh
```