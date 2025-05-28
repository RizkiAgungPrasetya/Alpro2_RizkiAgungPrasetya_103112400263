<h1 align="center">Laporan Praktikum Modul 11 <br> PENCARIAN NILAI ACAK </h1>
___
<h4 align="center">RIZKI AGUNG PRASETYA - 103112400263 </h4>
### Dasar Teori Pencarian Nilai Acak

Pencarian secara sekuensial ini adalah pencarian yang dilakukan dari data pertama, kedua hingga terakhir secara satu persatu dan berurutan. Ciri khas dari pencarian ini adalah proses pencarian akan berhenti ketika data yang dicari ditemukan, walaupun masih terdapat data yang belum dicek nilainya. Algoritma ini dikenal dengan nama Sequential Search, karena prosesnya melakukan pengecekan setiap elemen array secara satu persatu dan sekuensial dari data pertama hingga ditemukan atau data terakhir. algoritma binary search untuk array terurut membesar (ascending) akan berbeda dengan terurut mengecil (descending), sehingga algoritma ini tidak akan berjalan apabila terbalik. Misalnya array terurut secara membesar, tetapi algoritma binary search yang digunakan untuk array terurut mengecil. Hal ini mengakibatkan pencarian binary search tidak akan berhasil. Selanjutnya bagaimana contoh algoritma pencarian data apabila dituliskan ke dalam suatu fungsi pencarian dan diketahui array terurut secara mengecil atau descending.

___

## Guided

#### Soal 1
```go
package main

import "fmt"

func cariBarang(daftar []string, x string) bool {
    for _, barang := range daftar {
        if barang == x {
            return true
        }
    }
    return false
}

func main() {
    var n int
    var barangDicari string

    fmt.Print("Masukkan jumlah barang: ")
    fmt.Scan(&n)

    daftarBarang := make([]string, n)
    fmt.Println("Masukkan nama-nama barang:")
    for i := 0; i < n; i++ {
        fmt.Scan(&daftarBarang[i])
    }

    fmt.Print("Masukkan nama barang yang dicari: ")
    fmt.Scan(&barangDicari)

    ditemukan := cariBarang(daftarBarang, barangDicari)

    fmt.Println(ditemukan)
}
```
![](gd1.png)
>Code di atas adalah program yang mencari apakah sebuah barang ada dalam daftar barang yang dimasukkan oleh user. Dimulai dengan input jumlah barang yang ingin dimasukkan, kemudian pengguna diminta untuk menginputkan nama barang tersebut ke dalam array. Setelah itu, program meminta user untuk memasukkan nama barang yang ingin dicari. Fungsi cariBarang akan memeriksa setiap item dalam daftar barang, dan jika barang yang dicari ditemukan, fungsi ini mengembalikan nilai true, sebaliknya false jika tidak ditemukan. Hasil pencarian akan ditampilkan di layar.


#### Soal 2
```go
package main

import "fmt"

func main() {
    var kalimat string
    var karakter rune
    var cari []int

    kalimat = "algoritma pemograman"
    karakter = 'a'

    for i, ch := range kalimat {
        if ch == karakter {
            cari = append(cari, i)
        }
    }

    if len(cari) > 0 {
        fmt.Printf("Karakter ditemukan pada indeks: ")
        for i := 0; i < len(cari); i++ {
            fmt.Printf("%d ", cari[i])
        }
    } else {
        fmt.Println("Karakter tidak ditemukan.")
    }
}
```
![](Output/gd2.png)
>Code di atas adalah program untuk mencari semua posisi indeks dari karakter tertentu dalam sebuah kalimat. Dimulai dengan mendeklarasikan variabel kalimat yang berisi string "algoritma pemograman" dan variabel karakter yang diisi dengan karakter 'a'. Program kemudian menggunakan perulangan for dengan range untuk memeriksa setiap karakter dalam string dan membandingkannya dengan karakter yang dicari. Jika karakter ditemukan, indeksnya akan disimpan dalam slice cari. Setelah perulangan selesai, program akan menampilkan semua indeks tempat karakter ditemukan. Jika tidak ditemukan, program akan menampilkan pesan bahwa karakter tidak ditemukan.


#### Soal 3
```go
package main

import "fmt"

type Mahasiswa struct {
    nama string
    nim  string
}

func binarySearch(mahasiswa []Mahasiswa, nimCari string) int {
    kecil := 0
    besar := len(mahasiswa) - 1

    for kecil <= besar {
        mid := (kecil + besar) / 2
        
        if mahasiswa[mid].nim == nimCari {
            return mid
        } else if mahasiswa[mid].nim < nimCari {
            kecil = mid + 1
        } else {
            besar = mid - 1
        }
    }
    return -1
}

func main() {
    var X string

    mahasiswa := []Mahasiswa{
        {nama: "Andi", nim: "220001"},
        {nama: "Budi", nim: "220002"},
        {nama: "Citra", nim: "220003"},
        {nama: "Dina", nim: "220004"},
    }

    X = "220003"
    fmt.Println("Data mahasiswa:", mahasiswa)

    index := binarySearch(mahasiswa, X)

    if index != -1 {
        fmt.Printf("Data ditemukan di array index %d\n", index)
    } else {
        fmt.Println("Mahasiswa dengan NIM tersebut tidak ditemukan.")
    }
}
```
![](Output/gd3.png)
>Code di atas menggunakan algoritma binary search untuk mencari mahasiswa berdasarkan NIM dalam slice. Program mendeklarasikan tipe Mahasiswa dengan atribut nama dan nim. Fungsi binarySearch mencari  mahasiswa yang memiliki NIM tertentu dengan membandingkan NIM secara berulang. Di fungsi main, data mahasiswa dimasukkan ke dalam slice, dan program mencari NIM "220003", kemudian menampilkan jika ditemukan atau memberi tahu bahwa NIM tidak ditemukan.



___
## Unguided

### soal 1

Pada pemilihan ketua RT yang baru saja berlangsung, terdapat 20 calon ketua yang bertanding memperebutkan suara warga. Perhitungan suara dapat segera dilakukan karena warga cukup mengisi formulir dengan nomor dari calon ketua RT yang dipilihnya. Seperti biasa, selalu ada pengisian yang tidak tepat atau dengan nomor pilihan di luar yang tersedia, sehingga data juga harus divalidasi. Tugas Anda untuk membuat program mencari siapa yang memenangkan pemilihan ketua RT.

Buatlah program pilkart yang akan membaca, memvalidasi, dan menghitung suara yang diberikan dalam pemilihan ketua RT tersebut.
Masukan hanya satu baris data saja, berisi bilangan bulat valid yang kadang tersisipi dengan data tidak valid. Data valid adalah integer dengan nilai di antara 1 s.d. 20 (inklusif). Data berakhir jika ditemukan sebuah bilangan dengan nilai 0.

Keluaran dimulai dengan baris berisi jumlah data suara yang terbaca, diikuti baris yang berisi berapa banyak suara yang valid. Kemudian sejumlah baris yang mencetak data para calon apa saja yang mendapatkan suara.

```go
package main

import "fmt"

const batasCln = 20

func suara() ([]int, int) {
    var suara int
    var input []int

    fmt.Println("Masukkan suara:")

    for {
        fmt.Scan(&suara)
        if suara == 0 {
            break
        }
        input = append(input, suara)
    }
    return input, len(input)
}

  
func hitungHasil(input []int, totalMasuk int, perolehan *[]int) int {
    var totalSah int
    for j := 0; j < totalMasuk; j++ {
        s := input[j]
        if s >= 1 && s <= batasCln {
            (*perolehan)[s]++
            totalSah++
        }
    }
    return totalSah
}

func main() {
    var perolehan = make([]int, batasCln+1)

    input, totalMasuk := suara()

    totalSah := hitungHasil(input, totalMasuk, &perolehan)

    fmt.Print("Suara masuk: ", totalMasuk)
    fmt.Println("\nSuara sah: ", totalSah)

    for k := 1; k <= batasCln; k++ {
        if perolehan[k] > 0 {
            fmt.Printf("%d: %d\n", k, perolehan[k])
        }
    }
}
```
![](Output/gambar1.png)
  
>Code ini adalah program buat ngitung hasil pemilu versi simpel. Pertama, fungsi suara bakal minta user inputin suara, terus bakal stop kalau user ketik angka 0. Semua suara yang dimasukin disimpen di dalam list input, terus dihitung panjangnya pake len(input). Setelah itu, fungsi hitungHasil bakal ngecek satu-satu suara yang masuk, kalau suaranya valid (antara 1 sampai 20), bakal dihitung dan dimasukin ke dalam list perolehan. Di akhir, fungsi ini ngembaliin jumlah suara sah. Di bagian main, hasilnya langsung ditampilin, mulai dari total suara yang masuk, total suara sah, sampe siapa yang menang dan berapa banyak suaranya. 

### soal 2

Berdasarkan program sebelumnya, buat program pilkart yang mencari siapa pemenang pemilihan ketua RT. Sekaligus juga ditentukan bahwa wakil ketua RT adalah calon yang mendapatkan suara terbanyak kedua. Jika beberapa calon mendapatkan suara terbanyak yang sama, ketua terpilih adalah dengan nomor peserta yang paling kecil dan wakilnya dengan
nomor peserta terkecil berikutnya.

Masukan hanya satu baris data saja, berisi bilangan bulat valid yang kadang tersisipi dengan data tidak valid. Data valid adalah bilangan bulat dengan nilai di antara 1 s.d. 20 (inklusif). Data berakhir jika ditemukan sebuah bilangan dengan nilai 0.

Keluaran dimulai dengan baris berisi jumlah data suara yang terbaca, diikuti baris yang berisi berapa banyak suara yang valid. Kemudian tercetak calon nomor berapa saja yang menjadi pasangan ketua RT dan wakil ketua RT yang baru.

```go
package main

import "fmt"

const (
    maxCalon = 20
)  

func kotakSuara() ([]int, int) {
    var suara int
    var input []int

    fmt.Println("Masukkan suara:")
    for {
        fmt.Scan(&suara)
        if suara == 0 {
            break
        }
        input = append(input, suara)
    }
    return input, len(input)
}

func hitung(input []int, totalMasuk int, perolehan []int) int {
    var totalSah int
    
    for j := 0; j < totalMasuk; j++ {
        s := input[j]
        if s >= 1 && s <= maxCalon {
            perolehan[s]++
            totalSah++
        }
    }
    return totalSah
}

func cariKetuaWakil(perolehan []int) (int, int) {
    var ketua, wakil int
    var max1, max2 int

    for i := 1; i <= maxCalon; i++ {
        suara := perolehan[i]
        if suara > max1 {
            max2 = max1
            wakil = ketua
            max1 = suara
            ketua = i
        } else if suara == max1 && i < ketua {
            max2 = max1
            wakil = ketua
            ketua = i
        } else if suara > max2 {
            max2 = suara
            wakil = i
        } else if suara == max2 && i < wakil && i != ketua {
            wakil = i
        }
    }
    return ketua, wakil
}

func main() {
    perolehan := make([]int, maxCalon+1)

    input, totalMasuk := kotakSuara()
    totalSah := hitung(input, totalMasuk, perolehan)

    fmt.Printf("Suara masuk: %d\n", totalMasuk)
    fmt.Printf("Suara sah: %d\n", totalSah)

    ketua, wakil := cariKetuaWakil(perolehan)

    if totalSah > 0 {
        fmt.Printf("Ketua RT: %d\n", ketua)
        if wakil > 0 {
            fmt.Printf("Wakil ketua: %d\n", wakil)
        }
    }
}
```
![](Output/gambar2.png) 
>Code ini adalah program untuk ngitung hasil pemilihan ketua dan wakil ketua. Pertama, di fungsi kotakSuara, user diminta input suara yang dimulai dari angka 1 sampai 20, dan stop ketika angka 0 dimasukkan. Semua suara yang valid disimpan dalam array dan dihitung.
>
>Fungsi hitung ngecek suara yang valid dan ngitung suara sah yang masuk. Setelah itu, di fungsi cariKetuaWakil, kita tentuin ketua dan wakil berdasarkan suara terbanyak, kalau ada yang sama, ketua yang nomor kecil yang menang.
>
>Terakhir, di main, hasil suara masuk, suara sah, dan siapa ketua sama wakil ketua yang terpilih ditampilin.

### soal 3

Diberikan n data integer positif dalam keadaan terurut membesar dan sebuah integer lain k, apakah bilangan k tersebut ada dalam daftar bilangan yang diberikan? Jika ya, berikan indeksnya, jika tidak sebutkan "TIDAK ADA".

Masukan terdiri dari dua baris. Baris pertama berisi dua buah integer positif, yaitu n dan k. n menyatakan banyaknya data, dimana 1 < n <= 1000000. k adalah bilangan yang ingin dicari. Baris kedua berisi n buah data integer positif yang sudah terurut membesar.

Keluaran terdiri dari satu baris saja, yaitu sebuah bilangan yang menyatakan posisi data yang dicari (k) dalam kumpulan data yang diberikan. Posisi data dihitung dimulai dari angka 0. Atau memberikan keluaran "TIDAK ADA" jika data k tersebut tidak ditemukan dalam kumpulan.
Program yang dibangun harus menggunakan subprogram dengan mengikuti kerangka yang sudah diberikan berikut ini.

```go
package main

import "fmt"

const NMAX = 1000000
var data [NMAX]int

func isiArray(n int) {
    for i := 0; i < n; i++ {
        fmt.Scan(&data[i])
    }
}

func posisi(n, k int) int {
    low := 0
    high := n - 1

    for low <= high {
        mid := (low + high) / 2
        if data[mid] == k {
            return mid
        } else if data[mid] < k {
            low = mid + 1
        } else {
            high = mid - 1
        }
    }
    return -1
}

func main() {
    var n, k int

    fmt.Scan(&n, &k)
    
    isiArray(n)
    
    idx := posisi(n, k)
    
    if idx == -1 {
        fmt.Println("tidak ada")
    } else {
        fmt.Println(idx)
    }
}
```

![](Output/gambar3.png)
>Code ini adalah program nyari posisi angka dalam array pakai binary search. Pertama, fungsi isiArray  ngisi array data dengan inputan sebanyak `n` dari user.
>
>Setelah itu, fungsi posisi bakal ngecek posisi angka k dalam array pake binary search. Intinya, kita cari angka di tengah-tengah array, kalau lebih kecil, geser ke kiri, kalau lebih besar, geser ke kanan, terus lanjut nyari sampe ketemu atau nggak.
>
>Di bagian main, program minta input jumlah elemen n sama angka yang dicari k, terus array diisi dan program langsung cari posisi angka itu. Kalau ketemu muncul posisi indeksnya, kalau nggak terdapat output "tidak ada"