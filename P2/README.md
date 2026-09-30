# Modul P2

## Mini Project
Tidak ada mini project untuk modul ini

## Problem Set
### Set 1
```c
int nilai = 2;
switch(nilai) {
    case 1: 
        printf("Satu ");
    case 2: 
        printf("Dua ");
    case 3: 
        printf("Tiga ");
    default: 
        printf("Lainnya ");
}
```
1. Apa output pasti dari program tersebut jika dijalankan dan mengapa hasilnya demikian?
2. Kode apa yang kurang dari pernyataan switch di atas? 

### Set 2
```c
for(int i = 1; i <= 5; i++) {
    if(i % 2 == 0) {
        continue;
    }
    printf("%d ", i);
}
```
1. Angka berapa saja yang akan tercetak di layar terminal? 
2. Jelaskan bagaimana continue mempengaruhi hasil tersebut! 

### Set 3
```c
int angka[4] = {10, 20, 30, 40};
int total = 0;
for(int i = 0; i <= 4; i++) {
    total += angka[i];
}
printf("Total: %d", total);
```
Program ini tidak akan mengalami error saat dikompilasi (Build), namun memiliki sebuah bug. Temukan bug tersebut dan jelaskan alasannya berdasarkan aturan indeks Array! 

### Set 4
Diberikan sebuah array 1D yang menyimpan 7 nilai ujian mahasiswa: 
```c
int nilai[7] = {85, 70, 95, 60, 78, 88, 92}; 
```

Buatlah program menggunakan perulangan for untuk mencari dan menampilkan:
1. Nilai tertinggi dari array tersebut.
2. Nilai terendah dari array tersebut.
3. Rata-rata dari seluruh nilai ujian tersebut (tampilkan dalam bilangan desimal 2 angka di belakang koma).

### Set 5
Diberikan sebuah matriks ordo 3x3 (Array 2D) sebagai berikut:
```c
int matriks[3][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```
Buatlah program menggunakan nested loop (perulangan bersarang) untuk menghitung dan mencetak jumlah dari elemen-elemen diagonal utamanya (yaitu elemen dari kiri atas ke kanan bawah: 1 + 5 + 9). 

