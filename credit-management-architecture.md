# Arsitektur Sistem Manajemen Kredit (Proposed)

## Pendahuluan
Dokumen ini menguraikan arsitektur sistem manajemen kredit yang dirancang untuk menangani siklus hidup pinjaman secara end-to-end, mulai dari pengajuan hingga pelunasan, dengan fokus pada akurasi finansial dan transparansi.

## Komponen Utama
1. **Loan Origination System (LOS)**: Menangani aplikasi, scoring, dan persetujuan.
2. **Core Banking / Credit Management System**: Mengelola data peminjam, tenor, bunga, dan jadwal pembayaran.
3. **Formance Ledger (Fintech Engine)**: Sebagai sumber kebenaran (source of truth) untuk semua pergerakan dana.
4. **Payment Gateway Integration**: Untuk pencairan dan penagihan dana.

## Aliran Proses
- **Persetujuan**: Data kredit dikirim ke Ledger untuk pembuatan akun (chart of accounts).
- **Pencairan**: Ledger mencatat perpindahan dana dari akun sumber ke akun peminjam.
- **Pembayaran**: Setiap cicilan dipecah menjadi pokok, bunga, dan denda (jika ada) di dalam Ledger menggunakan skema double-entry.

## Keunggulan Desain
- **Immutability**: Semua transaksi tercatat permanen.
- **Scalability**: Menggunakan microservices yang terintegrasi dengan Ledger performa tinggi.
