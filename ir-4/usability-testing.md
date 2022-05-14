---
permalink: /ir-4/usability-testing
---

# Usability Testing and Evaluation

### Apa itu Usability Testing?

Setelah kita membuat suatu fitur untuk aplikasi kita, kita harus memeriksa apakah fitur tersebut sudah bejalan dengan baik. Salah satu cara untuk memeriksanya adalah dengan [testing](/ir-3/testing) dan menerapkan proses [TDD](/ir-1/tdd). Tetapi testing dan TDD saja tidak cukup karena testing dan TDD hanya memeriksa kebenaran sistem secara internal source code saja. Tetapi implementasi sebenarnya mungkin belum sempurna. Oleh karena itulah kita membutuhkan Usability Testing.

Usability testing adalah proses pengecekan penggunaan fitur secara langusng. Sehingga error apapun yang terjadi selama proses usability testing dapat langsung diketahui dan diperbaiki. Karena kalau tidak kita perbaiki, maka pasti pengguna akan mengalami error yang sama tersebut. Tentunya, sama dengan konsep coverage, semakin detil, banyak, dan lenkap usability test cases kita, maka kita bisa lebih memastikan bahwa aplikasi yang kita buat *error-free*.

### Bagaimana cara merancang usability test cases?

Sebuah test case yang baik memiliki beberapa komponen. Komponen-komponen tersebut adalah sebagai berikut.

1. **Test Case ID**

    Agar test cases kita lebih terorganisir, alangkah baiknya kalau kita memberi masing-masing test case sebuah ID yang unik antar satu test case dengan test case lainnya agar masing-masing test case dapat lebih mudah untuk diidentifikasi.

2. **Feature Details**

    Kita juga harus mencantumkan test case ini milik sprint keberapa dan user story yang mana. Kita juga harus mencantumkan test case ini milik subkomponen apa. Dengan begitu, kita bisa tahu test case ini dibuat untuk mengecek fitur apa.

3. **Test Case Priority**

    Kemudian kita harus menentukan seberapa penting test case ini dalam satuan tingkat prioritas. Ada beberapa tingkat prioritas test case, dengan yang paling tinggi proritasnya maka test case tersebut lebih penting dan harus dipastikan keberhasilannya secepat mungkin dan sebaik mungkin.

4. **Test Type**

    Ada 3 jenis test type: (1) Functionality, (2) UI/UX, dan (3) Security. Kita harus menentukan test case kita ini masuk ke dalam tipe yang mana. Test tipe functionality biasanya akan memeriksa fungsionalitas dari suatu fitur, memriksa apakah fitur tersebut sudah berjalan dengan benar. Test tipe UI/UX akan memeriksa segi tampilan dari fitur. Sedangkan tipe security akan memriksa keamanan dari fitur tersebut.

5. **Test Description**

    Kita juga harus mencantumkan deskripsi singkat tentang test ini yang disampaikan secara singkat, padat, dan jelas.

6. **Test Steps**

    Hal yang paling wajib adalah langkah-langkah pengerjaan test tersebut. Kita harus mencantumkan pre-kondisi dari test case ini apabila ada. Kemudian kita harus menjelaskan setiap langkah test dengan jelas agar tidak terjadi kesalahan ketika menjalankan test case tersebut.

7. **Expected Result**

    Terakhir, kita harus menjelaskan apa ekspektasi dari test case tersebut. Seperti apa kondisi yang diharapkan untuk terjadi dari test case tersebut.

### Seperti apa Usability Testing di proyek kami?

Kami melakukan usability testing pada setiap sprint. Kami membuat test cases untuk masing-masing user story pada sprint tersebut dan memeriksa semua fitur untuk user story tersebut. Masing-masing test case memiliki ID yang unik dan representatif sesuai dengan sprint, user story, fitur, dan tipe test. Setiap test cases juga memiliki deskripsi yang disampaikan secara singkat, padat, dan jelas beserta dengan langkah-langkah proses testing yang dismpaikan dengan jelas juga. Penjelasan ekspektasi test case juga tidak lupa kami cantumkan.

Selain itu, sebagai dokumentasi, kami juga mencatat waktu pelaksanaan test case beserta dengan nama orang yang menjalankan test tersebut. Kami juga mencatat semua masukan terhadap fitur yang sudah di-test tersebut.

```
Test Case ID: TC-8.1-U2
Sprint: 1
Story: 8
Feature ID: 1
Test Case Sub Component: Dashboard Tenaga Medis
Test Case Priority: P1
Test Type: UI/UX
Test Description: Dropdown menu untuk suatu tenaga medis
Test Step: 
 - Pre-Condition
    Pengguna berada di halaman dashboard tenaga medis
 - Steps
    1. Untuk suatu tenaga medis, klik dropdown di samping tabel
Expected Result: 
    Dropdown akan menyediakan akses ke beberapa fitur menu, antara lain:
     - Hapus tenaga medis
     - Mengubah informasi tenaga medis
Execution Date: 9 March 2022
Tester: Gabriel Enrique
```

> Contoh salah satu test case untuk usability testing kami
