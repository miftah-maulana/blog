---
author: "Miftah Maulana Wahab"
title: "Trik cepat rename file menggunakan Brace Expansion"
description : "Penerapan Brace Expansion dalam rename file"
date: 2025-08-14T20:37:05+07:00
tags: ["Linux","Bash","Tutorial"]
showToc: true
---

Seseorang yang bekerja dengan memegang server yang menggunakan sistem operasi Linux, biasanya dalam sehari-hari menjadi daily activity dalam management file seperti membuat, mengedit, ataupun menghapus file. File apasih yang dimaksud disini? yap, maksud saya disini file apapun. Bisa jadi file biasa yang berisikan data, file log-log, file script, atau bisa juga file konfigurasi. Dari membuat, mengedit, ataupun menghapus file saya akan fokus dalam hal mengedit. Tapi tidak terlalu dalam, yang di edit ialah nama file nya saja. Dalam case saya, biasanya pengeditan nama file dilakukan pada file konfigurasi. Contoh case nya, saya ingin melakukan editing pada file konfigurasi `konfigurasi.conf`, saya harus membuat backup file nya terlebih dahulu. Dalam case ini biasanya saya melakukan copy file yang ingin saya edit sebelum melakukan editing agar file lama/asli tetap masih bisa digunakan menjadi backup apabila editing yang saya lakukan keliru. Basic command yang biasanya dilakukan yaitu :

```bash
cp konfigurasi.conf konfigurasi.conf.backup-14-08-2025

#output saat di ls 
-----------------
konfigurasi.conf konfigurasi.conf.backup-14-08-2025
```

Dengan demikian saya bisa melakukan editing di file   `konfigurasi.conf` dengan leluasa karena file asli/lama nya sudah saya backup dengan nama `konfigurasi.conf.backup-14-08-2025`. Menurut saya, ada sedikit ke tidak praktisan saat dimana ingin melakukan backup namun kita menggunakan absolute ataupun relative path. saya coba jabarkan contoh dibawah dengan absolute path:

```bash
cp /home/miftah/konfigurasi.conf /home/miftah/konfigurasi.conf.backup-14-08-2025
```

Contoh seperti diatas yang menurut saya tidak efisien. Saya biasanya menggunakan Brace Expansion untuk mempersingkat command, sehingga command yang saya jalankan hanya begini :

```bash
cp /home/miftah/konfigurasi.conf{,.backup-14-08-2025}

# dimana outputnya saat di ls 
---------------------
konfigurasi.conf konfigurasi.conf.backup-14-08-2025
```

atau untuk lebih jelas bisa dilihat pada gambar dibawah :

![contoh brace](https://miftah-maulana.my.id/assets/images/brace-expansion/contoh-brace.png)


Refrensi :

https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html