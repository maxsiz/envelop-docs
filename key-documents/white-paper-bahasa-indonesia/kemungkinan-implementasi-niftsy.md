# Kemungkinan implementasi NIFTSY

Melihat pasar secara keseluruhan, interaksi berikut patut disoroti untuk bagian protokol ENVELOP (NIFTSY) yang akan diimplementasikan terlebih dahulu (MVP - Maret-April 2021, Alfa - Mei-Juli 2021):

1. **Pasar** (OpenSea, Rarible, bintang NFT, dan lainnya):
   1. Di satu sisi, poin-poin implementasi Protokol; di sisi lain, pembeli b2b produk NFT yang dibungkus dan kompleks lainnya. Artinya, untuk Proyek dan Protokol, pasar adalah titik penjualan eceran NFT yang dibuat dengan Protokol.
   2. Beberapa kasus mungkin terjadi. Ini salah satunya: pemegang NFT menjanjikan aset digital di dalam NFT urutan kedua yang baru dibuat, yang berfungsi sebagai nilai NFT yang tidak dapat dibakar untuk pemegang aset lainnya (ini menciptakan keseimbangan yang aman pada tingkat harga: Harga Dasar).
   3. Kehadiran nilai dasar yang dijamin yang didefinisikan sebagai Harga Dasar meningkatkan minat pembeli pada aset: apa pun bisa turun ke 0, tetapi jika aset mengandung dukungan minimal, itu jauh lebih baik daripada aset tanpa dukungan. Selain itu, pada tahap kedua, ada Oracle, yang memberikan penilaian independen atas aset dengan kompleksitas apa pun yang sudah ada di tahap pertama - WUM.
   4. Penulis/pemilik/orang lain pada saat peredaran NFT menetapkan mekanisme peningkatan nilai dasar NFT pada peristiwa tertentu (transaksi, penurunan, dll.) untuk meningkatkan daya tarik perdagangan NFT mereka: dan di sini Protokol berfungsi bersama dengan fungsi utilitarian Token NIFTSY.
2. **Protokol** (NFTx, NFT20, NFT, DoDoNFT, dll.):
   1. Pertama, layanan yang digunakan di bagian oracle dari Proyek, yaitu penyedia data untuk Protokol, hanyalah protokol yang berbeda, solusi blockchain, oracle jenis tertentu, dll.;
   2. Kedua, elemen tertanam dari protokol tingkat berikutnya dalam Proyek: yaitu Protokol dibangun pada tingkat L1, tetapi dimungkinkan untuk memperluas fungsinya dengan tingkat L2, mis. melalui implementasi Polygon.
3. Platform pembuatan NFT, termasuk - level bawah (L0/L1):
   1. Pertama-tama - penyedia NFT untuk agunan;
   2. Konsumen Aset, yang Protokolnya tidak diperiksa pada NFT yang dijanjikan dari setiap urutan aset kripto.
   3. Dengan demikian, Protokol berfungsi sebagai salah satu cara tidak hanya untuk membuat NFT, tetapi juga untuk memverifikasi secara otomatis dengan mengorbankan ada/tidaknya bagian yang dijaminkan pada saat yang bersamaan.
4. **Launchpad NFTs**:
   1. Protokol dapat digunakan untuk menjatuhkan token dalam format apa pun, selama mereka memiliki pembungkus NFT.
   2. Algoritma IDO melalui NFT:
      1. Startup (DAO) mengeluarkan serangkaian jenis NFT yang berbeda;
      2. Tumpuk token ERC/BEP-20/etc proyeknya ke dalam NFT. (Contoh: 100/500/1000/5000 dll. Token);
      3. Berikutnya - menentukan biaya untuk NFT;
      4. Terakhir - menjelaskan kondisi peluncuran NFT: katakanlah itu bisa dilakukan berdasarkan waktu - setelah 1 minggu / setelah dan/atau dengan ketinggian blok Ethereum/Bitcoin/BSC/etc tertentu. Selain itu, kondisinya tidak hanya dalam rentang waktu, tetapi juga dalam rentang kuantitatif atau peristiwa apa pun.
      5. Setelah NFT diterapkan, pihak lawan (peserta IDO) menerima jumlah ERC-20 dan/atau token lain yang dapat dipertukarkan ke dalam dompet (akun).
5. **Pasar penilaian NFT,** layanan analitis:
6. Protokol (digabungkan dengan Oracle dan Index) memungkinkan untuk membawa penentuan nilai yang tepat dari NFT berdasarkan alat analisis yang kompleks dengan akurasi yang diinginkan, seperti:
   1. ada nilai awal dari nilai intrinsik yang mendasarinya;
   2. koefisien / pengganda dari nilai yang mendasari urutan apa pun juga dapat diperkenalkan;
   3. karenanya - tidak sulit untuk menentukan nilai token, yang pada gilirannya dapat didukung oleh kumpulan likuiditas dan/atau parameter Harga Dasar lainnya;
   4. akhirnya, ketika Oracle terhubung, kami juga mendapatkan algoritme untuk memperkirakan nilai pasar NFT di luar subjek yang membutuhkan kepercayaan;
7. **DeFi**:
   1. Tentu saja, saat ini sudah ada kasus penggunaan NFT sebagai objek perdagangan, agunan, deposito, dll. Namun baru belakangan ini transfer likuiditas melalui segmen NFT menjadi mungkin.
   2. Padahal, ini berarti dalam 1-3 tahun ke depan kita akan mendapatkan jenis aset DeFi baru, dimana NFT sudah mengandung agunan, sedangkan agunan itu sendiri bisa serumit yang diinginkan, yang berarti entry threshold yang tinggi, sedangkan Protokol membuat masuk ke pasar tersedia secara umum.
8. **Game online (p2p - terutama)**:
   1. Format token 1155 dan 998 awalnya dibuat untuk industri game.
   2. Nilai agunan dari aset game menjadi bahan perdebatan terus-menerus dan Protokol dapat mengatasi masalah ini dengan dua cara:
      1. Melalui Oracle (lihat di bawah);
      2. Langsung - dengan memberikan harga ambang batas yang lebih rendah.
   3. Dimungkinkan juga untuk membuat drive multi-jaminan (Multi-collateral) dalam NFT awal, di mana setiap aset akan dialokasikan ke bagian drive yang sesuai dengan game tertentu (serangkaian game).
9. **Meta-universe**:
   1. Kategori ini bukan hanya sesuatu antara augmented reality (augmented/mixed), tapi ini semua tentang dunia online dalam game, ruang VR, dll.
   2. Contoh: jika Anda memiliki tanah, air, dan benih yang tepat, Anda dapat menumbuhkan pohon yang darinya Anda dapat memanen aset digital, dll. Tetapi jika pohon itu hanya tersedia di satu dunia, nilai benihnya akan rendah, sedangkan sulitnya aksesibilitas dari dunia yang berbeda justru akan membuat objek VR/AR/MR tersebut semakin bernilai.
   3. Sekali lagi, Protokol Multi-jaminan yang merupakan properti penting di sini.
10. **Pasar E-Sports**:
    1. Salah satu pesaing yang mungkin untuk pasar triliunan dolar.
    2. Sudah tersedia di dalamnya artefak berharga: mis. "senjata" bersyarat meningkatkan kekuatan dengan peningkatan nilai dasar intrinsik karena waktu penyimpanan yang lama, jumlah transaksi jual beli, perdagangan yang dikembangkan, dll.
    3. Di sisi lain masalah fan-token juga dimungkinkan, di mana lagi-lagi ada campuran dunia maya dan realitas nyata.
    4. Bagian terpisah dari kemungkinan penerapan Protokol adalah membungkus melalui NFT, di mana WUM dapat diterapkan pada hadiah, piala dan bonus lainnya; pengembangan lebih lanjut dimungkinkan, katakanlah, melalui penambahan properti ekonomi dengan mengalikan nilai acara.
    5. Tentu saja, tiket acara dan voucher hadiah yang nilainya meningkat pada tanggal acara, dan banyak lagi, juga dapat dipasarkan melalui protokol.
11. **Pasar Olahraga Klasik**:
    1. Bermain kartu untuk pemain favorit: industri sepak bola terkenal dengan ini saat ini, tetapi waktunya tidak lama lagi ketika semua olahraga akan didigitalkan sampai tingkat tertentu dan NFT jelas akan berperan di sini.
    2. Taruhan olahraga terdesentralisasi adalah area diskusi lain dan besar.
12. **Pasar realitas augmented (AR) dan virtual (VR)** itu sendiri, serta spesies baru (XR/MR) dan akuisisi aset digital sebagai akibat dari tindakan tertentu dalam ruang virtual:
    1. Mungkin contoh yang paling penting dan jelas pada saat yang sama adalah simpanan hadiah yang dapat diprogram. Ini sebagian diilustrasikan oleh film "Ready player one": sebenarnya, Project adalah Oasis dalam perspektif ini.
    2. Misi: kunci dan petunjuk yang tersembunyi di dalam ruangan dan apa pun yang dapat dibungkus dalam entitas digital juga mudah diimplementasikan menggunakan Protokol.
    3. Teka-teki: jawaban yang benar melepaskan potongan jaminan internal untuk kepentingan pemain dan/atau mereka yang bermain. Protokol dengan demikian merupakan bagian pertama dari integrasi industri game ke dalam kehidupan sehari-hari.
13. **Pasar musik**:
    1. Sebenarnya - Musik NFT: lagu / nada / ketukan dengan waktu rilis dan ketentuan kepengarangan yang dapat disesuaikan. Dengan kolaborasi yang direncanakan dengan proyek-proyek seperti SharpShark, Proyek dapat berpartisipasi dalam pengembangan industri hak cipta dan hak terkait di tingkat mana pun.
    2. Mengotomatiskan proses penyimpanan dan pengaksesan mp3/wav dan file lainnya, serta berbagi kepemilikan file tersebut.
    3. Penggunaan musik NFT di meta-universe: sambil memonetisasi setiap komponen.
14. **Pasar real estate**:
    1. Membuka kunci NFT (kepemilikan) asli ketika nilai agunan dasar tertentu tercapai - pengganti yang sangat baik untuk pinjaman hipotek dan sekaligus merupakan awal dari pasar baru untuk akuisisi real estat di luar lingkungan perbankan.
    2. Sewa melalui kunci pintar, di mana setiap akses adalah NFT, terbatas dalam waktu/jumlah penggunaan, serta perpanjangan hak kemudahan.
15. **Pasar keuangan klasik**:
    1. Obligasi sebagai NFT dengan agunan yang dijaminkan.
    2. Asuransi: NFT sebagai kontrak asuransi/polis digital dan kontrak lainnya. Sekali lagi: agunan minimal harus dari premi asuransi pertama.
    3. Transaksi portofolio/indeks: penyertaan dalam NFT sejumlah aset yang bergerak melalui dompet sesuai dengan kondisi terprogram, tetapi dengan cara yang sepenuhnya terbuka dan terdesentralisasi (masalah hukum adalah poin diskusi terpisah).
    4. Kartu hadiah digital: dengan peningkatan deposito sebagai dasar untuk mekanisme program loyalitas baru.
    5. NFT yang dapat diubah secara dinamis, terkait dengan tujuan. Contoh: gambar hitam putih sebuah mobil, yang menjadi berwarna karena jumlah yang diperlukan pada saldo mendekati akumulasi: katakanlah dengan akumulasi pada deposit, kumpulan likuiditas tim tunggal/keluarga/kelompok lain.
    6. Akses otomatis ke brankas digital melalui NFT sebagai kunci, dll. Pada saat yang sama, karena reputasi transaksional yang dihasilkan, brankas itu sendiri dapat menjadi jaminan.
16. **Pasar lotere NFT**:
    1. Jika anggaran lotere ditempatkan di dalam Multi-agunan, algoritma berikut mulai bekerja:
       1. Aset kripto seperti DAI disimpan di dalam Jaminan NFT, di dalam NFT ini ada banyak NFT lain yang berpartisipasi dalam pengundian kumpulan ini, ketika suatu peristiwa terjadi, dana dari Jaminan didistribusikan ke rekening pemegang. Pada saat yang sama, tiket itu sendiri dibuat sebagai NFT, membuat lotere benar-benar transparan. Masalah penting di sini adalah mekanisme penentuan angka acak, tetapi masalahnya berada di luar cakupan WP.
    2. Anggaran lotere berada di luar Ikrar:
       1. Kumpulan promosi dibuat dari ETH, BNB, ERC/BEP-20 (token proyek, stablecoin, token LP) dan/atau lainnya;
       2. Hanya kontrak pintar NIFTSY yang memiliki akses ke kumpulan, yang setelah terjadinya suatu peristiwa (misalnya tanggal pengundian tertentu): memilih sejumlah NFT acak dan mengirimkan konten kumpulan ke alamat yang ditentukan.
17. **Pasar lainnya:**
    1. Ada pemain lain dan seluruh segmen yang dapat mengambil manfaat dari Protokol, tetapi Protokol adalah bagian kecil dari Proyek, jadi mari kita coba menjelaskannya secara lengkap, mengungkapkan juga aspek utama Oracle dan Indeks, melihat Kasus dan prospek pengembangan Proyek dalam kaitannya dengan mereka.
