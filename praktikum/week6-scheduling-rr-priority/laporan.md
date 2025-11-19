
# Laporan Praktikum Minggu 6
Topik: Penjadwalan CPU – Round Robin (RR) dan Priority Scheduling

---

## Identitas
- **Nama**  : Andi Pratama 
- **NIM**   : 250202975
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  

1. Mahasiswa mampu memahami konsep dasar penjadwalan CPU, khususnya mekanisme kerja algoritma Round Robin dan Priority Scheduling.

2. Mahasiswa mampu mensimulasikan proses penjadwalan menggunakan data arrival time, burst time, dan prioritas untuk mendapatkan urutan eksekusi.

3. Mahasiswa mampu menghitung nilai Waiting Time (WT) dan Turnaround Time (TAT) secara tepat untuk kedua algoritma.

4. Mahasiswa mampu membandingkan kinerja algoritma berdasarkan hasil perhitungan WT dan TAT untuk menentukan algoritma yang lebih efisien.

5. Mahasiswa mampu menarik kesimpulan tentang kelebihan, kekurangan, serta kondisi penggunaan yang tepat dari Round Robin dan Priority Scheduling dalam sistem operasi.

   
---

## Dasar Teori

1. Penjadwalan CPU adalah mekanisme sistem operasi untuk menentukan proses mana yang mendapatkan giliran menggunakan CPU

2. Round Robin (RR) merupakan algoritma penjadwalan yang membagi waktu CPU secara merata kepada setiap proses menggunakan sebuah time quantum atau jatah waktu tertentu. 

3. Priority Scheduling adalah algoritma penjadwalan yang memilih proses berdasarkan tingkat prioritas. Proses dengan nilai prioritas tertinggi akan dieksekusi terlebih dahulu. Algoritma ini dapat bersifat preemptive maupun non-preemptive. Tujuannya adalah memastikan proses penting atau mendesak mendapatkan CPU lebih cepat.


---

## Langkah Praktikum
1. Siapkan data proses seperti berikut. 
   | Proses | Burst Time | Arrival Time | Priority |
   |:--:|:--:|:--:|:--:|
   | P1 | 5 | 0 | 2 |
   | P2 | 3 | 1 | 1 |
   | P3 | 8 | 2 | 4 |
   | P4 | 6 | 3 | 3 |

2. Siapkan alat perhitungan manual atau spreadsheet (Excel/Google Sheets).
3. Eksperimen 1 berdasarkan algoritma *Round Robin (RR)* dengan *time quantum (q)* = 3, hitung Waiting Time (WT) dan Turnaround Time (TAT) untuk tiap proses.
4. Simulasikan eksekusi menggunakan Gantt Chart dan catat sisa Burst Time tiap putaran
5. Eksperimen 2 berdasarkan algoritma *Priority Scheduling* (angka kecil = prioritas tinggi) dan hitung WT serta TAT nya seperti pada langkah 3. 
6. Buat tabel perbandingan rata-rata WT & TAT dari kedua eksperimen tersebut dan analisis perbedaannya.
7. Eksperimen 3 berdasarkan algoritma *Round Robin (RR)* dengan mengubah *time quantum (q)* menjadi 2 dan 5, hitung WT dan TAT nya, buat tabel perbandingan efek *quantum*.
8. Commit dan push hasil praktikum
 ```bash
   git add .
   git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
   git push origin main
   ```

---


## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![alt text](<screenshots/Eksperimen1dan2.jpg>)

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

Hasil Eksperimen 3:

![alt text](<screenshots/eksperimen3.jpg>)


| Proses | Arrival | Burst Time | Finish Time (P1) | Finish Time (P2) | Finish Time (P3) | Finish Time (P4) | TAT (FT-Arrival) | WT (TAT-Burst) |
   | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
   | P1 | 0 | 5 | 2 (sisa 3) | 10 (sisa 1) | 16 (selesai) | - | 16 - 0 = 16 | 16 - 5 = 11 |
   | P2 | 1 | 3 | 4 (sisa 1) | 11 (selesai) | - | - | 11 - 1 = 10 | 10 - 3 = 7 |
   | P3 | 2 | 8 | 6 (sisa 6) | 13 (sisa 4) | 18 (sisa 2) | 22 | 22 - 2 = 20 | 20 - 8 = 12 |
   | P4 | 3 | 6 | 8 (sisa 4) | 15 (sisa 2) | 20 (selesai) | - | 20 - 3 = 17 | 17 - 6 = 11 |
   | Total | | | | | | | 63 | 41 |
   | Average | | | | | | | 15,75 | 10,25 |

- Gantt Chart untuk RR q=2
```
     | P1 | P2 | P3 | P4 | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
     0    2    4    6    8   10    11   13   15   16   18   20   22
```

- Tabel perhitungan untuk *Time Quantum (q)* = 5

| Proses | Arrival | Burst Time | Finish Time (P1) | Finish Time (P2) | TAT (FT-Arrival) | WT (TAT-Burst) |
   | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
   | P1 | 0 | 5 | 5 (selesai) | - | 5 - 0 = 5 | 5 - 5 = 0  |
   | P2 | 1 | 3 | 8 (selesai) | - | 8 - 1 = 7 | 7 - 3 = 4 |
   | P3 | 2 | 8 | 13 (sisa 3) | 21 | 21 - 2 = 19 | 19 - 8 = 11 |
   | P4 | 3 | 6 | 18 (sisa 1) | 22 | 22 - 3 = 19 | 19 - 6 = 13 |
   | Total | | | | | 50 | 28 |
   | Average | | | | | 12,5 | 7 |

- Gantt Chart untuk RR q=5
```
     | P1 | P2 | P3 | P4 | P3 | P4 |
     0    5    8    13   18   21   22 
```

- Tabel perbandingan efek *Quantum*:

| Metrik / Time Quantum                | Quantum = 2                                                                        | Quantum = 5                                                                                  | Analisis / Efek yang Terjadi                                                                                          |
| :---: | :---: | :---: | :---: |
| Rata-rata Waiting Time (WT)        | 10.25                                                                                  | 7.00                                                                                             | Ketika quantum lebih besar, waktu tunggu rata-rata menurun karena proses lebih jarang dipreempt.                          |
| Rata-rata Turnaround Time (TAT)    | 15.75                                                                                  | 12.50                                                                                            | Turnaround time menurun karena setiap proses dapat menyelesaikan lebih banyak instruksi setiap giliran CPU.               |
| Observasi Umum                       | Quantum kecil membuat sistem lebih adil terhadap proses pendek tetapi overhead tinggi. | Quantum besar membuat sistem lebih efisien untuk proses panjang, namun fairness sedikit menurun. |                                              -                                                                             |

**Eksperimen 4 – Perbandingan RR dan Priority**

- Berikut tabel perbandingan hasil RR (*q*=3) dan Priority:

| Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
|:---:|:---:|:---:|:---:|:---:|
| RR | 8,5 | 14 | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
| Priority | 5,25 | 10,75 | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

---

## Analisis
Priority Scheduling lebih efisien pada data proses yang digunakan, karena menghasilkan waktu tunggu dan waktu penyelesaian yang lebih rendah. Sementara itu, Round Robin lebih adil karena semua proses mendapat giliran, tetapi memiliki performa yang lebih rendah akibat adanya banyak context switching.

---

## Kesimpulan
1. Priority Scheduling lebih efisien dibanding Round Robin karena menghasilkan rata-rata Waiting Time dan Turnaround Time yang lebih rendah, terutama karena proses berprioritas tinggi dieksekusi tanpa interupsi.


2. Round Robin memberikan keadilan bagi semua proses, tetapi memiliki performa lebih rendah akibat banyaknya context switching yang membuat proses dengan burst time besar menunggu lebih lama.


3. Pemilihan algoritma bergantung pada tujuan sistem: Priority lebih baik untuk efisiensi penyelesaian tugas, sedangkan Round Robin lebih cocok untuk sistem interaktif yang membutuhkan pemerataan waktu CPU.


---

## Quiz
1. Apa perbedaan utama antara Round Robin dan Priority Scheduling?    
   **Jawaban:Round Robin (RR) menekankan keadilan dan giliran, sedangkan Priority menekankan urutan berdasarkan kepentingan.**  
2. Apa pengaruh besar/kecilnya *time quantum* terhadap performa sistem?  
   **Jawaban:Jika time quantum terlalu kecil, proses sering sekali dihentikan dan digantikan, sehingga context switching menjadi sangat banyak dan sistem menjadi kurang efisien. Sebaliknya, jika time quantum terlalu besar, proses akan cenderung berjalan hingga hampir selesai seperti FCFS, sehingga mengurangi keadilan dan membuat proses lain menunggu lebih lama. Jadi, time quantum harus dipilih dengan ukuran yang seimbang agar sistem tetap responsif tanpa mengorbankan efisiensi.**  
3. Mengapa algoritma Priority dapat menyebabkan *starvation*?  ]  
   **Jawaban:Algoritma Priority dapat menyebabkan starvation karena proses dengan prioritas rendah terus-menerus tertunda oleh proses lain yang memiliki prioritas lebih tinggi.**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  Menyelesaikan tugas dengan tenggat waktu yang ketat.
- Bagaimana cara Anda mengatasinya? Membuat prioritas, memecah tugas menjadi bagian kecil, dan fokus pada satu hal pada satu waktu.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
