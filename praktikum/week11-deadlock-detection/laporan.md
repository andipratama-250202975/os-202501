
# Laporan Praktikum Minggu 11
Topik: Simulasi dan Deteksi Deadlock

---

## Identitas
- **Nama**  : Andi Pratatama  
- **NIM**   : 250202975  
- **Kelas** : 1IKRA

---

## Tujuan
1. Membuat program sederhana untuk mendeteksi deadlock.  
2. Menjalankan simulasi deteksi deadlock dengan dataset uji.  
3. Menyajikan hasil analisis deadlock dalam bentuk tabel.  
4. Memberikan interpretasi hasil uji secara logis dan sistematis.  
5. Menyusun laporan praktikum sesuai format yang ditentukan.

---

## Dasar Teori
1. Pengertian Deadlock
Deadlock adalah kondisi pada sistem komputer, khususnya sistem operasi, di mana dua atau lebih proses saling menunggu sumber daya yang sedang dipegang oleh proses lain sehingga tidak ada satu pun proses yang dapat melanjutkan eksekusinya.

2. Penyebab Terjadinya Deadlock
Deadlock terjadi karena adanya konflik dalam penggunaan sumber daya terbatas seperti CPU, memori, printer, atau file. Ketika proses meminta sumber daya secara bertahap dan sistem tidak dapat mengalokasikan semua sumber daya yang dibutuhkan sekaligus, maka dapat timbul situasi saling menunggu antar proses yang berujung pada deadlock.

3. Syarat Terjadinya Deadlock (Coffman Conditions)
Deadlock hanya dapat terjadi jika empat kondisi berikut terpenuhi secara bersamaan, yaitu mutual exclusion (sumber daya tidak dapat digunakan bersama), hold and wait (proses menahan sumber daya sambil menunggu sumber daya lain), no preemption (sumber daya tidak dapat diambil paksa), dan circular wait (terjadi siklus saling menunggu antar proses). Jika salah satu kondisi ini dihilangkan, maka deadlock dapat dicegah.

4. Dampak Deadlock terhadap Sistem
Deadlock dapat menurunkan kinerja sistem secara signifikan karena proses yang terlibat tidak dapat diselesaikan. Selain itu, sumber daya menjadi tidak efisien karena terkunci tanpa digunakan.
---

## Langkah Praktikum

   Membuat dataset sederhana yang berisi:
   - Daftar proses  
   - Resource Allocation  
   - Resource Request / Need

   Data tabel:

   | Proses | Allocation | Request |
   |:--|:--|:--|
   | Mobil_A | Jalur_Utara | Jalur_Timur |
   | Mobil_B | Jalur_Timur | Jalur_Selatan |
   | Mobil_C | Jalur_Selatan | Jalur_Utara |

2. **Implementasi Algoritma Deteksi Deadlock**

   Program:
   - Membaca data proses dan resource.  
   - Menentukan apakah sistem berada dalam kondisi deadlock.  
   - Menampilkan proses mana saja yang terlibat deadlock.

3. **Eksekusi & Validasi**

   - Menjalankan program dengan dataset uji.  
   - Memvalidasi hasil deteksi dengan analisis manual/logis.  
   - Menyimpan hasil eksekusi dalam bentuk screenshot.

4. **Analisis Hasil**

   - Menyajikan hasil deteksi dalam tabel (proses deadlock / tidak).  
   - Menjelaskan mengapa deadlock terjadi atau tidak terjadi.  
   - Mengaitkan hasil dengan teori deadlock (empat kondisi).

5. **Commit & Push**

   ```bash
   git add .
   git commit -m "Minggu 11 - Deadlock Detection"
   git push origin main
   ```
---


## Kode / Perintah

processes = {
    "P1": {"alloc": "R1", "request": "R2"},
    "P2": {"alloc": "R2", "request": "R3"},
    "P3": {"alloc": "R3", "request": "R1"}
}

def build_wait_for_graph(processes):
    resource_owner = {}
    for p in processes:
        resource_owner[processes[p]["alloc"]] = p

    wait_for = {}
    for p in processes:
        req = processes[p]["request"]
        if req in resource_owner:
            wait_for[p] = resource_owner[req]

    return wait_for


def detect_deadlock(wait_for):
    visited = set()
    stack = []

    def dfs(p):
        if p in stack:
            return stack[stack.index(p):] + [p]
        if p in visited:
            return None

        visited.add(p)
        stack.append(p)

        if p in wait_for:
            result = dfs(wait_for[p])
            if result:
                return result

        stack.pop()
        return None

    for p in wait_for:
        cycle = dfs(p)
        if cycle:
            return cycle

    return None

def resolve_deadlock(processes):
    while True:
        wait_for = build_wait_for_graph(processes)
        cycle = detect_deadlock(wait_for)

        if not cycle:
            print("\n✅ Tidak ada deadlock. Sistem aman.")
            break

        print("\n⚠️ Deadlock terdeteksi:")
        print(" -> ".join(cycle))

        # Pilih proses korban (proses terakhir sebelum kembali ke awal)
        victim = cycle[-2]
        print(f"❌ Menghentikan proses {victim}")

        released = processes[victim]["alloc"]
        print(f"🔓 Resource {released} dilepaskan")

        del processes[victim]

print("=== DEADLOCK DETECTION & SOLUTION ===")
resolve_deadlock(processes)

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
| Iterasi | Proses Aktif | Resource Dialokasikan | Status Sistem | Keterangan                                |
| ------- | ------------ | --------------------- | ------------- | ----------------------------------------- |
| 1       | P1, P2, P3   | R1→P1, R2→P2, R3→P3   | Deadlock      | Terjadi circular wait P1→P2→P3→P1         |
| 2       | P1, P2       | R1→P1, R2→P2          | Aman          | Proses P3 dihentikan, resource R3 dilepas |

Tabel 2. Proses yang Terlibat Deadlock
| Proses | Resource Dialokasikan | Resource Diminta | Status                         |
| ------ | --------------------- | ---------------- | ------------------------------ |
| P1     | R1                    | R2               | Terlibat deadlock              |
| P2     | R2                    | R3               | Terlibat deadlock              |
| P3     | R3                    | R1               | Terlibat deadlock (dihentikan) |

Tabel 3. Deadlock Pemulihan Tindakan
| Langkah | Tindakan                   | Dampak                            |
| ------- | -------------------------- | --------------------------------- |
| 1       | Mendeteksi siklus deadlock | Sistem teridentifikasi bermasalah |
| 2       | Menghentikan proses P3     | Resource R3 dilepaskan            |
| 3       | Evaluasi ulang sistem      | Deadlock tidak terjadi lagi       |

Berdasarkan hasil eksekusi program deteksi deadlock, sistem terdeteksi mengalami deadlock pada iterasi pertama. Deadlock terjadi karena adanya kondisi sirkular wait, di mana setiap proses menahan satu sumber daya dan menunggu sumber daya lain yang sedang dipegang oleh proses lain. Pola ini menyebabkan tidak ada satu pun proses yang dapat melanjutkan eksekusinya.

Untuk mengatasi kondisi tersebut, program menerapkan metode pemulihan deadlock dengan menghentikan salah satu proses yang terlibat, yaitu proses P3. Penghentian proses ini menyebabkan resource R3 tersisa, sehingga siklus saling menunggu terputus. Setelah dilakukan recovery, sistem dievaluasi kembali dan terbukti tidak lagi mengalami deadlock.

Hasil ini menunjukkan bahwa algoritma deteksi deadlock berbasis wait-for graph efektif dalam mengidentifikasi kondisi deadlock serta menentukan langkah pemulihan yang tepat. Dengan pemutusan satu proses, sistem dapat kembali ke kondisi aman tanpa perlu menghentikan seluruh proses yang berjalan.


---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. Apa perbedaan antara pencegahan , penghindaran , dan deteksi kebuntuan ?
   **Jawaban:1. Pencegahan Kebuntuan (Pencegahan Kebuntuan)
Pencegahan kebuntuan adalah pendekatan yang bertujuan untuk mencegah terjadinya kebuntuan sejak awal dengan cara memastikan bahwa setidaknya satu dari empat kondisi kebuntuan tidak pernah tercapai . Penghindaran Kebuntuan (Penghindaran Kebuntuan)
Penghindaran kebuntuan adalah metode yang mengizinkan sistem berjalan normal , tetapi setiap permintaan sumber daya akan dievaluasi terlebih dahulu untuk memastikan sistem tetap berada dalam keadaan aman (safe state) . Deteksi dan Pemulihan Kebuntuan (Deadlock Detection and Recovery)
Deteksi kebuntuan adalah pendekatan yang membiarkan kebuntuan terjadi , kemudian sistem akan mendeteksi keberadaannya menggunakan algoritma tertentu, seperti wait-for graph atau matriks resource. Setelah deadlock terdeteksi, sistem melakukan pemulihan , misalnya dengan menghentikan proses atau mengambil kembali sumber daya.**  
2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?
   
   **Jawaban: deteksi dedlock diperlukan sebagai kompromi antara keamanan dan efisiensi sistem , terutama pada lingkungan multi-proses dan multi-sumber daya yang kompleks, di mana skrip dan kinerja menjadi prioritas utama.**  
3. Apa kelebihan dan kekurangan pendekatan deteksi deadlock?
   
   **Jawaban:Pendekatan deteksi deadlock memiliki kelebihan utama berupa kekeliruan dan efisiensi penggunaan sumber daya . Sistem operasi tidak perlu membatasi proses secara ketat sejak awal, sehingga proses dapat meminta dan menggunakan sumber daya secara dinamis sesuai kebutuhan. Hal ini memungkinkan tingkat paralelisme yang tinggi dan pemanfaatan sumber daya yang lebih optimal, terutama pada sistem yang kompleks dan beban kerja tidak dapat diprediksi dengan pasti.
Namun, pendekatan ini juga memiliki beberapa kekurangan. Karena sistem membiarkan deadlock terjadi terlebih dahulu , kinerja sistem dapat terganggu sebelum deadlock terdeteksi. Selain itu, proses deteksi membutuhkan overhead kountukku**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? tugas yang banyak  
- Bagaimana cara Anda mengatasinya?  kerjakan tugasnya

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
