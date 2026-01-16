
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


### A. Persiapan & Instalasi
1.  Mengunduh file ISO **Ubuntu 24.04 Desktop** dan aplikasi **Oracle VirtualBox**.
    -  **Ubuntu 24.04 Desktop** : https://ubuntu.com/download/desktop
    -  **Oracle VirtualBox** : https://download.virtualbox.org/virtualbox/7.2.4/VirtualBox-7.2.4-170995-Win.exe
2.  Menginstal VirtualBox pada Dekstop (Host OS).

### B. Konfigurasi Awal (High Resource)
1.  Membuat Virtual Machine baru dengan nama `Linux-Ubuntu`.
2.  Mengatur spesifikasi awal VM:
    * **RAM:** 4096 MB (4 GB).
    * **CPU:** 2 Core.
3.  Menjalankan VM dan menunggu proses instalasi Ubuntu selesai hingga masuk ke desktop.

### C. Eksperimen VM Linux Ubuntu 24.04 LTS
1.  Setelah Konfigurasi selesai, klik open untuk membuka Virtual Machine
2.  Membuka **Terminal** dan menjalankan perintah dasar untuk mengecek spesifikasi sistem.
3.  Membuka aplikasi **Firefox** dan memutar video YouTube serta membuka 5 tab sekaligus untuk memberikan beban kerja (*stress test*).
4.  Membuka **System Monitor** untuk memantau grafik penggunaan RAM dan CPU saat beban tinggi.

### D. Eksperimen VM Mengurangi Resource
1.  Mematikan VM (*Shutdown*).
2.  Masuk ke menu **Settings > System** di VirtualBox.
3.  Menurunkan alokasi resource menjadi:
    * **RAM:** 2048 MB (2 GB).
    * **CPU:** 1 Core.
4.  Menyalakan kembali VM dan mengulangi pengujian dengan membuka Firefox.
5.  Mengamati terjadinya penurunan performa (*lag*) dan peningkatan penggunaan memori hingga mendekati batas maksimal.

### E. Analisis dan Dokumentasi
1. Mencatat proses praktikum dari awal persiapan hingga akhir.
2. Screenshot hasil instalasi virtual box kemudian simpan di `screenshors/instalasi_vm.png`
3. Screenshot hasil konfigurasi Virtual Machine Linux Ubuntu 24.04 LTS dan simpan di `screenshots/konfigurasi_resource.png`
4. Screenshot hasil eksperimen di OS Guest dan simpan di `screenshots/os_guest_running.png`
5. Mencatat konfigurasi Spesifikasi Host OS dan Spefisikasi Guest OS kemudian simpan di code/`catatan_konfigurasi`

### F. Commit & Push
   ```bash
   git add .
   git commit -m "Minggu 12 - Virtual Machine"
   git push origin main
   ```

---
---

## Kode / Perintah
```bash
# Sebelum perubahan
lscpu
free -h

# Setelah perubahan
lscpu
free -h
 ```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
Analisis Perilaku Sistem Operasi pada Virtual Machine Ubuntu 24.04 Berdasarkan Uji Instalasi dan Stress Test

Berdasarkan hasil instalasi dan pengujian beban kerja (stress test) pada Virtual Machine (VM) yang menjalankan Ubuntu 24.04, dapat dilakukan evaluasi terhadap kinerja sistem operasi dalam lingkungan virtual, khususnya pada aspek manajemen memori, pemrosesan CPU, serta mekanisme virtualisasi yang diterapkan.

1. Analisis Manajemen Memori

Hasil pengujian dengan menjalankan browser Firefox menggunakan lima tab aktif, yang meliputi pemutaran video YouTube dan aktivitas penelusuran web, menunjukkan pengaruh signifikan terhadap pengelolaan memori sistem.

Pada skenario dengan keterbatasan sumber daya (RAM sebesar 2GB sebagai pembanding), sistem mengalami penurunan performa yang cukup jelas. Ketika kapasitas memori fisik hampir atau telah penuh, kernel Linux akan mengalihkan sebagian data dari proses yang jarang digunakan ke ruang memori virtual (swap) yang berada pada media penyimpanan. Karena kecepatan akses disk jauh lebih rendah dibandingkan RAM, proses ini menimbulkan jeda respons sistem yang terasa lambat, bahkan tidak responsif.

Fenomena tersebut sesuai dengan konsep thrashing dalam teori sistem operasi, yaitu kondisi ketika sistem lebih banyak menghabiskan waktu untuk aktivitas paging memori dibandingkan mengeksekusi instruksi proses secara efektif.

2. Analisis Prosesor dan Penjadwalan

Konfigurasi penggunaan dua inti prosesor (2 Core CPU) pada pengujian utama terbukti meningkatkan kemampuan sistem dalam menangani beban kerja secara bersamaan.

Firefox sebagai aplikasi modern menggunakan pendekatan multi-proses, sehingga dengan dua core, penjadwal CPU pada Ubuntu dapat mendistribusikan tugas secara lebih optimal. Proses pemrosesan video dapat dijalankan pada satu inti, sementara layanan sistem dan proses latar belakang ditangani oleh inti lainnya secara paralel.

Jika dibandingkan dengan konfigurasi satu inti, sistem dengan dua core menunjukkan pengurangan overhead context switching. Pada CPU satu core, prosesor harus bergantian melayani aplikasi pengguna dan kernel sistem secara terus-menerus, yang berdampak pada meningkatnya latensi, seperti gerakan kursor yang tersendat saat beban kerja tinggi.

3. Analisis Mekanisme Virtualisasi (Peran Hypervisor)

Output dari perintah terminal uname -a dan free -h memberikan gambaran nyata mengenai peran hypervisor tipe-2 yang digunakan oleh VirtualBox.

Dalam hal abstraksi perangkat keras, sistem operasi tamu (Ubuntu) seolah-olah memiliki kendali penuh atas sumber daya seperti RAM 4GB dan sejumlah core CPU tertentu. Padahal, seluruh sumber daya tersebut secara fisik tetap dimiliki oleh sistem operasi host, yaitu Windows 11. VirtualBox berfungsi sebagai lapisan perantara yang menyediakan ilusi perangkat keras fisik bagi guest OS.

Selain itu, pengujian juga menunjukkan adanya isolasi kegagalan (fault isolation). Ketika Ubuntu berada pada kondisi beban tinggi, penggunaan memori pada sisi host memang meningkat. Namun, apabila VM mengalami hang atau crash, sistem host tetap berjalan normal tanpa mengalami kegagalan sistem. Hal ini menegaskan bahwa alokasi memori VM bersifat terisolasi dan berada dalam lingkungan sandbox yang aman.

---

## Kesimpulan
1. Manajemen memori pada VM sangat bergantung pada alokasi RAM, di mana keterbatasan memori menyebabkan penggunaan swap secara intensif. Kondisi ini menurunkan performa sistem dan dapat memicu thrashing, sehingga respons sistem menjadi lambat saat beban kerja tinggi.

2. Konfigurasi prosesor multi-core meningkatkan kinerja multitasking, karena penjadwalan proses dapat dilakukan secara paralel. Dibandingkan satu core, penggunaan dua core mampu mengurangi overhead context switching dan meningkatkan responsivitas sistem.

3. Hypervisor tipe-2 (VirtualBox) mampu menyediakan abstraksi dan isolasi yang efektif, sehingga guest OS dapat berjalan seolah-olah memiliki perangkat keras sendiri, tanpa memengaruhi stabilitas sistem operasi host meskipun terjadi beban tinggi atau kegagalan pada VM.
---

## Quiz
1. Perbedaan OS Host dan OS Tamu

OS host adalah sistem operasi utama yang berjalan langsung di perangkat keras fisik dan mengelola seluruh resource.
OS tamu adalah sistem operasi yang berjalan di dalam mesin virtual dan menggunakan resource yang dialokasikan oleh OS host melalui hypervisor.

2. Peran Hypervisor dalam Virtualisasi

Hypervisor berfungsi mengelola dan membagi sumber daya hardware kepada Virtual Machine, menyediakan abstraksi perangkat keras, serta menjaga isolasi antara OS host dan OS tamu.

3. Alasan Virtualisasi Meningkatkan Keamanan

Virtualisasi meningkatkan keamanan karena setiap sistem berjalan secara terisolasi. Jika OS tamu mengalami gangguan atau serangan, dampaknya tidak memengaruhi OS host maupun VM lain.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
