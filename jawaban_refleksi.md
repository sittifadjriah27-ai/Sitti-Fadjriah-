# Jawaban Refleksi — Latihan Blockchain

**Nama:**
**NIM:**
**Kelas:**

> Salin output `python cek_nilai.py` Anda di bawah ini:

```
==============================================================
Level Materi                           Lulus      Status
--------------------------------------------------------------
1     Fungsi hash SHA-256                7/7     SELESAI
2     Blockchain dasar (GfG)             8/8     SELESAI
3     Eksperimen tampering               9/9     SELESAI
4     Transaksi dalam blok             13/13     SELESAI
5     PoW dengan nonce                 10/10     SELESAI
6     Eksperimen difficulty            13/13     SELESAI
7     Tanda tangan digital             10/10     SELESAI
8     Jaringan & konsensus               7/7     SELESAI
9     Reward & saldo                   13/13     SELESAI
--------------------------------------------------------------
TOTAL                                  90/90        100%
==============================================================
```

---

## Level 1 — Fungsi Hash
1. Mengapa hash disebut sidik jari digital? Sebutkan tiga sifat fungsi hash kriptografis.
Hash disebut sidik jari digital karena setiap data memiliki nilai hash yang menjadi identitas unik dari data tersebut. Tiga sifat fungsi hash adalah deterministik (data yang sama menghasilkan hash yang sama), sulit dibalik ke data asli, dan memiliki efek avalanche (perubahan kecil pada data menghasilkan perubahan besar pada hash).
2.Berapa persen bit yang berubah ketika mengganti satu huruf? Coba 3 pasangan teks berbeda.
Ketika satu huruf diubah, jumlah bit hash yang berubah dapat berbeda-beda. Hal ini disebabkan oleh efek avalanche pada SHA-256. Perubahan kecil pada teks dapat menghasilkan perubahan besar pada nilai hash, bahkan mendekati 50% bit.
3.Apa yang terjadi jika hash_dict tidak memakai sort_keys=True?
Jika tidak menggunakan sort_keys=True, urutan key pada dictionary dapat memengaruhi hasil hash. Akibatnya, dua data dengan isi yang sama tetapi urutan key berbeda bisa menghasilkan hash yang berbeda. Hal ini dapat menyebabkan ketidaksesuaian data dalam blockchain.

## Level 2 — Blockchain Dasar
1.Apa fungsi previous_hash pada blok genesis, dan mengapa nilainya "0"?
previous_hash berfungsi sebagai penghubung antara satu blok dengan blok sebelumnya. Pada blok genesis, nilainya menggunakan "0" karena blok tersebut merupakan blok pertama sehingga belum memiliki blok sebelumnya.
2.Jalankan demo dengan difficulty 3, 4, dan 5. Catat nilai proof dan rasakan lamanya mining.
Semakin tinggi difficulty, semakin sulit proses mining karena program harus mencari nilai proof yang memenuhi persyaratan hash. Difficulty 3 lebih cepat dibandingkan difficulty 4 dan 5. Semakin tinggi difficulty, semakin banyak percobaan yang dibutuhkan dan waktu mining semakin lama.

| Difficulty | Proof blok #2 | Perkiraan waktu |
|---|---|---|
| 3 | | |
| 4 | | |
| 5 | | |

## Level 3 — Tampering
1.Saat mengubah data di blok posisi k, mengapa cari_tautan_putus melaporkan posisi k+1?
Karena ketika data pada blok ke-k diubah, nilai hash blok tersebut juga berubah. Akibatnya, previous_hash pada blok berikutnya tidak lagi sesuai sehingga kerusakan terdeteksi pada blok ke-k+1.
2.Mengapa perubahan pada blok terakhir tidak terdeteksi?
Karena blok terakhir tidak memiliki blok berikutnya yang menyimpan nilai previous_hash dari blok tersebut. Oleh sebab itu, perubahan pada blok terakhir tidak langsung terdeteksi melalui pemeriksaan tautan.
3.Setelah sambung_ulang, rantai palsu dianggap valid. Apa kelemahan desain PoW di artikel GfG?
Kelemahannya adalah proses Proof of Work pada desain tersebut tidak bergantung pada seluruh isi blok. Akibatnya, seseorang dapat mengubah data dan menyambungkan kembali rantai tanpa harus melakukan mining ulang dengan benar.

## Level 4 — Transaksi
1.Mengapa transaksi tidak langsung masuk ke blok, tetapi menunggu di pending_transactions?
Karena transaksi perlu dikumpulkan dan diperiksa terlebih dahulu sebelum dimasukkan ke dalam blok. Dengan adanya pending_transactions, transaksi yang belum diproses dapat disimpan sementara sampai proses mining dilakukan
2.Mengapa create_block harus memakai salinan list(self.pending_transactions)?
Agar transaksi yang dimasukkan ke blok menggunakan salinan data dan tidak mengubah daftar transaksi asli secara langsung. Jika tidak menggunakan salinan, dapat terjadi masalah ketika daftar transaksi berubah saat proses pembuatan blok berlangsung.

## Level 5 — PoW dengan Nonce
1.Bandingkan Level 3 dan Level 5: mengapa serangan "sambung ulang" gagal di sini?
Pada Level 3, data blok dapat dipalsukan dan rantai disambungkan kembali tanpa proses mining yang sebenarnya. Sedangkan pada Level 5, hash dibuat berdasarkan seluruh isi blok termasuk nonce. Jadi, ketika data diubah, hash juga berubah dan penyerang harus melakukan mining ulang agar rantai kembali valid.
2.Berapa percobaan hash yang dibutuhkan penyerang untuk memalsukan blok #1 dari 3 blok? Perkirakan biayanya jika rantai berisi 1.000 blok dan difficulty 6.
Berdasarkan hasil laporan saya, penyerang membutuhkan 358.202 percobaan hash untuk menambang ulang blok 1 sampai 3. Jika rantai berisi 1.000 blok dengan difficulty 6, proses penambangan ulang akan membutuhkan percobaan yang jauh lebih banyak sehingga memerlukan waktu dan sumber daya komputasi yang besar.

## Level 6 — Difficulty
1.Tampilkan tabel hasil eksperimen difficulty 1–5. Apakah hasilnya mendekati 16^d? Mengapa 16?
Hasil percobaan mining saya menunjukkan bahwa semakin tinggi difficulty, semakin banyak percobaan yang dibutuhkan. Nilai teori menggunakan rumus \(16^d\) karena setiap karakter hexadecimal memiliki 16 kemungkinan nilai, yaitu 0 sampai 9 dan A sampai F. Nilai tersebut merupakan perkiraan rata-rata, sehingga hasil percobaan sebenarnya bisa lebih kecil atau lebih besar.
2.Bitcoin menyesuaikan difficulty setiap 2.016 blok agar waktu blok sekitar 10 menit. Mengapa waktu blok perlu dijaga stabil?
Waktu blok perlu dijaga stabil agar proses penambangan dan penambahan blok tetap teratur. Jika waktu terlalu cepat, jumlah blok akan bertambah terlalu cepat. Sebaliknya, jika terlalu lambat, transaksi membutuhkan waktu lebih lama untuk mendapatkan konfirmasi.

## Level 7 — Tanda Tangan Digital
1.Apa perbedaan peran kunci privat, kunci publik, dan alamat?
Kunci privat digunakan untuk membuat tanda tangan digital dan harus dijaga kerahasiaannya. Kunci publik digunakan untuk memverifikasi tanda tangan, sedangkan alamat digunakan sebagai identitas pengguna untuk menerima transaksi.
2.Mengapa tanda tangan penipu valid tetapi transaksinya tidak sah?
Karena tanda tangan penipu memang valid menggunakan kunci miliknya sendiri, tetapi kunci tersebut tidak sesuai dengan alamat pengirim yang digunakan. Oleh karena itu, transaksi tetap dinyatakan tidak sah.
3.Apa yang terjadi jika kunci privat Anda hilang? Bagaimana jika dicuri?
Jika kunci privat hilang, saya dapat kehilangan akses untuk menggunakan dana pada alamat tersebut. Jika kunci privat dicuri, orang lain dapat menggunakannya untuk membuat transaksi dan mengambil dana tanpa izin.

## Level 8 — Jaringan & Konsensus
1.Gambarkan kondisi fork pada demo, lalu kondisi setelah resolve_conflicts.
Pada saat terjadi fork, jaringan memiliki beberapa cabang blockchain dengan panjang berbeda. Berdasarkan laporan saya, panjang rantai awal adalah 5, 3, 5, 4, dan 5. Setelah resolve_conflicts, seluruh node memiliki panjang rantai 5, tetapi belum sepakat karena masih terdapat rantai dengan panjang yang sama.
2.Apa yang terjadi pada transaksi fork-B setelah konsensus? Kaitkan dengan anjuran tunggu 6 konfirmasi di Bitcoin.
Transaksi yang berada pada cabang yang tidak dipilih sebagai rantai utama dapat menjadi tidak berlaku atau tidak tercatat dalam rantai utama. Karena itu, pengguna Bitcoin dianjurkan menunggu beberapa konfirmasi, misalnya 6 konfirmasi, agar transaksi lebih sulit terkena perubahan rantai atau reorganisasi.
3.Lampirkan output praktik server.
Praktik server dilakukan dengan menjalankan program pada tiga port berbeda untuk menguji komunikasi antar-node. Setiap node dapat saling berkomunikasi dan bertukar informasi blockchain untuk mencapai kesepakatan jaringan.

## Level 9 — Reward & Saldo
1.Dari mana koin pertama berasal jika semua orang memulai dengan saldo 0?
Koin pertama berasal dari proses mining melalui transaksi khusus yang disebut coinbase transaction. Transaksi ini memberikan hadiah kepada penambang yang berhasil membuat blok baru. Dengan demikian, saldo awal dapat terbentuk meskipun semua pengguna sebelumnya memiliki saldo 0
2.Mengapa validasi_ekonomi diperlukan walaupun chain_valid sudah ada?
Karena chain_valid hanya memeriksa keabsahan hubungan hash antarblok, sedangkan validasi_ekonomi memeriksa apakah transaksi dan saldo sesuai dengan aturan ekonomi. Contohnya, transaksi tidak boleh melebihi saldo yang dimiliki dan hadiah blok tidak boleh dicurangi. Berdasarkan laporan saya, validasi ekonomi berhasil dengan hasil True, tetapi berubah menjadi False ketika hadiah blok 1 dicurangi.
3.Bitcoin memakai model UTXO, bukan model saldo akun seperti di sini. Cari tahu satu perbedaannya.
Perbedaannya adalah model saldo akun mencatat jumlah saldo yang dimiliki setiap pengguna, sedangkan UTXO mencatat keluaran transaksi yang belum digunakan. Pada Bitcoin, transaksi menggunakan keluaran transaksi sebelumnya sebagai input untuk mengirim Bitcoin kepada orang lain. Jadi, saldo dihitung dari seluruh UTXO yang masih dimiliki pengguna.
