
# Laporan Praktikum Minggu 14
Topik: Deteksi Kebuntuan

---

## Identitas
- **Nama**  : Andi pratama  
- **NIM**   : 250202975  
- **Kelas** : IKRA

---

# 1. Pendahuluan (Introduction)

## 1.1 Latar Belakang

Perkembangan sistem komputer modern menuntut kemampuan pengelolaan sumber daya yang semakin kompleks, khususnya pada sistem operasi yang mendukung eksekusi banyak proses secara bersamaan. Dalam lingkungan multiprogramming dan multitasking, berbagai proses harus berbagi sumber daya terbatas seperti memori, perangkat input/output, dan prosesor. Kondisi ini, jika tidak dikelola dengan baik, dapat menimbulkan permasalahan serius yang dikenal sebagai kebuntuan (deadlock).

Deadlock merupakan keadaan ketika dua atau lebih proses saling menunggu pelepasan sumber daya yang sedang dipegang oleh proses lain, sehingga tidak ada satu pun proses yang dapat melanjutkan eksekusinya. Kondisi kebuntuan ini menyebabkan sistem menjadi tidak responsif, menurunkan kinerja, serta berpotensi mengakibatkan kegagalan layanan. Oleh karena itu, deadlock menjadi salah satu permasalahan penting yang harus diperhatikan dalam perancangan dan pengelolaan sistem operasi.

---
## 1.2 Rumusan Masalah

Berdasarkan latar belakang tersebut, rumusan masalah dalam praktikum ini adalah:
1. Apa yang dimaksud dengan kebuntuan (deadlock) dalam sistem operasi dan bagaimana kondisi tersebut dapat terjadi dalam pengelolaan sumber daya?
2. Bagaimana mekanisme dan algoritma deteksi kebuntuan diterapkan dalam sistem operasi untuk mengidentifikasi proses-proses yang mengalami kebuntuan?
3. Apa dampak terjadinya kebuntuan terhadap kinerja dan stabilitas sistem serta bagaimana langkah pemulihan yang dapat dilakukan setelah kebuntuan terdeteksi?

---

## 1.3 Tujuan

Tujuan dari pelaksanaan praktikum ini adalah:
1. Mengimplementasikan algoritma page replacement FIFO dan LRU.
2. Melakukan simulasi penggantian halaman menggunakan reference string tertentu.
3. Membandingkan kinerja algoritma FIFO dan LRU berdasarkan jumlah *page fault*.
4. Menganalisis kelebihan dan kekurangan masing-masing algoritma.

---

# 2. Metode (Methods)

## 2.1 Lingkungan Pengujian

Pengujian dilakukan dengan lingkungan sebagai berikut:
- Sistem Operasi: Windows  
- Metode Pengujian: Model simulasi menggambarkan proses sebagai individu (orang) dan sumber daya sebagai alat kerja yang digunakan bersama.
- Bahasa Pemograman: python

Lingkungan pengujian dibuat seragam untuk memastikan hasil yang diperoleh bersifat objektif dan dapat dibandingkan.

---
## 2.2 Skenario Pengujian

Skenario 1: Kondisi Deadlock
Pada skenario ini, sistem disusun dalam kondisi saling menunggu antarproses.
Orang A memegang sumber daya Pulpen dan meminta Buku.
Orang B memegang sumber daya Buku dan meminta Pulpen.
Tidak ada sumber daya yang bebas untuk dialokasikan.
Hasil yang diharapkan:
Sistem berada dalam kondisi deadlock karena terbentuknya siklus ketergantungan antara proses dan sumber daya.

Skenario 2: Kondisi Tidak Terjadi Deadlock
Pada skenario ini, salah satu proses tidak memegang sumber daya saat mengajukan permintaan.
Orang A memegang Pulpen dan meminta Buku.
Buku dalam keadaan bebas (tidak dipegang oleh proses lain).
Orang B tidak memegang sumber daya apa pun.
Hasil yang diharapkan:
Tidak terjadi kebuntuan karena permintaan sumber daya dapat terpenuhi dan proses dapat melanjutkan eksekusi.

Skenario 3: Pencegahan Deadlock melalui Pelepasan Sumber Daya
Pada skenario ini, salah satu proses melepaskan sumber daya yang dipegang.
Orang A melepaskan Pulpen sebelum meminta Buku.
Orang B memegang Buku dan tidak meminta sumber daya lain.
Sumber daya Pulpen menjadi tersedia.
Hasil yang diharapkan:
Deadlock dapat dihindari karena tidak terjadi kondisi saling menunggu antarproses.

---
## 2.3 Variabel Pengukuran

Variabel yang digunakan dalam praktikum ini meliputi:
- **Variabel bebas:** pola alokasi dan permintaan sumber daya oleh proses .
- **Variabel terikat:** kondisi sistem.
- **Variabel kontrol:** Jumlah proses yang digunakan dalam simulasi,Jumlah dan jenis sumber daya yang tersedia,Aturannya adalah sumber daya tidak dapat dibagikan secara bersamaan

Variabel ini dijaga tetap konstan agar hasil pengamatan hanya dipengaruhi oleh variabel bebas.

---

## 2.3 Langkah Eksperimen
Langkah eksperimen dilakukan secara berurutan sebagai berikut:
1.Mendefinisikan sejumlah proses yang merepresentasikan individu dalam kehidupan sehari-hari.
2.Menentukan sumber daya terbatas yang digunakan bersama oleh proses-proses tersebut.
3.Pengaturan kondisi awal di mana setiap proses memegang satu sumber daya dan meminta sumber daya lain.
4.Batasan simulasi untuk memeriksa apakah permintaan sumber daya dapat terpenuhi.
5.Mengidentifikasi kondisi saling menunggu antarproses yang menyebabkan tidak ada proses dapat melanjutkan aktivitasnya.
6.Menyimpulkan terjadinya deadlock apabila seluruh proses berada dalam keadaan menunggu tanpa adanya pelepasan sumber daya.

---

## 2.  Parameter/datatest

| Parameter          | Deskripsi                                   |
| ------------------ | ------------------------------------------- |
| Jumlah proses      | 2 proses (Orang A dan Orang B)              |
| Jumlah sumber daya | 2 sumber daya (Pulpen dan Buku)             |
| Status alokasi     | Setiap proses memegang satu sumber daya     |
| Status permintaan  | Setiap proses meminta satu sumber daya lain |
| Model hubungan     | One-to-one (satu proses – satu sumber daya) |


# 3. Hasil (Results)

## 3.1  Hasil Eksekusi Program

Hasil (Results)
1. Tabel Hasil Pengujian

Berdasarkan skenario pengujian yang telah dilakukan, diperoleh hasil sebagai berikut:

| No | Skenario Pengujian                  | Kondisi Sistem                         | Deadlock Terdeteksi | Keterangan                        |
| -- | ----------------------------------- | -------------------------------------- | ------------------- | --------------------------------- |
| 1  | Skenario Deadlock (saling menunggu) | Semua proses menunggu sumber daya lain | Ya                  | Terbentuk siklus ketergantungan   |
| 2  | Skenario Tidak Deadlock             | Terdapat sumber daya bebas             | Tidak               | Proses dapat melanjutkan eksekusi |
| 3  | Skenario Pelepasan Sumber Daya      | Salah satu proses melepas sumber daya  | Tidak               | Kebuntuan berhasil dihindari      |


Hasil pengujian menunjukkan bahwa deadlock terjadi ketika seluruh proses memegang satu sumber daya dan secara bersamaan meminta sumber daya lain yang tidak tersedia. Pada kondisi ini, tidak ada proses yang dapat melanjutkan eksekusi, sehingga sistem berada dalam keadaan kebuntuan.

Sebaliknya, pada skenario di mana terdapat sumber daya yang masih bebas atau salah satu proses bersedia melepaskan sumber daya yang sedang dipegang, deadlock tidak terjadi. Hal ini membuktikan bahwa keberadaan sumber daya bebas atau mekanisme pelepasan sumber daya sangat berpengaruh dalam mencegah kebuntuan.

---

3. Ringkasan Temua

Berdasarkan hasil praktikum, dapat dirangkum beberapa temuan utama sebagai berikut:
a. Dealock terjadi akibat adanya kondisi saling menunggu antarproses menuju sumber daya yang terbatas.
b. Siklus ketergantungan merupakan indikator utama dalam pendeteksian kebuntuan.
c. Deadlock dapat dihindari jika sistem memiliki sumber daya bebas atau menerapkan kebijakan pelepasan sumber daya oleh proses tertentu.

---

## 3.2 Tabel Perbandingan Hasil



# 4. Pembahasan (Discussion)


---
## 4.1 Analisis

Hasil simulasi menunjukkan bahwa algoritma FIFO menghasilkan **10 page fault**, sedangkan algoritma LRU menghasilkan **9 page fault**. Perbedaan ini terjadi karena algoritma FIFO hanya mempertimbangkan urutan waktu masuk halaman ke memori tanpa memperhatikan frekuensi atau pola penggunaannya.

Sebaliknya, algoritma LRU mengganti halaman yang paling lama tidak digunakan, sehingga lebih sesuai dengan prinsip *locality of reference*. Pendekatan ini memungkinkan sistem mempertahankan halaman yang masih sering diakses, sehingga mampu mengurangi jumlah *page fault* dan meningkatkan efisiensi penggunaan memori.

---

## 4.2  Kelebihan dan Kekurangan



---


# 5. Closing (Penutupan)

## 5.1 Kesimpulan


---

## 5.2 Saran


---


## 5.3 Quiz

1. **Mengapa format IMRAD membantu membuat laporan praktikum lebih ilmiah dan mudah dievaluasi?**  
  

2. **Apa perbedaan antara bagian Hasil dan Pembahasan?**  
   

3. **Mengapa sitasi dan daftar pustaka penting, bahkan untuk laporan praktikum?**  
  
---

## Daftar Pustaka



---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
