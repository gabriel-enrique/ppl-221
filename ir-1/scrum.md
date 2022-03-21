---
permalink: /ir-1/scrum
---

# Scrum

### Apa itu scrum?

Scrum adalah salah salah satu metode pengembangan perangkat lunak di mana proses pengerjaan dilakukan secara 'keroyokan'. Istilah scrum sendiri memang datang dari permainan rugby, kondisi di mana semua pemain berusaha mendapatkan bola. Dalam kata lain, 'mengeroyok' bola. Konsep yang sama digunakan untuk scrum dalam konteks pengembangan perangkat lunak, di mana semua developer mengerjakan proyek secara 'keroyokan'.

![](https://upload.wikimedia.org/wikipedia/commons/1/1a/ST_vs_Gloucester_-_Match_-_23.JPG)

> Scrum di dalam permainan rubgy

Secara singkat, di dalam scrum, akan ada beberapa spesifikasi program yang diperlukan. Spesifikasi program tersebut dinamakan **Product Backlog**. Di dalam scrum ada satu aktivitas yang dinamakan **Sprint**. Nah, untuk masing-masing sprint, kita boleh bebas memilih product backlog mana yang ingin kita kerjakan, atau product backlog juga bisa dipecah menjadi **task** yang lebih kecil lagi. Di sinilah proses 'keroyokan' terjadi.

### Work flow di dalam scrum

Sebelum mengerti bagaimana cara kerja scrum, ada baiknya kalau kita tahu siapa saja peran yang ada di dalam scrum framework. Berikut adalah peran yang ada di dalam scrum framework:

- **Product owner**: Product owner, atau bisa disingkat PO, adalah 'pemilik' produk atau *software* yang kita kembangkan. Product owner adalah orang yang paling paham apa saja keperluan dari *software* yang ingin dikembangkan. PO biasanya merancang product backlog dari *software* yang sedang dikembangkan. Perlu diingat kalau PO harus berupa satu orang individual saja. Artinya, kalau misalnya aplikasi yang ingin dikembangkan akan dimiliki oleh suatu perusahaan dengan banyak pemimpin, hanya ada satu orang perwakilan saja yang bisa menjadi PO. Tentunya PO juga harus setidaknya mengerti garis besar secara teknis tentang aplikasi yang ingin dikembangkan agar proses pengembangan perangkat lunak dapat berjalan secara realistis juga.

- **Scrum master**: Scrum master adalah orang yang bertanggung jawab untuk memastikan bahwa scrum berjalan dengan lancar dan sesuai aturan. Scrum master harus bisa memantau bagaimana scrum-nya sedang berjalan. Apakah ada rintangan? Kalau ada, maka scrum master harus dengan cepat dan sigap menghilangkan rintangan tersebut. Scrum master harus bisa melihat masalah apa yang kira-kira dihadapi oleh dev team. Scrum master harus bisa mengatasi masalah tersebut secepatnya, agar proses scrum bisa berjalan terus dengan lancar.

- **Dev team**: Developer bertugas untuk menulis *source code* dari software yang dikerjakan. Dev team di dalam scrum pada umumnya merupakan kelompok-kelompok developer ataupun perorangan, tergantung demgam kebutuhan scrum. Masing-masing kelompok nantinya akan bekerja untuk mengerjakan task yang diberikan ke kelompokk mereka masing-masing. Masing-masing kelompok tentunya akan memiliki task yang berbeda antar satu sama lain.

Setelah mengetahui peran di dalam scrum, berikut adalah alur kerja dari scrum:

1. **Inisiasi**: Dalam fase ini, product backlog dari *software* yang akan dikembangkan akan dibuat. Product backlog biasanya dimulai dari beberapa *Epic* yang terbuat dari beberapa *User Story*. Epic pada dasarnya adalah garis besar fitur yang akan dibuat untuk aplikasi yang akan dibangun. Sedangkan, user story adalah fitur-fitur yang lebih detail dari Epic yang dibutuhkan oleh user. User mana yang membutuhkan fitur tersebut, apa fitur yang mereka inginkan, dan mengapa mereka membutuhkan fitur tersebut. User story juga harus dibarengi dengan acceptance criteria agar kita nanti bisa menilai apakah fitur yang dikembangkan sudah sesuai dengan kebutuhan user.

2. **Sprint Planning**: Sprint planning adalah fase di mana setiap product backlog akan dinilai bobotnya. Biasanya nilai bobot yang digunakan akan mengikuti deret Fibonacci.  Kemudian dari masing-masing product backlog tersebut, akan dipecah lagi menjadi task yang lebih kecil. Setelah itu, PO akan menentukan **sprint goal** untuk sprint yang akan dilakukan. Terakhir, masing-masing dari dev team akan memilih product backlog atau task yang akan dikerjakan pada sprint ini. Tentu saja product backlog yang dipilih harus sesuai dengan sprint goal yang sudah ditentukan oleh PO tadi.

3. **Sprint**: Pada fase ini, masing-masing dev team mulai menulis *source code* yang sesuai dengan product backlog atau task yang mereka pilih pada saat sprint planning. Semua dev team juga akan mengadakan rapat harian yang disebut dengan *Daily Standup Meeting*. Daily standup meeting adalah rapat yang membahas tentang progress dari pengembangan *software*. Di dalam daily standup meeting, masing-masing dev team akan membahas tentang apa saja yang sudah dilakukan semenjak daily standup meeting sebelumnya, lalu apa yang akan dilakukan sebelum daily standup meeting berikutnya, terakhir ada masalah apa yang dihadapi. Daily standup meeting ini sangat berguna untuk memantau progress dari sprint. Selain itu, permasalahan yang muncul juga dapat diselesaikan secepatnya.

4. **Sprint review** dan **sprint retrospective**: Terakhir, setelah sprint selesai, akan dilaksanakan sprint review di mana PO akan memilih fitur mana saja yang ingin diaplikasikan kepada software untuk release tersebut. PO di sini juga berhak untuk menolak fitur untuk release tersebut kalau memang dinilai demikian. Setelah itu baru dilakukan sprint retrospective yang berupa semacam 'refleksi' dari sprint yang baru saja dilakukan. Sprint retrospective akan membahas tentang apa saja yang sudah baik dilakukan pada saat sprint dan apa saja yang buruk dan juga membahas apa saja yang harus mulai atau lanjut untuk dilakukan dan juga apa yang harus diberhentikan. Dengan adanya sprint retrospactive ini, setiap sprint akan semakin efisien dan efektif lagi daripada sprint sebelumnya.

<p align="center">
  <img src="https://i0.wp.com/weshare.or.id/wp-content/uploads/2021/08/4005244-scaled.jpg?resize=2560%2C1707&ssl=1"/>
</p>

> Diagram alur kerja scrum. Sumber: [weshare.or.id](https://weshare.or.id/scrum-project-management-apakah-itu/)

### Penerapan scrum di proyek kami

Dalam mengembangkan aplikasi kami, kami juga menerapkan scrum framework sebagai pola kerja kami. Product owner kami adalah Auki dan scrum master kami adalah Hanif Arkan. Saya sendiri berperan sebagai developer. Sebelum kami melakukan sprint planning, kami semua memutuskan apa saja product backlog yang sesuai dengan bantuan dan arahan PO. Kemudian pada saat sprint planning, kami memilih product backlog atau task mana yang ingin kami kerjakan. Pada saat sprint berjalan, kami melakukan daily standup meeting setiap hari untuk memantau progress pengerjaan. Terakhir, setelah nanti sprint-nya selesai, kami akan melakukan sprint review dan juga tidak lupa sprint retrosepctive.

### Scrum di PPL 2021

Proses penerapan scrum di PPL 2021 (Kelas B) kurang lebih sama seperti yang sudah dijelaskan di atas. Kalau di PPL 2021 PO dan Scrum Master juga ikut menjadi bagian dari dev team. Akan ada 4 kali sprint untuk PPL 2021 yang masing-masing sprint akan memakan waktu selama 3 minggu. Sprint selama 3 minggu tersebut mencakup sprint planning, sprint itu sendiri dan juga sprint review. Sedangkan untuk fase inisiasi dilakukan di luar masa sprint, sebelum sprint pertama dimulai.

Di setiap sprint planning, akan dilakukan pembagian tugas task dan product backlog. Masing-masing anggota kelompok boleh memilih task dan product backlog mana yang mereka ingin kerjakan untuk sprint tersebut. Untuk fase sprint-nya sendiri, daily standup meeting yang dilakukan tidak setiap hari, namun cukup 2 kali seminggu. 

Nanti di pertengahan sprint, akan dilakukan user acceptance test untuk mengecek apakah fitur-fitur yang dibuat sudah sesuai dengan harapan. 

Kemudian di akhir sprint, baru dilakukan sprint review di mana nanti dosen dan asdos akan melihat secara keseluruhan seperti apa deliverables yang disampaikan, yang kemudian baru dilanjutkan dengan sprint retrospective di mana anggota kelompok melakukan refleksi dan evalasi dari sprint tersebut.
