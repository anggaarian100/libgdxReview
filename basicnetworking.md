# Part 10: Basic Networking

Jaringan di LibGDX relatif primitif, yang mendukung hanya komunikasi socket. Dalam banyak kasus meskipun, itu lebih dari cukup. Akan menerapkan socket sangat sederhana berbasis aplikasi chatting. Kode ini banyak komentar, sehingga diskusi akan benar-benar cukup jarang.

Berikut code yang bisa diuji:
```
Paket com.gamefromscratch;

impor com.badlogic.gdx.ApplicationListener;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.Net.Protocol;
impor com.badlogic.gdx.graphics.GL20;
impor com.badlogic.gdx.graphics.OrthographicCamera;
impor com.badlogic.gdx.graphics.g2d.SpriteBatch;
impor com.badlogic.gdx.net.ServerSocket;
impor com.badlogic.gdx.net.ServerSocketHints;
impor com.badlogic.gdx.net.Socket;
impor com.badlogic.gdx.net.SocketHints;
impor com.badlogic.gdx.scenes.scene2d.InputEvent;
impor com.badlogic.gdx.scenes.scene2d.Stage;
imporcom.badlogic.gdx.scenes.scene2d.ui.Label;
impor com.badlogic.gdx.scenes.scene2d.ui.Skin;
impor com.badlogic.gdx.scenes.scene2d.ui.TextArea;
impor com.badlogic.gdx.scenes.scene2d.ui.TextButton;
impor com.badlogic.gdx.scenes.scene2d.ui.VerticalGroup;
impor com.badlogic.gdx.scenes.scene2d.utils.ClickListener;

impor java.io.BufferedReader;
import java.io.IOException;
impor java.io.InputStreamReader;
impor java.net.Inet4Address;
impor java.net.InetAddress;
impor java.net.NetworkInterface;
impor java.net.SocketException;
impor java.util.ArrayList;
impor java.util.Collections;
impor java.util.Enumeration;
import java.util.List;

public class Jaringan mengimplementasikan ApplicationListener {
     swasta OrthographicCamera kamera ;
    swasta SpriteBatch bets ;
    swasta Kulit kulit ;
    swasta Tahap tahap ;
    swasta Label labelDetails ;
    swasta Label labelMessage ;
    swasta TextButton tombol ;
    swasta textarea textIPAddress ;
    swasta textarea Pesanteks ;
    
    // Pilih resolusi yang 16: 9 tetapi tidak unreadibly kecil
     public static final mengapung VIRTUAL_SCREEN_HEIGHT = 960;
    public static final mengapung VIRTUAL_SCREEN_WIDTH = 540;
    
    
    @ Override
     public void menciptakan () {        
         kamera = baru OrthographicCamera (GDX. Grafis .getWidth (), GDX. Grafis .getHeight ());
        bets = baru SpriteBatch ();
        
        // Muat kulit UI kami dari file. Sekali lagi, saya menggunakan file termasuk dalam tes.
        // Membuat default.fnt yakin, default.png, uiskin. [Atlas / json / png] semua ditambahkan ke aset Anda
        kulit = baru Skin (. GDX file INTERNAL ( "data / uiskin.json" ));
        Tahap = baru Tahap ();
        // Kawat panggung untuk menerima masukan, karena kami menggunakan Scene2d dalam contoh ini
         GDX. masukan .setInputProcessor ( tahap );

        
        // Kode berikut loop melalui antarmuka jaringan yang tersedia
        // Perlu diingat, bisa ada beberapa interface per perangkat, misalnya
        // satu per NIC, satu per nirkabel aktif dan loopback
        // Dalam hal ini kita hanya peduli tentang alamat IPv4 (format xxxx)
        Daftar <String> alamat = baru ArrayList <String> ();
        mencoba {
            Pencacahan <NetworkInterface> interface = NetworkInterface.getNetworkInterfaces ();
            untuk (NetworkInterface ni: Collections.list (interface)) {
                 untuk (alamat InetAddress: Collections.list (ni.getInetAddresses ()))
                {
                    jika (alamat instanceof Inet4Address) {
                        addresses.add (address.getHostAddress ());
                    }
                }
            }
        } Catch (SocketException e) {
            e.printStackTrace ();
        }
        
        // Cetak isi array kita ke string. Ya, seharusnya menggunakan StringBuilder
         String ipAddress = baru String ( "" );
        untuk (String str: alamat)
        {
            ipAddress = ipAddress + str + "\ n" ;
        }
        
        // Sekarang setupt adegan UI kami
        
        // kelompok kelompok Vertikal isinya secara vertikal. Saya kira itu mungkin cukup jelas
        VerticalGroup vg = baru . VerticalGroup () ruang (3) .pad (5) .fill (); . // ruang (2) .pad (5) .fill ();. // ruang (3) .reverse () mengisi ().;
        // Mengatur batas-batas kelompok ke layar virtual seluruh
        vg.setBounds (0, 0, VIRTUAL_SCREEN_WIDTH , VIRTUAL_SCREEN_HEIGHT );
        
        // Buat kontrol kami
         labelDetails = baru Label (ipAddress, kulit );
        labelMessage = baru Label ( "Halo dunia" , kulit );
        tombol = baru TextButton ( "Kirim pesan" , kulit );
        textIPAddress = baru Textarea ( "" , kulit );
        Pesanteks = baru Textarea ( "" , kulit );

        // Tambahkan mereka ke tempat kejadian
         vg.addActor ( labelDetails );
        vg.addActor ( labelMessage );
        vg.addActor ( textIPAddress );
        vg.addActor ( Pesanteks );
        vg.addActor ( tombol );
        
        // Tambahkan adegan untuk tahap
         tahap .addActor (vg);
        
        // Setup viewport untuk memetakan layar untuk resolusi 480x640 maya
        // Seperti sebaliknya ini adalah terlalu kecil pada ponsel 1080p android saya.
        Tahap .setViewport ( VIRTUAL_SCREEN_WIDTH , VIRTUAL_SCREEN_HEIGHT , palsu );
        tahap .getCamera (). Posisi .set ( VIRTUAL_SCREEN_WIDTH / 2, VIRTUAL_SCREEN_HEIGHT / 2,0);
        
        // Sekarang kita membuat thread yang akan mendengarkan koneksi soket masuk
         baru Thread ( baru Runnable () {

            @ Override
             public void run () {
                ServerSocketHints serverSocketHint = baru ServerSocketHints ();
                // 0 berarti tidak ada batas waktu. Mungkin bukan ide terbesar dalam produksi!
                serverSocketHint. acceptTimeout = 0;
                
                // Buat server socket menggunakan protokol TCP dan mendengarkan pada 9021
                // Hanya satu aplikasi dapat mendengarkan port pada suatu waktu, perlu diingat banyak port dicadangkan
                // terutama di angka yang lebih rendah (seperti 21, 80, dll)
                ServerSocket ServerSocket = GDX. net .newServerSocket (. Protokol TCP , 9021, serverSocketHint);
                
                // Simpul selamanya
                 sementara ( benar ) {
                     // Buat socket
                     Socket socket = serverSocket.accept ( nol );
                    
                    // Baca data dari soket menjadi BufferedReader
                     penyangga BufferedReader = baru BufferedReader ( baru InputStreamReader (socket.getInputStream ()));
                    
                    mencoba {
                         // Baca ke baris baru berikutnya (\ n) dan menampilkan teks pada labelMessage
                         labelMessage .setText (buffer.readLine ());    
                    } Catch (IOException e) {
                        e.printStackTrace ();
                    }
                }
            }
        }).mulai(); // Dan, memulai thread berjalan
        
        // Kawat sebuah klik pendengar untuk tombol kita
        tombol .addListener ( baru ClickListener () {
             @ Override 
             public void diklik (event InputEvent, mengambang x, mengambang y) {
                
                // Ketika tombol diklik, dapatkan teks pesan atau membuat default nilai string
                 String textToSend = baru String ();
                jika ( Pesanteks .getText (). panjang () == 0)
                    textToSend = "Tidak banyak bicara tapi gemar mengklik tombol \ n" ;
                lain
                     textToSend = Pesanteks .getText () + ( "\ n" ); // Brute untuk baris baru sehingga readline mendapat garis
                
                SocketHints socketHints = baru SocketHints ();
                // Socket akan waktu kami di 4 detik
                 socketHints. connectTimeout = 4000;
                // membuat soket dan terhubung ke server masuk dalam kotak teks (format xxxx) pada port 9021
                 Socket socket = GDX. net .newClientSocket (. Protokol TCP , textIPAddress .getText (), 9021, socketHints);
                mencoba {
                     // tulis pesan kami masuk ke aliran
                     socket.getOutputStream () menulis (textToSend.getBytes ()).;
                } Catch (IOException e) {
                    e.printStackTrace ();
                }
            }
        });
    }

    @ Override
     public void buang () {
         bets .dispose ();
    }

    @ Override
     public void render () {        
        GDX. gl .glClearColor (0.5f, 0.5f, 0.5f, 1);
        GDX. gl .glClear (GL20. GL_COLOR_BUFFER_BIT );
        bets .setProjectionMatrix ( kamera . gabungan );
        bets .begin ();
        Tahap .draw ();
        bets END ();
    }

    @ Override
     public void resize ( int lebar, int tinggi) {
    }

    @ Override
     public void pause () {
    }

    @ Override
     public void melanjutkan () {
    }
}
```
Dan hasil dari kode tersebut seperi ini:<br>
<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=image_1119.png" /> 

Dua nilai atas adalah alamat IP v4 dari mesin Anda berjalan pada. Anda harus memasukkan ini dalam salinan lain dari aplikasi yang ingin chatting dengan. Alamat ini secara unik mengidentifikasi mesin Anda di internet, sementara kita ditentukan port (9021) menggunakan kode. Pikirkan port seperti kotak surat di sebuah gedung apartemen. Alamat jalan dari bangunan sebanding dengan alamat IP, sedangkan PORT ini mirip dengan nomor apartemen. nilai-nilai pelabuhan pergi dari 1 sampai 65.536, meskipun beberapa dicadangkan. Sebagian besar port disediakan adalah> 100, jadi ketika memilih port untuk aplikasi pemain mencari untuk melihat apakah alamat tersebut adalah pelabuhan khusus (seperti 80 untuk komunikasi HTTP, atau 21 untuk FTP), atau hanya memilih nilai tinggi acak. Mesin Anda dapat memiliki beberapa alamat, satu per adapter jaringan dan mungkin lebih, terutama jika Anda menjalankan software virtualisasi seperti VMWare. Lalu ada nilai 127.0.0.1, ini adalah alamat khusus yang dikenal sebagai adapter loop kembali, dan alamat yang menunjuk kembali pada dirinya sendiri.
<br>
Di mana saat mengatakan “Hello World”, ini adalah di mana setiap pesan yang masuk akan ditampilkan.
<br>
Pada textbox pertama, pemain memasukkan alamat IP dari mesin yang ingin mengirim pesan kepada. Dalam contoh ini, pemain benar-benar dapat mengirim pesan kepada diri sendiri, cukup masukkan alamat IP sendiri. Akhirnya textbox kedua adalah teks pesan untuk mengirim. Tentu saja Anda mengirim pesan dengan menekan tombol Kirim Pesan. Penjelesan lebih luas kita bisa lihat di laman berikut [Basic Networking](http://www.gamefromscratch.com/post/2014/03/11/LibGDX-Tutorial-10-Basic-networking.aspx)
