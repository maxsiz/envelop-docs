# Protokol

Masalah pertama yang harus dipecahkan oleh Proyek adalah objektivitas data agunan. Bagian ini ditangani oleh Protokol - yaitu memformalkan dalam entitas onchain dari blockchain apa pun melalui mekanisme NFT.

Mari kita ingat Kewajiban hutang yang dijaminkan (Collateralised debt obligations/CDO) - kewajiban hutang yang dijaminkan: inilah dan credit default swaps (credit default swaps/CDS) yang menyulut api krisis 2007-2009. Mengapa?

Yang paling penting karena tidak jelas apa yang ada di balik "sekuritas" ini, apa yang ada di balik peringkat mereka - bahkan jika mereka adalah yang tertinggi, yaitu AAA, apa pengaruh suku bunga mengambang yang menjadi dasar pinjaman, yang menjadi dasar CDO ini pada gilirannya berbasis? Apa yang terjadi di AS pada tahun 2008 mungkin terjadi di Rusia 2021 dan puluhan negara lain dengan tingkat ekonomi yang berbeda. Tapi kenapa tepatnya?

Karena belum ada mekanisme agunan yang dibuat untuk instrumen keuangan yang kompleks. Namun, sebagian dari prinsip mereka melekat pada pasar DeFi yang mapan, meskipun masih "mentah". Mari kita coba mengklarifikasi dan dengan demikian mengungkapkan tujuan utama ENVELOP (NIFTSY) dan tokennya.

### NFT sebagai ETF orde baru dan sejarah singkat NIFTSY

Pertama, apa itu ETF? Exchange-traded fund (ETF) adalah dana indeks yang unitnya (saham) diperdagangkan di bursa. Artinya, hampir satu unit, tetapi "tidak seperti reksa dana indeks, saham ETF dapat ditangani dengan cara yang sama seperti saham biasa dalam perdagangan yang diperdagangkan di bursa.

Mengapa pasar crypto membutuhkan ini? Jawabannya ada beberapa:

* Pertama, jauh lebih nyaman bagi pendatang baru untuk mengambil portofolio (dibahas di bawah) daripada membangun sendiri dari awal, kecuali jika kita berbicara tentang 10 mata uang/token teratas. Lihat saja sejarah pasar kripto dari 2009 (1 aset) hingga 2021 (lebih dari 7000 aset, tidak termasuk derivatif), untuk memahami bahwa model seperti itu akan diminta.
* Kedua, bagi investor profesional, pembagian portofolio, diversifikasi, penilaian aset yang objektif adalah penting dan di sini keragaman juga membingungkan. Tetapi yang paling penting, itu tidak selalu memungkinkan penilaian yang cepat dan akurat dari aset-aset tersebut. Masalah lain adalah mempersulit pertukaran portofolio, untuk mengungkapkannya atau, sebaliknya, untuk tetap anonim. Transaksi OTC memerlukan penjamin agunan, sedangkan ETF yang dibuat melalui NFT hanya dapat diperdagangkan melalui Protokol.
* Ketiga, evolusi sistem p2p adalah bukti langsung bahwa aturan Pareto berfungsi: 80% aktivitas dibuat oleh 20% pemain. Setidaknya awalnya. Dan di sini penting untuk menghindari manipulasi: Protokol menyediakan kemungkinan ini secara tepat, dan Oracle dan Indeks memperluas fungsionalitas ke sistem objektif lengkap dari aset yang dinilai sendiri.

Protokol adalah dasar untuk protokol urutan berikutnya: yaitu, sementara solusi blockchain apa pun adalah level L0/L1, sebuah protokol dapat terletak di bidang L1/L2 dan seterusnya. Dan inilah yang ditawarkan NIFTSY dalam nada ini:

* Pertama, tokenisasi saluran pembayaran: dalam hal ini, tidak masalah apakah kita melihat implementasi tertentu (Plasma, Lighting Network) atau agregasinya (Plasma + ZK-rollup, jembatan tingkat yang berbeda), apakah kita mengambil blockchain tunggal atau integrasi multi-rantai, tetapi yang penting adalah bahwa jalan keluar dari rantai utama itu dapat dan harus digunakan, menyediakan likuiditas untuk saluran itu sendiri (antar pihak) dan aset yang dibungkus melaluinya (sebelum menutup saluran). Dalam hal ini, mekanisme yang sama dari Protokol lintas rantai berlaku seperti saat Proyek menghubungkan ekonomi offline dengan proyek online.
* Kedua, Protokol tidak bekerja dengan sendirinya, tetapi bersama-sama dengan elemen lain berfungsi sebagai fitur penemuan harga lintas pasar terdesentralisasi dari solusi blockchain apa pun. Artinya, apakah Anda melakukan setoran fiat aman dan menukarnya dengan jumlah token dan/atau koin yang sama dengan urutan berbeda dalam ekonomi p2p, atau menukar aset setara yang dibungkus NFT di blockchain yang berbeda, mekanisme Protokol akan menjadi sama, dan dengan demikian dapat diverifikasi untuk setiap peserta transaksi.
* Ketiga, Protokol adalah normalisasi hubungan antara peserta yang berbeda di pasar DEX, DAO (DeFI): terlepas dari SaO (subjek-objek) peserta mana. Untuk alasan ini, Proyek dapat diintegrasikan tidak hanya dengan pasar p2p klasik, tetapi juga, misalnya, dengan solusi IoT, di mana aktor utamanya adalah perangkat yang dapat diprogram, skrip evaluasi perangkat keras, atau (semi) sistem AI otonom yang menyediakan layanan langsung interaksi antara elemen IoT yang berbeda.
* Keempat, Protokol sebenarnya menciptakan kemungkinan agregasi likuiditas melalui transfer lintas rantai kepemilikan NFT: b2bx, 1inch dan aggregator likuiditas serupa dapat dianggap sebagai analog terdekat, tetapi dengan perbedaan bahwa mereka mewakili generasi pertama dari cabang evolusioner ini. Bola DAO & DEX.

Namun, kemungkinan Protokol tidak berakhir di situ. Mari kita coba menggambarkannya secara singkat, tetapi secara rinci dari perspektif perkembangan umum.

Di satu sisi, tren menuju integrasi DeFi dan NFT jelas hari ini, karena token yang dapat dipertukarkan (ERC-20, TRC-20, BIP-20, dll.) dapat ditukar pada tingkat yang berbeda: pertukaran atom, jika kita berbicara tentang solusi blockchain (DCR-LTC dan lainnya); melalui protokol pintar seperti Bancor; langsung melalui solusi DEX & DAO, implementasi pertama dan paling sederhana adalah DeFi. Di sisi lain, berkat pembungkus NFT pertukaran antara solusi blockchain yang berbeda (selanjutnya juga disebut sebagai DDS: sistem terdesentralisasi dan/atau terdistribusi) dimungkinkan tanpa menggunakan jembatan atau bahkan implementasi yang lebih kompleks. Contoh aspek ini - Uniswap, YFI.Finance, AAVE - ada di atas.

Tetapi pada saat yang sama muncul aspek penting lainnya - masalah pasar NFT itu sendiri. Berikut adalah beberapa di antaranya:

* Pertama, pasar NFT awalnya dipahami terlalu sempit, bukan pada tingkat teoretis di mana ada format seperti ERC-721, ERC-998, ERC-1050 dan banyak lainnya yang terus berkembang, tetapi justru pada tingkat aplikasi, seperti NFT ceruk yang menjadi permintaan antara 2014 dan 2021 sangat kecil: industri game, seni digital, avatarisasi off-line. Tetapi bahkan ceruk ini mampu memberikan kontribusi kapitalisasi yang cukup solid ke pasar: baik dalam hal cek rata-rata per NFT dan parameter maksimum yang diizinkan serta total proyek.
* Kedua, NFT dalam banyak hal rentan terhadap serangan tidak pada tingkat protokol dan DDS secara umum, tetapi pada tingkat pengakuisisi utama - entitas: dimulai dengan fakta bahwa substitusi ID (pengidentifikasi) yang terlihat dari suatu entitas yang melekat pada NFT dimungkinkan dan bahkan jika itu juga ada online (NFT phishing), belum lagi integrasi off-line yang kompleks, hingga fakta bahwa cukup sulit bagi orang awam yang sederhana, baru memasuki industri, untuk menentukan harga non- token yang sepadan.
* Ketiga, NFT juga memiliki penyakit anak lainnya yang melekat pada setiap proyek inovasi dalam masa pertumbuhan:
* Kapasitas jaringan rendah;
* Kekurangan likuiditas di pasar;
* Yang lain.

Seperti yang dijelaskan oleh CTO NIFTSY, M. Sizykh, dengan benar dan akurat, "Saya pikir fitur umum dari protokol adalah:

1. Onchain. Semua peristiwa dari dunia luar adalah kasus penggunaan Protokol, atau protokol lapisan LAINNYA yang dibangun di atas inti onchain kami.
2. Segala sesuatu tentang NFT".

Artinya, segala sesuatu yang dilakukan di luar Protokol (pada tingkat di bawah, di atas dan/atau beberapa tingkat di atas) adalah protokol tingkat baru (L0, L2, L3), atau oracle yang entah bagaimana berinteraksi dengannya, atau semacam entitas ketiga.

Konon, ada dua jenis Oracle utama:

1. Oracle yang menghubungkan blockchain ke dunia luar: chain.link adalah contohnya.
2. Oracle yang menganalisis blockchain dan menghasilkan kumpulan data di dalamnya, dan data tersebut sudah digunakan oleh solusi blockchain lainnya, yang terdesentralisasi termasuk: chainalytics.com.

Dalam hal ini, kita berbicara tentang poin pertama dan kedua sekaligus, yaitu tipe ketiga dari Oracle - sintetis: di satu sisi - ia harus menganalisis semua data yang datang melalui Protokol, dan di sisi lain - untuk menghubungkan Protokol dengan dunia luar.

Itulah sebabnya studi pasar ini dan segmennya dilakukan pada November-Desember 2020 (studi #01 dan studi #02), dan kemudian - pada musim semi 2021 - arsitektur keseluruhan ENVELOP (NIFTSY) dikembangkan, dan kemudian MVP, dipresentasikan di Hackathon dari pertukaran crypto terbesar, Binance, di antara yang lain.

Karena alasan inilah, dalam menjawab pertanyaan, "masalah apa yang dipecahkan oleh Protokol?" - adalah tanggapan bersama tim bahwa masalah pertama dan utama yang diselesaikan adalah mengamankan NFT dengan menempatkan berbagai digital, dan di masa depan, aset BUKAN digital, token apa pun di dalam Kontainer/Agunan (Agunan), atau drive agunan. Ini bisa dibungkus bitcoin (wBTC dan lainnya), token ERC-20 dan/atau BIP-20, berbagai jenis mata uang kripto, dll. Protokol ini awalnya dibangun di atas blockchain Ethereum (termasuk melalui lapisan L2 - misalnya Polygon) dan BSC, tetapi di masa mendatang (lihat Roadmap) direncanakan untuk membuat implementasi pada Flow, WAX, Solana, Polkadot, Cosmos, Avalanche, dan DRS lainnya, karena kami sangat yakin bahwa lintas rantai adalah masa depan semua sistem terdesentralisasi dan terdistribusi. Hal yang sama berlaku untuk solusi lapisan kedua dan selanjutnya.

Mari kita rangkum kesimpulan tentang Protokol:

1. Hal ini memungkinkan penyatuan WUM;
2. Memiliki jaminan sederhana atau multi agunan (Multi-collateral);
3. Berisi bagian penyimpanan statis (tidak dapat diisi ulang) dan dinamis;
4. Untuk pengguna rata-rata - berfungsi sebagai evaluasi NFT tingkat nol dari pesanan apa pun (serta turunan apa pun);
5. Untuk pemain b2b - menyediakan mekanisme untuk menangani likuiditas yang dibungkus dengan NFT dari pesanan apa pun di satu sisi; di sisi lain - menyediakan mekanisme yang jelas untuk membuat NFT (merupakan b2b-pemasok NFT);
6. Untuk dana (pensiun, asuransi, investasi, lindung nilai, dll.) bertindak sebagai alat penilaian aset objektif di mana setiap klien dana menerima NFT tanpa bungkus pada suatu peristiwa/tanggal dan selalu tahu persis tingkat jaminan utama NFT itu.

Tetapi Protokol tidak dapat dan seharusnya tidak menyelesaikan semua masalah pasar NFT dan hubungannya dengan DeFi dan industri lainnya. Ini adalah bagaimana Oracle muncul.
