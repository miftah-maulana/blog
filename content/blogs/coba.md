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

![tmux command only part 2](https://miftah-maulana.my.id/assets/images/TMUX/tmux_command_only_part_2.png)

![tmux command only](https://miftah-maulana.my.id/assets/images/TMUX/tmux_command_only.png)

Kedua gambar diatas merupakan output apabila memulai sesi TMUX dengan command `tmux` saja. Bisa dilihat pada gambar nama default ketika saya menjalankan command `tmux` nama sesi nya "0".

![tmux new -s](https://miftah-maulana.my.id/assets/images/TMUX/tmux_new_-s.png)

![tmux new -s part 2](https://miftah-maulana.my.id/assets/images/TMUX/tmux_new_-s_part_2.png)

Kedua gambar diatas merupakan output apabila memulai sesi TMUX dengan command `tmux new -s <nama-sesi>` . Bisa dilihat pada gambar diatas saya membuat sesi TMUX dengan nama "miftah". Lalu bagaimana caranya untuk keluar dari sesi? Untuk keluar dari sesi TMUX bisa menggunakan shortcut dengan menekan kombinasi pada keyboard `Ctrl+b` kemudian `d`. Maka output nya anda akan keluar dari sesi TMUX (bisa dilihat pada gambar dibawah)

![ctrl+b+d](https://miftah-maulana.my.id/assets/images/TMUX/ctrl+b+d.png)

Kemudian apabila ingin masuk kembali ke sesi sebelumnya sudah keluar, bisa menggunakan command `tmux a -t <nama-sesi>`. Apabila lupa dengan nama sesi yang baru saja atau sudah sebelumnya dibuat, untuk melihat sesi apa TMUX siapa saja yang berjalan bisa pada komputer/server kita bisa menggunakan command `tmux ls` (bisa dilihat pada gambar dibawah).

![tmux ls](https://miftah-maulana.my.id/assets/images/TMUX/tmux_ls.png)

Sebenarnya bisa saja kita keluar dengan menggunakan kombinasi `Ctrl+d`, namun apabila kita menjalankan kombinasi keyboard tersebut maka otomatis sesi tmux yang sudah kita buat akan langsung hilang. Ini sebenarnya saya tidak rekomendasikan karna takutnya ketika saya sedang menjalankan command line yang prosesnya panjang dan niatnya saya tinggal untuk mengerjakan pekerjaan lain, malah terhenti karena sesi tmux nya hilang :)