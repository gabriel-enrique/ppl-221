---
permalink: /ir-3/devops
---

# DevOps

### Apa itu DevOps?

Dalam mengembangkan perangkat lunak, kita pastinya ingin membawa perubahan dan penambahan fitur dengan cepat ke pengguna. Setiap hari, atau bahkan setiap jamnya, bisa ada perubahan baru yang bisa langsung dimanfaatkan oleh pengguna. Kalau begitu, idealnya adalah setiap kali kita melakukan perubahan, kita juga ingin langsung mengirim (*ship*) *software* kita ke pengguna. Tetapi, mengingat bahwa perubahan tersebut datang begitu cepat, akan merepotkan apabila setiap kali kita selesai menambahkan perubahan, kita juga harus sekalian melakukan *deployment*.

Di sinilah DevOps hadir sebagai 'alat' bantu. DevOps dapat digunakan untuk mengotomasi proses deployment tersebut setiap kali ada perubahan yang ditandai dengan adanya `push` ke repositori online. Kebanyakan repositori online memiliki fitur DevOps-nya sendiri-sendiri. GitLab punya GitLab CI, GitHub punya GitHub Actions, dan seterusnya. Untuk seterusnya, kita akan menggunakan GitLab CI sebagai contoh.

### Bagaimana cara kerja DevOps?

GitLab CI dapat dirancang agar berjalan secara otomatis ketika kita melakukan `push` ke GitLab. Ketika kita melakukan `push`, GitLab CI akan menjalankan sebuah Pipeline. Pipeline tersebut akan berisi serangkaian Jobs yang akan dijalankan oleh GitLab Runner. Berapa Job yang harus dikerjakan? Apa yang dikerjakan oleh Job tersebut? Itu semua bisa kita atur.

![](https://miro.medium.com/max/2625/1*0xThN67QmQrdTryi_XwCFQ.png)

> Alur DevOps menggunakan GitLab CI yang umum dilakukan. Sumber: [Implementasi Gitlab CI/CD untuk Test dan Deploy Aplikasi Laravel](https://medium.com/@davidhsianturi/implementasi-gitlab-ci-cd-untuk-test-dan-deploy-aplikasi-laravel-9c5dab7ce138)

Untuk mulai menggunakan GitLab CI, kita harus membuat file `.gitlab-ci.yml` di `root` project folder. File tersebutlah yang berisi alur dari Pipeline dan apa yang harus dikerjakan pada masing-masing Job. Kita bisa membuat alur pipeline kita sendiri. Mungkin kita hanya ingin menjalankan suatu Job jika dan hanya jika Job lainnya sudah selesai. Kita bisa mengatur hal tersebut di dalam file `.gitlab-ci.yml` tersebut. Kita juga bisa membuat Job sesuai dengan apa yang kita inginkan. Kita bisa merancang Job yang memastikan bahwa program kita menjalankan *test*-nya dengan benar, atau Job yang melakukan deployment secara otomatis, atau bahkan yang lainnya, dan hal ini bisa kita lakukan dengan mengatur file `.gitlab-ci.yml` tadi.

### Membangun file `.gitlab-ci.yml`

Kita bisa mulai dari memilih `image` untuk Pipeline kita. Image yang dimaksud adalah Docker Image, semacam sistem, yang nantinya akan digunakan sebagai sistem untuk menjalankan Pipeline tersebut. Misal kita sedang membuat aplikasi menggunakan Python dan Django, kita bisa langsung memilih `image` yang sesuai dengan aplikasi kita tersebut.

```yml
default:
  image: python:3.9.10-buster
```

Kita juga bisa mendaftarkan `stages` dari Pipeline kita. Misal Pipeline yang ingin kita bangun akan mengecek program kita sesuai dengan test yang ada dan jika berhasil maka program akan di-*deploy*. Maka kita butuh dua `stage`: `test` dan `deploy`. Tetapi perlu diingat bahwa untuk bisa menjalankan test, program kita harus di-`build` terlebih dahulu. Oleh karena itu, jangan lupa tambahkan juga stage `build`.

```yml
default:
  image: python:3.9.10-buster

stages:
    - build
    - test
    - deploy
```

Setelah itu, baru kita bisa memulai untuk membuat Job yang kita inginkan. Berikut adalah contoh Job yang dapat dirancang agar bisa memnuhi kebutuhan kita yang sudah dijelaskan sebelumnya.

```yml
default:
  image: python:3.9.10-buster

stages:
    - build
    - test
    - deploy

migrations:
    stage: build
    script:
        - python3 manage.py makemigrations
        - python3 manage.py migrate
        - python3 manage.py check

unit_testing:
    stage: test
    needs: ['migrations']
    script:
        - coverage run manage.py test
        - coverage report -m
        - coverage xml
```

> Untuk Job deployment, spesifikasi Job-nya bisa berbeda-beda, tergantung dari services yang kita gunakan untuk men-deploy aplikasi tersebut.

Kita bisa menspesifikasikan judul dari masing-masing Job, misal `migrations` dan `unit_testing`. Kita juga bisa menspesifikasikan masing-masing Job tersebut masuk ke dalam `stage` yang mana. Kalau ada suatu Job yang perlu Job lain untuk selesai terlebih dahulu sebelum memulai Job-nya sendiri, kita bisa mendaftarkan Job mana yang perlu ditunggu di dalam `needs`.

Bagian paling krusial dari suatu Job adalah `script`-nya. Di bagian `script` kita akan menulis perintah-perintah yang harus dijalankan. Tentunya perintah yang kita tulis harus sesuai dengan Job tersebut. Perintah-perintah pada bagian `script` berisi perintah yang selayaknya kita jalankan kalau ingin melakukan Job tersebut secara manual.

Tentunya masih banyak lagi pengaturan yang bisa kita gunakan untuk memodifikasi GitLab CI Pipeline agar bisa sesuai dengan kebutuhan kita. Pengaturan-pengaturan yang bisa kita atur dapat kita baca di dokumentasi GitLab CI.

### Penerapan DevOps di proyek kami

Proyek kami tentunya menggunakan bantuan GitLab CI agar kami bisa memeriksa kalau program kami berjalan dengan benar, sesuai dengan test yang sudah ada. Kami juga membutuhkan GitLab Ci untuk melakukan deployment ke server agar perubahan yang kami `push` ke repositori dapat langsung masuk juga ke server.

Sesuai dengan spesifikasi PPL 2021, ada beberapa pengaturan yang harus digunakan agar Pipeline kami sesuai dengan ketentuan. Pipeline yang berjalan ketika adanya `push` tidak akan sama untuk setiap branch. Bahkan kalau target branch nya saja berbeda jenis Pipeline yang berjalan juga bisa berbeda.

Untuk feature branch yang ingin di-merge ke PBI branch, kami hanya menjalankan test saja agar kami bisa memastikan bahwa program yang kami tulis memang lolos uji. Untuk PBI branch yang ingin di-merge ke staging, Pipeline akan menjalankan Job tambahan untuk melakukan sonarscan. Sedangkan untuk branch staging dan master, ada Job tambahan yang akan melakukan deployment ke staging environment dan release environment.

Dengan adanya GitLab CI ini, alur kerja kelompok kami menjadi lebih cepat dan efisien, karena ada banyak hal yang harus diperiksa dan dilakukan yang dapat dijalankan secara otomatis oleh Pipeline.
