---
author: "Miftah Maulana Wahab"
title: "Terminal Multiplexer(TMUX)"
description : "Pengenalan dan pengoperasian singkat Terminal Multiplexer (TMUX)"
date: 2024-02-01T00:49:52+07:00
tags: ["Linux","Tools","Server"]
showToc: true
---

Terminal Multiplexer atau yang sejauh ini dikenal sebagai TMUX, berdasarkan pengalaman saya selama bekerja menggunakannya merupakan salah satu tools dalam Linux yang menurut saya sangat membantu 
bagi yang biasa bekerja menggunakan terminal/ssh ke dalam server yang menggunakan sistem operasi Linux. Salah satu kegunaan TMUX yang paling membantu saya dalam pekerjaan adalah ketika saya diharuskan menjalankan
sebuah command line dalam Linux misalnya menjalankan instalasi dan update package, atau Scripting yang dimana dalam proses jalannya command line tersebut membutuhkan waktu yang lama atau tidak sebentar saya tidak perlu khawatir proses yang berjalan itu akan terhenti di tengah jalan atau menuju akhir karena koneksi atau session saya yang terputus dari server. Karena TMUX ini akan berjalan membuat sesi dan sesi tersbut tidak akan hilang selama server tempat kita menjalankan TMUX itu tidak mati atau sesi kita di hentikan. Pada konten ini saya akan menjelaskan dengan singkat cara menggunakan TMUX dan beberapa shortcut dalam TMUX yang biasa saya gunakan untuk membantu dalam pekerjaan saya.

Sebelumnya apabila TMUX belum di install pada server anda, bisa menggunakan cara berikut :

| Distro | Command Instalasi |
|------|------|
| Arch Linux | pacman -S tmux |
| Debian/Ubuntu | apt install tmux |
| Fedora | dnf install tmux |
| RHEL/CentOS | yum install tmux |
| macOS | brew install tmux |
| openSUSE | zypper install tmux |

Setelah proses instalasi selesai, jalankan TMUX menggunakan command `tmux` atau `tmux new -s <nama-sesi>` untuk memulai sesi. Bedanya kedua command tesebut adalah apabila menjalankan command `tmux` saja ia akan membuat sesi dengan nama default dari tmux, sedangkan apabila `tmux new -s` itu akan membuat sesi dengan nama sesi sesuai dengan nama sesi yang kita inginkan. 

![tmux command only](https://miftah-maulana.my.id/assets/images/TMUX/tmux_command_only.png)

![tmux command only part 2](https://miftah-maulana.my.id/assets/images/TMUX/tmux_command_only_part_2.png)


Kedua gambar diatas merupakan output apabila memulai sesi TMUX dengan command `tmux` saja. Bisa dilihat pada gambar nama default ketika saya menjalankan command `tmux` nama sesi nya "0".