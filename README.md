# Landing Page — Progress Measurement & EVM E-Book

Landing page statik (HTML/CSS/JS tanpa framework) untuk e-book
*Project Progress Measurement & Earned Value Management* — ditulis oleh Apex Business Solutions,
dijual & diedarkan oleh **Molife Marketing** (akaun ToyyibPay).

**Live:** https://apexebook-evm.netlify.app
**Repo:** https://github.com/halidasina/apexebook-evm
**Bill ToyyibPay:** https://toyyibpay.com/EVM

Ada 2 halaman:
- `index.html` — landing page utama (butang beli terus ke ToyyibPay: `https://toyyibpay.com/EVM`)
- `terima-kasih.html` — halaman selepas bayar, ada butang muat turun e-book terus (self-hosted PDF + backup link Google Drive)

## Setup ToyyibPay (kena buat sekali sahaja)

1. **Return URL** — dalam borang bill ToyyibPay (kalau ada field tu), set ke:
   `https://apexebook-evm.netlify.app/terima-kasih.html`
   ToyyibPay akan redirect customer terus ke situ lepas bayar, dengan `status_id`, `billcode`,
   `order_id`, `transaction_id` sebagai query param — page tu dah handle both success/fail state secara automatik.

2. **Kalau tiada field Return URL** (ToyyibPay bagi "small box" untuk teks lepas bayar sahaja) —
   copy-paste teks ni ke dalam box tersebut:

   ```
   Terima kasih atas pembelian anda! Sila klik link di bawah untuk muat turun eBook anda:
   https://apexebook-evm.netlify.app/terima-kasih.html

   Sebarang masalah, WhatsApp kami: wa.me/601111535800
   ```

3. **Tarikh countdown "Harga Pelancaran"** dalam `index.html` set ke `2026-07-16T23:59:59+08:00`.
   Tukar tarikh ni bila promosi nak dilanjutkan/tamat.

## Redeploy lepas edit fail

```
netlify deploy --prod --dir=.
```

(Site sudah linked ke project `apexebook-evm` di Netlify.) Atau push ke GitHub — kalau site
disambung ke auto-deploy dari repo, cukup `git push`.

```
git add .
git commit -m "update landing page"
git push
```

## ⚠️ Nota penting: fail PDF di repo ini PUBLIC

`assets/Progress-Measurement-EVM-Guide-Apex-2026.pdf` disimpan terus dalam repo GitHub (public)
dan site Netlify. Ini bermakna sesiapa yang jumpa URL fail terus (contohnya dari GitHub atau
inspect network tab) **boleh muat turun tanpa bayar** — tiada proteksi payment-gate sebenar pada
static hosting macam ni. Ini risiko biasa untuk seller kecil guna static site + ToyyibPay,
tapi elok tahu had ini. Kalau nak proteksi lebih ketat kemudian (contohnya link sekali-guna atau
emel automatik lepas bayar), boleh upgrade ke Netlify Function / email automation — bukan
keperluan sekarang.

## Struktur fail

- `index.html` — landing page
- `terima-kasih.html` — halaman lepas bayar + muat turun e-book
- `style.css` — semua styling dikongsi oleh kedua-dua halaman (tema navy + gold)
- `netlify.toml` — konfigurasi deploy Netlify
- `assets/Progress-Measurement-EVM-Guide-Apex-2026.pdf` — fail e-book sebenar yang dimuat turun customer
