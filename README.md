# Modul 10 Asynchronous Programming

## Reflection 1.2.

Saat menambahkan println! setelah spawner.spawn, teks tersebut akan tercetak di sebelum pesan dari dalam blok async ("howdy!" dan "done!") karena asynchronus programming memungkinkan unit kerja berjalan secara terpisah dari thread aplikasi utama. Hal ini terjadi karena Futures di Rust bersifat lazy dan tidak akan melakukan apa pun kecuali didorong secara aktif hingga selesai oleh sebuah executor. Dalam program ini, fungsi spawner.spawn hanya bertugas wrap future ke dalam sebuah Task dan mengirimkannya ke dalam antrean (ready_queue) melalui channel, namun tidak langsung mengeksekusinya. Karena executor baru benar-benar mulai memproses antrean dan memanggil fungsi poll pada tugas-tugas tersebut saat perintah executor.run() dijalankan, instruksi synchronous yang ada di thread utama akan selesai dieksekusi lebih dulu sebelum tugas asynchronous yang baru saja didaftarkan sempat berjalan.
