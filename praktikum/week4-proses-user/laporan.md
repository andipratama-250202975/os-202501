
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Andi Pratama  
- **NIM**   : 250202975  
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
Setelah menyelesaikan tugas ini, mahasiswa mampu:

1.Menjelaskan konsep proses dan user dalam sistem operasi Linux.
2.Menampilkan daftar proses yang sedang berjalan dan statusnya.
3.Menggunakan perintah untuk membuat dan mengelola user.
4.Menghentikan atau mengontrol proses tertentu menggunakan PID.
5.Menjelaskan kaitan antara manajemen user dan keamanan sistem.


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

## C. Langkah Pengerjaan
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).  
   - Pastikan Anda sudah login sebagai user non-root.  
   - Siapkan folder kerja:
     ```
     praktikum/week4-proses-user/
     ```

2. **Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
   - Jelaskan setiap output dan fungsinya.  
   - Buat user baru (jika memiliki izin sudo):
     ```bash
     sudo adduser praktikan
     sudo passwd praktikan
     ```
   - Uji login ke user baru.

3. **Eksperimen 2 – Monitoring Proses**
   Jalankan:
   ```bash
   ps aux | head -10
   top -n 1
   ```
   - Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.  
   - Simpan tangkapan layar `top` ke:
     ```
     praktikum/week4-proses-user/screenshots/top.png
     ```

4. **Eksperimen 3 – Kontrol Proses**
   - Jalankan program latar belakang:
     ```bash
     sleep 1000 &
     ps aux | grep sleep
     ```
   - Catat PID proses `sleep`.  
   - Hentikan proses:
     ```bash
     kill <PID>
     ```
   - Pastikan proses telah berhenti dengan `ps aux | grep sleep`.

5. **Eksperimen 4 – Analisis Hierarki Proses**
   Jalankan:
   ```bash
   pstree -p | head -20
   ```
   - Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`).  
   - Catat hasilnya dalam laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 4 - Manajemen Proses & User"
   git push origin main
   ```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
**Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
 - Jelaskan setiap output dan fungsinya.
  - `whoami` = Perintah whoami digunakan untuk menampilkan nama pengguna (username) yang sedang aktif atau login di sistem Linux.
     - Perintah `whoami` fungsinya untuk menampilkan nama pengguna yang sedang login di sistem.
     - Hasil `faiqatha` menunjukkan bahwa user yang sedang aktif atau menjalankan terminal bernama *faiqatha*.
 - ` id` = Perintah id fungsinya untuk menampilkan identitas pengguna dan grup yang sedang aktif di sistem Linux.
     - `uid=1000(faiqatha)` artinya user id fungsinya menunjukan id unik  user *faiqatha* yang sedang login. 
     - `gid=1000(faiqatha)` artinya group ID Utama fungsinya Menunjukkan ID grup utama tempat user *faiqatha* tergabung.
     - `groups=...` artinya grup tambahan fungsinya Menampilkan daftar grup lain yang memberi izin dan akses tertentu.


  - `groups` = Perintah groups digunakan untuk menampilkan daftar grup tempat user saat ini tergabung.

| Grup        | Arti                  | Fungsi                                                      |
| ----------- | --------------------- | ----------------------------------------------------------- |
| **adm**     | Administrator logs    | Dapat membaca file log sistem.                              |
| **dialout** | Serial port access    | Mengakses perangkat serial seperti modem.                   |
| **cdrom**   | CD/DVD access         | Mengakses dan menggunakan perangkat CD/DVD.                 |
| **floppy**  | Floppy access         | Mengakses disket (floppy drive).                            |
| **sudo**    | Superuser privileges  | Menjalankan perintah dengan hak akses administrator (root). |
| **audio**   | Audio devices         | Mengelola dan menggunakan perangkat suara.                  |
| **dip**     | Dial-up networking    | Mengatur koneksi jaringan manual (mis. PPP).                |
| **video**   | Video devices         | Mengakses perangkat grafis atau kamera.                     |
| **plugdev** | Plug and Play devices | Mengelola perangkat eksternal seperti USB drive.            |
| **users**   | General users         | Grup umum untuk semua pengguna biasa.                       |
| **netdev**  | Network devices       | Mengelola perangkat jaringan (Wi-Fi, Ethernet).             |

   - Perintah `sudo adduser praktikan` digunakan untuk menambah user baru bernama praktikan.

| Bagian                                          | Makna                                               | Fungsi                                                                                            |
| ----------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **sudo**                                        | Menjalankan perintah dengan hak akses administrator | Memungkinkan user biasa (*faiqatha*) menjalankan perintah yang memerlukan izin root.              |
| **adduser praktikan**                           | Menambahkan pengguna baru bernama *praktikan*       | Membuat akun baru di sistem Linux lengkap dengan home directory dan pengaturan awal.              |
| **[sudo] password for faiqatha:**               | Permintaan kata sandi pengguna                      | Sistem meminta password *faiqatha* untuk memastikan ia berhak menjalankan perintah sebagai admin. |
| **fatal: The user `praktikan' already exists.** | Pesan kesalahan                                     | Menunjukkan bahwa user bernama *praktikan* sudah ada, jadi tidak bisa dibuat lagi.                |

   - Perintah `sudo passwd` praktikan berfungsi untuk mengubah atau menetapkan password baru bagi akun praktikan.
     
| Baris Output                              | Makna                                                  | Fungsinya                                                                                |
| ----------------------------------------- | ------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| **sudo**                                  | Menjalankan perintah dengan hak akses administrator    | Memungkinkan user (misalnya *faiqatha*) mengubah password milik user lain (*praktikan*). |
| **passwd praktikan**                      | Mengatur atau mengubah password untuk user *praktikan* | Digunakan untuk menetapkan kata sandi baru pada akun tersebut.                           |
| **New password:**                         | Sistem meminta password baru                           | Admin mengetik kata sandi baru untuk user *praktikan*.                                   |
| **Retype new password:**                  | Konfirmasi ulang password                              | Memastikan password yang dimasukkan benar dan sama dengan sebelumnya.                    |
| **passwd: password updated successfully** | Password berhasil diperbarui                           | Menandakan proses penggantian kata sandi selesai tanpa error.                            |

---

 **Eksperimen 2 – Monitoring Proses**
  ```bash
   ps aux | head -10
   top -n 1
   ```
- Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.
  
| Kolom       | Arti                               | Fungsi                                                                                                                          |
| ----------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **USER**    | Nama pengguna pemilik proses       | Menunjukkan siapa yang menjalankan proses tersebut (misalnya `root` atau `faiqatha`).                                           |
| **PID**     | Process ID (Nomor proses)          | Nomor unik yang diberikan sistem untuk mengidentifikasi setiap proses.                                                          |
| **%CPU**    | Persentase penggunaan CPU          | Menunjukkan seberapa banyak CPU digunakan oleh proses tersebut. Semakin tinggi angkanya, semakin berat proses tersebut bekerja. |
| **%MEM**    | Persentase penggunaan memori (RAM) | Menunjukkan berapa banyak memori yang dipakai proses dibanding total RAM sistem.                                                |
| **COMMAND** | Nama atau perintah yang dijalankan | Menunjukkan program atau perintah apa yang sedang berjalan (contoh: `/sbin/init`, `systemd-journald`, `snapfuse`, dll).         |

   - USER: root → proses dijalankan oleh user root
   - PID: 59 → ID prosesnya 59
   - %CPU: 0.0 → hampir tidak menggunakan CPU
   - %MEM: 0.4 → menggunakan 0,4% dari RAM
   - COMMAND: /usr/lib/systemd/systemd-journald → nama program yang dijalankan.

---

**Eksperimen 3 – Kontrol Proses**
   - Catat PID proses `sleep`. 
     ```bash
     sleep 1000 &
     ps aux | grep sleep
     ```
      - Catat PID proses `sleep`.
     ```bash
     andi         944  0.0  0.0   3124  1068 pts/0    S    14:13   0:00 sleep 1000
     andi         946  0.0  0.1   4088  1968 pts/0    S+   14:13   0:00 grep --color=auto sleep
      ````
  - Hentikan proses:
     ```bash
    ` kill 964`
     -bash: syntax error near unexpected token `newline'
     [3]+  Terminated              sleep 1000
     ```
     
---

 **Eksperimen 4 – Analisis Hierarki Proses**
   Jalankan:
   ```bash
   pstree -p | head -20
   ```
   - Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`).  
   - Catat hasilnya dalam laporan.
   ```bash  
systemd(1)-+-agetty(199)
           |-agetty(217)
           |-cron(151)
           |-dbus-daemon(152)
           |-init-systemd(Ub(2)-+-SessionLeader(343)---Relay(345)(344)---bash(345)-+-head(968)
           |                    |                                                  |-pstree(967)
           |                    |                                                  |-sleep(944)
           |                    |                                                  `-sleep(950)
           |                    |-init(8)---{init}(9)
           |                    |-login(346)---bash(449)
           |                    `-{init-systemd(Ub}(10)
           |-polkitd(788)-+-{polkitd}(790)
           |              |-{polkitd}(791)
           |              `-{polkitd}(792)
           |-rsyslogd(192)-+-{rsyslogd}(246)
           |               |-{rsyslogd}(247)
           |               `-{rsyslogd}(255)
           |-systemd(435)---(sd-pam)(436)
           |-systemd-journal(59)
           |-systemd-logind(164)
   ```


  - Proses utama (induk) dalam sistem adalah `systemd (PID 1)`.Ini adalah proses pertama yang dijalankan saat sistem Linux booting.
  - Semua proses lain seperti `agetty`, `cron`, `dbus-daemon`, `rsyslogd`, dan `snapd` adalah turunan (child process) dari `systemd`.
  - Proses yang kamu jalankan di terminal (misalnya `pstree`, `head`, dan `sleep`) juga akhirnya diturunkan dari `systemd` melalui `bash` (shell yang kamu pakai).

---

## Kesimpulan
1. User dan Grup = Setiap pengguna punya ID unik dan grup untuk mengatur hak akses.
2. Perintah penting = `whoami`, `id`, `groups` untuk cek info user : `adduser`, `passwd` untuk menambah dan mengubah user/password.
3. Proses sistem = `ps` dan `top` untuk memantau proses, CPU, dan memori.

---
## D. Tugas & Quiz
### Tugas
1. Dokumentasikan hasil semua perintah dan jelaskan fungsi tiap perintah.
**Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
 - `whoami`
     - Perintah `whoami` digunakan untuk menampilkan nama pengguna (username) yang sedang aktif atau login di sistem Linux.Fungsi mengetahui identitas user yang sedang menjalankan terminal.
 - `id`
     - Perintah `id` digunakan untuk menampilkan identitas pengguna dan grup yang sedang aktif di sistem Linux. 
 - `groups`
    - Perintah `groups` digunakan untuk menampilkan daftar grup tempat user saat ini tergabung.

 **Eksperimen 2 – Monitoring Proses**
  ```bash
   ps aux | head -10
   top -n 1
   ```
- `ps aux | head -10`
   - Perintah ini menampilkan daftar proses yang sedang berjalan di sistem Linux. Perintah ini menampilkan daftar proses yang sedang berjalan di sistem Linux. digunakan untuk melihat semua proses aktif beserta pengguna, ID, dan sumber daya yang digunakan (CPU dan memori).Kolom-kolom seperti USER, PID, %CPU, %MEM, dan COMMAND membantu kita memantau dan mengelola proses yang berjalan di sistem Linux.
- `top -n 1`
   -Perintah top digunakan untuk memantau proses yang sedang berjalan secara real-time di sistem Linux — mirip seperti “Task Manager” di Windows.
  
**Eksperimen 3 – Kontrol Proses**
   ```bash
    sleep 1000 &
    ps aux | grep sleep
  ```
 ```bash
  kill <PID>
 ```
- `sleep 1000 &`
    - `sleep 1000`  memerintahkan sistem untuk *tidur* atau berhenti sejenak selama 1000 detik.
    -  `&` menandakan bahwa proses dijalankan di background, sehingga terminal tetap bisa digunakan untuk perintah lain
- `ps aux | grep sleep`
    - `ps aux`  menampilkan daftar lengkap semua proses yang sedang aktif.
    - `|`  pipe, digunakan untuk meneruskan output dari `ps aux` ke perintah berikutnya.
    - `grep sleep`  mencari teks *sleep* di hasil keluaran tersebut.
- `kill 494`
    - `kill` mengirim sinyal ke proses. Secara default mengirim sinyal `SIGTERM` untuk meminta proses berhenti dengan aman.
    - `494` nomor PID dari proses target yang ingin dihentikan.

     
2. Gambarkan hierarki proses dalam bentuk diagram pohon (`pstree`) di laporan.
   
 ```bash  
systemd(1)─┬─agetty(230)
            ├─cron(200)
            ├─dbus-daemon(201)
            ├─rsyslogd(227)
            ├─snapd(216)
            └─init-systemd(ub(2))─┬─SessionLeader(973)─┬─Relay(978)─┬─bash(978)─┬─head(1293)
                                                         ├─pstree(1292)
                                                         ├─sleep(1280)
                                                         └─sleep(1288)
  ```

3. Jelaskan hubungan antara user management dan keamanan sistem Linux.
  - User management dan keamanan sistem Linux saling berkaitan erat. Dengan pengaturan user, group, dan permission yang baik, administrator dapat mengontrol akses, melindungi data penting, mencegah kesalahan pengguna, dan memperkuat keamanan sistem secara keseluruhan.
   
4. Upload laporan ke repositori Git tepat waktu.


---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
