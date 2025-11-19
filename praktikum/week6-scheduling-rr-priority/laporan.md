
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : [Nama Mahasiswa]  
- **NIM**   : [NIM Mahasiswa]  
- **Kelas** : [Kelas]

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---


## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

**Eksperimen 1 – Round Robin (RR)**
- *Time quantum (q)* = 3.  
- Berikut tabel perhitungan *Waiting Time* dan *Turnaround Time*:

| Proses | Arrival | Burst Time | Finish Time (P1) | Finish Time (P2) | Finish Time (P3) | TAT (FT-Arrival) | WT (TAT-Burst) |
   | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
   | P1 | 0 | 5 | 3 (sisa 2) | 14 (selesai) | - | 14 - 0 = 14 | 14 - 5 = 9  |
   | P2 | 1 | 3 | 6 (selesai) | - | - | 6 - 1 = 5 | 5 - 3 = 2 |
   | P3 | 2 | 8 | 9 (sisa 5) | 17 (sisa 2) | 22 | 22 - 2 = 20 | 20 - 8 = 12 |
   | P4 | 3 | 6 | 12 (sisa 3) | 20 (selesai) | - | 20 - 3 = 17 | 17 - 6 = 11 |
   | Total | | | | | | 56 | 34 |
   | Average | | | | | | 14 | 8,5 |
   
- Simulasi Gantt Chart untuk Round Robin (RR):
 
 ```
     | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
     0    3    6    9   12   14   17   20   22
```

**Eksperimen 2 – Priority Scheduling (Non-Preemptive)**

- Urutan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi): P1 > P2 > P4 > P3

*(P1 dijalankan lebih dulu karena sistem non-preemptive dan datang di waktu 0/saat CPU kosong, meskipun P2 memiliki Priority lebih tinggi)*   
- Lakukan perhitungan manual untuk:
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     ```
- Berikut tabel perhitungannya:

| Proses | Priority | Start | Arrival (A) | Burst (B) |  WT = Start − A |    TAT = WT + B |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|     P1 | 2 |     0 |           0 |         5 |               0 |   0 + 5 = 5 |
|     P2 | 1 |     5 |           1 |         3 |   5 − 1 = 4 |   4 + 3 = 7 |
|     P4 | 3 |     8 |           3 |         6 |   8 − 3 = 5 |  5 + 6 = 11 |
|     P3 | 4 |    14 |           2 |         8 | 14 − 2 = 12 | 12 + 8 = 20 |
| Total | | | | | 21 | 43 |
| Average | | | | | 5,25 | 10,75 |

- Simulasi Gantt Chart untuk Priority Scheduling:
```
     | P1 | P2 | P4 | P3 |
     0    5    8    14   22  
```

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
