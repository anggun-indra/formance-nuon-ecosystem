# Implementasi Teknis Aliran Dana Kredit dengan Formance

## Struktur Akun (Ledger)
Untuk setiap kredit, kita mendefinisikan struktur akun berikut:
- `source:bank:vault`: Sumber dana utama.
- `customer:loan:principal:{id}`: Saldo pokok pinjaman nasabah.
- `customer:loan:interest:{id}`: Akrual bunga.
- `revenue:interest`: Pendapatan bunga perusahaan.

## Transaksi 1: Pencairan (Disbursement)
Memindahkan dana dari bank ke nasabah.
```json
{
  "postings": [
    {
      "source": "source:bank:vault",
      "destination": "customer:loan:principal:001",
      "amount": 5000000,
      "asset": "IDR"
    }
  ]
}
```

## Transaksi 2: Akrual Bunga Bulanan
```json
{
  "postings": [
    {
      "source": "world",
      "destination": "customer:loan:interest:001",
      "amount": 50000,
      "asset": "IDR"
    }
  ]
}
```

## Transaksi 3: Pembayaran Cicilan
Alokasi dana masuk untuk menutup bunga terlebih dahulu, kemudian pokok.
```json
{
  "postings": [
    {
      "source": "customer:wallet",
      "destination": "revenue:interest",
      "amount": 50000,
      "asset": "IDR"
    },
    {
      "source": "customer:wallet",
      "destination": "source:bank:vault",
      "amount": 450000,
      "asset": "IDR"
    }
  ]
}
```
