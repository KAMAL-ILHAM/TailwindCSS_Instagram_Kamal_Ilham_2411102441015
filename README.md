## Pertanyaan README

### 1. Jelaskan keputusan `grid-cols/gap` di tiap breakpoint - kenapa begitu?

Keputusan ini mengikuti prinsip **mobile-first** untuk memastikan tampilan optimal di semua ukuran layar.

* **Header Profil (`grid-cols-3`):** Layout ini secara konsisten membagi area untuk foto (1 kolom) dan info (2 kolom). Di layar lebar (`md:`), `gap` diperbesar menjadi `md:gap-8` agar elemen tidak terlihat terlalu rapat dan lebih seimbang.
* **Galeri Postingan (`grid-cols-1 sm:grid-cols-3 lg:grid-cols-4`):**
    * **Mobile (`grid-cols-1`):** Satu kolom agar setiap foto terlihat jelas.
    * **Tablet (`sm:grid-cols-3`):** Berubah ke 3 kolom khas Instagram. `gap` sengaja dibuat sangat kecil (`sm:gap-1`) untuk menciptakan tampilan grid yang rapat.
    * **Desktop (`lg:grid-cols-4`):** Menjadi 4 kolom untuk mengisi ruang yang lebih lebar saat sidebar muncul, menjaga proporsi gambar tetap ideal.

---

### 2. Bagaiamana kamu memanfaatkan utility responsive tailwind untuk memecahkan masalah layout yang muncul di mobile?

Utility responsive Tailwind digunakan untuk mengatasi keterbatasan ruang di layar kecil dengan cara:

1.  **Menukar Komponen:** Menyembunyikan elemen besar dan menampilkan alternatif yang ringkas. Contohnya, **sidebar desktop** (`hidden lg:flex`) disembunyikan dan digantikan oleh **navigasi atas & bawah mobile** (`lg:hidden`).
2.  **Mengatur Ulang Layout:** Membuat duplikat elemen yang hanya muncul di ukuran layar tertentu. Contohnya, **statistik pengikut** yang horizontal di desktop (`hidden sm:flex`) diubah menjadi vertikal di bawah *highlights* khusus untuk mobile (`sm:hidden`).
3.  **Adaptasi Ukuran & Spasi:** Mengubah ukuran properti sesuai breakpoint, seperti **padding** (`px-0 sm:px-4`) dan **ukuran gambar** (`w-[90px] sm:w-[150px]`) agar pas di setiap layar.

---

### 3. Jelaskan trade-off antara memakai banyak utility classes vs membuat component CSS sendiri

Ini adalah pilihan antara kecepatan dan kerapian kode jangka panjang.

* **Utility Classes (Cara Tailwind):**
    * **Kelebihan:** Sangat cepat untuk membangun UI langsung di HTML tanpa perlu file CSS terpisah. Styling bersifat lokal dan tidak mudah bentrok.
    * **Kekurangan:** Membuat HTML terlihat penuh dan panjang dengan banyak kelas dan sulit untuk me-maintain elemen yang berulang (tidak DRY).

* **Component CSS (misal dengan `@apply`):**
    * **Kelebihan:** Menjaga HTML tetap bersih dan semantik (`<button class="btn-primary">`). Mudah untuk mengubah desain semua komponen serupa dari satu tempat (prinsip DRY).
    * **Kekurangan:** Memperlambat development karena harus bolak-balik antara file HTML dan CSS.

**Solusi Terbaik:** Gunakan **pendekatan hybrid**. Pakai *utility classes* untuk layout dan styling unik, lalu buat *component class* (`@apply`) untuk elemen yang sering digunakan berulang kali seperti tombol atau kartu.

# Clone Profil Instagram dengan Tailwind CSS

Proyek ini adalah upaya untuk mereplikasi antarmuka pengguna (UI) halaman profil Instagram (versi desktop dan mobile) menggunakan **Tailwind CSS**.

---

## Penjelasan Desain

### Replikasi UI Instagram 

Desain ini berfokus pada meniru tampilan dan nuansa halaman profil Instagram, khususnya pada bagian tata letak profil, statistik, Sorotan (Highlights), dan grid postingan.

#### Responsif Penuh
Implementasi ini memastikan tata letak beradaptasi dengan baik antara tampilan seluler (kecil) dan desktop/tablet (besar).

* **Desktop (`lg`)**: Terdapat bilah sisi **(Sidebar)** navigasi permanen di sebelah kiri dengan ikon dan teks, meniru tata letak Instagram yang lebih baru.
* **Mobile/Tablet (Default)**: Sidebar disembunyikan. Navigasi atas dan bawah yang `fixed` digunakan untuk pengalaman yang mirip dengan aplikasi seluler.

#### Komponen Kunci

* **Navbar & Sidebar**: Menggunakan properti `fixed` dan *breakpoint* `lg:` untuk mengatur visibilitas dan tata letak navigasi.
* **Header Profil**: Menggunakan **Grid CSS** (`grid grid-cols-3`) untuk menata foto profil, detail, dan tombol tindakan, dengan penyesuaian tata letak (`sm:`, `md:`) agar terlihat seperti Instagram pada berbagai ukuran layar.
* **Sorotan (Highlights)**: Menggunakan `overflow-x-auto` dan kelas utilitas `.no-scrollbar` (didefinisikan dalam `<style>`) untuk membuat daftar gulir horizontal tanpa bilah gulir, seperti di aplikasi.
* **Grid Postingan**: Menggunakan **Grid CSS** (`grid grid-cols-1 sm:grid-cols-3 lg:grid-cols-4`) untuk menampilkan gambar-gambar postingan secara responsif.
* **Efek Hover Postingan**: Menyertakan efek *hover* yang menampilkan jumlah *likes* dan komentar, diimplementasikan dengan kelas utilitas `group` dan `group-hover:`.

#### Warna dan Tipografi

* Menggunakan skema warna yang mendekati UI Instagram, terutama warna latar belakang (`bg-stone-50`), teks utama (`text-zinc-800`), dan batas (`border-stone-300`).
* Font **'Grand Hotel'** digunakan untuk logo "Instagram", meniru tampilan aslinya.

---

## Teknologi yang Digunakan

* **HTML5**: Struktur dasar halaman.
* **Tailwind CSS (CDN)**: Digunakan untuk seluruh *styling* dan membuat desain responsif dengan cepat.
* **Font Awesome**: Digunakan untuk ikon-ikon yang ada di navigasi dan detail postingan.
* **Google Fonts**: Digunakan untuk mengimpor font **Grand Hotel**.

---

## Pertanyaan Reflektif

1.  **Pendekatan Responsif**: Dalam mengimplementasikan tata letak untuk desktop (sidebar) dan mobile (navbar atas/bawah), apa tantangan utama dalam menjaga **konsistensi tampilan** (seperti *padding* dan *margin*) di kedua mode?
2.  **Ketergantungan CDN**: Proyek ini menggunakan Tailwind CSS melalui CDN. Jika Anda memutuskan untuk mem-build proyek ini menggunakan *build tool* (seperti PostCSS atau Vite) dan PurgeCSS, bagaimana Anda akan mengkonfigurasi file `tailwind.config.js` agar hanya menyertakan kelas yang benar-benar digunakan, mengingat Anda juga mendefinisikan *custom* CSS (`.font-grand-hotel` dan `.no-scrollbar`)?
3.  **Aksesibilitas (A11Y)**: Ikon di sidebar dan navigasi mobile tidak memiliki teks yang terlihat pada semua ukuran (seperti ikon "Cari" atau "Reels"). Bagaimana Anda dapat meningkatkan **aksesibilitas** untuk pengguna *screen reader* sambil tetap mempertahankan desain visual saat ini? (Petunjuk: Pikirkan tentang atribut HTML).
4.  **Optimalisasi Gambar**: Banyak gambar yang digunakan (profil, sorotan, postingan) langsung dimuat sebagai `<img>`. Bagaimana Anda akan mengoptimalkan **pemuatan gambar** untuk meningkatkan performa halaman (misalnya, untuk tampilan mobile yang mungkin membutuhkan resolusi lebih rendah), tanpa menggunakan *framework* JavaScript?
