# VIX Front End Core Initiative - Ecommerce catalog Website

Pada task terakhir VIX Front End Core Initiative ini, tim Front End akan bekerja sama dengan tim UI/UX dan tim Backend untuk membentuk sebuah interface dari sebuah website Ecommerce. Tugas utama dalam proyek ini adalah membuat dua halaman yaitu "Men’s Clothing" dan "Women’s Clothing". Berikut adalah poin-poin utama yang dikerjakan:

1. **Menampilkan Data dari API:** Data akan diambil dari API https://fakestoreapi.com. Setiap index dari 1 hingga 20 akan memiliki kategori yang berbeda. Sebagai contoh, https://fakestoreapi.com/products/1 memiliki kategori "men’s clothing".

2. **Tampilan Produk Dinamis:** Pada halaman produk, hanya akan ditampilkan satu produk pada satu waktu. Namun, produk tersebut akan berubah setiap kali pengguna menekan tombol "Next Product".

3. **Loading Element:** Ketika aplikasi menunggu balasan dari API, akan ada loading skeleton element/loader yang akan ditampilkan. Ini bertujuan untuk menjaga desain tetap UX friendly. .

## API Call

Saya menggunakan API Ecommerce dari https://fakestoreapi.com. Dokumentasi lengkap mengenai API ini dapat ditemukan di [sini](https://fakestoreapi.com/docs).

- API akan diakses dengan endpoint https://fakestoreapi.com/products/index, di mana "index" adalah angka dari 1 hingga 20.
- API akan dipanggil setiap kali pengguna menekan tombol "Next Product". Index akan diinkrementasi setiap kali tombol tersebut ditekan. Index ini akan digunakan untuk mengambil data dari API.

- Setelah menerima respons dari API, akan dilakukan pengecekan kategori produk. Jika kategori adalah "men’s clothing" atau "women’s clothing", respons akan disimpan dalam variabel data. Jika kategori adalah yang lain, respons akan diabaikan.

- Untuk menghindari error saat mengambil data dari API, jika index sudah mencapai 20, maka index akan diatur ulang ke 1. Ini disebabkan karena API hanya menyediakan 20 jenis produk.

## Komponen Desain

Proyek ini memiliki tiga jenis desain: men section, women section, dan unavailable product. Semua desain mengimplementasikan Vanilla CSS (CSS tanpa framework).

Dalam proyek Vue saya menggunakan class binding untuk memeriksa kategori produk. Jika kategori adalah "men’s clothing", maka akan digunakan class CSS yang berkaitan dengan desain "Page-Men section". Jika kategori adalah "women’s clothing", akan digunakan class CSS yang berkaitan dengan desain "Page-Women section". Jika kategori adalah yang lain, akan digunakan class CSS yang berkaitan dengan desain "Page-Unavailable product".

---

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
