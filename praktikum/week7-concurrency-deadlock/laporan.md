
# Laporan Praktikum Minggu 7
Topik:  Sinkronisasi Proses dan Masalah Deadlock

---

## Identitas Kelompok
- **Nama**  : - Muhammad Maulidana Nerazzuri  (250202922)

- **Nama**              - Andi Pratama (250202975)

              - Prima Radita Pratama (2502029..) 
- **Kelas** : 1IKRA

---

## Tujuan
1. Memahami cara proses berjalan secara bersamaan (concurrency)
2. Mencegah kondisi race condition
3. Menguasai mekanisme pengendalian akses ke resource bersama
4. Meningkatkan efisiensi dan kinerja sistem
5. Membangun kemampuan merancang program paralel yang aman 

---

## Dasar Teori

1. Konkurensi dan Critical Section
Saat beberapa proses/thread berjalan bersamaan, mereka dapat mengakses data atau resource yang sama. Bagian kode yang mengakses resource bersama disebut critical section, dan harus dilindungi agar tidak terjadi race condition.

2. Mekanisme Sinkronisasi
Untuk mengatur akses ke critical section, digunakan mekanisme seperti mutex, semaphore, monitor, dan lock. Tujuan utamanya adalah memastikan hanya satu proses mengakses resource pada satu waktu serta menjaga konsistensi data.

3. Kondisi Terjadinya Deadlock
Deadlock muncul ketika proses saling menunggu resource yang tidak akan pernah dilepaskan. Empat syarat deadlock menurut Coffman adalah: mutual exclusion, hold and wait, no preemption, dan circular wait.

4. Penanganan Deadlock

Ada tiga pendekatan utama yaitu:

    Pencegahan (prevention): Menghilangkan salah satu dari empat kondisi deadlock.

    Penghindaran (avoidance): Menggunakan analisis alokasi resource (misal Banker’s Algorithm).

    Deteksi & Pemulihan (detection & recovery): Mengizinkan deadlock terjadi lalu mendeteksinya dan memulihkan sistem.

5. Resource Allocation & State System
Sistem operasi memetakan resource ke proses. Kesalahan dalam pengalokasian atau sinkronisasi dapat menyebabkan deadlock atau kondisi kompetisi. Karena itu, desain algoritma sinkronisasi dan manajemen resource menjadi aspek utama percobaan.

---

## Langkah Praktikum
1. **Persiapan Tim**
   - Bentuk kelompok beranggotakan 3–4 orang.  
   - Tentukan ketua dan pembagian tugas (analisis, implementasi, dokumentasi).

2. **Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)**
   - Implementasikan versi sederhana dari masalah *Dining Philosophers* tanpa mekanisme pencegahan deadlock.  
   - Contoh pseudocode:
     ```text
     while true:
       think()
       pick_left_fork()
       pick_right_fork()
       eat()
       put_left_fork()
       put_right_fork()
     ```
   - Jalankan simulasi atau analisis alur (boleh menggunakan pseudocode atau diagram alur).  
   - Identifikasi kapan dan mengapa deadlock terjadi.

3. **Eksperimen 2 – Versi Fixed (Menggunakan Semaphore / Monitor)**
   - Modifikasi pseudocode agar deadlock tidak terjadi, misalnya:
     - Menggunakan *semaphore (mutex)* untuk mengontrol akses.
     - Membatasi jumlah filosof yang dapat makan bersamaan (max 4).  
     - Mengatur urutan pengambilan garpu (misal, filosof terakhir mengambil secara terbalik).  
   - Analisis hasil modifikasi dan buktikan bahwa deadlock telah dihindari.

4. **Eksperimen 3 – Analisis Deadlock**
   - Jelaskan empat kondisi deadlock dari versi pertama dan bagaimana kondisi tersebut dipecahkan pada versi fixed.  
   - Sajikan hasil analisis dalam tabel seperti contoh berikut:

     | Kondisi Deadlock | Terjadi di Versi Deadlock | Solusi di Versi Fixed |
     |------------------|---------------------------|------------------------|
     | Mutual Exclusion | Ya (satu garpu hanya satu proses) | Gunakan semaphore untuk kontrol akses |
     | Hold and Wait | Ya | Hindari proses menahan lebih dari satu sumber daya |
     | No Preemption | Ya | Tidak ada mekanisme pelepasan paksa |
     | Circular Wait | Ya | Ubah urutan pengambilan sumber daya |

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua diagram, screenshot simulasi, dan hasil diskusi di:
     ```
     praktikum/week7-concurrency-deadlock/screenshots/
     ```
   - Tuliskan laporan kelompok di `laporan.md` (format IMRaD singkat: *Pendahuluan, Metode, Hasil, Analisis, Diskusi*).

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 7 - Sinkronisasi Proses & Deadlock"
   git push origin main
   ```





---

## Hasil Eksekusi
1. **Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)**

- Implementasi sederhana (pseudocode):

| No | Pseudocode                                              |
| -- | ------------------------------------------------------- |
| 1  | Start                                                   |
| 2  | Prepare 5 forks arranged in a circle                    |
| 3  | Initialize 5 philosophers: P1, P2, P3, P4, P5           |
| 4  | All philosophers begin in the *thinking* state          |
| 5  | Philosophers P1–P5 enter the *ready* state              |
| 6  | P1–P5 each pick up their left fork                      |
| 7  | P1–P5 attempt to pick up their right fork               |
| 8  | The right fork is not available → philosopher waits  |
| 9 | All philosophers end up waiting for the right fork      |
| 10 | Each philosopher holds one fork and waits for the other |
| 11 | A *deadlock* occurs                                     |
| 12 | No philosopher is able to eat                           |
| 13 | No philosopher can release the fork they hold           |
| 14 | The system remains stuck in the deadlock condition      |
| 15 | Finish                                                  |

- Output:

| No | Output                                       |
| -- | -------------------------------------------- |
| 1  | Simulation started                           |
| 2  | All philosophers begin thinking              |
| 3  | Philosophers P1–P5 switch to ready state     |
| 4  | P1 picks up left fork                        |
| 5  | P2 picks up left fork                        |
| 6  | P3 picks up left fork                        |
| 7  | P4 picks up left fork                        |
| 8  | P5 picks up left fork                        |
| 9  | P1 attempts to pick up right fork (blocked)  |
| 10 | P2 attempts to pick up right fork (blocked)  |
| 11 | P3 attempts to pick up right fork (blocked)  |
| 12 | P4 attempts to pick up right fork (blocked)  |
| 13 | P5 attempts to pick up right fork (blocked)  |
| 14 | All philosophers are holding their left fork |
| 15 | All right forks are unavailable              |
| 16 | No philosopher is able to proceed            |
| 17 | System enters **deadlock**                   |
| 18 | No philosopher can eat                       |
| 19 | Simulation stops in deadlock state           |
| 20 | Finish                                       |

- Hasil Identifikasi:

Deadlock pada simulasi Dining Philosophers terjadi ketika semua filsuf sudah mengambil garpu di sebelah kiri mereka dan mencoba meraih garpu di sebelah kanan, sehingga masing-masing memegang satu garpu dan menunggu garpu yang dipegang filsuf lain. Hal ini terjadi karena empat kondisi penting terpenuhi sekaligus: garpu hanya bisa dipegang satu filsuf pada satu waktu (mutual exclusion), filsuf menahan garpu sambil menunggu garpu lain (hold and wait), garpu yang dipegang tidak bisa diambil paksa oleh filsuf lain (no preemption), dan terjadi lingkaran menunggu antar filsuf (circular wait). Akibatnya, tidak ada filsuf yang bisa makan dan sistem akhirnya macet dalam deadlock.

2. **Eksperimen 2 – Versi Fixed (Menggunakan Semaphore / Monitor)**

- Modifikasi pseudocode (deadlock-free):

| No | Pseudocode                                                                       |
| -- | -------------------------------------------------------------------------------- |
| 1  | Start                                                                            |
| 2  | Prepare 5 forks arranged in a circle                                             |
| 3  | Initialize 5 philosophers: P1, P2, P3, P4, P5                                    |
| 4  | All philosophers begin in the thinking state                                     |
| 5  | Philosophers P1–P5 enter the ready state                                         |
| 6  | Limit maximum 4 philosophers to attempt eating simultaneously                    |
| 7  | Philosophers pick up forks: P1–P4 pick left then right, P5 picks right then left |
| 8  | If a fork is not available, philosopher waits until it becomes available         |
| 9  | Each philosopher acquires both forks successfully when available                 |
| 10 | Philosopher eats                                                                 |
| 11 | Philosopher releases both forks after eating                                     |
| 12 | Next philosopher attempts to eat following the same rules                        |
| 13 | Deadlock is avoided by limiting philosophers and reversing order for P5          |
| 14 | Simulation continues without any system halt                                     |
| 15 | Finish                                                                           |

- Output:

| No | Output                                                              |
| -- | ------------------------------------------------------------------- |
| 1  | Simulation started                                                  |
| 2  | All philosophers begin thinking                                     |
| 3  | Philosophers P1–P5 switch to ready state                            |
| 4  | Limit applied: max 4 philosophers can attempt eating simultaneously |
| 5  | P1 picks up left fork                                               |
| 6  | P2 picks up left fork                                               |
| 7  | P3 picks up left fork                                               |
| 8  | P4 picks up left fork                                               |
| 9  | P5 picks up right fork first, then left fork                        |
| 10 | All philosophers successfully acquire both forks when available     |
| 11 | P1–P5 eat without waiting indefinitely                              |
| 12 | P1 releases both forks after eating                                 |
| 13 | P2 releases both forks after eating                                 |
| 14 | P3 releases both forks after eating                                 |
| 15 | P4 releases both forks after eating                                 |
| 16 | P5 releases both forks after eating                                 |
| 17 | Next philosophers attempt eating following the same rules           |
| 18 | Deadlock is avoided                                                 |
| 19 | Simulation continues smoothly                                       |
| 20 | Finish                                                              |

- Analisis Hasil Modifikasi:
Hasil modifikasi pada simulasi Dining Philosophers berhasil mencegah deadlock karena beberapa strategi diterapkan secara bersamaan. Pertama, membatasi maksimal 4 filsuf yang bisa makan bersamaan memastikan selalu ada setidaknya satu garpu bebas, sehingga tidak ada yang saling menunggu selamanya. Kedua, filsuf terakhir mengambil garpu dalam urutan terbalik, sehingga circular wait tidak terbentuk. Ketiga, penggunaan semaphore/mutex untuk tiap garpu menjaga agar hanya satu filsuf yang memegang garpu pada satu waktu dan filsuf lain menunggu dengan tertib. Kombinasi strategi ini membuat setiap filsuf bisa memperoleh kedua garpu saat giliran mereka, makan, lalu melepaskan garpu tanpa ada yang terjebak menunggu selamanya. Dengan begitu, sistem berjalan lancar, semua filsuf bisa makan, dan deadlock berhasil dihindari.

3. **Eksperimen 3 – Analisis Deadlock**

| Kondisi Deadlock | Terjadi di Versi Deadlock                                | Solusi di Versi Fixed                                                                      |
| ---------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Mutual Exclusion | Ya, setiap garpu hanya bisa dipegang satu filsuf         | Menggunakan semaphore/mutex untuk mengontrol akses garpu                             |
| Hold and Wait    | Ya, filsuf memegang garpu kiri sambil menunggu kanan     | Membatasi jumlah filsuf makan bersamaan (max 4), sehingga selalu ada garpu bebas           |
| No Preemption    | Ya, garpu tidak bisa diambil paksa                       | Tetap, tapi deadlock dicegah dengan strategi urutan dan batasan filsuf                     |
| Circular Wait    | Ya, semua filsuf menunggu garpu berikut secara melingkar | Ubah urutan pengambilan garpu untuk filsuf terakhir (kanan dulu), memutus lingkaran 


---

## Kesimpulan
Dari eksperimen Dining Philosophers, bisa disimpulkan bahwa deadlock terjadi ketika semua filsuf memegang garpu kiri dan menunggu garpu kanan, karena empat kondisi deadlock terpenuhi: mutual exclusion, hold and wait, no preemption, dan circular wait. Deadlock ini bisa dihindari dengan beberapa strategi sederhana tapi efektif, seperti membatasi jumlah filsuf yang bisa makan bersamaan, membalik urutan pengambilan garpu untuk filsuf terakhir, serta menggunakan semaphore atau mutex untuk mengatur akses garpu. Dengan cara ini, semua filsuf bisa makan secara bergantian tanpa ada yang terjebak menunggu, sehingga sistem berjalan lancar dan garpu dapat digunakan secara efisien.



---

## Quiz
1. Sebutkan empat kondisi utama penyebab deadlock.  
**Jawaban:**
   - Mutual Exclusion (Saling Mengecualikan)   
      
      Hanya ada satu proses saja yang boleh memakai resource. Proses yang lain harus menunggu sampai proses sebelumnya benar benar selesai.

   - Hold and Wait (Menahan dan Menunggu)   
      
      Suatu proses yang menunggu resource yang sedang digunakan proses lainnya dalam waktu yang lama hingga resource tersebut selesai digunakan.

   - No Preemption (Tidak Bisa Diambil Secara Paksa) 
      
      Sebuah resource tidak boleh diambil paksa oleh proses lainnya, sehingga peoses tersebut harus menunggu proses sebelumnya selesai.

   - Circular Wait (Menunggu Secara Melingkar) 
      
      Keadaan yang di mana suatu proses membutuhkan resource yang sedang dipakai proses lainnya, yang menyebabkan terjadinya antrian.

 2. Mengapa sinkronisasi diperlukan dalam sistem operasi?  

   **Jawaban:**

   Sinkronisasi dalam sistem operasi diperlukan untuk mencegah terjadinya masalah konkurensi, seperti kerusakan data dan konflik, serta untuk menjaga integritas dan konsistensi data saat banyak proses mengakses sumber daya bersamaan.
3. Jelaskan perbedaan antara *semaphore* dan *monitor*.

   **Jawaban:**

   Perbedaannya adalah semaphore bekerja dengan pengaturan manual, sedangkan monitor memberikan pengaturan otomatis. Semaphore itu sebenarnya alat bantu sinkronisasi tingkat rendah yang cara kerjanya pakai hitungan dan dua operasi dasar: wait dan signal. Karena semuanya diatur manual oleh pembuat program, semaphore itu cukup fleksibel, tapi juga gampang bikin salah kalau lupa manggil salah satu operasinya. Biasanya semaphore dipakai untuk ngatur berapa banyak proses yang boleh akses resource tertentu atau buat sinkronisasi yang sederhana antar proses.

   Sementara itu, monitor adalah mekanisme sinkronisasi yang lebih rapi dan otomatis karena mutual exclusion-nya sudah diurus oleh sistem atau bahasa pemrogramannya. Di dalam monitor, hanya satu proses yang boleh masuk dalam satu waktu, dan ada condition variable yang bisa dipakai proses untuk nunggu kondisi tertentu lewat operasi wait dan signal. Karena lebih terstruktur, monitor jauh lebih gampang dipakai dan lebih aman, terutama kalau critical section-nya cukup rumit.
  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
