---
permalink: /ir-2/clean-code
---

# Clean Code

### Apa itu clean code?

Clean code adalah suatu konsep yang digunakan untuk menunjukkan bahwa program yang kita buat itu 'bersih'. Lantas apa yang dimaksud dengan 'bersih'? Program kita dinilai 'bersih' ketika program kita dapat dengan mudah dibaca dan dipahami oleh orang lain. Dalam proses pengembangan perangkat lunak, akan terlibat banyak sekali orang. Seringkali, program yang seseorang buat akan diperlukan oleh orang lain. Kalau misal kode yang dibuat itu sulit untuk dibaca dan dipahami, maka hal tersebut dapat menghambat kinerja orang lain yang membutuhkan bagian program tersebut. Atau bahkan yang lebih parah adalah ketika orang lain harus melanjutkan pekerjaan orang tersebut. Kalau misalnya orang lain tersebut tidak dapat memahami apa yang ditulis oleh orang sebelumnya, maka orang lain tersebut pastinya akan kesulitan.

### Apa saja yang membuat program kita 'bersih'?

Ada beberapa cara yang bisa dilakukan agar kita bisa menerapkan clean code dengan baik.

1. Komentar yang efisien

    Komentar (comments) adalah salah satu hal yang penting di dalam programing. Komentar bisa kita tambahkan untuk memberikan penjelasan yang lebih manusiawi untuk bagian program yang sulit untuk dibaca. Tetapi terlalu banyak komentar juga tidak baik. Biasanya kita terlalu banyak menulis komentar karena program yang kita buat sulit untuk dipahami. Alangakah baiknya, daripada kita menulis komentar yang banyak agar kode kita yang sulit dimengerti itu lebih mudah untuk dimengerti, lebih baik kalau kita menulis program yang lebih mudah dipahami agar kita tidak perlu menulis komentar yang terlalu banyak.

2. Penamaan yang baik

    Dalam memberikan nama untuk suatu variabel atau fungsi, alangkah baiknya kalau kita menggunakan penamaan yang deskriptif. Kita harus memberikan nama yang baik sedemikian sehingga ketika variabel atau fungsi tersebt dibaca oleh orang lain, orang lain tersebut dapat dengan mudah paham apa isi, kegunaan, ataupun nilai dari variabel atau fungsi tersebut. Dengan melakukan hal tersebut, maka dapat dijamin kalau program kita nantinya akan lebih enak dibaca dan lebih mudah dipahami.

3. Implementasi fungsi yang sederhana

    Ketika kita mengimplementasikan suatu fungsi, cobalah untuk membuat fungsi tersebut sesederhana mungkin. Kalau misalnya fungsi kita sudah terlalu panjang, coba untuk memecah fungsi tersebut menjadi beberapa fungsi yang lebih kecil lagi. Suatu fungsi yang baik adalah fungsi yang hanya melakukan satu hal dan satu hal saja. Kalau misal fungsi yang kita buat melakukan lebih dari satu hal, maka lebih baik kalau fungsi tersebut kita pecah menjadi beberapa fungsi yang lebih kecil lagi. Dengan melakukan hal ini, ketika kita membaca suatu fungsi, maka kita dapat dengan cepat paham apa yang dilakukan oleh fungsi tersebut.

4. Exception handling

    Error adalah teman sehari-hari developer. Tidak ada hari tanpa error. Kita bahkan justru akan bingung kalau kita tidak mendapatkan error pada saat pertama kali mencoba menjalankan program. Oleh kerana itu, kita harus menulis pesan error yang baik agar kalau nanti errornya muncul, error tersebut akan mudah dipahami sebab terjadinya. Dengan demikian, error tersebut juga dapat diselesaikan dengan cepat dan efektif juga. Kita harus membuat pesan error yang sudah sesuai dengan kesepakatan seluruh anggota tim pengembang, sehingga semua anggota dapat paham akan error yang mungkin akan terjadi di kemudian hari. 

5. Hindari duplikasi kode

    Kita harus membuat progam yang tidak memiliki duplikasi kode. Kalau misalnya kita melihat ada bebrapa bagian yang terus-menerus hadir di berbagai bagian kode kita, coba pertimbangkan untuk membungkus bagian tersebut ke dalam sebuah fungsi. Dengan demikian, program akan lebih mudah untuk dibaca. Untuk mencegah terjadinya duplikasi kode, ada baiknya kalau kita mendesain program yang modular, di mana bagian-bagian program yang sering dijalankan berulang kali akan dimasukkan ke dalam suatu fungsi yang ditulis sekali. Kemudian kalau bagian tersebut perlu dijalankan, yang perlu dilakukan hanyalah menjalankan fungsi tersebut.

6. Layout yang baik

    Program yang kita baut harus diformat dengan layout yang mudah dibaca. Coba untuk perbanyak whitespaces di dalam program kita. Kalau misal ada banyak baris kode yang bertumpuk, coba lihat di bagian mana kita bisa memebrikan baris-baris kosong. Pisahkan kode menjadi beberapa blok yang masing masing bloknya merupakan bagian progarm yang saling berhubungan. Dengan memperbanyak whitespaces, membaca program dapat lebih mudah untuk dipahami karena adanya whitespaces bisa membuat membaca program lebih tidak memusingkan.

### Penerapan clean code di codebase kami

Proyek kami sangat memerlukan implementasi clean code yang baik untuk seluruh *codebase* kami. Ini menjadi sangat penting karena kami bekerja dalam sebuah tim. Semua orang nanti akan melanjutkan program kita dan juga menggunakan program kita sebagai acuan untuk program mereka. Oleh karena itu, kita harus menerapkan clean code yang baik agar kita tidak menylitkan teman-teman kita. Terlebih lagi, untuk melakukan merge branch via merge request, kita harus melakukan code review terlebih dahulu. Kalau misalnya program yang kita buat tidak dapat dibaca karena kita tidak menerapakan clean code dengan baik, maka bagaimana caranya teman kita bisa melakukan code review? Justru nanti ditakutkan kalau teman kita gagal untuk melihat kesalahan-kesalahan yang ada di program kita karena meraka terlalu pusing dan kesulitan untuk membaca dan memahami program yang kita buat.

Berikut adalah beberapa *code snippet* yang diambil langsung dari proyek kami yang dapat menunjukkan penerapan clean code di dalam proyek kami.

```py
    # ...

    def test_create_jadwal_tenaga_medis_invalid(self):
        self.assertEqual(JadwalTenagaMedis.objects.count(), 0)
        data = {
            # all missing fields
        }
        url = reverse(self.create_jadwal_tenaga_medis_url, kwargs={ "tenaga_medis_id" : self.tenaga_medis_profile.id })
        response = self.client.post(url, data=data)
        self.assertEqual(response.status_code, status.HTTP_400_BAD_REQUEST)
        self.assertEqual(JadwalTenagaMedis.objects.count(), 0)
    
    # ...
```

> Contoh di atas menunjukkan penggunaan comments yang baik. Fungsi test tersebut harus jelas untuk dibaca. Tidak ada baris di dalam fungsi tersebut yang perlu diberi komentar karena memang sudah jelas apa yang dilakukan pada setiap barisnya. Satu-satunya comment yang dinilai perlu untuk ditulis adalah pada bagian `data`. Comment tersebut perlu untuk menandakan bahwa memang tidak ada apa-apa di dalam `dict` tersebut agar yang membaca fungsi tersebut tidak kebingungan.

```py
# ...

class JadwalTenagaMedisAPI(APIView):

    permission_classes = [
        IsStafPermission
    ]

    def get(self, request: Request, jadwal_tenaga_medis_id: int, format=None):
        jadwal_tenaga_medis = get_object(JadwalTenagaMedis, pk=jadwal_tenaga_medis_id)
        if jadwal_tenaga_medis is None:
            return Response(
                { "error": f"no 'jadwal tenaga medis' found with id : {jadwal_tenaga_medis_id}" },
                status=status.HTTP_404_NOT_FOUND,
            )
        serializer = JadwalTenagaMedisSerializer(jadwal_tenaga_medis)
        return Response(data=serializer.data, status=status.HTTP_200_OK)

    def patch(self, request: Request, jadwal_tenaga_medis_id: int, format=None):
        jadwal_tenaga_medis = get_object(JadwalTenagaMedis, pk=jadwal_tenaga_medis_id)
        if jadwal_tenaga_medis is None:
            return Response(
                { "error": f"no 'jadwal tenaga medis' found with id : {jadwal_tenaga_medis_id}" },
                status=status.HTTP_404_NOT_FOUND,
            )
        serializer = JadwalTenagaMedisSerializer(instance=jadwal_tenaga_medis, data=request.data, partial=True)
        if serializer.is_valid(raise_exception=True):
            try:
                serializer.save()
                return Response(serializer.data, status=status.HTTP_200_OK)
            except serializers.ValidationError as errors:
                errors = json.loads(json.dumps(errors.__dict__["detail"]))
                return Response(errors, status=status.HTTP_400_BAD_REQUEST)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
    
    def delete(self, request: Request, jadwal_tenaga_medis_id: int, format=None):
        jadwal_tenaga_medis = get_object(JadwalTenagaMedis, pk=jadwal_tenaga_medis_id)
        if jadwal_tenaga_medis is None:
            return Response(
                { "error": f"no 'jadwal tenaga medis' found with id : {jadwal_tenaga_medis_id}" },
                status=status.HTTP_404_NOT_FOUND,
            )
        jadwal_tenaga_medis.delete()
        return Response(
            { "success": "delete success" }, 
            status=status.HTTP_200_OK
        )

# ...
```

> Contoh di atas menggambarkan beberapa konsep-konsep clean code.
> - Komentar yang efisien: Tidak ada comments yang perlu untuk `class` di atas karena memang setiap bagiannya sudah jelas dan tidak memerlukan penjelasan tambahan dari comments.
> - Penamaan yang baik: Nama-nama fungsi dan variabel pada `class` tersebut sudah sangat dapat menggambarkan apa yang dilakukan dan disimpan oleh fungsi dan variabel yang bersangkutan.
> - Implementasi fungsi yang sederhana: Fungsi-fungsi yang dibuat telah didesain agar sederhana. Fungsi yang ditulis tidak terlalu panjang dan hanya melakukan satu hal saja.
> - Exception handling: Jika terjadi error, maka pesan error yang diberikan akan memberikan penjelasan mengapa terjadi error agar nantinya kalau ada rekan anggota yang mendapatkan error tersebut, mereka bisa langsung tahu apa masalahnya. 
> - Hindari duplikasi kode: Tidak ada duplikasi kode yang membuat `class` di atas menjadi panjang. Semua kode ditulis sedemikian sehingga tidak terjadi duplikasi kode.
> - Layout yang baik: Penggunaan whitespace dimanfaatkan dengan baik. Kita bisa membedakan yang mana fungsi yang mana `class` hanya dari melihat seklias (*skimming*).
