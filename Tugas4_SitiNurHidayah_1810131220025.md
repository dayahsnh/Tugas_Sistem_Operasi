# STRUKTUR SISTEM OPERASI

## Perbedaan antara Struktur Sederhana, Pendekatan Berlapis, dan Kernel Mikro


### -Struktur Sederhana-

<img width="438" alt="Sistem Monolotik" src="https://user-images.githubusercontent.com/74997946/192281750-6bb6a644-0f77-44ac-bf9b-caf0a6978b84.png">


Sistem monolitik merupakan struktur sistem operasi sederhana yang dilengkapi dengan operasi “dual” pelayanan {sistem call} yang diberikan oleh sistem operasi. Model sistem call dilakukan dengan cara mengambil sejumlah parameter pada tempat yang telah ditentukan sebelumnya, seperti register atau stack dan kemudian mengeksekusi suatu intruksi trap tertentu pada monitor mod.
Mekanisme dan prinsip kerja model struktur monolitik sistem operasi ini adalah sebagai berikut:

1. User program melakukan “trap” pada karnel

2. Intruksi berpindah dari user mode ke monitor mode dan mentransfer control ke sistem operasi.

3. Sistem operasi mengecek parameter — parameter dari pemanggilan tersebut, untuk menentukan sistem call mana yang memanggil.

4. Sistem operasi menunjuk ke suatu table yang berisi slot ke-k yang menunjuk sistem call K (Kontrol).

5. Kontrol akan dikembalikan kepada user program, jika sistem call telah selesai mengerjakan tugasnya.

Tatanan ini memberikan suatu struktur dasar dari sistem operasi sebagai berikut :

1. Program utama meminta service procedure.

2. Kumpulan service procedure yang dibaca oleh sistem call.

3. Kumpulan utility procedure yang membantu service procedure.


### -Pendekatan Berlapis-

<img width="396" alt="p4 berlapis" src="https://user-images.githubusercontent.com/74997946/192282337-50789058-1e34-4c0d-ad8f-43201adbe3aa.png">

Sistem operasi dibentuk secara hirarki berdasar lapisan — lapisan, dimana lapisan-lapisan bawa memberi layanan lapisan lebih atas. Lapisan yang paling bawah adalah perangkat keras dan yang paling tinggi adalah user- interface. Sebuah lapisan adalah implementasi dari obyek abstrak yang merupakan enkapsulasi dari data dan operasi yang bisa memanipulasi data tersebut. Struktur berlapis dimaksudkan untuk mengurangi kompleksitas rancangan dan implementasi sistem operasi.
Jumlah lapisan sistem operasi berlapis dapat berbeda-beda. Sistem berlapis yang hanya terdiri dari 6 lapisan pasti akan lebih padat jika dibandingkan dengan sistem berlapis dengan 12 lapisan.

Contoh lapisan sistem operasi berlapis dengan 6 lapisan adalah :
•	Lapisan 0 = Mengatur alokasi prosesor, pertukaran proses, dan dasar multi programming di CPU.
•	Lapisan I = Mengalokasikan ruang proses pada memori utama sehingga dapat menahan proses saat tidak ada ruang yang tersedia di memori utama.
•	Lapisan 2 = Mengatur komunikasi antar proses dan operator console.
•	Lapisan 3 = Mengatur peranti M/K dan menampung informasi dalam proses kerja sistem operasi.
•	Lapisan 4 = Menampung program utama pengguna.
•	Lapisan 5 = Mengatur sistem operator.


### -Kernel Mikro-

<img width="391" alt="p4 kernel mikro" src="https://user-images.githubusercontent.com/74997946/192283114-3098e483-20f7-4234-b3d1-cc2263274c2f.png">


Sistem operasi yang menggunakan micro kernel umumnya secara dramatis memiliki kinerja di bawah kinerja sistem operasi yang menggunakan monolithic kernel. Hal ini disebabkan oleh adanya overhead yang terjadi akibat proses input/output dalam kernel yang ditujukan untuk mengganti konteks (context switch) untuk memindahkan data antara aplikasi dan server.
Contoh Sistem operasi yang menggunakan struktur ini adalah : TRU64 UNIX, MacOSX dan QNX.


