# For Regular Students

## Mini Project
Tidak ada mini project untuk modul ini

## Problem Set
### Set 1
```c
#include <stdio.h>

int x = 10; 

void proses() {
    int x = 5; 
    x = x + 2;
}

int main() {
    printf("%d ", x);
    proses();
    printf("%d", x);
    return 0;
}
```
1. Berapakah nilai yang akan tercetak di layar saat program dijalankan? 
2. Mengapa pemanggilan fungsi proses(); tidak merubah nilai yang dicetak pada printf kedua? 

### Set 2
```c
#include <stdio.h>

int kali_dua(int a) {
    a = a * 2;
    return a;
}

int main() {
    int angka = 4;
    kali_dua(angka);
    printf("Hasil: %d", angka);
    return 0;
}
```
Jika program dijalankan, output yang muncul adalah Hasil: 4, bukan 8. 
1. Jelaskan secara teknis mengapa variabel angka di dalam main() tidak berubah! 
2. Bagaimana cara memperbaiki kode di dalam main() agar outputnya menjadi 8? 

### Set 3
```c
#include <stdio.h>

int main() {
    cetak_pesan();
    return 0;
}

void cetak_pesan() {
    printf("Halo dari fungsi!");
}
```

Program di atas akan menghasilkan pesan error atau warning saat dikompilasi (Build). 
1. Mengapa hal tersebut bisa terjadi? 
2. Perbaiki masalahnya! 

### Set 4
```c
#include <stdio.h>

int jumlahkan(int n) {
    if (n == 0) { 
        return 0;
    } else {
        return n + jumlahkan(n - 1);
    }
}

int main() {
    printf("%d", jumlahkan(-3));
    return 0;
}
```
Jika kita memanggil fungsi jumlahkan(-3) dengan argumen angka negatif seperti pada fungsi main() di atas, apa yang akan terjadi pada program tersebut? Hubungkan jawabanmu dengan konsep Base Case pada fungsi rekursi! 

### Set 5
```c
#include <stdio.h>

void cetak_angka(int n) {
    if (n > 0) { // Base case tersirat: berhenti jika n <= 0
        cetak_angka(n - 1); // Pemanggilan rekursif
        printf("%d ", n);
    }
}

int main() {
    cetak_angka(3);
    return 0;
}
```
1. Jika program tersebut dijalankan, apakah output yang tercetak di layar adalah 3 2 1 atau 1 2 3? Jelaskan secara teknis mengapa urutan angka tersebut yang tercetak!
2. Jika kita ingin mengubah output-nya menjadi urutan sebaliknya, bagian kode mana yang harus dipindahkan letaknya?
