---
author: "Miftah Maulana Wahab"
title: "Terminal Multiplexer(TMUX)"
description : "Pengenalan dan pengoperasian singkat Terminal Multiplexer (TMUX)"
date: 2024-02-01T00:49:52+07:00
tags: ["Linux","Tools","Server"]
showToc: true
---

![tmux logo](https://miftah-maulana.my.id/assets/images/TMUX/tmux-logo.png)

_Terminal Multiplexer_ atau yang sejauh ini dikenal sebagai TMUX, 
berdasarkan pengalaman saya selama menggunakannya, merupakan salah satu tools open source yang menurut saya sangat membantu bagi yang biasa bekerja menggunakan terminal/_ssh_ ke dalam server yang menggunakan sistem operasi Linux. 
Salah satu kegunaan TMUX yang paling membantu saya dalam pekerjaan adalah ketika saya diharuskan menjalankan sebuah _command line_ dalam Linux misalnya menjalankan instalasi dan _update package_, 
atau menjalankan _script_ yang dimana dalam proses jalannya _command line_ tersebut membutuhkan waktu yang lama atau tidak sebentar, saya tidak perlu khawatir proses yang berjalan itu akan terhenti di tengah jalan atau menuju akhir karena koneksi 
atau _session_ saya yang terputus dari server. Karena TMUX ini akan berjalan membuat sesi dan sesi tersbut tidak akan hilang selama server tempat kita menjalankan TMUX itu tidak mati atau sesi kita di hentikan. 
Pada tulisan ini saya akan menjelaskan dengan singkat cara menggunakan TMUX dan beberapa _shortcut_ dalam TMUX yang biasa saya gunakan untuk membantu dalam pekerjaan saya.


Sebelumnya apabila TMUX belum di install pada server anda, bisa menggunakan cara berikut :

| Distro | Command Instalasi |
| ------ | ------ |
| Arch Linux | pacman -S tmux |
| Debian/Ubuntu | apt install tmux |
| Fedora | dnf install tmux |
| RHEL/CentOS | yum install tmux |
| MacOS | brew install tmux |
| OpenSUSE | zypper install tmux |

Setelah proses instalasi selesai, jalankan TMUX menggunakan _command_ `tmux` atau `tmux new -s <nama-sesi>` untuk memulai sesi. Bedanya kedua _command_ tersebut adalah apabila menjalankan _command_ `tmux` saja ia akan membuat sesi dengan nama _default_ dari tmux, sedangkan apabila `tmux new -s` itu akan membuat sesi dengan nama sesi sesuai dengan nama sesi yang kita inginkan. 

![tmux command only part 2](https://miftah-maulana.my.id/assets/images/TMUX/tmux_command_only_part_2.png)

![tmux command only](https://miftah-maulana.my.id/assets/images/TMUX/tmux_command_only.png)

Kedua gambar diatas merupakan _output_ apabila memulai sesi TMUX dengan _command_ `tmux` saja. Bisa dilihat pada gambar nama _default_ ketika saya menjalankan _command_ `tmux` nama sesi nya "0".

![tmux new -s](https://miftah-maulana.my.id/assets/images/TMUX/tmux_new_-s.png)

![tmux new -s part 2](https://miftah-maulana.my.id/assets/images/TMUX/tmux_new_-s_part_2.png)

Kedua gambar diatas merupakan _output_ apabila memulai sesi TMUX dengan _command_ `tmux new -s <nama-sesi>` . Bisa dilihat pada gambar diatas saya membuat sesi TMUX dengan nama "miftah". Lalu bagaimana caranya untuk keluar dari sesi? Untuk keluar dari sesi TMUX bisa menggunakan _shortcut_ dengan menekan kombinasi pada keyboard `Ctrl+b` kemudian `d`. Maka _output_ nya anda akan keluar dari sesi TMUX (bisa dilihat pada gambar dibawah)

![ctrl+b+d](https://miftah-maulana.my.id/assets/images/TMUX/ctrl+b+d.png)

Kemudian apabila ingin masuk kembali ke sesi sebelumnya, bisa menggunakan _command_ `tmux a -t <nama-sesi>`. Apabila lupa dengan nama sesi yang baru saja atau sudah sebelumnya dibuat, untuk melihat sesi apa TMUX siapa saja yang berjalan bisa pada komputer/server kita bisa menggunakan _command_ `tmux ls` (bisa dilihat pada gambar dibawah).

![tmux ls](https://miftah-maulana.my.id/assets/images/TMUX/tmux_ls.png)

Sebenarnya bisa saja kita keluar dengan menggunakan kombinasi `Ctrl+d`, namun apabila kita menjalankan kombinasi tersebut maka otomatis sesi tmux yang sudah kita buat akan hilang. Ini sebenarnya saya tidak rekomendasikan karna takutnya ketika saya/kita sedang menjalankan _command line_ yang prosesnya panjang dan dapat saya tinggal untuk mengerjakan pekerjaan lain, malah terhenti karena sesi tmux nya hilang :)

1. Membuat beberapa panel.

![panel atas bawah](https://miftah-maulana.my.id/assets/images/TMUX/window_atas_bawah.png)
![panel kesamping](https://miftah-maulana.my.id/assets/images/TMUX/window_kesamping.png)

_Shortcut_ untuk membuat beberapa panel ini terbagi 2 yaitu untuk membuat _split_ panel baru kesamping dan kebawah. Untuk membuat panel baru kesamping menggunakan kombinasi `Ctrl+b` kemudian `%`, sedangkan untuk membuat panel baru kebawah menggunakan kombinasi `Ctrl+b` kemudian `"`. _Shortcut_ ini biasanya saya gunakan untuk membandingkan isi dari kedua file yang berbeda. Seperti di gambar saya membandingkan isi file `log1` dan `log2`. Kemudian _shortcut_ ini juga bisa digunakan untuk membandingkan file konfigurasi antar server. Misalnya saya ingin membandingkan isi konfig pada `server a` dan `server b`, dengan _shortcut_ ini saya bisa membandingkan kedua isi konfig `server a` dan `server b` hanya dengan membuat panel baru kemudian _ssh_ ke `server a` atau `b`. Hanya saja ada kententuannya yaitu tempat saya menjalankan tmux ini adalah server _jumphost_ atau server yang harus bisa mengakses `server a` dan `server b`.

2. Berpindah panel.

![pindah panel](https://miftah-maulana.my.id/assets/images/TMUX/pindah_window.png)

_Shortcut_ ini ada hubungannya dengan _shortcut_ yang pertama. Untuk berpindah panel dari panel lama ke panel yang baru kita buat dapat menggunakan kombinasi `Ctrl+b` kemudian `🡠🡩🡢🡣`tergantung keinginan kita ingin berpindah ke panel mana. _Shortcut_ ini memungkinkan kita untuk membuat beberapa _split_ panel dengan cara _shortcut_ yang pertama(bisa lihat hasilnya gambar dibawah).

![beberapa split panel](https://miftah-maulana.my.id/assets/images/TMUX/beberapa_split_screen.png)

3. Mengubah posisi panel.

Kadang kala ketika saya membuat banyak panel dalam _session_ ini akan terjadi dimana panel berantakan, ada yang lebar ada yang sempit yang mengakibatkan ketika saya sedang menjalankan _command line_ atau membaca informasi dari server menjadi tidak nyaman. _Shortcut_ untuk mengubah posisi panel ini menurut saya berguna untuk merapihkan posisi panel menjadi lebih tertata rapih. Untuk _shortcut_ nya sendiri dapat menggunakan kombinasi `Ctrl+b` kemudian `spasi`. Mungkin untuk lebih jelas nya dapat dilihat pada gambar dibawah ini. 

![posisi panel before](https://miftah-maulana.my.id/assets/images/TMUX/posisi_screen_before.png)

![posisi panel after](https://miftah-maulana.my.id/assets/images/TMUX/posisi_screen_after.png)

Oiya untuk _shortcut_ ini komposisi panelnya dapat berubah-ubah dengan terus menekan kombinasi `Ctrl+b` kemudian `spasi` sampai anda menemukan komposisi panel yang dirasa anda inginkan.

4. Zoom in dan zoom out pada panel.

_Shortcut_ ini menggunakan kombinasi `Ctrl+b` kemudian `z` untuk _zoom in_ kedalam panel, dan kombinasi `Ctrl+b` kemudian `z` lagi untuk _zoom out_ nya. Untuk lebih jelasnya dapat dilihat pada 2 gambar dibawah.

![zoom before](https://miftah-maulana.my.id/assets/images/TMUX/zoom_in_dan_zoom_out_before.png)
![zoom after](https://miftah-maulana.my.id/assets/images/TMUX/zoom_in_dan_zoom_out_after.png)

Apabila dirasa _shortcut_ ke 3 masih dirasa kurang untuk membuat saya nyaman untuk menjalankan _command line_ atau membaca informasi dari server, maka saya gunakan _shortcut_ ini untuk membuat saya lebih nyaman dalam menjalankan _command line_ atau membaca informasi dari server.

5. Menghapus/_kill_ panel.

Apabila panel yang dibuat sudah terlalu banyak dan dirasa sudah tidak dibutuhkan, maka _shortcut_ ini dapat membantu untuk menghapus/_kill_ panel yang sudah tidak digunakan. _Shortcut_ ini menggunakan kombinasi `Ctrl+b` kemudian `x` kemudian akan muncul dialog `yes/no` bisa ketik `y` kemudian tekan `enter`. Untuk contohnya dapat dilihat pada 2 gambar dibawah.

![hapus panel before](https://miftah-maulana.my.id/assets/images/TMUX/hapus_screen_before.png)
![hapus panel after](https://miftah-maulana.my.id/assets/images/TMUX/hapus_screen_after.png)

6. Membuat kolom panel terbaru.

Mungkin membingungkan dimana poin 6 ini sebenarnya mirip pada poin 1. Secara fungsional memang sama namun _shortcut_ ini berbeda dimana pada _shortcut_ ini adalah membuat kolom panel terbaru jika panel yang kita gunakan di kolom pertama kali membuat sesi tmux ini sudah tidak cukup lagi. Mungkin lebih jelas saya jabarkan pada gambar dibawah ini.

![ctrl+b+c before](https://miftah-maulana.my.id/assets/images/TMUX/ctrl+b+c_before.png)
![ctrl+b+c after](https://miftah-maulana.my.id/assets/images/TMUX/ctrl+b+c_after.png)

Nah dari gambar diatas terlihat saya membuat kolom baru karena kolom pertama saat saya membuat sesi tmux ini sudah tidak cukup. Untuk _shortcut_ nya sendiri dapat menggunakan kombinasi `ctrl+b` kemudian `c`. Untuk menghapus kolom terbaru yang sudah dibuat dapat langsung saja menggunakan kombinasi `Ctrl+d`. Pertanyaannya adalah bagaimana jika kita ingin kembali ke kolom sebelumnya apabila sudah membuat kolom panel terbaru? Untuk kembali atau berpindah dari kolom 1 ke kolom 2 begitupun sebaliknya dapat menggunakan kombinasi `Ctrl+b` kemudian `p`, p disini saya artikan sebagai _previous_ atau kombinasi `Ctrl+b` kemudian `n` yang dimana `n` disini saya artikan sebagai _next_.

7. _Scrolling up and down_.

_Shortcut_ untuk _scrolling_ ke atas dan bawah dalam tmux bisa menggunakan kombinasi `Ctrl+b` kemudian `PageUp`. Nah untuk _scrolling_ ke atas bisa tekan terus `PageUp` nya, lalu untuk _scroll_ kebawah dengan `PageDown`. Untuk keluar nya bisa menekan key `q` atau saya sebut `quit`.

8. Fitur _Synchronize Panes_.

Nah ini merupakan fitur yang jitu dari TMUX menurut saya. Fitur _synchronize panes_ ini adalah fitur yang membuat antara panel 1 dan panel 2 ini dapat mengetik secara bersamaan. Lebih detailnya adalah contoh saya diharuskan menjalankan _command line_ `apt-update` pada `server a` sampai `i`, tentunya akan merepotkan jika saya sudah membuat _split_ panel kemudian _ssh_ dari `server a` sampai server `i` lalu berpindah panel dari `a` sampai `i` untuk menjalankan _command line_ `apt-update` secara satu persatu. Nah dengan _synchronize panes_ semua dapat dilakukan secara berbarengan. _Shortcut_ untuk mengaktifkan fitur _synchronize panes_ yakni dengan kombinasi `Ctrl+b` kemudian `:` lalu ketikan `set synchronize-panes` dan tekan `enter`. Maka dengan otomatis fitur ini akan aktif. Untuk menonaktifkan fitur ini dapat menggunakan cara yang sama seperti saat anda mengaktifkan fitur _synchronize panes_ ini. Berikut saya berikan contoh gambar setelah diaktifkan fitur _synchronize panes_ ini.

![synchronize panes](https://miftah-maulana.my.id/assets/images/TMUX/synchronize-panes.png)




9. Fitur Mouse.

Tidak kalah jitu, fitur mouse ini singkatnya adalah fitur untuk mengaktifkan mode mouse pada tmux yang dimana ketika kita aktifkan fitur ini, kita dapat berpindah dari panel 1 ke panel lainnya dengan hanya klik mouse ke panel yang kita inginkan. Tidak hanya itu, kita juga bisa _scroll_ dan juga _copy paste_ tanpa harus menggunakan _shortcut_ ke 7. Cara mengaktifkan dan menonaktifkan fitur ini ialah dengan kombinasi `Ctrl+b` kemudian `:` lalu ketikan `set mouse` dan tekan `enter`.


Kira-kira sekian beberapa _shortcut_ pada tmux yang biasa saya gunakan untuk membantu saya dalam pekerjaan. Semoga tulisan ini dapat membantu, apabila ada kesalah pemahaman atau kekeliruan dari tulisan saya, _feel free_ untuk dikoreksi dan didiskusikan bersama karena saya pun masih belajar sampai tulisan ini dibuat. Akhir kata terima kasih sudah membaca _and have a nice day_! :D




Refrensi : https://github.com/tmux/tmux/wiki



