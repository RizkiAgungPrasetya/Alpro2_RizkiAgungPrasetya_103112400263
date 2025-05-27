<h1 align="center">Laporan Praktikum Modul 12 & 13 <br> PENGURUTAN DATA </h1>
___
<h4 align="center">RIZKI AGUNG PRASETYA - 103112400263 </h4>
### Dasar Teori Pengurutan Data

Sorting adalah proses mengatur data dalam urutan tertentu, biasanya dalam urutan menaik atau menurun. Dalam konteks pemrograman, sorting sering diterapkan pada struktur data seperti array atau daftar untuk mengoptimalkan pencarian atau analisis data. Ada berbagai algoritma sorting, seperti bubble sort, quicksort, dan insertion sort, yang memiliki cara dan efisiensi yang berbeda-beda dalam mengatur elemen-elemen data. Proses ini tidak hanya membantu dalam pengorganisasian tetapi juga memungkinkan pengguna untuk memahami hubungan antar elemen data dengan lebih baik.

___

## Guided

### Soal 1

Diberikan n bilangan bulat positif. Buat program untuk mengurutkan angka ganjil secara membesar (ascending) dan angka genap secara mengecil (descending), lalu gabungkan hasilnya dengan ganjil duluan. Gunakan selection sort dalam proses pengurutan. Masukan: Baris pertama berisi bilangan bulat n (1 ≤ n ≤ 100). Baris kedua berisi n bilangan bulat positif.

Keluaran: Satu baris berisi angka ganjil terurut membesar diikuti angka genap terurut mengecil.

Contoh Masukan: 10 12 7 3 2 9 6 8 1 11 4 
Contoh Keluaran: 1 3 7 9 11 12 8 6 4 2

```go
package main

import "fmt"

func sorting(arr []int) []int {
    ganjil := []int{}
    genap := []int{}

    for i := 0; i < len(arr); i++ {
        if arr[i]%2 == 0 {
            genap = append(genap, arr[i])
        } else {
            ganjil = append(ganjil, arr[i])
        }
    }

    for i := 0; i < len(ganjil)-1; i++ {
        for j := i + 1; j < len(ganjil); j++ {
            if ganjil[j] < ganjil[i] {
                ganjil[i], ganjil[j] = ganjil[j], ganjil[i]
            }
        }
    }

    for i := 0; i < len(genap)-1; i++ {
        for j := i + 1; j < len(genap); j++ {
            if genap[j] > genap[i] {
                genap[i], genap[j] = genap[j], genap[i]
            }
        }
    }
    return append(ganjil, genap...)
}

func main() {
    angka := []int{12, 7, 3, 2, 9, 6, 8, 1, 11, 4}
    angkaTerurut := sorting(angka)
    fmt.Println(angkaTerurut)
}
```
![](guided1.png)
>Code di atas adalah sorting yang terdiri dari 2 function untuk menentukan ganjil genap pada sebuah array. Sorting di atas menggunakan sorting selection dimana terdapat perulangan di dalam perulangan dan terdapat percabangan untuk membedakan dan memisahkan antara angka ganjil dan angka genap


### Soal 2

Sebuah kelas memiliki sejumlah siswa yang telah mengikuti ujian. Tugas Anda adalah membuat program yang membaca nilai-nilai ujian siswa yang disimpan dalam struct berisi nim dan nilai, kemudian mengurutkan nilai-nilai tersebut dari yang tertinggi ke yang terendah menggunakan insertion sort. Masukan: Baris pertama berisi sebuah bilangan bulat n (1 ≤ n ≤ 100), yang menyatakan jumlah siswa. Baris kedua berisi n bilangan bulat, masing-masing mewakili nilai ujian siswa (0–100).Keluaran: Satu baris yang berisi nilai-nilai ujian yang sudah terurut dari yang terbesar ke yang terkecil.

Contoh Masukan: 6 75 60 90 80 100 65

Contoh Keluaran: 100 90 80 75 65 60

```go
package main

  

import "fmt"

  

type identitas struct {

    nama  string

    nilai int

}

  

func nilaiujian(arr []identitas) {

    var temp identitas

    for i := 1; i < len(arr); i++ {

        temp = arr[i]

        j := i

        for j > 0 && temp.nilai > arr[j-1].nilai {

            arr[j] = arr[j-1]

            j--

        }

        arr[j] = temp

    }

}

  

func main() {

    orang := []identitas{

        {"Fakhri", 75},

        {"Vito", 90},

        {"Hamam", 85},

        {"Dhany", 85},

        {"Rifa", 80},

  

    }

    nilaiujian(orang)

    for i := 0; i < len(orang); i++ {

        fmt.Println(orang[i].nama, ": ", orang[i].nilai)

    }

}
```
![](guided2.png)
>Code di atas adalah program yang mengurutkan daftar nilai ujian dari beberapa orang berdasarkan nilai tertinggi ke terendah.  Fungsi nilaiujian digunakan untuk mengurutkan  data identitas berdasarkan nilai ujian . sorting menggunakan insertion sort. Pada setiap eksekusi program, nilai yang lebih besar akan dipindahkan ke posisi yang lebih depan dalam slice sehingga akhirnya semua data terurut berdasarkan nilai ujian, dengan nilai tertinggi di posisi pertama.


___
## Unguided

### soal 1

Hercules, preman terkenal seantero ibukota, memiliki kerabat di banyak daerah. Tentunya Hercules sangat suka mengunjungi semua kerabatnya itu.

Diberikan masukan nomor rumah dari semua kerabatnya di suatu daerah, buatlah program rumahkerabat yang akan menyusun nomor-nomor rumah kerabatnya secara terurut membesar menggunakan algoritma selection sort.

Masukan dimulai dengan sebuah integer 𝒏 (0 < n < 1000), banyaknya daerah kerabat Hercules tinggal. Isi 𝒏 baris berikutnya selalu dimulai dengan sebuah integer 𝒎 (0 < m < 1000000) yang menyatakan banyaknya rumah kerabat di daerah tersebut, diikuti dengan rangkaian bilangan bulat positif, nomor rumah para kerabat.

Keluaran terdiri dari n baris, yaitu rangkaian rumah kerabatnya terurut membesar di masing-masing daerah.

```go
package main

import "fmt"

func Ngurutin(arr []int) {

    for i := 0; i < len(arr)-1; i++ {
        minIdx := i
        for j := i + 1; j < len(arr); j++ {
            if arr[j] < arr[minIdx] {
                minIdx = j
            }
        }
        arr[i], arr[minIdx] = arr[minIdx], arr[i]
    }
}

func MasukkanData() {
    var n int
    var data [][]int

    fmt.Scanln(&n)

    for i := 0; i < n; i++ {
        var row []int
        var jumlah int

        fmt.Scan(&jumlah)

        for j := 0; j < jumlah; j++ {
            var num int
            fmt.Scan(&num)
            row = append(row, num)
        }

        Ngurutin(row)

        data = append(data, row)
    }

    for i := range data {
        fmt.Println(data[i])
    }
}

func main() {
    MasukkanData()
}
```
![](MODUL%2012%20&%2013%20PENGURUTAN%20DATA/Output/soal1.png)
  
>Code di atas adalah program yang mengurutkan setiap baris array yang dimasukkan oleh user secara terpisah dan menampilkan hasilnya. Sorting yang digunakan adalah selection sort. Fungsi MasukkanData berfungsi untuk menerima input dari user. Program pertama-tama meminta jumlah baris array yang akan dimasukkan kemudian, untuk setiap baris, program akan meminta jumlah elemen pada baris tersebut, diikuti dengan memasukkan nilai-nilai elemen tersebut satu per satu. Setelah nilai-nilai dimasukkan, fungsi Ngurutin dipanggil untuk mengurutkan setiap baris array tersebut. Setiap baris yang sudah diurutkan kemudian ditambahkan ke dalam array  data.

### soal 2

Belakangan diketahui ternyata Hercules itu tidak berani menyeberang jalan, maka selalu diusahakan agar hanya menyeberang jalan sesedikit mungkin, hanya diujung jalan. Karena nomor rumah sisi kiri jalan selalu ganjil dan sisi kanan jalan selalu genap, maka buatlah program kerabat dekat yang akan menampilkan nomor rumah mulai dari nomor yang ganjil lebih dulu terurut membesar dan kemudian menampilkan nomor rumah dengan nomor genap terurut mengecil.

Format Masukan masih persis sama seperti sebelumnya.

Keluaran terdiri dari n baris, yaitu rangkaian rumah kerabatnya terurut membesar untuk nomor ganjil, diikuti dengan terurut mengecil untuk nomor genap, di masing-masing daerah.

```go
package main

import "fmt"

func Ngurutin(arr []int) {
    dataUrut := 0
    
    for i := 0; i < len(arr); i++ {
        if arr[i]%2 != 0 {
            arr[i], arr[dataUrut] = arr[dataUrut], arr[i]
            dataUrut++
        }
    }

    for i := 0; i < dataUrut-1; i++ {
        dataMin := i
        for j := i + 1; j < dataUrut; j++ {
            if arr[j] < arr[dataMin] {
                dataMin = j
            }
        }
        arr[i], arr[dataMin] = arr[dataMin], arr[i]
    }

    for i := dataUrut; i < len(arr)-1; i++ {
        dataMax := i
        for j := i + 1; j < len(arr); j++ {
            if arr[j] > arr[dataMax] {
                dataMax = j
            }
        }
        arr[i], arr[dataMax] = arr[dataMax], arr[i]
    }
}

func MasukkanData() {

    var n int
    var data [][]int

    fmt.Scanln(&n)

    for i := 0; i < n; i++ {
        var row []int
        var jumlah int
        
        fmt.Scan(&jumlah)

        for j := 0; j < jumlah; j++ {
            var num int
            
            fmt.Scan(&num)
            row = append(row, num)
        }

        Ngurutin(row)

        data = append(data, row)
    }

    for i := range data {
        fmt.Println(data[i])
    }
}

func main() {
    MasukkanData()
}
```
![](MODUL%2012%20&%2013%20PENGURUTAN%20DATA/Output/soal2.png) 
>Jadi, code di atas ini fungsinya buat ngurutin angka-angka. Pertama-tama, program bakal pisahin angka ganjil dan genap. Angka ganjil bakal dipindahin ke depan, terus setelah itu, angka ganjil diurutkan dari kecil ke besar pake  selection sort. Setelah itu, angka genap yang tersisa bakal diurutkan dari besar ke kecil.
>Fungsi `MasukkanData` itu buat input data dari user. Pertama-tama, dia minta jumlah baris array, terus tiap baris bakal diisi dengan angka sesuai jumlah yang diminta. Setiap baris yang udah diinput langsung diproses dan diurutkan sesuai aturan tadi.

> Terakhir, program bakal nampilin array yang udah diproses dan diurutkan. Jadi, intinya, ini semacam sorting tapi dengan trik misah-misahin angka ganjil dan genap, dan ngurutinnya beda-beda cara buat tiap jenisnya.

### soal 3

Kompetisi pemrograman yang baru saja berlalu diikuti oleh 17 tim dari berbagai perguruan tinggi ternama. Dalam kompetisi tersebut, setiap tim berlomba untuk menyelesaikan sebanyak mungkin problem yang diberikan. Dari 13 problem yang diberikan, ada satu problem yang menarik. Problem tersebut mudah dipahami, hampir semua tim mencoba untuk menyelesaikannya, tetapi hanya 3 tim yang berhasil. Apa sih problemnya?

"Median adalah nilai tengah dari suatu koleksi data yang sudah terurut. Jika jumlah data genap, maka nilai median adalah rerata dari kedua nilai tengahnya. Pada problem ini, semua data merupakan bilangan bulat positif, dan karenanya rerata nilai tengah dibulatkan ke bawah."
Buatlah program median yang mencetak nilai median terhadap seluruh data yang sudah terbaca, jika data yang dibaca saat itu adalah 0.

Masukan berbentuk rangkaian bilangan bulat. Masukan tidak akan berisi lebih dari 1000000 data, tidak termasuk bilangan 0. Data 0 merupakan tanda bahwa median harus dicetak, tidak termasuk data yang dicari mediannya. Data masukan diakhiri dengan bilangan bulat -5313.

Keluaran adalah median yang diminta, satu data per baris.

```go
package main

import "fmt"

func selectionSort(arr []int) {
    var i, j, minIdx, temp int

    for i = 0; i < len(arr)-1; i++ {
        minIdx = i
        for j = i + 1; j < len(arr); j++ {
            if arr[j] < arr[minIdx] {
                minIdx = j
            }
        }

        temp = arr[i]
        arr[i] = arr[minIdx]
        arr[minIdx] = temp

    }
}

func hitungMedian(data []int) int {
    var n, tengah, median int

    n = len(data)
    selectionSort(data)

    if n%2 == 1 {
        tengah = n / 2
        median = data[tengah]
    } else {
        tengah = n / 2
        median = (data[tengah-1] + data[tengah]) / 2
    }
    return median
}

  

func main() {

    var input int
    var data []int
    var salinan []int
    var hasil int

    for {
        fmt.Scan(&input)

        if input < 0 {
            break
        } else if input == 0 {
            if len(data) > 0 {
                salinan = make([]int, len(data))
                copy(salinan, data)
                hasil = hitungMedian(data)
                fmt.Println(hasil)
            }
        } else {
            data = append(data, input)
        }
    }
}
```

![](MODUL%2012%20&%2013%20PENGURUTAN%20DATA/Output/soal3.png)
> Code di atas ini adalah program untuk menghitung nilai median dari sekumpulan angka yang dimasukkan oleh user. Sorting menggunakan  selection sort untuk mengurutkan data sebelum menghitung median. Fungsi selectionSort digunakan untuk mengurutkan array dari kecil ke besar menggunakan. Setiap kali mencari elemen terkecil, elemen tersebut dipindahkan ke posisi yang sesuai. Fungsi hitungMedian menerima data yang sudah terurut, kemudian menghitung median. Kalau jumlah data ganjil, median adalah angka yang ada di tengah. Kalau jumlah data genap, median adalah rata-rata dari dua angka yang ada di tengah.


### soal 4

Buatlah sebuah program yang digunakan untuk membaca data integer seperti contoh yang diberikan di bawah ini, kemudian diurutkan (menggunakan metoda insertion sort), dan memeriksa apakah data yang terurut berjarak sama terhadap data sebelumnya.

Masukan terdiri dari sekumpulan bilangan bulat yang diakhiri oleh bilangan negatif. Hanya bilangan non negatif saja yang disimpan ke dalam array.

Keluaran terdiri dari dua baris. Baris pertama adalah isi dari array setelah dilakukan pengurutan, sedangkan baris kedua adalah status jarak setiap bilangan yang ada di dalam array. "Data berjarak x" atau "data berjarak tidak tetap".

```go
package main

import "fmt"

func urut(data []int) ([]int, string) {
    var jarak int = -1
    var dataAwal int = data[0]

    for i := 1; i < len(data); i++ {
        key := data[i]
        j := i - 1
        for j >= 0 && data[j] > key {
            data[j+1] = data[j]
            j--
        }
        data[j+1] = key
    }

    berjarkTetap := true

    for i := 1; i < len(data); i++ {
        dataAkhir := data[i]
        jarakData := dataAkhir - dataAwal

        if jarak == -1 {
            jarak = jarakData
        } else if jarakData != jarak {
            berjarkTetap = false
            break
        }

        dataAwal = dataAkhir
    }

    status := "Data berjarak acak"

    if berjarkTetap {
        status = fmt.Sprintf("Data berjarak %d", jarak)
    }

    return data, status
}

func main() {
    var input []int
    var num int

    for {
        fmt.Scan(&num)
        if num < 0 {
            break
        }
        input = append(input, num)
    }

    dataUrut, status := urut(input)

    fmt.Println(dataUrut)
    fmt.Println(status)
}
```

![](MODUL%2012%20&%2013%20PENGURUTAN%20DATA/Output/soal4.png)
>Code di atas adalah program untuk mengurutkan data yang dimasukkan oleh user, kemudian memeriksa apakah data yang dimasukkan memiliki jarak antar elemen. Sorting ini menggunakan algoritma insertion sort untuk mengurutkan data, dan setelah itu memeriksa apakah jarak antara angka-angka dalam data tetap sama atau acak. Fungsi urut pertama-tama mengurutkan data menggunakan insertion sort. Setelah itu, fungsi ini memeriksa apakah jarak antara elemen-elemen data tetap (misalnya, 2, 4, 6, 8, dst.) atau tidak. Jarak antara elemen dihitung berdasarkan selisih antara angka-angka yang berurutan dalam array. Jika jaraknya konsisten, maka program akan menyatakan bahwa data memiliki jarak tetap. Jika tidak, maka data dianggap memiliki jarak acak.


### soal 5

Kompetisi pemrograman yang baru saja berlalu diikuti oleh 17 tim dari berbagai perguruan tinggi ternama. Dalam kompetisi tersebut, setiap tim berlomba untuk menyelesaikan sebanyak mungkin problem yang diberikan. Dari 13 problem yang diberikan, ada satu problem yang menarik. Problem tersebut mudah dipahami, hampir semua tim mencoba untuk menyelesaikannya, tetapi hanya 3 tim yang berhasil. Apa sih problemnya?

"Median adalah nilai tengah dari suatu koleksi data yang sudah terurut. Jika jumlah data genap, maka nilai median adalah rerata dari kedua nilai tengahnya. Pada problem ini, semua data merupakan bilangan bulat positif, dan karenanya rerata nilai tengah dibulatkan ke bawah."
Buatlah program median yang mencetak nilai median terhadap seluruh data yang sudah terbaca, jika data yang dibaca saat itu adalah 0.

Masukan berbentuk rangkaian bilangan bulat. Masukan tidak akan berisi lebih dari 1000000 data, tidak termasuk bilangan 0. Data 0 merupakan tanda bahwa median harus dicetak, tidak termasuk data yang dicari mediannya. Data masukan diakhiri dengan bilangan bulat -5313.

Keluaran adalah median yang diminta, satu data per baris.

```go
package main

import "fmt"

const nMax = 7919

type Buku struct {
    id, judul, penulis, penerbit string
    eksemplar, tahun, rating     int
}

type DaftarBuku [nMax]Buku

func daftarkanBuku(pustaka *DaftarBuku, n *int) {
    fmt.Scan(n)
    for i := 0; i < *n; i++ {
        fmt.Scan(&(*pustaka)[i].id, &(*pustaka)[i].judul, &(*pustaka)[i].penulis, &(*pustaka)[i].penerbit, &(*pustaka)[i].eksemplar, &(*pustaka)[i].tahun, &(*pustaka)[i].rating)
    }
}

func cetakTerfavorit(pustaka DaftarBuku, n int) {
    terfavorit := pustaka[0]

    for i := 1; i < n; i++ {
        if pustaka[i].rating > terfavorit.rating {
            terfavorit = pustaka[i]
        }
    }

    fmt.Println("Buku terfavorit:")

    fmt.Printf(terfavorit.judul, terfavorit.penulis, terfavorit.penerbit, terfavorit.tahun, terfavorit.rating)
}

func urutBuku(pustaka *DaftarBuku, n int) {

    for i := 1; i < n; i++ {
        temp := (*pustaka)[i]
        j := i - 1
        for j >= 0 && (*pustaka)[j].rating < temp.rating {
            (*pustaka)[j+1] = (*pustaka)[j]
            j--
        }
        (*pustaka)[j+1] = temp
    }
}

func cetak5Terbaru(pustaka DaftarBuku, n int) {
    if n > 5 {
        n = 5
    }

    fmt.Println("\n5 Judul Buku dengan rating tertinggi:")
    
    for i := 0; i < n; i++ {
        fmt.Printf("%d. %s\n", i+1, pustaka[i].judul)
    }
}

func cariBuku(pustaka DaftarBuku, n, r int) {

    kiri, kanan := 0, n-1
    ditemukan := false
    
    var foundBooks []Buku

    for kiri <= kanan {
        tengah := (kiri + kanan) / 2
        if pustaka[tengah].rating == r {
            foundBooks = append(foundBooks, pustaka[tengah])
            i := tengah - 1
            for i >= 0 && pustaka[i].rating == r {
                foundBooks = append(foundBooks, pustaka[i])
                i--
            }
            i = tengah + 1
            
            for i < n && pustaka[i].rating == r {
                foundBooks = append(foundBooks, pustaka[i])
                i++
            }
            ditemukan = true

            break

        } else if pustaka[tengah].rating < r {
            kanan = tengah - 1
        } else {
            kiri = tengah + 1
        }
    }

    if ditemukan {
        fmt.Printf("\nBuku dengan rating %d ditemukan:\n", r)
        for i := 0; i < len(foundBooks); i++ {
            fmt.Printf("%s, %s, %s, %d, %d, %d\n", foundBooks[i].judul, foundBooks[i].penulis, foundBooks[i].penerbit, foundBooks[i].tahun, foundBooks[i].eksemplar, foundBooks[i].rating)
        }
    } else {
        fmt.Println("Tidak ada buku dengan rating seperti itu")
    }
}

func main() {
    var pustaka DaftarBuku
    var nPustaka, ratingCari int

    daftarkanBuku(&pustaka, &nPustaka)

    fmt.Scan(&ratingCari)

    urutBuku(&pustaka, nPustaka)

    cetakTerfavorit(pustaka, nPustaka)

    cetak5Terbaru(pustaka, nPustaka)

    cariBuku(pustaka, nPustaka, ratingCari)

}
```

![](MODUL%2012%20&%2013%20PENGURUTAN%20DATA/Output/soal5.png)
> Jadi, code di atas ini buat ngelola data buku, mulai dari daftar buku, ngurutkan berdasarkan rating, sampai nyari buku dengan rating tertentu. Pertama-tama, ada tipe data Buku yang nyimpen informasi kayak ID, judul, penulis, penerbit, tahun, rating, dan jumlah eksemplar buku. Fungsi daftarkanBuku buat input buku-buku ke dalam array pustaka yang ukurannya sampai 7919 buku. Fungsi `urutBuku` ngurutkan buku-buku itu berdasarkan rating, dari yang tertinggi ke terendah.

> Terus, ada fungsi cetakTerfavorit yang bakal nampilin buku dengan rating tertinggi (buku terfavorit). Fungsi cetak5Terbaru bakal nampilin 5 buku dengan rating tertinggi (kalau ada lebih dari 5). Terakhir, ada fungsi cariBuku yang nyari buku berdasarkan rating tertentu dan nampilin detailnya. Singkatnya, program ini buat ngatur data buku, nyortir berdasarkan rating, dan nyari buku dengan rating tertentu. Jadi cocok buat katalog buku atau perpustakaan deh!