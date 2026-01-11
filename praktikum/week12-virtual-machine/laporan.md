
# Laporan Praktikum Minggu 12
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Andi pratama  
- **NIM**   : 250202975  
- **Kelas** : 1 IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menginstal perangkat lunak virtualisasi (VirtualBox/VMware).  
2. Membuat dan menjalankan sistem operasi guest di dalam VM.  
3. Mengatur konfigurasi resource VM (CPU, RAM, storage).  
4. Menjelaskan mekanisme proteksi OS melalui virtualisasi.  
5. Menyusun laporan praktikum instalasi dan konfigurasi VM secara sistematis.

---

## Dasar Teori
1.  **Virtualisasi (Virtualization)**
   
    Virtualisasi adalah teknologi yang memungkinkan satu komputer fisik (Host) untuk menjalankan beberapa sistem operasi (Guest) secara bersamaan dengan membagi sumber daya *hardware* secara efisien. Ini menciptakan lapisan abstraksi antara *hardware* fisik dan sistem operasi.

2.  **VirtualBox**
   
    VirtualBox adalah perangkat lunak virtualisasi yang memungkinkan pengguna menciptakan mesin virtual untuk menjalankan satu atau lebih sistem operasi tambahan secara bersamaan di dalam satu komputer fisik. Fungsi utamanya adalah menyediakan lingkungan terisolasi untuk menguji perangkat lunak, mempelajari instalasi sistem operasi yang berbeda (seperti Linux di dalam Windows), serta memfasilitasi pengembangan aplikasi lintas platform tanpa risiko merusak sistem operasi utama.

3.  **Host OS vs Guest OS**
    * **Host OS:** Sistem operasi fisik yang menjalankan komputer (Windows 11).
    * **Guest OS:** Sistem operasi virtual yang berjalan di dalam *container* virtual (Ubuntu Linux).

4.  **Isolasi Resource & Sandboxing**
   
    Virtualisasi menyediakan mekanisme keamanan di mana kerusakan pada Guest OS (misalnya terkena virus atau *crash*) tidak akan memengaruhi Host OS. Setiap VM berjalan dalam lingkungan terisolasi (*sandbox*) yang memiliki jatah CPU dan RAM sendiri.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  
2. [Pertanyaan 2]  
   **Jawaban:**  
3. [Pertanyaan 3]  
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
