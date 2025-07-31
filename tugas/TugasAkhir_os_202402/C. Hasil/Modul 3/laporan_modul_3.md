# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Egalian Lalintang>`
**NIM**: `<240202833>`
**Modul yang Dikerjakan**: Modul 3 – Manajemen Memori Tingkat Lanjut (Copy-on-Write dan Shared Memory

---

## 📌 Deskripsi Singkat Tugas

Melakukan modifikasi kernel xv6 untuk mengimplementasikan:

* Copy-on-Write Fork (CoW): Optimalisasi fork agar tidak langsung menyalin seluruh memori, melainkan hanya menyalin saat halaman diubah (write).

* Shared Memory: Menambahkan syscall shmget() dan shmrelease() agar dua proses dapat berbagi satu halaman memori, mirip dengan System V Shared Memory.

## 🛠️ Rincian Implementasi

* Menambahkan array ref_count[] dan fungsi incref() / decref() di vm.c

* Menambahkan flag PTE_COW di mmu.h untuk menandai halaman CoW

* Membuat fungsi cowuvm() di vm.c sebagai pengganti copyuvm()

* Mengubah fork() di proc.c agar menggunakan cowuvm()

* Menangani page fault dengan memeriksa PTE_COW di trap.c

* Mengubah semua kalloc()/ kfree() agar menggunakan reference counting yang sesuai

Shared Memory ala System V
* Menambahkan struktur global shmtab[] di vm.c untuk menyimpan shared memory (maks. 16 entri)

* Membuat syscall sys_shmget() dan sys_shmrelease() di sysproc.c

* Menambahkan syscall number baru di syscall.h

* Menambahkan deklarasi syscall di user.h dan usys.S

---

## ✅ Uji Fungsionalitas

cowtest Menguji fork() dengan teknik Copy-on-Write

shmtest Menguji shmget() dan shmrelease() antar proses




---

## 📷 Hasil Uji

Lampirkan hasil uji berupa screenshot atau output terminal. Contoh:

### 📍 Contoh Output `cowtest`:

```
Child sees: Y
Parent sees: X
```

### 📍 Contoh Output `shmtest`:

```
Child reads: A
Parent reads: B
```

Jika ada screenshot:

```
![hasil cowtest](./screenshots/cowtest_output.png)
```

---

## ⚠️ Kendala yang Dihadapi

Tuliskan kendala (jika ada), misalnya:

* Salah implementasi `page fault` menyebabkan panic
* Salah memetakan alamat shared memory ke USERTOP
* Proses biasa bisa akses audit log (belum ada validasi PID)

---

## 📚 Referensi

Tuliskan sumber referensi yang Anda gunakan, misalnya:

* Buku xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, GitHub Issues, diskusi praktikum

---

