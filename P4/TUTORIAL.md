# 🚀 Modul Tutorial untuk Asistensi : Struct & Pointer

**Studi Kasus:** Aplikasi CLI Minimarket & Membership

**Tujuan Pembelajaran:** Memahami cara manipulasi data langsung pada memori (*Pass by Reference*) dengan bahasa C.

Selamat datang di sesi asistensi! Kita akan mempelajari dua konsep terakhir yang sangat krusial di bahasa C (Pointer & Struct) secara bertahap, lalu menggabungkannya menjadi satu proyek akhir nyata.

## 1. 🎯 Materi Dasar Pointer

### Konsep Dasar (Wajib Paham!)

Pointer adalah variabel khusus yang tidak menyimpan sebuah nilai langsung (seperti angka 10), melainkan menyimpan **alamat memori** di mana nilai tersebut berada.

Dua operator sakti yang **wajib** kamu ketahui saat bermain dengan pointer:

* 📌 **Reference (`&`) - *Address-of Operator*:**
  Digunakan untuk **mengambil alamat** dari sebuah variabel.
  *(Analogi: "Di mana letak rumah Budi?")*

* 🔑 **Dereference (`*`) - *Value-at Operator*:**
  Digunakan untuk **mengakses atau mengubah isi/nilai** dari alamat yang ditunjuk oleh pointer.
  *(Analogi: "Buka pintu rumah di alamat tersebut, lalu ganti isinya!")*

### 💻 Hands-on 1: Membuat Pointer dan Menggunakannya

```
#include <stdio.h>

int main() {
    int angka = 10;
    // ptrAngka menyimpan alamat dari 'angka'. Gunakan simbol & (Reference)
    int *ptrAngka = &angka; 

    printf("Nilai angka awal: %d\n", angka);
    printf("Alamat memori angka: %p\n", &angka);
    
    // Menggunakan simbol * (Dereference) untuk melihat nilainya
    printf("Nilai yang ditunjuk ptrAngka: %d\n", *ptrAngka);

    // Mengubah nilai secara langsung ke memori aslinya via pointer
    *ptrAngka = 25;
    printf("\nNilai angka setelah diubah via pointer: %d\n", angka);

    // --- Pointer pada Array ---
    int arr[3] = {100, 200, 300};
    // Nama array itu sendiri sudah merepresentasikan alamat elemen pertama, jadi tidak perlu &
    int *ptrArr = arr; 
    printf("\nElemen pertama array: %d\n", *ptrArr);
    printf("Elemen kedua array: %d\n", *(ptrArr + 1));

    // 🎯 TODO MINI-CHALLENGE 1:
    // Coba ganti nilai elemen KETIGA array (angka 300) menjadi 999 menggunakan pointer ptrArr!
    // Tulis kodemu di bawah ini lalu print hasilnya:
    

    return 0;
}

```

### 💻 Hands-on 2: Beda *Pass by Reference* dan *Pass by Value*

Ini adalah alasan utama mengapa kita menggunakan pointer saat membuat sebuah fungsi!

```
#include <stdio.h>

// Pass by Value (Hanya mengirimkan fotokopian / salinan data)
void tambahValue(int x) {
    x = x + 10;
}

// Pass by Reference (Mengirimkan kunci akses ke alamat aslinya)
void tambahReference(int *x) {
    *x = *x + 10;
}

int main() {
    int nilai1 = 5;
    int nilai2 = 5;

    tambahValue(nilai1);
    printf("Setelah Pass by Value: %d (TIDAK BERUBAH)\n", nilai1);

    // Wajib pakai & untuk mengirimkan alamatnya
    tambahReference(&nilai2); 
    printf("Setelah Pass by Reference: %d (BERUBAH!)\n", nilai2);

    // 🎯 TODO MINI-CHALLENGE 2:
    // 1. Buat fungsi baru bernama 'kurangReference(int *x)' di atas int main().
    // 2. Buat fungsinya mengurangi nilai sebanyak 2.
    // 3. Panggil fungsi tersebut untuk mengurangi nilai2, lalu print hasilnya!
    

    return 0;
}

```

## 2. 📦 Materi Dasar Struct

### Konsep Dasar (Bungkus Variabel)

Struct digunakan untuk mengelompokkan beberapa variabel (bisa berbeda tipe data) ke dalam satu nama atau entitas. Bayangkan seperti membuat form pendaftaran yang punya kolom nama, umur, dan alamat.

> 💡 **PENTING: DOT (.) VS ARROW (->)**
>
> * Jika kamu mengakses variabel struct secara normal, gunakan **titik (`.`)**. Contoh: `mhs1.umur`
>
> * Jika kamu mengakses struct menggunakan **POINTER**, kamu **WAJIB** menggunakan **panah (`->`)**. Contoh: `ptrMhs->umur`. (Ini akan sangat berguna di proyek akhir kita nanti!).

*(Catatan: Di modul ini kita memakai `typedef struct` agar kodenya lebih singkat, jadi tidak perlu terus-terusan menulis awalan kata `struct`)*.

### 💻 Hands-on 1: Membuat dan Menggunakannya

```
#include <stdio.h>
#include <string.h>

typedef struct {
    char nama[50];
    int umur;
    // 🎯 TODO MINI-CHALLENGE 3 (Bagian 1):
    // Tambahkan atribut baru yaitu 'IPK' dengan tipe data float di sini!
} Mahasiswa;

int main() {
    Mahasiswa mhs1;
    
    // Ingat! Tipe data char array tidak bisa diisi pakai tanda = (sama dengan).
    // Kita WAJIB menggunakan strcpy (String Copy)
    strcpy(mhs1.nama, "Budi Santoso"); 
    mhs1.umur = 20;
    
    // 🎯 TODO MINI-CHALLENGE 3 (Bagian 2):
    // Berikan nilai IPK (misal: 3.85) untuk mhs1, lalu print bersama nama dan umurnya!

    printf("Nama: %s, Umur: %d\n", mhs1.nama, mhs1.umur);
    return 0;
}

```

### 💻 Hands-on 2: Membuat Nested Struct (Struct Bersarang)

```
#include <stdio.h>
#include <string.h>

typedef struct {
    char namaJalan[50];
    int kodePos;
} Alamat;

typedef struct {
    char nama[50];
    Alamat rumah; // Memasukkan struct Alamat ke dalam struct Karyawan
} Karyawan;

int main() {
    Karyawan k1;
    strcpy(k1.nama, "Anisa");
    strcpy(k1.rumah.namaJalan, "Jl. Raya ITS");
    k1.rumah.kodePos = 60111;

    printf("%s tinggal di %s (%d)\n", k1.nama, k1.rumah.namaJalan, k1.rumah.kodePos);
    
    // 🎯 TODO MINI-CHALLENGE 4:
    // Coba ubah kodePos rumah Anisa menjadi 60115, lalu print ulang kalimat di atas!

    return 0;
}

```

### 💻 Hands-on 3: Membuat Database Sederhana dengan Array

```
#include <stdio.h>

typedef struct {
    int id;
    int nilai;
} DataUjian;

int main() {
    // Inisialisasi instan untuk array of struct
    DataUjian kelas[3] = {
        {101, 85},
        {102, 90},
        {103, 78}
    };

    for(int i = 0; i < 3; i++) {
        printf("ID: %d - Nilai: %d\n", kelas[i].id, kelas[i].nilai);
    }

    // 🎯 TODO MINI-CHALLENGE 5:
    // Buat sebuah variabel 'totalNilai', lalu loop array 'kelas' untuk menjumlahkan semua nilainya.
    // Setelah loop selesai, print rata-rata nilainya!

    return 0;
}

```

## 3. 🏪 Tutorial Membangun Aplikasi CLI Minimarket

Sekarang waktunya menyatukan semua puzzle! Kita akan mulai membangun proyek utama menggunakan konsep Struct dan Pointer yang baru saja kita pelajari.

### Step 1: Membuat Struct yang Diperlukan

Kita membutuhkan `Barang` dan `Member`.

```
#include <stdio.h>
#include <string.h>

typedef struct {
    char nama[50];
    int harga;
    int stock;
} Barang;

typedef struct {
    char nama[50];
    int poin;
} Member;

int main() {
    printf("[STEP 1 OK] Struct Barang dan Member berhasil disiapkan.\n");
    return 0;
}

```

### Step 2: Membuat Database Dasar

Kita akan menginisialisasi 5 Barang dan 2 Member menggunakan *Array of Struct* di dalam fungsi `main()`.

```
#include <stdio.h>
#include <string.h>

// Deklarasi disembunyikan agar kita fokus pada data (Asumsikan struct di atas sudah ada)
typedef struct { char nama[50]; int harga; int stock; } Barang;
typedef struct { char nama[50]; int poin; } Member;

int main() {
    Barang dbBarang[5] = {
        {"Sabun", 5000, 10},
        {"Sampo", 15000, 5},
        {"Roti", 12000, 8},
        {"Susu", 25000, 15},
        {"Kopi", 22000, 20}
    };

    Member dbMember[2] = {
        {"Anisa", 500},
        {"Budi", 100}
    };

    printf("[STEP 2 OK] Database awal berhasil dimuat!\n");
    return 0;
}

```

### Step 3: Membuat Fungsi Transaksi (Pointer Beraksi!)

Di sini **Pointer bekerja!** Perhatikan penggunaan operator panah (`->`).

Fungsi ini akan memotong jumlah stok asli di memori, dan menambahkan poin member jika belanjaannya >= 20.000.

```
#include <stdio.h>

typedef struct { char nama[50]; int harga; int stock; } Barang;
typedef struct { char nama[50]; int poin; } Member;

// --- Fungsi Dasar Tampilan ---
void cekBarang(Barang db[], int ukuran) {
    printf("\n--- Katalog Barang ---\n");
    for(int i = 0; i < ukuran; i++) {
        printf("%d. %s - Rp%d (Stok: %d)\n", i+1, db[i].nama, db[i].harga, db[i].stock);
    }
}
void cekMember(Member db[], int ukuran) {
    printf("\n--- Data Member ---\n");
    for(int i = 0; i < ukuran; i++) {
        printf("%d. %s - Poin: %d\n", i+1, db[i].nama, db[i].poin);
    }
}

// --- FUNGSI UTAMA (Menggunakan Pointer) ---
// Menerima pointer Barang (*b) dan pointer Member (*m)
void beliBarang(Barang *b, Member *m, int qty) {
    if (b->stock >= qty) {
        b->stock -= qty; // Manipulasi memori asli via operator panah ->
        
        int total = b->harga * qty;
        printf("\n[TRANSAKSI BERHASIL] Membeli %d %s. Total: Rp%d\n", qty, b->nama, total);

        // Cek syarat poin & pastikan pointer member tidak kosong (NULL)
        if (total >= 20000 && m != NULL) {
            m->poin += 100;
            printf("[INFO] Selamat! Member %s mendapat +100 Poin!\n", m->nama);
        }
    } else {
        printf("\n[TRANSAKSI GAGAL] Stok %s tidak mencukupi!\n", b->nama);
    }
}

int main() {
    printf("[STEP 3 OK] Fungsi Transaksi berhasil dicompile!\n");
    return 0;
}

```

### Step 4: Menggabungkan Semuanya Menjadi Aplikasi CLI

Jalankan blok kode di bawah ini untuk melihat simulasi minimarket kita berjalan!

```
#include <stdio.h>
#include <string.h>

typedef struct { char nama[50]; int harga; int stock; } Barang;
typedef struct { char nama[50]; int poin; } Member;

void cekBarang(Barang db[], int ukuran) {
    printf("\n--- Katalog Barang ---\n");
    for(int i=0; i<ukuran; i++) {
        printf("%d. %s - Rp%d (Stok: %d)\n", i+1, db[i].nama, db[i].harga, db[i].stock);
    }
}
void cekMember(Member db[], int ukuran) {
    printf("\n--- Data Member ---\n");
    for(int i=0; i<ukuran; i++) {
        printf("%d. %s - Poin: %d\n", i+1, db[i].nama, db[i].poin);
    }
}
void beliBarang(Barang *b, Member *m, int qty) {
    if (b->stock >= qty) {
        b->stock -= qty;
        int total = b->harga * qty;
        printf("\n[TRANSAKSI] %d %s Terjual. Total: Rp%d\n", qty, b->nama, total);
        if (total >= 20000 && m != NULL) {
            m->poin += 100;
            printf("  -> Member %s mendapat +100 Poin!\n", m->nama);
        }
    } else {
        printf("\n[GAGAL] Stok %s (Tersisa: %d) tidak cukup untuk dibeli sebanyak %d!\n", b->nama, b->stock, qty);
    }
}

int main() {
    // 1. Setup Database
    Barang dbBarang[5] = { {"Sabun", 5000, 10}, {"Sampo", 15000, 5}, {"Roti", 12000, 8}, {"Susu", 25000, 15}, {"Kopi", 22000, 20} };
    Member dbMember[2] = { {"Anisa", 500}, {"Budi", 100} };

    printf("=== SELAMAT DATANG DI MINIMARKET =\n");
    cekBarang(dbBarang, 5);
    cekMember(dbMember, 2);

    // 2. Simulasi Transaksi
    // INGAT! Pakai simbol & (Reference) untuk me-passing alamat struct di dalam array!
    beliBarang(&dbBarang[3], &dbMember[1], 2); // Budi beli 2 Susu (50k) -> Dapat poin
    beliBarang(&dbBarang[0], &dbMember[0], 1); // Anisa beli 1 Sabun (5k) -> Ga dapat poin
    beliBarang(&dbBarang[2], NULL, 3);         // Pembeli tanpa member beli 3 Roti (36k)

    // 🎯 TODO MINI-CHALLENGE 6:
    // Coba simulasikan Budi membeli "Sampo" sebanyak 10 buah di bawah ini (Pasti akan gagal karena stok cuma 5).


    // 3. Buktikan bahwa data termodifikasi
    printf("\n= UPDATE DATA SETELAH TRANSAKSI ===");
    cekBarang(dbBarang, 5);
    cekMember(dbMember, 2);

    return 0;
}

```

## 🛠️ 4. TUGAS PRAKTIKUM: Tantangan Wajib

**PILIH 2 DARI 3 TANTANGAN BERIKUT:**
Tambahkan/modifikasi kode dari *Step 4* untuk mengimplementasikan fitur di bawah ini menggunakan konsep Pointer.

### 1. Update Harga Barang (Modifikasi Angka)

Buat fungsi `void updateHarga(Barang *b, int hargaBaru)` yang bisa dipanggil oleh Admin untuk merevisi harga suatu barang secara permanen.

> 💡 **TIPS UPDATE HARGA:**
>
> Kamu cukup melakukan reassignment nilai di dalam fungsi tersebut (contoh: `b->harga = hargaBaru`). Cobalah panggil fungsinya di `main` dan lihat perubahannya melalui fungsi `cekBarang`.

### 2. Update Nama Barang (Koreksi Typo)

Buat fungsi `void updateNama(Barang *b, char namaBaru[])`.

> 💡 **TIPS UPDATE STRING:**
>
> Ingat, di dalam bahasa C, kamu **TIDAK BISA** menimpa *array of char* langsung menggunakan tanda sama dengan (contoh: `b->nama = namaBaru` itu **SALAH**). Kamu wajib menggunakan pustaka `<string.h>` dan menggunakan fungsi `strcpy(b->nama, namaBaru)`.

### 3. Tukar Poin = Diskon (Logika)

Modifikasi logika dalam fungsi `beliBarang`. Jika member memiliki poin di atas atau sama dengan `1000`, maka otomatis berikan diskon 10% dari total belanjanya, dan poin member dikurangi 1000!

> 💡 **TIPS TUKAR POIN:**
>
> Tambahkan *if-statement* di dalam blok kode yang menangani total harga. Pastikan kamu mengecek apakah `m` tidak `NULL` terlebih dahulu, baru kemudian cek `m->poin >= 1000`. Jika ya, potong poin dengan `m->poin -= 1000` dan hitung ulang variabel `total`.

## 🏆 5. BONUS: Tantangan Tambahan

Bagi kamu yang ingin mendapatkan nilai maksimal (*A/A+*), selesaikan tantangan tambahan yang akan membuat aplikasimu terasa seperti program sungguhan!

### Menu Interaktif (Looping CLI)

Ubah program pada *Step 4* yang tadinya berjalan sekali dan langsung selesai secara statis, menjadi sebuah **aplikasi interaktif yang berjalan terus-menerus** hingga pengguna memilih opsi "Keluar".

> 💡 **TIPS EKSEKUSI TANTANGAN BONUS:**
>
> 1. **Gunakan Infinite Loop:** Bungkus seluruh alur logika yang ada di dalam fungsi `main()` (setelah inisialisasi database awal) ke dalam perulangan `while(1)` atau `do-while`.
>
> 2. **Buat Tampilan Menu:** Cetak navigasi menu menggunakan `printf` setiap kali *looping* dimulai.
>
>    Contoh: `[1] Lihat Barang | [2] Beli Barang | [3] Cek Member | [4] Keluar`
>
> 3. **Terima Input Pengguna:** Gunakan `scanf` untuk menangkap pilihan menu pengguna, kemudian manfaatkan `switch-case` untuk mengeksekusi instruksi sesuai nomor yang dipilih.
>
> 4. **Keluar dari Aplikasi:** Jika pengguna memilih menu 4, jalankan perintah `break;` untuk keluar dari perulangan, yang otomatis akan membuat program berhenti berjalan.