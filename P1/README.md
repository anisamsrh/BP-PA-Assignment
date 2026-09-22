# Modul P1

## Mini Project : Foodie Special ID Generator
```bash
----------------------------------------------
|   
|   ID            : ??????????????
|   Name          : Agus
|   Favorite Food : Nasi Padang
|
----------------------------------------------
```
Tugas Anda aadalah membuat kode program untuk menghasilkan output di atas. Anda harus mendesain cara untuk mencipatakan ID yang unik berdasarkaan input karakteristik dari pemilik ID. Kriteria desain ID :
1. Minimal mengambil 3 input
2. Minimal sepanjang 10 karakter dengan kombinasi huruf-angka
3. Hasil akhir ID harus sudah pernah melalui proses konkantenasi {clue : menggunakan sprintf()} dan minimal 2 operasi
4. Tidak boleh menggunakan library selain stdio.h

### Contoh:
Input yang diambil : 
1. Nama => Agus
2. Favorite Drink => Milkshake
3. Umur => 21 tahun

Hasil ID : **A97921186S** (Inisial nama + (1000 - umur) + umur + (ASCII M + ASCII m => inisial favorite drink) + Akhiran nama)

## Problem Set
### SET 1
```bash
#include <stdio.h>

int main() {
    int sisi, luas;
    printf("Luas persegi adalah: %d", luas);
    return 0;
}
```
1. Mengapa output luas kemungkinan besar bukan 0 melainkan angka acak yang besar? Hubungkan jawaban Anda dengan konsep inisialisasi pada halaman 10.
2. Jika baris luas = sisi * sisi; ditambahkan tepat setelah deklarasi, apakah masalah selesai? Jelaskan urutan eksekusi yang benar.

### SET 2
```bash
int nilai_tugas = 85;
int nilai_uts = 80;
float rata_rata = (nilai_tugas + nilai_uts) / 2;
printf("Rata-rata: %d", rata_rata);
```
1. Temukan dua kesalahan fatal pada kode di atas terkait penggunaan tipe data dan format specifier.
2. Apa yang akan tercetak di layar jika kode dijalankan tanpa perbaikan?
3. Perbaiki baris printf agar menampilkan output desimal yang benar.

### SET 3
```bash
int nomor_urut;
printf("Masukkan nomor: ");
scanf("%d", nomor_urut); // Baris ini bermasalah
```
1. Secara teknis, apa yang dikirimkan ke fungsi scanf() jika kita lupa menuliskan operator &? (Rujuk hal. 18).
2. Mengapa hal ini bisa menyebabkan program mengalami crash atau Segmentation Fault? Hubungkan dengan konsep alamat memori.

## Grading - Penilaian
Jika Anda mengerjakan sesuai instruksi dan aturan di [Petunjuk Tugas Asistensi](../README.md), nilai minimal Anda adalah 80. Nilai Anda akan bertambah sesuai keaktifan dan performa Anda selama sesi asistensi. \
**Nilai Asistensi Spesial 100** akan diberikan pada 1 orang dengan desain ID paling kreatif yang akan ditentukan di akhir sesi (tidak berlaku untuk susulan). 

