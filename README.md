```html
Repository
	Modules
		Package  A
			File A1
			File A2

		Package B
			File B1
			File B2

1 Golang repository bisa terdiri dari 1 module atau lebih, tetapi umumnya hanya 1 module

Module adalah sekumpulan package yang dirilis bersamaan

Package adalah sekumpulan source code ( file ) dalam folder yang sama yang dikompile bersamaan

===============================================================================================

go.mod -> Mendeklarasikan module, sub module, dst

Module path berfungsi untuk sebagai:
1. prefix untuk import package package didalam module tersebut
2. Go akan cek melihat alamat tersebut untuk mengunduh code module tersebut


==============================================================================================
								GOPATH VS GOROOT VS GOJEK
==============================================================================================
https://golang.org/cmd/go/#hdr-GOPATH_environment_variable
https://www.jetbrains.com/help/go/configuring-goroot-and-gopath.html
https://stackoverflow.com/questions/7970390/what-should-be-the-values-of-gopath-and-goroot

GOPATH => untuk memberitahu dimana lokasi instalasi golang, supaya bisa menjalankan perintah go
GOROOT => Memberitau dimana SDK Go berada. Gaperlu diubah kecuali mau ubah versi go.
==============================================================================================

==============================================================================================
								First Golang Project
==============================================================================================
Buat sebuah folder bernama golang
go mod init github.com/onesinus/golang
Akan terbuat otomatis sebuah file go.mod yang isinya sebagai berikut
	go.mod
	module github.com/onesinus/golang
	go 1.15

Buat sebuah file hello.go dan isi dengan code ini
	package main

	import "fmt"

	func main() {
		fmt.Println("Hello, world.")
	}

jalankan perintah go install

	go install github.com/onesinus/golang

Kode go install module diatas akan membuat file binary yang dapat dijalankan
sehingga jika kita menjalankan perintah ini

	$HOME/go/bin/golang

Akan muncul Hello, world. 

Sesuai kode yang kita buat pada hello.go

Sekarang kita akan membuat sebuah folder ( module baru ) dan memanggil module tersebut dari file hello.go

buat sebuah folder bernama controllers dan buat sebuah file bernama HelloController.go dengan isi code sebagai berikut

	package controller

	import "fmt"

	func HelloMethod() {
		fmt.Println("Hello, world.")
	}

kemudian jalankan perintah go mod init github.com/onesinus/golang/controllers

pada go.mod didalam folder golang ( root folder ) tambahkan code untuk me-replace penggunaan code pada controller sementara masih proses develop code ( belum production )

	replace github.com/onesinus/golang/controllers => ./controllers

Sehingga keseluruhan code pada go.mod di root folder menjadi seperti ini

	module github.com/onesinus/golang

	go 1.15

	replace github.com/onesinus/golang/controllers => ./controllers

	require github.com/onesinus/golang/controllers v0.0.0-00010101000000-000000000000

```