# Arsitektur Integrasi Formance Ledger - MRTJ (Nuon Ecosystem)

## 🏗️ Posisi Formance Ledger dalam Sistem MRTJ
Formance Ledger bertindak sebagai **Source of Truth (Pusat Kebenaran)** untuk semua pergerakan dana di ekosistem MRTJ. Ia tidak menggantikan mesin AFC atau App Wallet, melainkan menjadi "mesin akuntansi" di belakangnya.

### 🧩 Diagram Arsitektur (Mermaid)

```mermaid
graph TD
    User((User)) -->|Tap RFID/QR| AFC[Mesin AFC / Gate MRTJ]
    User -->|Top-up/Cek Saldo| Wallet[Nuon Wallet App]

    subgraph "Integration Layer (Nuon Service - To be Developed)"
        API[API Gateway / Business Logic]
        Auth[Auth & Validation]
    end

    subgraph "Core Ledger (Formance Stack)"
        FL[Formance Ledger Engine]
        DB[(PostgreSQL)]
    end

    AFC -->|Send Transaction| API
    Wallet -->|Request Transaction| API
    API -->|Execute Numscript| FL
    FL <--> DB

    subgraph "Settlement"
        Bank[Bank Partner / Escrow]
        MRTJ[Akun Pendapatan MRTJ]
    end

    FL -->|Atomic Transfer| MRTJ
    FL -->|Reconciliation| Bank
```

## 🛠️ Apa yang Harus Kita Develop?
1.  **Middleware Integration Service:** Layanan (Go/Python) yang menerima data dari mesin AFC dan menerjemahkannya menjadi perintah *posting* ke Formance Ledger.
2.  **Numscript Engine:** Skrip untuk logika pembagian pendapatan (misal: pembagian antara operator sarana dan prasarana).
3.  **Settlement Worker:** Sistem otomatis untuk memindahkan dana dari akun penampung ke akun bank mitra setiap akhir hari.

## 🛡️ Mengapa Formance Ledger?
Formance Ledger adalah standar industri untuk sistem keuangan modern.
- **Battle-Tested:** Digunakan oleh berbagai platform fintech dunia untuk mengelola jutaan transaksi.
- **Pendanaan Kuat:** Baru saja mendapatkan pendanaan **Seri A sebesar $21 Juta** pada tahun 2025.
- **Bukti Pendanaan:** [Formance Secures $21M Series A for Ledger-as-a-Service Platform](https://www.formance.com/blog/formance-series-a-funding)

---
*Dokumen ini diperbarui berdasarkan RFI Sistem Manajemen Kredit/Pembayaran MRTJ.*
