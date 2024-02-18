# pengolahan lembar jawaban objektif (OMR).

1. **Baca Kunci Jawaban dari File CSV**
   
    Pada awalnya, kode ini membaca kunci jawaban dari sebuah file CSV. Dalam OMR, kunci jawaban seringkali tersimpan dalam format yang dapat dibaca oleh komputer, seperti CSV. Dengan menggunakan Pandas, kunci jawaban dimuat ke dalam sebuah struktur data yang bisa diakses selanjutnya.

2. **Proses Pengolahan Gambar**

    Setelah kunci jawaban dibaca, gambar yang berisi lembar jawaban diimpor dan diproses. Langkah-langkahnya meliputi:
   
    - Konversi ke citra abu-abu (grayscale)
    - Pemulusan (blurring) dengan filter Gaussian untuk mengurangi noise
    - Deteksi tepi menggunakan metode Canny untuk menemukan tepi objek dengan lebih baik
   
    Hal ini membantu mempersiapkan gambar untuk proses berikutnya, yaitu identifikasi kontur-kontur objek dalam gambar.

3. **Temukan Kontur Dokumen**

    Kode ini bertujuan untuk menemukan kontur yang mewakili dokumen (lembar jawaban) dalam gambar yang telah diproses. Kontur yang ditemukan akan digunakan sebagai panduan untuk mengekstrak dan menganalisis jawaban dari lembar jawaban.

4. **Transformasi Perspektif Empat Titik**

    Langkah ini mentransformasi perspektif empat titik pada gambar. Ini diperlukan untuk memastikan bahwa lembar jawaban yang dipindai memiliki orientasi yang tepat dan tidak terdistorsi. Dengan cara ini, jawaban di lembar jawaban dapat dianalisis secara konsisten.

5. **Thresholding Otsu**

    Proses thresholding Otsu digunakan untuk menghasilkan gambar biner dari gambar yang telah diproses sebelumnya. Ini membantu dalam memisahkan jawaban yang diisi oleh siswa dari latar belakang atau noise pada lembar jawaban.

6. **Proses Pengenalan Jawaban**

    Pada tahap ini, setiap kotak jawaban pada lembar jawaban diidentifikasi dan dievaluasi. Ini dilakukan dengan menghitung jumlah piksel putih di dalam setiap kotak jawaban. Jawaban yang benar kemudian dibandingkan dengan kunci jawaban yang telah dimuat sebelumnya.

7. **Hitung Skor**

    Setelah semua jawaban diidentifikasi, skor akhir dihitung. Skor dihitung berdasarkan jumlah jawaban yang benar dan jumlah total pertanyaan yang ada dalam lembar jawaban. Skor ini kemudian dicetak pada gambar sebagai umpan balik visual bagi pengguna.

Dengan demikian, serangkaian kode ini menggambarkan proses umum dalam pengolahan lembar jawaban objektif, yang meliputi pra-pemrosesan gambar, deteksi objek, identifikasi jawaban, dan perhitungan skor.
