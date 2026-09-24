# n8n Telegram API Bot

Workflow otomatis untuk mengambil data dari REST API, memformatnya, lalu mengirimkannya ke Telegram menggunakan n8n.

## 1. Nama Proyek

**Automated API Data Fetcher & Telegram Distribution System**  
Daily Motivation Bot berbasis n8n.

## 2. Latar Belakang Masalah

Mendistribusikan informasi harian, pengumuman, atau pembaruan data secara manual ke grup komunikasi tim:

- Memakan waktu.
- Rentan terlewat.
- Bersifat repetitif.

## 3. Solusi yang Ditawarkan

Proyek ini membangun workflow serverless menggunakan **n8n** untuk:

1. Menerima perintah teks dari pengguna melalui Telegram.
2. Mengambil data dari REST API eksternal.
3. Memformat data menggunakan n8n Expressions.
4. Mengirimkan hasilnya kembali ke Telegram secara otomatis.

Dengan demikian, proses distribusi informasi dapat berjalan tanpa intervensi manual.

## 4. Arsitektur Workflow

```text
Telegram Trigger
      ↓
HTTP Request (REST API)
      ↓
Data Transformation (Expressions)
      ↓
Telegram Action
```
<img width="1916" height="936" alt="image" src="https://github.com/user-attachments/assets/f82d339b-2f49-4288-8685-f5daba92cb16" />


## 5. Teknologi yang Digunakan

| Teknologi | Fungsi |
| --- | --- |
| **n8n** | Platform workflow automation |
| **Telegram Bot API** | Antarmuka untuk menerima dan mengirim pesan |
| **ZenQuotes Public API** | Sumber data kutipan motivasi |

## 6. Node n8n yang Digunakan

- **Telegram Trigger** — menerima pesan dari pengguna.
- **HTTP Request** — melakukan request dengan metode `GET` ke REST API.
- **Telegram Action** — mengirimkan pesan teks ke pengguna atau grup Telegram.

## 7. Input dan Pemrosesan Data

### Input

Perintah teks yang dikirimkan pengguna melalui Telegram.

### Processing

Node **HTTP Request** melakukan pemanggilan ke endpoint API eksternal. Data JSON yang diterima memiliki format berikut:

```json
{
  "q": "quote",
  "a": "author"
}
```

Data kemudian diekstrak menggunakan n8n Expressions, misalnya:

```text
{{ $json.q }}
{{ $json.a }}
```

Hasil ekstraksi digunakan untuk menyusun pesan yang akan dikirimkan melalui Telegram.
<img width="709" height="287" alt="image" src="https://github.com/user-attachments/assets/c6d1296f-c831-458f-b43a-2cc9eb9d2df6" />


## 8. Output

Pesan teks dinamis yang dikirimkan secara otomatis ke Chat ID Telegram yang ditentukan.

Contoh format pesan:

```text
"Quote of the day"
— Author
```
<img width="720" height="835" alt="image" src="https://github.com/user-attachments/assets/da800230-7e10-4370-8ae8-eb611f16abc2" />


## 9. Keamanan dan Error Handling

- Token API Telegram disimpan menggunakan **Credentials Manager** di n8n.
- Token tidak ditulis secara langsung (*hardcoded*) di dalam node atau workflow.
- Workflow dapat dikembangkan lebih lanjut dengan menambahkan penanganan error untuk kegagalan request API atau pengiriman pesan.

## 10. Nilai Bisnis

Workflow ini membantu menghilangkan intervensi manual dalam proses pencarian dan pengiriman informasi harian.

Konsepnya juga dapat dikembangkan untuk mengirimkan:

- Laporan laba-rugi harian.
- Notifikasi ketika server mengalami gangguan.
- Peringatan atau *lead alert* dari CRM.
- Pengumuman otomatis ke grup komunikasi tim.

Dengan struktur workflow yang fleksibel, sistem dapat direplikasi dan disesuaikan untuk berbagai kebutuhan bisnis.
