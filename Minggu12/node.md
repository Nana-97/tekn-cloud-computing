Bergabung dengan node Pekerja ke Swarm
Bagian 3: Menyebarkan aplikasi di beberapa host
Sekarang setelah Anda memiliki swarm up dan running, sekarang saatnya untuk menggunakan aplikasi tidur kami yang sangat sederhana.
Anda akan melakukan prosedur berikut dari node1 .
Langkah 3.1 - Menyebarkan komponen aplikasi sebagai layanan Docker
Kami sleepaplikasi menjadi sangat populer di internet (karena memukul Reddit dan HN). Orang suka itu. Jadi, Anda harus mengukur aplikasi Anda untuk memenuhi permintaan puncak. Anda harus melakukan ini di beberapa host untuk ketersediaan tinggi juga. Kami akan menggunakan konsep Layanan untuk mengukur aplikasi kami dengan mudah dan mengelola banyak wadah sebagai satu kesatuan.
Layanan adalah konsep baru di Docker 1.12. Mereka bekerja dengan kawanan dan dimaksudkan untuk wadah yang sudah berjalan lama.
Anda akan melakukan prosedur ini dari node1 .
Mari kita sebarkan sleepsebagai Layanan di Docker Swarm kami.