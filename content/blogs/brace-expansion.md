---
author: "Miftah Maulana Wahab"
title: "Trik cepat rename file menggunakan Brace Expansion"
description : "Penerapan Brace Expansion dalam rename file"
date: 2025-08-14T20:37:05+07:00
tags: ["Linux","Bash","Tutorial"]
showToc: true
---

Pada pekerjaan saya yang sudah pasti berhubungan dengan sistem operasi Linux, dalam sehari-hari sudah menjadi _daily activity_ dalam hal _management_ file seperti membuat, mengedit, ataupun menghapus file. File apasih yang dimaksud disini? yap, yang dimaksud disini file apapun yang ada dalam server tersebut. Bisa jadi file biasa yang berisikan data seperti log-log server, file script, atau bisa juga file konfigurasi. Dari membuat, mengedit, ataupun menghapus file, kali ini saya akan fokus dalam hal mengedit. Tapi tidak terlalu dalam, yang diedit ialah nama file-nya saja. Saya ambil dari _real case_ nya, disini saya ingin melakukan _editing_ pada file konfigurasi `konfigurasi.conf`. Sesuai _Standard Of Procedure_(SOP), sebelum melakukan _editing_ saya harus membuat backup file-nya terlebih dahulu. Kenapa? agar apabila saat proses editing terdapat kekeliruan ataupun kesalahan saya dapat melakukan _rollback_ dengan cepat. Saya biasa menggunakan metode _copy_ file dalam proses backup yang dimana _basic command_-nya biasanya :

```bash
cp konfigurasi.conf konfigurasi.conf.backup-14-08-2025

#output saat di ls 
-----------------
konfigurasi.conf konfigurasi.conf.backup-14-08-2025
```

Dengan demikian saya bisa leluasa melakukan editing pada file `konfigurasi.conf` karena file asli/lama nya sudah saya _backup_ dengan nama `konfigurasi.conf.backup-14-08-2025`. Namun menurut saya, ada sedikit kurang praktis/efisien saat dimana ingin melakukan _backup_ namun kita menggunakan _absolute_ ataupun _relative path_. saya coba jabarkan contoh dibawah dengan _absolute path_:

```bash
cp /home/miftah/konfigurasi.conf /home/miftah/konfigurasi.conf.backup-14-08-2025
```

Contoh seperti diatas yang menurut saya tidak efisien. Saya biasanya menerapkan _Brace Expansion_ untuk mempersingkat _command_, sehingga _command_ yang saya jalankan hanya begini :

```bash
cp /home/miftah/konfigurasi.conf{,.backup-14-08-2025}

# dimana outputnya saat di ls 
---------------------
konfigurasi.conf konfigurasi.conf.backup-14-08-2025
```

atau untuk lebih jelas hasilnya bisa dilihat pada gambar dibawah ini:

![contoh brace](https://miftah-maulana.my.id/assets/images/brace-expansion/contoh-brace.png)

Namun apasih _Brace Expansion_ itu? Nah biar mempersingkat mungkin bisa dibaca terlebih dahulu pada link refrensi berikut : https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html .Tentunya _Brace Expansion_ ini tidak hanya dapat digunakan pada _command_ `cp` saja. Ekspansi ini bisa juga digunakan dengan _command-command_ lain kok. Salah satu yang berdekatan dengan `cp` atau _copy_  biasanya adalah _command_ _move_ atau yang sering dikenal dengan `mv`. Selain untuk memindahkan file, `mv` juga bisa digunakan untuk _rename_ file(mungkin pembaca sudah lebih tahu ya disini). Nah biasanya kita menjalankan perintah `mv` itu dengan cara `mv` <file-yang-ingin-di-rename> <nama-file-yang-baru> atau mungkin lebih jelas bila dengan gambar di bawah ini yang saya praktikan. 

![mv brace](https://miftah-maulana.my.id/assets/images/brace-expansion/mv-brace.png)

nah _Brace Expansion_ juga bisa saya terapkan dalam aktivitas _rename_ file. Contoh _real case_ nyata-nya lagi adalah kembali nih saya mempunyai file `konfigurasi.conf` lama yang saya ingin ganti dengan `konfigurasi.conf` yang terbaru. Sesuai SOP, `konfigurasi.conf` yang lama harus saya backup terlebih dahulu sebelum menerapkan file `konfigurasi.conf` yang baru. Jelasnya mungkin bisa lihat yang saya praktikan pada gambar di bawah ini.

![praktik](https://miftah-maulana.my.id/assets/images/brace-expansion/praktek.png)

Singkatnya, pada gambar diatas file dengan nama `konfigurasi.conf` adalah file konfigurasi _existing_ yang akan saya _update_ isinya. Sedangkan file dengan nama `konfigurasi-terbaru.conf` adalah file konfigurasi yang isinya sama, namun sudah saya lakukan _update_ dari file `konfigurasi.conf`/_existing_. Nah saya meng-implementasikan _Brace Expansion_ dalam _case_ ini guna mempersingkat dan menghindari kesalahan apabila saya masih menggunakan _basic command_. Saya sedikit jelaskan secara singkat _command_ yang saya praktikan dibawah ini.

```bash
$ mv brace/konfigurasi.conf{,.bak} #bash akan mengekspansi 2 string sama dengan artinya menjalankan command mv brace/konfigurasi.conf brace/konfigurasi.conf.bak 

$ mv brace/konfigurasi{-terbaru.conf,.conf} #mengekspansi command sama dengan artinya dengan menjalankan command mv brace/konfigurasi-terbaru.conf brace/konfigurasi.conf
```

Tentunya menurut saya, dengan menggunakan mekanisme _Brace Expansion_ ini membuat lebih singkat dan mungkin bisa meminimalisir _typo_ saat menuliskan _command_ dengan _absolute_ atau _relative_ path.


