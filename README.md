# KELOMPOK 5 P2 - APPRISE
  - Hasan Fadilah (G6401231051)
  - Hannan Azhari Batubara (G6401231052)
  - Cokorda Gede Satria Widnyana Putra (G6401231064)
  - Jofattan Faiz Betryan (G6401231066)
  - Jordan Vieno Simamora (G6401231135)
  
![Tampilan Screenshot Aplikasi](https://raw.githubusercontent.com/hasanfadils/KDJK5-K2/refs/heads/main/Screenshoot/Apprise%20Logo.png)
[Sekilas Tentang](#sekilas-tentang) | [Instalasi&Setup](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)

## Sekilas Tentang

**Apprise** adalah sebuah library dan command line tool (CLI) untuk mengirimkan notifikasi ke hampir semua layanan notifikasi populer, seperti Telegram, Discord, Slack, Amazon SNS, Gotify, Email (SMTP/Gmail), dan lainnya.
Tujuan utamanya adalah memberikan satu cara yang sederhana, ringan, dan seragam untuk mengirim notifikasi tanpa perlu menulis integrasi untuk setiap layanan satu per satu.


**Prasyarat**  
  - Python (versi terbaru disarankan, ≥ 3.7)  
  - pip (package manager Python)  

## Instalasi & Set Up
- Membuat virtual environment dengan python 3.12
   
```bash
py -3.12 -m venv .venv
```

- Virtual Environment
   
```bash
.\.venv\Scripts\Activate.ps1
```

- Git clone 

digunakan untuk melakukan unduh sumber kode
git clone https://github.com/caronc/apprise-api.git
cd apprise-api

- Install dev

Lakukan langkah ini untuk memasang proyek dari folder saat ini ke venv dalam mode editable sekaligus menginstal paket ekstra “dev”, sehingga semua dependensi terpenuhi dan setiap perubahan kode langsung terbaca saat menjalankan Apprise API

```bash
pip install -e ".[dev]"
```

- Run server

Jalankan server di alamat http://127.0.0.1:8000/

```bash
python manage.py runserver
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

Contoh script shell untuk instalasi dan mengirim notifikasi otomatis:
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
