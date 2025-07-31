# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi
**Semester**: Genap / Tahun Ajaran 2024–2025
**Nama**: `<Febri Muhsinin>`
**NIM**: `<240202835>`
**Modul yang Dikerjakan**:
`Modul 2 – Penjadwalan CPU Lanjutan (Priority Scheduling Non-Preemptive)`

---

## 📌 Deskripsi Singkat Tugas

Modul ini berfokus pada modifikasi mekanisme penjadwalan proses dalam kernel **xv6-public**. Algoritma bawaan **Round Robin** diubah menjadi **Non-Preemptive Priority Scheduling**, dengan fitur:

* Penambahan atribut `priority` pada struktur proses.
* Implementasi syscall baru `set_priority(int)` untuk mengatur prioritas proses.
* Scheduler dimodifikasi agar selalu menjalankan proses RUNNABLE dengan prioritas tertinggi (angka terkecil).

---

## 🛠️ Rincian Implementasi

Langkah-langkah yang dilakukan antara lain:

* Menambahkan field `priority` ke dalam `struct proc` di `proc.h`.
* Inisialisasi nilai default `priority = 60` pada fungsi `allocproc()` di `proc.c`.
* Membuat system call `set_priority(int)`:

  * Tambah nomor syscall di `syscall.h`
  * Tambah deklarasi di `user.h` dan entri di `usys.S`
  * Registrasi syscall di `syscall.c`
  * Implementasi handler `sys_set_priority()` di `sysproc.c`
* Modifikasi fungsi `scheduler()` di `proc.c` agar memilih proses dengan prioritas tertinggi (terkecil) secara non-preemptive.
* Membuat program uji `ptest.c` untuk memverifikasi urutan eksekusi proses berdasarkan prioritas.
* Menambahkan `_ptest` ke daftar `UPROGS` di `Makefile`.

---

## ✅ Uji Fungsionalitas

Program pengujian yang digunakan:

* `ptest`: Memverifikasi bahwa proses dengan prioritas lebih tinggi (angka lebih kecil) dieksekusi lebih dulu, sesuai dengan konsep non-preemptive.

---

## 📷 Hasil Uji

### 📍 Contoh Output `ptest`

```
Child 2 selesai     
Child 1 selesai     
Parent selesai
```

---

## ⚠️ Kendala yang Dihadapi

* Lupa mengatur nilai default `priority` saat proses dibuat, menyebabkan nilai acak di scheduler.
* Kelupaan menambahkan syscall di `usys.S` menyebabkan error saat pemanggilan `set_priority()`.

---

## 📚 Referensi

* Dokumentasi xv6 MIT: [https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* Repositori xv6-public: [https://github.com/mit-pdos/xv6-public](https://github.com/mit-pdos/xv6-public)
* Diskusi praktikum, dokumentasi syscall di UNIX-like systems.

---
