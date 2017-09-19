# Part 16: Using a Camera

Pada dasarnya kamera bertanggung jawab untuk menjadi "mata" di dunia permainan. Ini adalah analogi bagaimana cara kerja kamera video di dunia nyata. Lalu viewport mewakili bagaimana tampilan kamera ditampilkan. Cara mudah untuk menggambarkannya adalah dengan memikirkan kotak kabel HD atau satelit TV HD. Sinyal video masuk ke kotak(kamera), inilah gambar yang akan ditampilkan. Lalu perangkat TV  menampilkan sinyal yang masuk(viewport).

Gambaran sederhananya:
* Kamera - sebagai mata di tempat kejadian, menentukan apa yang pemain bisa lihat, digunakan oleh LibGDX untuk membuat scene.
* Viewport - mengontrol bagaimana hasil render dari kamera ditampilkan ke pemain, baik itu dengan black bar, stretched atau tidak melakukan apa-apa sama sekali.

Di LibGDX ada dua jenis kamera, yaitu PerspectiveCamera dan the OrthographicCamera. Jika kita mengerjakan game 2D, biasanya menggunakan kamera Orthographic, sementara jika kita bekerja dalam 3D, kemungkinan besar kita menggunakan kamera Perspektif. Untuk mengetahui lebih lanjut tentang kamera di LibGDX, kunjungi halaman berikut [Camera](http://www.gamefromscratch.com/post/2014/12/08/LibGDX-Tutorial-Part-16-Cameras.aspx)

