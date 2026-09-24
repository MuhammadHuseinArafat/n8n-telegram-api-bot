# n8n-telegram-api-bot

1. Project Name
Automated API Data Fetcher & Telegram Distribution System (Daily Motivation Bot)

2. Business Problem
Mendistribusikan informasi harian, pengumuman, atau pembaruan data secara manual ke dalam grup komunikasi tim memakan waktu, rentan terlewat, dan sangat repetitif.

3. Proposed Solution
Membangun serverless workflow menggunakan n8n yang secara otomatis menarik data dari eksternal REST API, memformat data tersebut, dan mendistribusikannya langsung ke Telegram tanpa intervensi manusia.

4. Workflow Architecture
Telegram Trigger ➡️ HTTP Request (REST API) ➡️ Data Transformation (Expressions) ➡️ Telegram Action

5. Tools Used

n8n (Workflow Automation)

Telegram Bot API (Messaging Interface)

ZenQuotes Public API (Data Source)

6. n8n Nodes Used

Telegram Trigger (On Message)

HTTP Request (GET Method)

Telegram Action (Send Text Message)

7. Input & Processing

Input: Perintah teks dari pengguna di Telegram.

Processing: HTTP GET Request mengeksekusi panggilan ke endpoint API eksternal. Data JSON yang diterima {"q": "quote", "a": "author"} diekstrak menggunakan n8n Expressions ({{ $json.q }}) agar formatnya sesuai dengan template pesan yang diinginkan.

8. Output
Pesan teks dinamis yang dikirimkan secara instan ke Chat ID Telegram spesifik.

9. Security & Error Handling (Basic)

API Token Telegram diamankan di dalam sistem Credentials Manager n8n, tidak disisipkan (hardcoded) di dalam node.

10. Business Value & Time Saved

Mengeliminasi 100% intervensi manusia dalam proses pencarian dan pengiriman data harian.

Scalable: Konsep ini dapat direplikasi untuk mengirimkan laporan laba-rugi harian, notifikasi server down, atau lead alert dari CRM langsung ke HP eksekutif.
