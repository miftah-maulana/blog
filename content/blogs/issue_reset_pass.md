---
author: "Miftah Maulana Wahab"
title: "Issue Reset Password Grafana"
description : "Journal troubleshoot saat ingin reset password grafana"
date: 2025-02-26T00:16:05+07:00
tags: ["Linux", "Grafana", "Monitoring"]
showToc: true
---

![grafana_logo](https://miftah-maulana.my.id/assets/images/Grafana_issue/grafana_logo.png)

Terdapat issue gagal masuk Grafana dikarenakan administrator yang lupa kata sandi user admin pada service Grafana. Beranjak dari masalah tersebut dilakukan reset password dari sisi server. Berikut cara, kendala, 
beserta work arround yang saya dan tim lakukan untuk reset password admin Grafana.

Berdasarkan dokumentasi dari Grafana yang saya dan tim baca untuk me-reset password admin pada grafana dapat dilakukan dengan command :

```
$ grafana cli admin reset-admin-password <new-password>
```

Namun ketika sudah dijalankan keluar pesan error dengan log : 

```
CRIT[09-26|08:30:10] failed to parse "/etc/grafana/grafana.ini": open /etc/grafana/grafana.ini: no such file or directory
```

Setelah dilakukan penelusuran melalui forum dan community grafana, solusi yang ditemukan mencoba untuk menggunakan homepath yakni dengan menambah paramete homepath di command sehingga menjadi :
```
$ sudo grafana cli --homepath "/usr/share/grafana" admin reset-admin-password  <new-pasword>
```
Namun output yang dihasilkan dari command tersebut tetap sama. Kemudian mencoba melakukan identifikasi ke konfigurasi grafana.service. Ternyata ditemukan untuk konfigurasi homepath pada service grafana di server 
yang sedang issue ini bukan pada "/usr/share/grafana", melainkan pada "/opt/grafana-8.2.3". Kurang lebih untuk konfigurasi systemd grafana.service nya pada server yang sedang bermasalah seperti berikut :

```
# /etc/systemd/system/grafana.service
[Unit]
Description=Grafana

[Service]
User=root
ExecStart=/opt/grafana-8.2.3/bin/grafana-server -homepath /opt/grafana-8.2.3 web

[Install]
WantedBy=default.target
```

Akhirnya dilakukan perbaikan command seperti berikut :
- Sebelumnya :
```
$ sudo grafana cli --homepath "/usr/share/grafana" admin reset-admin-password <new-password>
```
- Menjadi :
```
$ sudo grafana cli --homepath "/opt/grafana-8.2.3" admin reset-admin-password <new-password>
```

Namun output yang keluar tetap dengan error yang sama yaitu :

```
CRIT[09-26|08:36:10] failed to parse "/etc/grafana/grafana.ini": open /etc/grafana/grafana.ini: no such file or directory
```
Setelah di teliti error log ini menunjukan bahwasannya menuju kepada file "grafana.ini" yang tidak ditemukan ketika melakukan eksekusi reset password. Akhirnya dilakukan penelusuran untuk file grafana.ini 
berada dimana, dan setelah dicari ternyata file ".ini" pada server ini bukan menggunakan nama "grafana.ini", melainkan "defaults.ini", bisa dilihat pada gambar.

![defaults.ini](https://miftah-maulana.my.id/assets/images/Grafana_issue/defaults_ini.png)

lalu berikut untuk pemecahan final yang saya dan tim lakukan untuk menangani issue reset admin password service grafana pada server yang akhirnya berhasil untuk di reset passwordnya :

```
$ cd /opt/grafana-8.2.3 
$ ls (kemudian menemukan adanya direktori conf)
$ ls conf/ (kemudian menemukan adanya file .ini dengan nama defaults.ini, bukan grafana.ini)
$ sudo grafana-cli --homepath /opt/grafana-8.2.3/ --config conf/defaults.ini admin reset-admin-password <new-password> (menambahkan parameter --config agar pada saat command dijalankan mengarah ke konfig defaults.ini)
```
![end_prosess](https://miftah-maulana.my.id/assets/images/Grafana_issue/end_process_password_success_reset.png)


Refrensi :
- https://grafana.com/docs/grafana/latest/cli/#reset-admin-password
- https://community.grafana.com/t/admin-password-reset/19455
