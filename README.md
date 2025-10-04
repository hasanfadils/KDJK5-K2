# KELOMPOK 5 P2 - APPRISE
  - G6401231051	Hasan Fadilah
  - G6401231052	Hannan Azhari Batubara
  - G6401231064	Cokorda Gede Satria Widnyana Putra
  - G6401231066	Jofattan Faiz Betryan
  - G6401231135	Jordan Vieno Simamora
  
![Tampilan Screenshot Aplikasi](https://github.com/hasanfadils/KDJK5-K2/blob/main/Screenshot%202025-10-04%20164903.png?raw=true)

## Sekilas Tentang

**Apprise** adalah sebuah library dan command line tool (CLI) untuk mengirimkan notifikasi ke hampir semua layanan notifikasi populer, seperti Telegram, Discord, Slack, Amazon SNS, Gotify, Email (SMTP/Gmail), dan lainnya.
Tujuan utamanya adalah memberikan satu cara yang sederhana, ringan, dan seragam untuk mengirim notifikasi tanpa perlu menulis integrasi untuk setiap layanan satu per satu.


**Prasyarat**  
  - Python (versi terbaru disarankan, ≥ 3.7)  
  - pip (package manager Python)  

**Langkah instalasi dalam CLI**  
  ```bash
  pip install apprise
  ```
 

## Konfigurasi 
Beberapa konfigurasi yang dapat dilakukan:
- Menambahkan URL notifikasi (Telegram, Slack, Discord, dsb.) ke dalam skrip konfigurasi.
- Mengatur syntax notifikasi yang umum dan intuitif.
- Mengaktifkan dukungan gambar dan attachment (jika layanan mendukung).
Plugin tambahan (misalnya integrasi login pihak ketiga) tidak diperlukan, karena Apprise sudah support multi-platform notification secara native.


##  Maintenance

Tidak ada konfigurasi maintenance yang rumit.
Namun, untuk sistem server:
- Bisa menambahkan cron job untuk otomatisasi backup notifikasi log.
- Monitoring performa karena Apprise mengirim pesan secara asynchronous.

## Otomatisasi

Bisa dibuat script shell untuk otomatisasi:
 ```bash
 #!/bin/bash
pip install apprise
apprise -t "Judul Pesan" -b "Isi notifikasi" "discord://token/..."
apprise -t "Hello via Email" -b "Ini pesan lewat Gmail" "mailto://user@gmail.com:password@smtp.gmail.com"
```

## Cara Pemakaian

Tampilan aplikasi: berbasis CLI, tidak memiliki GUI bawaan.
Fungsi utama:
- Mengirim notifikasi teks ke berbagai layanan (Telegram, Slack, Discord, Email/Gmail, dll).
- Mendukung attachment (gambar/file) jika layanan memungkinkan.
- Pesan dikirim secara asynchronous → respon cepat.
 ```bash
  apprise -t "Hello" -b "Ini pesan dari Apprise" "tgram://TOKEN/CHAT_ID"
apprise -t "Notifikasi Email" -b "Pesan lewat Gmail" "mailto://user@gmail.com:password@smtp.gmail.com"
```


## Pembahasan

**Kelebihan :**
- Satu library untuk hampir semua layanan notifikasi.
- Lightweight dan cepat.
- Syntax seragam dan intuitif.
- Mendukung attachment (gambar/file).
- Support banyak platform termasuk Email/Gmail.
  
**Kekurangan :**
- Tidak ada GUI bawaan (hanya CLI dan library).
- Fungsi terbatas hanya untuk notifikasi, bukan aplikasi chatting penuh.
- Bergantung pada API layanan pihak ketiga (jika berubah, perlu update).
  
**Perbandingan :**
- Dibanding coding manual API Telegram/Slack/SMTP, Apprise jauh lebih ringkas.
- Dibanding Pushover atau Firebase, Apprise lebih fleksibel (multi-platform), tapi mungkin tidak selengkap fitur native platform tertentu.


## Referensi
- Dokumentasi resmi: https://github.com/caronc/apprise
