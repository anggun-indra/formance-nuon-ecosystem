# Formance Ledger & Nuon Ecosystem Documentation

Dokumentasi ini berisi panduan instalasi Formance Ledger Standalone dan arsitektur sistem pembayaran terintegrasi Nuon Wallet.

## 🏗️ Arsitektur Nuon Ecosystem

Sistem ini mengintegrasikan dompet digital (Wallet) dengan infrastruktur fisik (RFID/Subway Tap Machine) menggunakan Formance Ledger sebagai jantung transaksi atomik.

```text
       [ USER LAYER ]                [ EDGE LAYER ]
      +--------------+               +--------------+
      |  Nuon Wallet |               |   Subway     |
      |   (Mobile)   |               |  Tap Machine |
      +------+-------+               +------+-------+
             |                              |
             | (REST API/JSON)              | (MQTT/gRPC/HTTPS)
             v                              v
      +---------------------------------------------+
      |          INTEGRATION & AUTH LAYER           |
      |   (API Gateway & Business Logic Service)    |
      +---------------------------------------------+
             |                              |
             | (Mapping Account ID)         | (Numscript Execution)
             v                              v
      +---------------------------------------------+
      |        CORE LEDGER (Formance V2)            |
      |  +---------------------------------------+  |
      |  |        TRANSACTIONAL ACCOUNTS         |  |
      |  |---------------------------------------|  |
      |  | @world        --> [Top-up Source]     |  |
      |  | users:idx:bal --> [User Main Balance] |  |
      |  | merch:mrt:rev --> [Subway Revenue]    |  |
      |  | system:hold   --> [Escrow/Pending]    |  |
      |  +---------------------------------------+  |
      +---------------------------------------------+
             |                              |
             v                              v
      +----------------+             +----------------+
      |   PostgreSQL   |             |  Data Archive  |
      | (Source Truth) |             |  (Audit Log)   |
      +----------------+             +----------------+
```

---

## 🚀 Panduan Instalasi (Step-by-Step)

### 1. Persiapan Lingkungan
Pastikan sistem Anda sudah terinstal Docker dan Docker Compose.

### 2. Mengambil Konfigurasi
Anda bisa menggunakan file `docker-compose.yml` dan `Caddyfile` yang sudah disesuaikan untuk akses melalui alamat IP lokal (misal: `192.168.10.13`).

### 3. Menjalankan Layanan
Gunakan perintah berikut di terminal:
\`bash
docker-compose up -d
\`

### 4. Verifikasi Instalasi
Akses layanan berikut melalui browser:
*   **Console UI:** http://[IP-ANDA]:3000
*   **API Info:** http://[IP-ANDA]:8080/api/ledger/_info

---

## 💡 Konsep Double-Entry di Formance
Sistem ini menjamin integritas data dengan memastikan setiap transaksi memiliki sumber (`source`) dan tujuan (`destination`) yang seimbang.

Contoh transaksi Top-up:
\`json
{
  "postings": [
    {
      "amount": 100000,
      "asset": "IDR",
      "destination": "users:indra:wallet",
      "source": "world"
    }
  ]
}
\`

---
*Dibuat secara otomatis oleh Elisa (OpenClaw Assistant) untuk Mas Indra.*
