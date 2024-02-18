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

Dengan demikian, serangkaian kode ini menggambarkan proses umum dalam pengolahan lembar jawaban objektif, yang meliputi pra-pemrosesan gambar, deteksi objek, identifikasi jawaban, dan perhitungan sko


Dalam script yang diberikan untuk melakukan analisis lembar jawaban objektif, digunakan beberapa fungsi yang disediakan oleh pustaka OpenCV (cv2), pustaka imutils, dan pustaka NumPy. Berikut adalah fungsi-fungsi yang digunakan dalam script tersebut:

1. **OpenCV (cv2)**:
    - `cv2.imread()`: Membaca gambar dari file.
    - `cv2.cvtColor()`: Mengubah ruang warna gambar.
    - `cv2.GaussianBlur()`: Melakukan operasi pemulusan gambar dengan filter Gaussian.
    - `cv2.Canny()`: Mendeteksi tepi dalam gambar.
    - `cv2.findContours()`: Mencari kontur dalam gambar.
    - `cv2.threshold()`: Melakukan thresholding pada gambar.
    - `cv2.drawContours()`: Menggambar kontur pada gambar.
    - `cv2.putText()`: Menambahkan teks ke gambar.
    - `cv2.imshow()`: Menampilkan gambar di jendela.
    - `cv2.waitKey()`: Menunggu penekanan tombol pada jendela.
    - `cv2.destroyAllWindows()`: Menutup semua jendela yang ditampilkan.

2. **imutils**:
    - `imutils.perspective.four_point_transform()`: Melakukan transformasi perspektif empat titik.
    - `imutils.contours.sort_contours()`: Mengurutkan kontur berdasarkan ukuran atau lokasi.

3. **NumPy**:
    - `np.arange()`: Membuat array berurutan.
    - `np.zeros()`: Membuat array nol.
    - `np.asarray()`: Mengubah daftar menjadi array NumPy.
    - `np.count_nonzero()`: Menghitung jumlah elemen yang bukan nol dalam array.

Dengan menggunakan fungsi-fungsi ini, script dapat membaca, memproses, dan menganalisis gambar lembar jawaban secara efektif. Setiap fungsi memiliki peran khusus dalam proses analisis, seperti pembacaan gambar, transformasi perspektif, deteksi tepi, dan identifikasi jawaban yang benar.
