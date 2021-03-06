---
permalink: /ir-1/tdd
---

# Test Driven Development (TDD)

### Apa itu TDD?

Test Driven Development, atau yang lebih dikenal dengan istilah TDD, adalah salah satu konsep yang diterapkan dalam proses pengembangan perangkat lunak. TDD sendiri, sesuai dengan namanya, berfokus pada testing dalam proses pengembangan perangkat lunaknya. Testing yang dimaksud di sini ada beberapa macam, salah satunya adalah unit testing. Unit testing adalah sebuah test yang dijalankan untuk memeriksa fungsionalitas bagian kecil dari *source code* program kita. Biasanya, unit test akan memeriksa kebenaran suatu fungsi, keberadaan suatu elemen, dan sebagainya. 

Nah, karena adanya test tersebut, program yang kita kembangkan akan terhindar dari permasalahan error. Mengapa? Karena kalau ada bagian program yang mengandung error, error tersebut akan terdeteksi pada saat testing sehingga program tersebut yang dapat menimbulkan error tidak akan di-*deliver* ke pengguna.

### Bagaimana cara menerapkan TDD?

Proses TDD terdiri dari 3 langkah utama. Setiap langkah harus dijalankan secara linear. Langkah-langkah tersebut antara lain:

1. **red**: Pada tahap ini, kita tidak boleh langsung mengimplementasi fitur atau program kita. Kita hanya boleh membuat test yang akan memvalidasi bagian program yang kita akan tulis. Lalu setelah selesai mendesain dan membuat test tersebut, kita harus melakukan commit dengan tag \[RED\]. Perhatikan juga pada tahap ini, test yang baru kita buat tersebut harus gagal (*fail*).

    ```js
    describe('addition function', () => {
      it('should add 2 given numbers', () => {
        const result = add(1, 9)
        
        expect(result).toBe(10)
        expect(result).not.toBe(8)
      })
    })
    ```

2. **green**: Kemudian, setelah melakukan tahap **red**, kita baru boleh menulis dan membuat implementasi program yang akan membuat test kita pada tahap **red** tadi lulus (*pass*). Kita juga tidak boleh mengimplementasi fitur yang cakupannya berada di luar test yang kita buat pada tahap **red** sebelumnya. Setelah selesai, lakukan commit dengan tag \[GREEN\].

    ```js
    function add(a, b) {
        const result = a + b
        
        return result
    }
    ```

3. **refactor**: Tahapan ini sebenarnya tidak wajib dilakukan. Pada tahap ini, kita dapat melakukan *refactoring* bagian program yang kita nilai kurang efisien. Walaupun begitu, perlu diingat bahwa ketika melakukan *refactoring*, kita tidak boleh mengubah fungsionalitas program secara keseluruhan. Dengan demikian, test yang sudah ada tidak akan *fail* lagi.

<p align="center">
  <img src="https://womanonrails.com/images/tdd-basics/tdd.gif"/>
</p>

> Diagram alur penerapan TDD. Sumber: [womanonrails.com](https://womanonrails.com/tdd-basic).

### Penerapan TDD di aplikasi kami

Di dalam proyek kami, Jiva, kami menerapkan konsep TDD untuk seluruh *code base* program kami, baik untuk bagian *frontend* maupun *backend*. 

Untuk saya pribadi, sampai pada saat menulis Individual Review ini, saya bertanggung jawab untuk membangun *frontend* aplikasi kami. Kami menggunakan *framework* React sebagai *framework* utama frontend kami. React sendiri menggunakan konsep komponen untuk membangun halaman website.

Dalam menerapkan konsep TDD ketika membangun *frontend* aplikasi kami, saya selalu membuat test terlebih dahulu sebelum menambahkan elemen ataupun komponen apapun ke dalam tampilan website kami. Kemudian, setelah saya selesai membuat test-nya, saya baru mulai mengimplementasi elemen dan komponen website tersebut. Dengan demikian, kalau nantinya bagian frontend yang sekarang saya pegang akan diambil alih oleh rekan satu proyek saya, tidak akan terjadi perubahan layout yang jauh berbeda dengan desain utama pada prototype yang kami sudah desain. Hal ini dapat terwujud karena sudah ada test yang menjaga tampilan tersebut.

Di bawah ini merupakan salah satu contoh penerapan TDD yang diambil langsung dari *codebase* kami. Sebagai gambaran, tampilan yang ingin dibuat adalah seperti berikut.

<p align="center">
  <img src="./img/DashboardTenagaMedis.png"/>
</p>

Sebelum kita bisa mulai membuat tampilan tersebut, kita harus membuat test-nya terlebih dahulu. Di dalam test tersebut, kita akan memeriksa apakah komponen-komponen utama dari tampilan halaman tersebut sudah hadir atau tidak. Untuk itu, kita dapat menggunakan bantuan [Jest Framework](https://jestjs.io/).

```js
describe('DashboardTenagaMedis', () => {
  beforeEach( async () => {
    render(
      <DashboardTenagaMedis />
    );
  });

  it('should render', () => {
    const main = screen.getByRole('main');

    expect(main).toBeInTheDocument();
  });

  it('should have the page main heading', () => {
    const heading = screen.getByRole('heading', {
      name: /Daftar Tenaga Medis/,
    });

    expect(heading).toBeInTheDocument();
  });

  it('should have the tenaga medis list table', () => {
    const table = screen.getByRole('table');
    
    expect(table).toBeInTheDocument();
  });

  it('should have the tambah tenaga medis button', () => {
    const button = screen.getByRole('link', {
      name: /Tambah Tenaga Medis/,
    });

    expect(button).toBeInTheDocument();
    expect(button).toHaveAttribute('href', expect.stringMatching(/\/klinik\/\d+\/\d+\/tenaga-medis\/create/));
  });
});
```

Setelah test tersebut dibuat, coba jalankan test-nya. Pasti test-nya akan *fail*. Ini karena memang kita belum melakukan implementasi apa-apa. Tetapi ini sudah sesuai alur TDD. Oleh karena itu, kita lakukan commit dengan pesan \[RED\]. Setelah commit, baru kita bisa membuat implementasinya, agar test-nya bisa *pass* semua.

```js
function DashboardTenagaMedis() {
  return (
    <main>
      <Layout>
        <div>
          <h1>Daftar Tenaga Medis</h1>

          <TenagaMedisTable />

          <Button href={`/klinik/${idKlinik}/${idCabang}/tenaga-medis/create`}>Tambah Tenaga Medis</Button>
        </div>
      </Layout>
    </main>
  );
}

export default DashboardTenagaMedis;
```

Setelah kita buat implementasinya seperti itu, coba jalankan test-nya lagi. Kali ini seharusnya test-nya akan *pass*. Langkah selanjutnya adalah kita melakukan commit dengan pesan \[GREEN\]. Dengan demikian, alur TDD kita sudah selesai. Dalam contoh kasus ini, tidak ada bagian program yang perlu direfactor. Walaupun demikian, kalaupun ada bagian yang diperlukan refactor, maka hasil refactor tersebut tidak boleh membuat test yang sudah dibuat menjadi gagal.

> Contoh di atas merupakan contoh asli dari *codebase*, tetapi yang ditampilkan hanya beberapa bagian saja agar lebih relevan dan tidak membingungkan. Untuk contoh penuhnya, dapat diakses melalui tautan berikut:
> - [File test](https://gitlab.cs.ui.ac.id/ppl-fasilkom-ui/2022/Kelas-B/pencari-kelulusan/jiva-frontend/-/blob/staging/__tests__/tenagaMedis/index.test.jsx)
> - [File implementasi](https://gitlab.cs.ui.ac.id/ppl-fasilkom-ui/2022/Kelas-B/pencari-kelulusan/jiva-frontend/-/blob/staging/pages/klinik/%5BidKlinik%5D/%5BidCabang%5D/tenaga-medis/index.js)
