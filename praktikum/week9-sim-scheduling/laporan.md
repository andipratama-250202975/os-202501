
# Laporan Praktikum Minggu 9
Topik: Simulasi Algoritma Penjadwalan CPU

---

## Identitas
- **Nama**  : Andi pratama  
- **NIM**   : 250202975  
- **Kelas** : 1 IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
1. Membuat program simulasi algoritma penjadwalan FCFS dan/atau SJF.
2. Menjalankan program dengan dataset uji yang diberikan atau dibuat sendiri.
3. Menyajikan output simulasi dalam bentuk tabel atau grafik.
4. Menjelaskan hasil simulasi secara tertulis.
5. Mengunggah kode dan laporan ke Git repository dengan rapi dan tepat waktu.

---

## Dasar Teori
- Penjadwalan CPU adalah mekanisme penting dalam sistem operasi untuk menentukan urutan eksekusi proses pada prosesor.
- Algoritma First-Come, First-Served (FCFS) bekerja dengan prinsip antrian, di mana proses yang datang lebih dahulu akan dieksekusi lebih dahulu, sehingga sederhana namun dapat menimbulkan masalah convoy effect.
- Algoritma Shortest Job First (SJF) memilih proses dengan burst time paling pendek, yang secara teoritis menghasilkan waktu rata-rata tunggu paling optimal, meskipun sulit diimplementasikan karena memerlukan prediksi akurat terhadap burst time. 


---

## Langkah Praktikum
   Buat dataset proses minimal berisi:

   | Proses | Arrival Time | Burst Time |
   |:--:|:--:|:--:|
   | P1 | 0 | 6 |
   | P2 | 1 | 8 |
   | P3 | 2 | 7 |
   | P4 | 3 | 3 |

2. **Implementasi Algoritma**
   Program harus:
   - Menghitung *waiting time* dan *turnaround time*.  
   - Mendukung minimal **1 algoritma (FCFS atau SJF non-preemptive)**.  
   - Menampilkan hasil dalam tabel.

3. **Eksekusi & Validasi**
   - Jalankan program menggunakan dataset uji.  
   - Pastikan hasil sesuai dengan perhitungan manual minggu sebelumnya.  
   - Simpan hasil eksekusi (screenshot).

4. **Analisis**
   - Jelaskan alur program.  
   - Bandingkan hasil simulasi dengan perhitungan manual.  
   - Jelaskan kelebihan dan keterbatasan simulasi.

5. **Commit & Push**
   
   ```bash
---

## Kode / Perintah
# Dataset proses
processes = [
    {"id": "P1", "arrival": 0, "burst": 6},
    {"id": "P2", "arrival": 1, "burst": 8},
    {"id": "P3", "arrival": 2, "burst": 7},
    {"id": "P4", "arrival": 3, "burst": 3},
]

current_time = 0

print("Proses | AT | BT | Start | Finish | WT | TAT")
print("------------------------------------------------")

for p in processes:
    start_time = max(current_time, p["arrival"])
    finish_time = start_time + p["burst"]
    waiting_time = start_time - p["arrival"]
    turnaround_time = finish_time - p["arrival"]

    print(f"{p['id']:>5} | {p['arrival']:>2} | {p['burst']:>2} |"
          f" {start_time:>5} | {finish_time:>6} |"
          f" {waiting_time:>2} | {turnaround_time:>3}")

    current_time = finish_time

    SJF

print("-" * 80)
print(f"{'Rata-rata':<36}{rata_waiting:<10.2f}{rata_turnaround:<12.2f}")# PROGRAM SIMULASI SJF (Non-Preemptive)

# Data proses
proses = [
    {"nama": "P1", "arrival": 0, "burst": 6},
    {"nama": "P2", "arrival": 1, "burst": 8},
    {"nama": "P3", "arrival": 2, "burst": 7},
    {"nama": "P4", "arrival": 3, "burst": 3},
]

waktu_sekarang = 0
total_waiting = 0
total_turnaround = 0
selesai = []

print("SJF (Shortest Job First - Non Preemptive)")
print("-" * 80)
print(f"{'Proses':<8}{'Burst':<8}{'Arrival':<10}{'Start':<8}{'Waiting':<10}{'Turnaround':<12}{'Finish':<8}")
print("-" * 80)

while proses:
    # Ambil proses yang sudah datang
    tersedia = [p for p in proses if p["arrival"] <= waktu_sekarang]

    # Jika belum ada proses yang datang
    if not tersedia:
        waktu_sekarang += 1
        continue

    # Pilih proses dengan burst time terkecil
    proses_terpendek = min(tersedia, key=lambda x: x["burst"])
    proses.remove(proses_terpendek)

    start = waktu_sekarang
    waiting = start - proses_terpendek["arrival"]
    turnaround = waiting + proses_terpendek["burst"]
    finish = start + proses_terpendek["burst"]

    waktu_sekarang = finish
    total_waiting += waiting
    total_turnaround += turnaround

    print(f"{proses_terpendek['nama']:<8}{proses_terpendek['burst']:<8}{proses_terpendek['arrival']:<10}"
          f"{start:<8}{waiting:<10}{turnaround:<12}{finish:<8}")

    selesai.append(proses_terpendek)

rata_waiting = total_waiting / len(selesai)
rata_turnaround = total_turnaround / len(selesai)




## Hasil Eksekusi
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/68b493db-14e7-4c01-aee8-f5cc6765da14" />
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/8384a5e3-4bab-4b96-8a85-e142e77700a8" />


---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
- Akurasi Simulasi: Program simulasi yang dibuat terbukti akurat dalam menghitung waiting time dan turnaround time, di mana hasilnya konsisten dengan perhitungan manual menggunakan Excel.
  
- Perbandingan Efisiensi: Algoritma SJF (Shortest Job First) memberikan nilai rata-rata waiting time yang lebih rendah ($6,25$) dibandingkan FCFS ($8,75$), membuktikan bahwa memprioritaskan proses pendek meningkatkan efisiensi waktu tunggu.
  
- Karakteristik Algoritma: FCFS jauh lebih mudah diimplementasikan secara logika karena hanya mengikuti urutan kedatangan, sedangkan SJF memerlukan logika tambahan untuk memantau status waktu CPU dan melakukan pengurutan berdasarkan burst time terkecil.
---


## Quiz
1. [Mengapa simulasi diperlukan untuk menguji algoritma scheduling?]  
   **Jawaban:**
   
Simulasi digunakan dalam pengujian algoritma *CPU scheduling* karena memberikan lingkungan yang aman, terkontrol, dan efisien. Berikut alasan utamanya:
A. Aman untuk Sistem
Pengujian algoritma scheduling secara langsung pada sistem operasi nyata berisiko mengganggu kinerja sistem. Dengan simulasi, pengujian dapat dilakukan tanpa memengaruhi sistem yang sedang berjalan.

B. Memudahkan Perbandingan Algoritma
Simulasi memungkinkan pengujian beberapa algoritma seperti **FCFS**, **SJF**, **Priority**, dan **Round Robin** menggunakan data proses yang sama, sehingga hasil perbandingan menjadi lebih objektif.

C. Kondisi Pengujian Dapat Dikontrol
Parameter seperti *arrival time*, *burst time*, *priority*, dan *time quantum* dapat diatur sesuai kebutuhan, sesuatu yang sulit dilakukan pada sistem nyata.

D. Analisis Kinerja Lebih Mudah
Melalui simulasi, metrik kinerja seperti:
- Waiting Time
- Turnaround Time
- Response Time  
dapat dihitung dan dianalisis dengan jelas.

E. Efisien dari Segi Waktu dan Biaya
Simulasi tidak memerlukan perangkat keras tambahan dan dapat dijalankan berulang kali dengan cepat.

F. Membantu Pemahaman Konsep
Visualisasi seperti **Gantt Chart** memudahkan pemahaman alur eksekusi proses dan cara kerja algoritma scheduling.

Kesimpulan
Simulasi merupakan metode yang efektif untuk menguji dan membandingkan algoritma scheduling secara aman, efisien, dan terkontrol sebelum diterapkan pada sistem operasi nyata.


2. [Apa perbedaan hasil simulasi dengan perhitungan manual jika dataset besar?]  
   **Jawaban:**
Perbedaan Hasil Simulasi dan Perhitungan Manual pada Dataset Besar

| Aspek                     | Simulasi                                      | Perhitungan Manual                          |
|---------------------------|-----------------------------------------------|---------------------------------------------|
| Akurasi                   | Tinggi dan konsisten karena otomatis          | Rentan kesalahan manusia                    |
| Efisiensi Waktu           | Sangat cepat meskipun dataset besar           | Sangat lambat dan tidak efisien             |
| Kompleksitas Algoritma    | Mampu menangani algoritma kompleks            | Sulit menangani proses yang berulang        |
| Konsistensi Hasil         | Konsisten untuk input yang sama               | Kurang konsisten                            |
| Penanganan Dataset Besar  | Efektif untuk ratusan hingga ribuan data      | Tidak praktis untuk dataset besar           |
| Visualisasi Hasil         | Mudah menghasilkan tabel dan Gantt Chart      | Visualisasi dibuat manual dan rawan salah   |
| Kelayakan Penggunaan      | Cocok untuk analisis dan implementasi nyata   | Cocok untuk pembelajaran dasar (dataset kecil) |

Kesimpulan
Untuk dataset besar, simulasi lebih unggul dibandingkan perhitungan manual karena lebih akurat, efisien, dan konsisten.

3. [ Algoritma mana yang lebih mudah diimplementasikan? Jelaskan.]  
   **Jawaban:**  
Algoritma yang lebih mudah diimplementasikan adalah **FCFS (First Come First Served)**, karena:
- Proses dijalankan sesuai urutan kedatangan.
- Tidak memerlukan proses pemilihan atau perbandingan burst time.
- Logika program sederhana dan mudah dipahami.
- Cocok untuk implementasi dasar dan pembelajaran awal.

---


## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
