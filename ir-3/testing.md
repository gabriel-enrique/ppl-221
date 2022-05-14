---
permalink: /ir-3/testing
---

# Testing

### Apa itu Testing?

Ketika menulis program, menulis programnya saja tidak cukup. Kita harus dapat memastikan bahwa fungsionalitas program tersebut memang berjalan sesuai dengan intensi kita. Kita dapat memastikan hal ini dengan membuat test. Testing adalah salah satu metode yang digunakan oleh *developer* untuk memastikan bahwa porgram yang mereka terus terbukti kebenaranya dan fungsionalitas-nya sudah sesuai dengan yang diharapkan.

Selain sekedar untuk membuktikan kebenaran dan mengecek fungsionalitas program, testing juga dapat dijadikan sebagai pelindung program dari kerusakan. Misalnya kita punya suatu fungsi yang melakukan suatu hal. Kita sudah punya test-nya dan test-nya juga sudah *pass*. Kemudian, di kemudian hari, karena satu dan lain hal, kita ingin melakukan perubahan terhadap fungsi tersebut tanpa mengubah fungsionalitas. Lantas, kita harus memastikan bahwa perubahan yang kita lakukan tersebut tidak akan mengubah fungsionalitas fungsi tersebut. Karena kita sudah punya test-nya, yang perlu kita lakukan untuk memastikan bahwa fungsionalitas fungsi tersebut masih benar hanyalah menjalankan test tersebut.

### Bagaimana cara membuat test?

Untuk menunjukkan bagaimana cara kita membuat test yang baik, saya akan menggunakan contoh dari *project* saya yang pernah saya kerjakan. Project ini adalah [StudyHelper Bot](https://gitlab.com/advprog.c12/study-helper-bot), sebuah bot Discord yang memiliki berbagai tools untuk membantu proses belajar mengajar di Discord.

```java
    // CommandServiceImpl.java
    // ...

    @Override
    public void processMessage(Message message) {
        String commandName = extractCommandName(message, prefix);
        List<String> commandArgs = extractCommandArgs(message);
        Command command = commandRepository.getCommandByName(commandName);

        ValidityStatus validityStatus = commandValidator.validate(message, commandArgs, command);

        if (validityStatus == ValidityStatus.VALID) {
            command.executeCommand(message, commandArgs);
        } else {
            sendInvalidResponse(validityStatus, message, command);
        }
    }

    // ...    
```

> Full source code [here](https://gitlab.com/advprog.c12/study-helper-bot/-/blob/master/src/main/java/io/java/studyhelper/studyhelper/service/CommandServiceImpl.java)

Misalnya kita punya program seperti di atas. Fungsi tersebut akan menerima sebuah `Message` dan akan mencoba untuk mengambil `commandName` dan `commandArgs` dari `Message` tersebut. Kemudian dari `commandName` akan dicari sebuah `Command` yang sesuai dengan `commandName` tersebut. Kemudian setelah itu, `Command` tersebut akan dicek validitasnya berdasarkan `Message` dan `commandArgs`-nya. Setelah itu, tergantung dari hasil pengecekan validitasnya, kalau valid, makan `Command` tersebut akan dijalankan, kalau tidak maka akan dikirim balasan yang menunjukkan bahwa `Command` yang ingin dijalankan oleh `Message` itu invalid.

```java
    // CommandServiceImplTest.java
    // ...

    @Test
    public void testProcessMessageValid() {
        Message message = mock(Message.class);
        MessageChannel messageChannel = mock(MessageChannel.class);
        Command command = mock(Command.class);
        String messageContent = "!commandName args1 args2";

        when(message.getContentRaw()).thenReturn(messageContent);
        when(message.getChannel()).thenReturn(messageChannel);
        when(commandRepository.getCommandByName(anyString())).thenReturn(command);

        when(command.isArgsRequired()).thenReturn(false);
        when(command.isGuildOnly()).thenReturn(false);
        when(command.isDMOnly()).thenReturn(false);

        commandService.processMessage(message);

        verify(commandRepository, times(1)).getCommandByName(anyString());
        verify(command, times(1)).executeCommand(any(Message.class), any(ArrayList.class));
    }

    // ...
```

> Full source code [here](https://gitlab.com/advprog.c12/study-helper-bot/-/blob/master/src/test/java/io/java/studyhelper/studyhelper/service/CommandServiceImplTest.java)

Untuk mengecek fungsi tersebut, tentunya kita membutuhkan `Message`. Tetapi membuat object `Message` sungguhan tidak ada gunanya ketika testing, kita bisa melakukan sesuatu yang disebut dengan **mock**. Mocking adalah proses di mana kita membuat object 'bohongan' dari suatu class. Nantinya, mock object yang kita buat bisa kita spesifikasikan apa saja sifat yang dimiliki oleh object tersebut. Selain `Message`, kita juga butuh mock object `MessageChannel` dan `Command`.

Kemudian setelah dibuat object-object yang diperlukan, kita bisa mulai menulis sifat dari mock object tersebut. Ketika method `getContentRaw()` milik `Message` tadi dipanggil, maka kita ingin agar yang di-return adalah `messageContent`. Ketika method `getChannel()` milik `Message` tadi dipanggil, maka kita ingin agar yang di-return adalah `MessageChannel` mock object yang kita buat tadi. Kita harus menspesifikasikan apa saja yang akan direturn oleh mock object kita sesuai dengan apa saja yang dipanggil secara intrinsik ketika fungsi yang sedang kita test dijalankan.

Kemudian seteleh itu, kita baru mulai menjalankan fungsi yang sedang kita test.

Terakhir, kita melakukan pengecekan apakah fungsi yang sedang kita test ini sudah berjalan sesuai dengan harapan. Kita tahu bahwa apapapun yang terjadi, fungsi `getCommandByName` milik `commandRepository` akan dipanggil tepat satu kali.

> Catatan: Banyak bagian dari contoh code snippet di atas yang memerlukan pengetahuan tentang library [JDA](https://github.com/DV8FromTheWorld/JDA) dan juga pemahaman tentang bagian program lain untuk dapat memahaminya 

### Mengapa kita perlu `mock`?

Ketika membuat test, kita hanya memeriksa kebenaran dari fungsi tersebut saja. Fungsi-fungsi yang dipanggi di dalam fungsi tersebut tidak perlu kita periksa kebenarannya, kita bisa mengasumsikan bahwa fungsi intrinsik tersebut sudah benar. Kita hanya fokus untuk memeriksa kebenaran dari fungsi yang kita ingin test saja, tidak lebih dan tidak kurang. Oleh karena itu kita melakukan mock agar object yang kita inginkan bisa kita buat sendiri seperti apa fungsionalitasnya. Tentunya nanti harus ada test yang memeriksa kebenaran semua fungsi intrinsik tersebut.

### Penerapan testing di kelompok kami

Kami selalu membuat test agar kami bisa merasa aman bahwa program yang kami tulis memang sudah sesuai dengan keiinginan dan intensi kita. Kita juga membuat test agar coverage dari progam yang kita buat juga bisa tinggi dan meng-*cover* kebanyakan program kita.

Kami sering sekali melakukan refactoring dan perubahan fitur. Tidak jarang ada rasa khawatir dari diri kami. Apakah apa yang baru saya tulis benar? Apakah program yang saya tulis akan membuat bagian lain dari progam menjadi rusak? Pertanyaan-pertanyaan seperti ini selalu ada di piiran kami setiap kali kami menulis program. Tetapi rasa khawatir tersebut akan hilang karena kami sudah punya test yang dapat memastikan bahwa, iya, memang benar bahwa program yang baru saja ditulis benar dan tidak akan membuat bagian dari program lain menjadi rusak.

```js
describe('CreateTenagaMedis', () => {  
  beforeEach(() => {
    nextRouter.useRouter = jest.fn();
    nextRouter.useRouter.mockImplementation(() => ({ 
      route: '/klinik/1/1/tenaga-medis/create', 
      query: { idKlinik: 1, idCabang: 1 },
      isReady: true, 
    }));
    render(
      <Provider store={store}>
        <CreateTenagaMedis />
      </Provider>
    );
  });


  afterEach(() => {
    let assignMock = jest.fn();
    delete window.location;
    window.location = { assign: assignMock };
    assignMock.mockClear();
  });

  // ...
```

> Contoh *mocking* pada `__tests__/tenagaMedis/create.test.jsx`. Mocking dilakukan untuk mock NEXT router agar kita bisa melakukan spesifikasi query pada url.
