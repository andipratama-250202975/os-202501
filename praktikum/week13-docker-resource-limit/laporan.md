
# Laporan Praktikum Minggu 13
Topik: Docker – Resource Limit (CPU & Memori)

---

## Identitas
- **Nama**  : Andi Pratama  
- **NIM**   : 250202975  
- **Kelas** : IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, siswa mampu:

Menulis Dockerfile sederhana untuk sebuah aplikasi/skrip.
Membangun image dan menjalankan container.
Jangkauan wadah dengan kekuatan CPU dan memori .
Mengamati dan menjelaskan perbedaan eksekusi kontainer dengan dan tanpa batas sumber daya.
Menyusun laporan praktikum secara runtut dan sistematis.

---

## Dasar Teori

Docker adalah platform untuk menjalankan aplikasi di dalam container yang bersifat ringan dan terlindungi dari sistem utama. Container memungkinkan aplikasi berjalan secara konsisten karena sudah dilengkapi dengan ketergantungan yang dibutuhkan. Docker menyediakan fitur menyediakan sumber daya seperti CPU dan memori menggunakan parameter tertentu saat menjalankan container. Pembatasan CPU berpengaruh pada kecepatan eksekusi program, sedangkan memori menentukan jumlah maksimum RAM yang dapat digunakan. Jika penggunaan memori melebihi batas yang ditentukan, container akan dihentikan secara otomatis oleh sistem. Pemantauan penggunaan resource dapat dilakukan menggunakan perintah docker statsuntuk melihat kinerja container secara real-time.

---

## Langkah Praktikum

   - Pastikan Docker terpasang dan berjalan.
   - Verifikasi:
     ```bash
     docker version
     docker ps
     ```

2. **Membuat Aplikasi/Skrip Uji**

   Buat program sederhana di folder `code/` (bahasa bebas) yang:
   - Melakukan komputasi berulang (untuk mengamati limit CPU), dan/atau
   - Mengalokasikan memori bertahap (untuk mengamati limit memori).

3. **Membuat Dockerfile**

   - Tulis `Dockerfile` untuk menjalankan program uji.
   - Build image:
     ```bash
     docker build -t week13-resource-limit .
     ```

4. **Menjalankan Container Tanpa Limit**

   - Jalankan container normal:
     ```bash
     docker run --rm week13-resource-limit
     ```
   - Catat output/hasil pengamatan.

5. **Menjalankan Container Dengan Limit Resource**

   Jalankan container dengan batasan resource (contoh):
   ```bash
   docker run --rm --cpus="0.5" --memory="256m" week13-resource-limit
   ```
   Catat perubahan perilaku program (mis. lebih lambat, error saat memori tidak cukup, dll.).

6. **Monitoring Sederhana**

   - Jalankan container (tanpa `--rm` jika perlu) dan amati penggunaan resource:
     ```bash
     docker stats
     ```
   - Ambil screenshot output eksekusi dan/atau `docker stats`.

7. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 13 - Docker Resource Limit"
   git push origin main
   ```

---
2. Perintah yang dijalankan. 


---

## Kode / Perintah
```bash

import time
import sys

data = []
print("Program dimulai...")
sys.stdout.flush()

try:
    i = 0
    while True:
        for _ in range(5_000_000):
            pass

        data.append("X" * 5_000_000)  # ±5 MB
        i += 1
        print(f"Iterasi ke-{i}, alokasi memori bertambah")
        sys.stdout.flush()
        time.sleep(1)

except MemoryError:
    print("MemoryError: Memori tidak cukup!")
```


---

## Srenshott hasil

<img width="1920" height="1200" alt="Screenshot (39)" src="https://github.com/user-attachments/assets/b4e1ed66-5625-4c7c-8c8c-bed62ce8117a" />

## Analisis

1. **Analisis Pembatasan Memori (Memory Limit)**
   * Pada **Eksekusi Tanpa Limit**, kolom `LIMIT` menunjukkan angka **4.744GiB**, yang merupakan total RAM yang tersedia di laptop/host. Ini berarti container bebas menggunakan memori sebanyak mungkin hingga host kehabisan RAM.
   * Pada **Eksekusi Dengan Limit**, kolom `LIMIT` berubah menjadi **256MiB**. Ini membuktikan flag `--memory="256m"` berhasil memerintahkan *cgroups* untuk membatasi alokasi.
   * Aplikasi mengalokasikan data sebesar **150MB**. Karena 150MB < 256MB, program tetap berjalan lancar. Namun, jika limit diubah di bawah 150MB (misalnya 100MB), container akan mengalami *OOM Kill (Out of Memory)* dan dimatikan paksa oleh kernel.


2. **Analisis Pembatasan CPU (CPU Limit)**
   * Pada percobaan tanpa limit (**Gambar 2**), durasi komputasi adalah **0.1774 detik**.
   * Pada percobaan dengan limit `--cpus="0.5"` (**Gambar 4**), durasi meningkat menjadi **0.1850 detik**.
   * **Penjelasan:** Limit `0.5` berarti container hanya boleh menggunakan 50% dari siklus 1 core CPU setiap periodenya. Meskipun perbedaannya terlihat kecil (karena beban komputasi 50.000 prima masih tergolong ringan untuk prosesor modern), adanya kenaikan waktu eksekusi menunjukkan bahwa *throttling* CPU sedang terjadi. Jika beban komputasi diperberat (misal: 1 juta bilangan prima), perbedaan waktu akan menjadi jauh lebih signifikan (bisa 2x lebih lambat).

---

## Kesimpulan
1. **Docker Resource Limit** bekerja dengan memanfaatkan fitur kernel Linux (*cgroups*) untuk membatasi akses container terhadap CPU dan Memori host.
2. Perintah `docker stats` sangat krusial untuk memantau apakah limitasi yang kita set (seperti `--memory="256m"`) benar-benar diterapkan pada container yang berjalan.
3. Pembatasan resource sangat penting dalam lingkungan produksi untuk mencegah satu container yang "rakus" (misalnya karena *memory leak* atau *infinite loop*) menghabiskan sumber daya server yang dapat menyebabkan layanan lain terganggu (*Noisy Neighbor effect*).

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
