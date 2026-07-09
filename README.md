# Landing Page — Progress Measurement & EVM E-Book

Landing page statik (HTML/CSS/JS tanpa framework) untuk e-book
*Project Progress Measurement & Earned Value Management* — ditulis oleh Apex Business Solutions,
dijual & diedarkan oleh **Molife Marketing** (akaun ToyyibPay).

Ada 2 halaman:
- `index.html` — landing page utama (butang beli terus ke ToyyibPay: `https://toyyibpay.com/EVM`)
- `terima-kasih.html` — halaman selepas bayar, ada butang muat turun e-book terus

## Sebelum deploy — kena tukar dulu

1. **Tarikh countdown "Harga Pelancaran".** Dalam `index.html`, cari:
   `new Date('2026-07-16T23:59:59+08:00')` — tukar ke tarikh tamat promosi sebenar.
2. **Return URL kat ToyyibPay** (kalau ada field tu dalam borang create bill) — set ke:
   `https://<site-anda>.netlify.app/terima-kasih.html`
   ToyyibPay akan redirect customer terus ke situ lepas bayar, dengan `status_id`, `billcode`,
   `order_id`, `transaction_id` sebagai query param — page tu dah handle both success/fail state.
3. Anda tak boleh dapat URL Netlify sebenar sehingga dah deploy (langkah bawah) — deploy dulu,
   baru copy URL tu balik ke ToyyibPay.

## Deploy ke GitHub + Netlify

### 1. Create repo di GitHub
- Pergi ke github.com → New repository → bagi nama (contoh `evm-ebook-landing`) → Create.
- Jangan tambah README/gitignore (folder ni dah ada fail).

### 2. Push fail ni ke repo
Buka terminal dalam folder `evm-ebook-landing/` ni, run:

```
git init
git add .
git commit -m "Landing page: Progress Measurement & EVM e-book"
git branch -M main
git remote add origin https://github.com/<username>/<nama-repo>.git
git push -u origin main
```

### 3. Connect ke Netlify
- Log masuk netlify.com → **Add new site → Import an existing project**
- Pilih GitHub → pilih repo yang baru push tadi
- Build settings: **kosongkan Build command**, **Publish directory = `.`** (root)
- Deploy site

Netlify akan bagi URL automatik (contoh `random-name-123.netlify.app`).
Boleh tukar ke domain custom kemudian di **Site settings → Domain management**.

### 4. Lengkapkan loop ToyyibPay
- Copy URL Netlify anda.
- Kembali ke borang bill ToyyibPay → isi **Return URL** (jika ada) dengan
  `https://<url-netlify-anda>/terima-kasih.html`
- Isi **Extra Email Content** dengan teks yang disediakan (rujuk mesej chat / bawah).

## Struktur fail

- `index.html` — landing page
- `terima-kasih.html` — halaman lepas bayar + muat turun e-book
- `style.css` — semua styling dikongsi oleh kedua-dua halaman
- `netlify.toml` — konfigurasi deploy Netlify
- `assets/Progress-Measurement-EVM-Guide-Apex-2026.pdf` — fail e-book sebenar yang dimuat turun customer
