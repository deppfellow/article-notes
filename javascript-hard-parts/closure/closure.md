# Closure - Konsep Penting dalam Javascript

Baru-baru ini saya mulai mereview lagi konsep-konsep Javascript yang masih kurang dipahami saat pertama kali belajar Javascript. Sampai satu waktu saya menonton video dari Will Sentance di *series*-nya, *"Javascript: The Hard Parts"* dan perlu saya tegaskan kalau pembahasannya terkait Closure benar-benar membuat saya berpikir "Wahh, gini tohh ternyata *closure*".

Jadi di artikel ini, ingin saya bahas konsep Closure dan bagaimana cara kerjanya dalam Javascript. Tapi sebelum itu, saya ingin menyampaikan kalau pembaca diasumsikan sudah mengerti apa itu:

1. Konsep fungsi (*function*) dan *execution scope* (e.g. *global scope*, *local scope*) dalam pemrograman
2. Sintaks dasar dari Javascript



---

## Pre-requisite

Sebelum memulai pembahasan, 3 prinsip dasar Javascript yang penting diketahui. Pertama, Javsacript akan mengeksekusi kode baris demi baris, yang dinamakan **thread of execution**. Kedua, setiap informasi yang ditemui Javascript saat proses eksekusinya, variabel, konstanta, ataupun fungsi, informasi tersebut akan disimpan ke dalam **memory**. Ketiga, Javascript mencatat fungsi apa yang sedang berjalan, yang disimpan ke dalam **call stack**, dan membuat *execution context* untuk fungsi tersebut.

Oke, jadi 3 prinsip dasar. **Thread of execution**, **memory**, dan **call stack**. Misalkan kita memiliki kode seperti dibawah ini:

<img src="D:\any_code\article-notes\javascript-hard-parts\closure\img\prereq-code.png" alt="prereq-code" style="zoom:50%;" />

Yang terjadi adalah:

1. Javascript berada pada *global environment*, `global()` masuk ke dalam **call stack**, membuat *global execution context*, dengan **global memory** untuk menyimpan semua informasi pada lingkup tersebut.
2. Baris 1, didefinisikan konstanta dengan label `num` dan value `3`, disimpan ke **global memory**.
3. Baris 2, didefinisikan fungsi `multiplyBy2` yang menerima satu parameter `input`. Disimpan ke **global memory**.
4. Baris 7, didefinisikan konstanta `output` dengan valuenya adalah hasil pemanggilan fungsi `multiplyBy2` dengan argument `num`. Nah, pada proses ini, yang terjadi ialah:
   1. Javascript memasukkan `multiplyBy2()` ke dalam **call stack**, membuat *local execution context*, dengan **LOCAL MEMORY YANG HANYA TERSEDIA SELAMA PEMANGGILAN FUNGSI `multiplyBy2` BERLANGSUNG**.
   2. Proses eksekusi `multiplyBy2`, didefinisikan konstanta `result` dengan value `input + 2` yang disimpan ke dalam **local memory**.
   3. Berikutnya, konstanta `result` dikembalikan dan nilainya disimpan ke label `output` yang ada di **global memory**. `multiplyBy2()` dikeluarkan dari **call stack**, dan kembali menjalankan `global()`.
   4. **Setelah itu, seluruh *local execution context* beserta *local memory* dari proses eksekusi `multplyBy2` dihapus**.
5. Baris 8, konstanta `newOutput` dibuat dengan valuenya adalah hasil pemanggilan `multiplyBy2`. Pada proses ini, *local execution context* yang baru dibuat kembali dan proses seperti pada poin nomor 4, tetapi sekarang menggunakan argument `10`.

Poin yang perlu diperhatikan yaitu pada poin nomor 4 dan 5, *local execution context* yang baru, dibuat untuk menjalankan setiap pemanggilan fungsi `multiplyBy2`. Setelah pemanggilan masing-masing fungsi selesai, *local execution context* tersebut akan dihapus dan "mustahil" untuk komputer mengetahui lagi informasi apa yang telah dijalankan sebelumnya ("mustahil" dengan tanda kutip, sebab Javascript memiliki cara untuk menyimpan informasi yang dihapus tersebut, yap! *closure*).



---

## Higher Order Function

Singkatnya, untuk setiap fungsi yang didefinisikan pada Javascript, parameter dari fungsi tersebut bisa berbentuk apapun. String, integer, object, bahkan fungsi bisa menjadi argument dari fungsi lainnya. Inilah mengapa sering disebut istilah ***"Javascript as first class function"***. Perhatikan kode berikut:

<img src="D:\any_code\article-notes\javascript-hard-parts\closure\img\high-order-func-code.png" alt="high-order-func-code" style="zoom: 50%;" />

Dari kode diatas, kita memberikan fungsi `multiplyBy2` dan `addBy7` sebagai argument ke fungsi `copyAndManipulate`. Dalam kasus ini, `multiplyBy2` dan `addBy7` disebut sebagai *callback*.



---

## Closure

Sekarang perhatikan kode berikut:

<img src="D:\any_code\article-notes\javascript-hard-parts\closure\img\closure-code.png" alt="closure-code" style="zoom:50%;" />

Mari kita jabarkan eksekusi kode tersebut:

1. Baris 1, didefinisikan fungsi `outer` dan disimpan ke **global memory**
2. Baris 8, konstanta `myNewFunction` dibuat dengan nilainya adalah hasil pemanggilan fungsi `outer`.
   1. *Local execution context* dibuat beserta ***local memory*** dari pemanggilan fungsi `outer`
   2. Di dalamnya, dibuat fungsi baru `incrementCounter`
   3. Referensi ke `incrementCounter` dikembalikan, dan **seluruh *local execution context* beserta *local memory* dari fungsi `outer` dihapus**.
3. Baris 9, pemanggilan `myNewFunction`, yang mereferensi ke fungsi `incrementCounter`, dijalankan

Jelas? oke, sampai sini dulu. Sekarang pertanyaannya. Saat `myNewFunction` dijalankan, apa yang dilakukan Javascript? Mencoba untuk melakukan increment ke variabel `counter` yang sebelumnya dideklarasikan di fungsi `outer`.

TAPI --- ingat sebelumnya kalau *local execution context* dan ***local memory*** dari fungsi `outer` SUDAH DIHAPUS, yang atinya semua informasi terkait variabel `counter` juga ikut dihapus. Sedangkan yang dikembalikan dari fungsi `outer` HANYA referensi kepada fungsi `incrementCounter`. Jadi, bagaimana bisa Javascript tau apa itu variabel `counter` yang perlu di-*increment* dalam pemanggilan fungsi `myNewFunction`.

Jawabannya, dibalik layar, Javascript punya *hidden property* yang bernama `[scope]`. Kita tidak bisa mengakses hidden property ini dengan cara apapun. Tetapi, melalui properti ini, saat suatu fungsi dikembalikan dari pemanggilan fungsi lain, Javscript mengambil seluruh data dan informasi disekitar fungsi tersebut, dan ikut dikembalikan bersama referensi fungsi yang dikembalikan. Sehingga, pada kasus diatas, `incrementCounter` yang dikembalikan dari pemanggilan fungsi `outer`, juga ikut mengambil semua informasi disekitarnya, dan pada hal ini, adalah variabel `counter`. Informasi yang ikut dikembalikan ini dinamakan ***lexical environment***.

Karena itulah konsep ini dinamakan ***closure***, sebab kita tidak bisa mengubah ataupun memanggil ***lexical environment*** ini, KECUALI dengan memanggil fungsi `incrementCounter` yang ada memproses variabel pada ***lexical environment***, yang pada kasus diatas, dijalankan dengan memanggil konstanta `myNewFunction`. Maka melanjutkan proses sebelumnya:

4. Setelah baris 9 dijalankan, fungsi `incrementCounter` dijalankan dengan memeriksa ***lexical environment*** terhadap informasi variabel `counter` dan melakukan *increment*.
5. Baris 10, dilakukan hal yang sama pada baris 9.



---

## Manfaat dari Closure

Setelah semua hal tersebut, apa memangnya kegunaan dari konsep closure? Closure sangat berguna dalam Javascript sebab:

1. **Helper function**: kita bisa membuat fungsi yang hanya bisa dipanggil sekali, dikenal dengan nama ***once***. Bisa juga digunakan untuk menyimpan seluruh hasil pemanggilannya. yang dikenal dengan ***memoize***, 
2. **Module pattern**: melalui closure, kita bisa menyimpan informasi dari pemanggilan fungsi tanpa mengkotori **global memory**.
3. **Asynchronous Javascript**: misalnya konsep **Promises** yang sering didengar di Javascript. Melalui closure, kita bisa menggunakan data yang tersimpan melalui closure untuk dijalankan melalui **Promises** (dijelaskan lebih lanjut di *asynchronous javascript*).