
# Laporan Praktikum Minggu 13
Topik: Docker – Resource Limit (CPU & Memori)
---

## Identitas
- **Nama**  : Andi Pratama  
- **NIM**   : 250202975  
- **Kelas** : IKRA

---

## Tujuan

---

## Dasar Teori

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.
    
1.) **Persiapan Lingkungan**

   - Pastikan Docker terpasang dan berjalan.
   - Verifikasi:
     ```bash
     docker version
     docker ps
     ```

2.) **Membuat Aplikasi/Skrip Uji**

   Program sederhana di folder `code/` (bahasa Python) yang:
   - Melakukan komputasi berulang (untuk mengamati limit CPU), dan/atau
   - Mengalokasikan memori bertahap (untuk mengamati limit memori).

3.) **Membuat Dockerfile**

   - Tulis `Dockerfile` untuk menjalankan program uji.
   - Build image:
     ```bash
     docker build -t week13-resource-limit .
     ```

4.) **Menjalankan Container Tanpa Limit**

   - Jalankan container normal:
     ```bash
     docker run --rm week13-resource-limit
     ```
   - Catat output/hasil pengamatan.

5.) **Menjalankan Container Dengan Limit Resource**

   Jalankan container dengan batasan resource (contoh):
   ```bash
   docker run --rm --cpus="0.5" --memory="256m" week13-resource-limit
   ```
   Catat perubahan perilaku program (mis. lebih lambat, error saat memori tidak cukup, dll.).

6.) **Monitoring Sederhana**

   - Jalankan container (tanpa `--rm` jika perlu) dan amati penggunaan resource:
     ```bash
     docker stats
     ```
   - Ambil screenshot output eksekusi dan/atau `docker stats`. 

7.)  Melakukan commit ketika sudah selesai.

2. Perintah yang dijalankan. 


---

## Kode / Perintah
Potongan kode atau perintah utama:


---

## Quiz
1. Mengapa container perlu dibatasi CPU dan memori?

Container perlu dibatasi CPU dan memori agar satu container tidak menggunakan sumber daya secara berlebihan dan mengganggu container lain maupun sistem host. Pembatasan ini membantu menjaga stabilitas sistem, memastikan pembagian resource yang adil, serta mencegah terjadinya overload yang dapat menyebabkan penurunan performa atau crash.

2. Apa perbedaan VM dan container dalam konteks isolasi sumber daya?

Virtual Machine (VM) menyediakan isolasi yang kuat karena setiap VM memiliki sistem operasi sendiri dan sumber daya yang dialokasikan secara terpisah oleh hypervisor. Sebaliknya, container berbagi kernel sistem operasi host, sehingga isolasinya lebih ringan dan efisien, tetapi tidak sekuat VM dalam hal pemisahan lingkungan sistem.

3. Apa dampak limit memori terhadap aplikasi yang boros memori?

Pembatasan memori pada aplikasi yang boros memori dapat menyebabkan penurunan kinerja, aplikasi menjadi lambat, atau berhenti berjalan jika batas memori terlampaui. Dalam beberapa kasus, sistem akan menghentikan proses (out-of-memory kill) untuk menjaga kestabilan sistem secara keseluruhan.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
