---
permalink: /ir-3/refactoring
---

# Refactoring

### Apa itu Refactoring?

Ketika menulis program, seringkali apa yang pertama kali kita tulis bukanlah program yang terbaik. Tidak jarang bahkan kita harus menulis ulang suatu bagian kode yang sama sampai berkali-kali sampai kita bisa mendapatkan kode yang benar dengan kualitas kode yang baik. Tetapi kita juga harus ingat, ketika mengubah bagian dari program agar bisa memiliki kualitas yang lebih baik, kita harus memastikan bahwa program tersebut masih berjalan dengan baik dan sesuai dengan yang seharusnya.

Proses mengubah bagian progam tetapi tidak mengubah fungsionalitas tersebut dikenal dengan istilah refactoring. Di dalam proses pengembangan perangkat lunak, refactoring adalah salah satu aktivitas yang sering dilakukan. Seringkali kita butuh untuk melakukan refactoring agar kita bisa mendapatkan performa yang lebih baik atau juga agar program yang kita tulis dapat dengan mudah dibaca dan dipahami oleh orang lain.

### Kapan kita harus melakukan refactoring?

Terkadang, kapan kita harus melakukan refactoring dapat ditandai dengan beberapa kejadian. Ketika kita menulis suatu bagian kode yang berulang-ulang, ada baiknya kalau kita melakukan refactoring segera. Bagian progam yang sama yang ditulis berulang-ulang menandakan bahwa ada duplikasi di dalam program kita, dan hal tersebut harus dihilangkan dengan cara refactoring.

Kita juga dapat melakukan refactoring ketika kita ingin menambahkan fitur baru ke dalam progam kita. Fitur yang kita tambahkan tersebut nantinya akan dibaca oleh orang lain, sehingga kita memiliki tanggung jawab untuk menulis progam yang berkulitas dan mudah dipahami dengan cara melakukan refactoring secara berkala. Begitupun kalau ketika kita sedang menambahkan fitur baru yang memanfaatkan fitur yang sudah ada dan kebetulan fitur tersebut perlu untuk di-refactor. Ada baiknya jika kita melakukan refactor terlebih dahulu terhadap bagian fitur teresbut. Hal tersebut akan memudahkan kita juga dan tentunya orang lain.

Refactoring juga dapat dilakukan ketika kita sedang mengatasi suatu permasalahan atau bug yang muncul di dalam progam kita. Sebelum mulai untuk mencari dan menyelesaikan permasalahannya, coba untuk refactor kalau bisa. Begitupun setelah permasalahan tersebut selesai dan teratasi, jangan lupa untuk lakukan refactor agar program yang kita tulis tetap memiliki kualitas yang baik.

Kita juga dapat melakukan refactoring pada bagian-bagian program yang dinilai memiliki performa yang kurang baik. Misalnya ada bagian di dalam program kita yang memerlukan sorting. Tetapi algoritma sorting yang digunakan masih pelan seperti bubble sort. Kita dapat melakukan refactoring pada bagian program tersebut agar menggunakan algoritma sorting yang lebih cepat misalnya merge sort. Tentunya untuk kasus refactoring yang seperti ini, ada baiknya kalau bagian program sudah ada testnya, agar ketika nanti kita selesai melakukan refactoring, bagian program tersebut masih bekerja sesuai dengan spesifikasinya.

### Penerapan refactoring di proyek kami

Di dalam proyek kami, tidak jarang kami melakukan refactoring. Jumlah bug yang muncul di dalam program tentunya tidak sedikit. Hasil scan dari quality gate juga seringkali menunjukan hasil yang kurang memuaskan karena adanya *code smells* dan *duplications* yang banyak. Oleh karena itu kami sering sekali melakukan refactoring.

Biasanya refactoring yang dilakukan adalah membuat program yang sudah ada menjadi lebih mudah untuk dibaca dan dipahami, mengingat bahwa semua anggota secara aktif perlu sering melihat dan memahami banyak bagian program. Kami biasanya mengganti nama variabel agar lebih mudah dipahami, menambahkan *whitespaces*  agar program lebih tersegmentasi sehingga lebih mudah dibaca, dan juga memasukkan bagian program yang sering muncul ke dalam suatu fungsi agar program yang ditulis tidak tingkat memilikki duplikasi yang tingga.

**Sebelum refactoring:**

```js
const lineChecker = (line, isFirstLine) => {
  let document = ``;

  if (line !== "" && isFirstLine) {
    document += `<h1>${line}</h1>`;
  } else if (line !== "" && !isFirstLine) {
    document += `<p>${line}</p>`;
  } else if (line === "") {
    document += "<br />";
  }

  return document;

};
```

**Sesudah refactoring:**

```js
const lineChecker = (line, isFirstLine) => {
  if (line === "") {
    return "<br />";
  }

  if (isFirstLine) {
    return `<h1>${line}</h1>`;
  } else {
    return `<p>${line}</p>`;
  }
};
```

> Contoh sebelum dan sesudah refactoring. Sumber code snippet: [How would you refactor this JS function?](https://dev.to/p42/how-would-you-refactor-this-js-function-4n71)
