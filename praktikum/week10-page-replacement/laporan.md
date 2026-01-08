 /># Laporan Praktikum Minggu 10
Topik: Manajemen Memori – Page Replacement (FIFO & LRU)

---

## Identitas
- **Nama**  : Andi pratama  
- **NIM**   : 250202975  
- **Kelas** : 1 IKRA

---

## Tujuan
1. Mengimplementasikan algoritma page replacement FIFO dalam program.
2. Mengimplementasikan algoritma page replacement LRU dalam program.
3. Menjalankan simulasi page replacement dengan dataset tertentu.
4. Membandingkan performa FIFO dan LRU berdasarkan jumlah *page fault*.
5. Menyajikan hasil simulasi dalam laporan yang sistematis.

---

## Dasar Teori
1. Manajemen Memori
Manajemen memori adalah bagian dari sistem operasi yang bertugas mengatur penggunaan memori utama agar dapat digunakan secara efisien oleh banyak proses.
2. Konsep Page Replacement
Page replacement adalah proses pemilihan halaman di memori utama yang akan dikeluarkan ketika terjadi page fault dan tidak tersedia frame kosong. Tujuan utama page replacement adalah meminimalkan jumlah page fault dan meningkatkan kinerja sistem.
3. Algoritma FIFO (First In First Out)
FIFO merupakan algoritma page replacement paling sederhana. Algoritma ini menggantikan halaman yang paling awal masuk ke memori, tanpa memperhatikan seberapa sering atau seberapa baru halaman tersebut digunakan.
4. Algoritma LRU (Least Recently Used)
LRU menggantikan halaman yang paling lama tidak digunakan berdasarkan asumsi bahwa halaman yang baru digunakan kemungkinan akan digunakan kembali. Algoritma ini lebih optimal dibanding FIFO karena mempertimbangkan pola penggunaan halaman.

---

## Langkah Praktikum

   Gunakan *reference string* berikut sebagai contoh:
   ```
   7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
   ```
   Jumlah frame memori: **3 frame**.

2. **Implementasi FIFO**

   - Simulasikan penggantian halaman menggunakan algoritma FIFO.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

3. **Implementasi LRU**

   - Simulasikan penggantian halaman menggunakan algoritma LRU.
   - Catat setiap *page hit* dan *page fault*.
   - Hitung total *page fault*.

4. **Eksekusi & Validasi**

   - Jalankan program untuk FIFO dan LRU.
   - Pastikan hasil simulasi logis dan konsisten.
   - Simpan screenshot hasil eksekusi.

5. **Analisis Perbandingan**

   Buat tabel perbandingan seperti berikut:

   | Algoritma | Jumlah Page Fault | Keterangan |
   |:--|:--:|:--|
   | FIFO | ... | ... |
   | LRU | ... | ... |


   - Jelaskan mengapa jumlah *page fault* bisa berbeda.
   - Analisis algoritma mana yang lebih efisien dan alasannya.

6. **Commit & Push**
  commit
   ```bash
   git add .
   git commit -m "Minggu 10 - Page Replacement FIFO & LRU"
   git push origin main
   ```

---

## Kode / Perintah
# ============================================
# Program Simulasi Page Replacement
# Algoritma FIFO dan LRU
# ============================================

pages = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
frame_size = 3


def print_header(title):
    print("\n" + "=" * 50)
    print(title)
    print("=" * 50)
    print("Step | Page | Frames\t\t | Status")
    print("-" * 50)


def fifo(pages, frame_size):
    frames = []
    page_faults = 0
    page_hits = 0

    print_header("SIMULASI FIFO")

    for i, page in enumerate(pages, start=1):
        if page in frames:
            page_hits += 1
            status = "Page Hit"
        else:
            page_faults += 1
            status = "Page Fault"
            if len(frames) < frame_size:
                frames.append(page)
            else:
                frames.pop(0)
                frames.append(page)

        print(f"{i:>4} | {page:^4} | {str(frames):<16} | {status}")

    print("\nRingkasan FIFO")
    print("Total Page Hit   :", page_hits)
    print("Total Page Fault :", page_faults)
    return page_faults


def lru(pages, frame_size):
    frames = []
    page_faults = 0
    page_hits = 0

    print_header("SIMULASI LRU")

    for i, page in enumerate(pages, start=1):
        if page in frames:
            page_hits += 1
            status = "Page Hit"
            frames.remove(page)
            frames.append(page)
        else:
            page_faults += 1
            status = "Page Fault"
            if len(frames) < frame_size:
                frames.append(page)
            else:
                frames.pop(0)
                frames.append(page)

        print(f"{i:>4} | {page:^4} | {str(frames):<16} | {status}")

    print("\nRingkasan LRU")
    print("Total Page Hit   :", page_hits)
    print("Total Page Fault :", page_faults)
    return page_faults


# ======================
# Program Utama
# ======================
print("STRING REFERENSI :", pages)
print("JUMLAH FRAME     :", frame_size)

fifo_faults = fifo(pages, frame_size)
lru_faults = lru(pages, frame_size)

print("\n" + "=" * 50)
print("PERBANDINGAN HASIL")
print("=" * 50)
print("FIFO Page Fault :", fifo_faults)
print("LRU  Page Fault :", lru_faults)

if fifo_faults > lru_faults:
    print("Kesimpulan: LRU lebih efisien dibanding FIFO")
elif fifo_faults < lru_faults:
    print("Kesimpulan: FIFO lebih efisien dibanding LRU")
else:
    print("Kesimpulan: FIFO dan LRU sama efisien")

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
