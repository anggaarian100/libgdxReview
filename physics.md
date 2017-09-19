# Part 13: Physics Part 1 – A Basics Simulation

Secara physics teknis bukan bagian dari LibGDX itu sendiri, melainkan diimplementasikan diberbagai game engine lainnya. Physics yang digunakan di LibGDX adalah sistem physic Box2D yang populer sebagai library yang telah di porting di setiap platform dan bahasa yang pernah digunakan.

Jika belum pernah menggunakan physic sebelumnya, sebaiknya dimulai dengan dasar tentang apa dilakukan physic tersebut dan cara kerjanya. Pada dasarnya physics mengambil informasi scene yang kita berikan, lalu menghitung gerakan "realistis" dengan menggunakan perhitungan fisika. Penjelesannya seperti berikut:

* Digambarkan semua entitas fisika di dunia ke physics engine, eperti volume, massa, kecepatan, dll
* Physics engine selalu melakukan update, bisa per frame atau per interval
* Physic engine menghitung bagaimana world berubah, apa bertabrakan dengan apa, berapa banyak efek gravitasi setiap benda, kecepatan atau posisi saat ini, dll.
* Kita mengambil hasil simulasi fisikanya dan memperbarui world sesuai apa yang kita lakukan terhadapnya.

Sebagai penerapan pertama, simak penjelasan awal dari laman berikut untuk mengetahui dasar dari physics [Physics Engine](http://www.gamefromscratch.com/post/2014/08/27/LibGDX-Tutorial-13-Physics-with-Box2D-Part-1-A-Basic-Physics-Simulations.aspx)
