
# Project UTS Pengolahan Citra

## Langkah - Langkah Pengerjaan

1. Import Library

Terdapat 3 library yang dipakai pada pengerjaan project ini yang pertama yaitu :

- OpenCV (cv2) : Library yang berguna untuk pengolahan gambar dan video. Berfungsi sebagai membaca, menulis, dan memanipulasi gambar dan video, seperti deteksi objek, segmentasi, pengolahan citra, dan visualisasi.
- Matplotlib.pypllot yang disingkat dengan nama plt merupakan library untuk membuat visualisasi seperti membuat plot, grafik, histogram, dan visualisasi data lain.
- Numpy yang disingkat dengan nama np adalah library yang digunakan untuk fungsi matematika seperti operasi matematika pada gambar, memanipulasi warna, transformasi goemetris dan operasi matriks.

2. Membaca dan Menampilkan gambar

Agar dapat menampilkan gambar dapat menggunakan library OpenCV dan Matplotlib dengan fungsi cv2.imread yang digunakan untuk membaca gambar dari file yang sudah dibikin. Hasil pembacaan gambar disimpan dalam variabel 'img'. Fungsi plt.imshow(img) digunakan untuk menampilkan gambar dalam bentuk array. Argumen yang diberikan ke dalam fungsi ini adalah variabel 'img', yang merupakan gambar yang telah dibaca oleh library OpenCV. Fungsi ini akan memnampilkan gambar tersebut.

3. Mengubah skema warna BGR ke RGB 

Mengubah warna menggunakan fungsi cv2.cvtcolor(), argumen pertama ialah variabel 'img' meruapakan gambar yang telah dibaca dan argumen kedua (cv2.COLOR_BRG2BGR) konversi yang awalnya berada dalam format BGR kemudian diubah menjadi format RGB. Library matplotlib menggunakan skema warna RGB secara default untuk menampilkan gambar.

4. Pemurnian Warna

Sebelum memurnikan warna kita Mengambil baris dan kolom dari gambar, Mengambil jumlah baris dan kolom dari matriks gambar. Penjelasan rinci :

- img.shape, Properti shape pada objek gambar (dalam hal ini, variabel img) mengembalikan tuple yang berisi dimensi gambar. Tuple ini memiliki tiga elemen: jumlah baris, jumlah kolom, dan jumlah saluran warna (biasanya 3 untuk gambar berwarna).
- [:2]: Notasi slicing ini digunakan untuk membatasi tuple hanya hingga elemen kedua (indeks ke-0 dan ke-1), yang mewakili jumlah baris dan jumlah kolom. Ini dilakukan karena kita hanya tertarik pada dimensi spasial gambar, bukan pada jumlah saluran warna.
- [baris, kolom] = img.shape[:2]: Hasil dari operasi slicing tersebut ditugaskan ke dalam variabel baris dan kolom. Sekarang, variabel baris akan berisi jumlah baris dalam gambar, sedangkan variabel kolom akan berisi jumlah kolom dalam gambar.

Untuk memurnikan gambar mencari elemen warna (R/G/B) dengan intensitas tertinggi dan warna intensitas kedua tertinggi kemudian melakukan pembandingan keduanya dengan mencari selisih antar keduanya dan kemudian menghitung apakah mereka lebih besar dari 10 (kemungkinkan bukan putih) atau kurang dari 10 (kemungkinan putih), dan apabila warna piksel kemungkinan bukan putih (>10) maka warna-warna lain (selain warna dengan intensitas maksimum) akan menjadi 0 (sehingga piksel menjadi warna yang murni R/G/B).

5. Proses Mencerahkan gambar

Proses pencerahan gambar menggunakan nilai beta dengan langkah-langkah berikut :

- Inisialisasi Parameter: Nilai beta (69 dalam kasus ini) digunakan untuk menentukan seberapa jauh gambar akan dicerahkan.

- Inisialisasi Citra Terang: Citra terang (citra_cerah) diinisialisasi sebagai matriks nol dengan dimensi yang sama dengan gambar asli. Ini akan menjadi tempat menyimpan hasil pencerahan.

- Pencerahan Pixel: Setiap piksel dalam gambar asli (img) dicerahkan dengan menambahkan nilai beta ke nilai pikselnya. Hal ini dilakukan dengan iterasi melalui setiap piksel dalam gambar asli menggunakan dua loop for. Nilai piksel yang dicerahkan (gyx) ditambahkan ke citra terang (citra_cerah) pada posisi yang sesuai.

- Konversi Tipe Data: Setelah proses pencerahan selesai, tipe data citra terang diubah menjadi tipe data unsigned integer 8-bit (np.uint8). Hal ini diperlukan karena nilai piksel dalam gambar harus berada dalam rentang 0 hingga 255.

- Menampilkan Gambar dan Histogram(analisis histogram): Menggunakan Matplotlib, dua subplot dibuat. Subplot pertama menampilkan gambar asli dan histogramnya, sedangkan subplot kedua menampilkan citra terang (hasil pencerahan) dan histogramnya. Ini memberikan pembandingan visual antara gambar asli dan gambar yang telah dicerahkan. Gambar yang telah dicerahkan sesuai dengan menambahan beta yang dilakukan, misalkan beta 30 maka nilai piksel asli akan ditambahkan 30 dari nilai asli.

6. Deteksi warna (Soal 1)

Terdapat 3 warna yang dipudarkan yaitu merah, hijau dan biru : 

- Warna Merah 
    - Ekstraksi Saluran Warna Merah : Saluran warna merah (Red) dari citra terang (citra_cerah) diekstraksi menggunakan slicing [:,:,0]. Ini berarti kita mengambil semua baris dan kolom, tetapi hanya saluran warna merah (indeks 0).

    - Membuat Subplot : Dua subplot dibuat dengan menggunakan plt.subplots(1,2, figsize=(10,5)). Subplot pertama akan menampilkan citra saluran warna merah, sementara subplot kedua akan menampilkan histogram dari gambar asli.

    - Menampilkan Saluran Warna Merah : Subplot pertama menampilkan saluran warna merah dari citra terang menggunakan imshow() dengan menentukan cmap='gray' agar warnanya ditampilkan dalam skala abu-abu. Ini memungkinkan kita untuk melihat tingkat kecerahan piksel pada saluran warna merah.

    - Menampilkan Histogram(analisis histogram): Subplot kedua menampilkan histogram dari gambar asli dengan menggunakan hist(). Histogram ini memberikan distribusi frekuensi dari intensitas piksel dalam gambar pada saluran warna merah. Rentang intensitas piksel adalah 0 hingga 255.

- Warna hijau
    - Ekstraksi Saluran Warna Hijau: Saluran warna hijau (Green) dari citra terang (citra_cerah) diekstraksi menggunakan slicing [:,:,1]. Ini berarti kita mengambil semua baris dan kolom, tetapi hanya saluran warna hijau (indeks 1).

    - Membuat Subplot: Dua subplot dibuat dengan menggunakan plt.subplots(1,2, figsize=(10,5)). Subplot pertama akan menampilkan citra saluran warna hijau, sementara subplot kedua akan menampilkan histogram dari gambar asli (saluran warna merah).

    - Menampilkan Saluran Warna Hijau: Subplot pertama menampilkan saluran warna hijau dari citra terang menggunakan imshow() dengan menentukan cmap='gray' agar warnanya ditampilkan dalam skala abu-abu. Ini memungkinkan kita untuk melihat tingkat kecerahan piksel pada saluran warna hijau.

    - Menampilkan Histogram(analisis histogram): Subplot kedua menampilkan histogram dari gambar asli (saluran warna hijau) dengan menggunakan hist(). Histogram ini memberikan distribusi frekuensi dari intensitas piksel dalam gambar pada saluran warna hijau. Rentang intensitas piksel adalah 0 hingga 255.

- Warna biru
    - Ekstraksi Saluran Warna Biru: Saluran warna biru (Blue) dari citra terang (citra_cerah) diekstraksi menggunakan slicing [:,:,2]. Ini berarti kita mengambil semua baris dan kolom, tetapi hanya saluran warna biru (indeks 2).

    - Membuat Subplot: Dua subplot dibuat dengan menggunakan plt.subplots(1,2, figsize=(10,5)). Subplot pertama akan menampilkan citra saluran warna biru, sementara subplot kedua akan menampilkan histogram dari gambar asli (saluran warna merah).

    - Menampilkan Saluran Warna Biru: Subplot pertama menampilkan saluran warna biru dari citra terang menggunakan imshow() dengan menentukan cmap='gray' agar warnanya ditampilkan dalam skala abu-abu. Ini memungkinkan kita untuk melihat tingkat kecerahan piksel pada saluran warna biru.

    - Menampilkan Histogram(analisis histogram): Subplot kedua menampilkan histogram dari gambar asli (saluran warna biru) dengan menggunakan hist(). Histogram ini memberikan distribusi frekuensi dari intensitas piksel dalam gambar pada saluran warna biru. Rentang intensitas piksel adalah 0 hingga 255.

7. Ambang Batas (Soal 2)

Operasi pada gambar untuk menghasilkan citra biner menggunakan berbagai ambang batas (thresholds). Berikut penjelasannya : 

- Konversi ke Grayscale: Pertama, gambar asli dikonversi menjadi citra grayscale menggunakan fungsi cv2.cvtColor() dengan konversi dari RGB ke grayscale  (cv2.COLOR_RGB2GRAY). Ini dilakukan agar operasi thresholding dapat diterapkan pada citra grayscale, yang hanya memiliki satu saluran warna.

- Membuat Subplot: Dua subplot 2x2 dibuat dengan plt.subplots(2, 2, figsize=(10, 7)). Subplot ini akan menampung hasil citra biner dari beberapa operasi thresholding.

- Thresholding dengan Berbagai Ambang Batas:

    - cv2.threshold() digunakan untuk menghasilkan citra biner dari citra grayscale dengan menggunakan ambang batas tertentu.
    - Empat ambang batas yang berbeda digunakan untuk menghasilkan citra biner, masing-masing disebut binary1, binary2, binary3, dan binary4.
    - Ambang batas ini dipilih secara subjektif dan dapat disesuaikan sesuai kebutuhan aplikasi. Citra biner dihasilkan dengan cara mengubah piksel ke putih (255) jika nilainya melewati ambang batas, dan menjadi hitam (0) jika tidak.
- Menampilkan Citra Biner dan Memberi Judul: Setiap citra biner ditampilkan pada subplot yang sesuai dengan menggunakan imshow() dengan colormap 'binary' untuk menunjukkan citra biner secara visual. Judul dari setiap subplot diset untuk membedakan antara operasi thresholding yang berbeda.

- Teori Pendukung Ambang Batas

Ambang batas (threshold) adalah salah satu teknik yang umum digunakan dalam pemrosesan citra untuk mengubah citra grayscale menjadi citra biner. Tujuan dari ambang batas adalah untuk membagi piksel dalam citra menjadi dua kelompok berdasarkan intensitasnya: satu kelompok yang dianggap sebagai objek (foreground) dan yang lainnya sebagai latar belakang (background).

Langkah-langkah dalam Ambang Batas:

    - Pemilihan Ambang Batas: Langkah pertama dalam proses thresholding adalah pemilihan ambang batas yang sesuai. Ambang batas ini bisa tetap (fixed) atau dapat dihitung secara adaptif berdasarkan karakteristik lokal di sekitar setiap piksel.

    - Segmentasi: Setelah ambang batas dipilih, setiap piksel dalam citra grayscale dianalisis. Jika intensitas piksel melebihi ambang batas, piksel tersebut dianggap sebagai bagian dari objek (foreground), dan jika tidak, itu dianggap sebagai bagian dari latar belakang (background).

    - Penggunaan Hasil Thresholding: Citra biner yang dihasilkan dari proses thresholding dapat digunakan untuk berbagai tujuan, seperti segmentasi objek, ekstraksi fitur, deteksi tepi, pengenalan pola, dll.



