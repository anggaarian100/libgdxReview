# Part 9:  Scene2D Part 3 – Scene Management

Sejauh ini sudah melihat apa yang Scene2D menyediakan dalam hal Aktor, Actions serta penanganan input, sekarang lihat beberapa fungsi manajemen adegan itu menyediakan. Salah satu kemampuan yang sangat kuat dari Scene2D adalah pengelompokan. Mari kita melompat ke kanan dengan sebuah contoh. Dalam contoh ini ada dua grafik:



Berikut code yang bisa diuji:
```
Paket com.me.mygdxgame;

impor com.badlogic.gdx.ApplicationListener;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.graphics.GL10;
impor com.badlogic.gdx.graphics.Texture;
impor com.badlogic.gdx.graphics.g2d.Batch;
impor com.badlogic.gdx.graphics.g2d.TextureRegion;
impor com.badlogic.gdx.scenes.scene2d.Actor;
impor com.badlogic.gdx.scenes.scene2d.Group;
impor com.badlogic.gdx.scenes.scene2d.Stage;
mengimpor statis com.badlogic.gdx.scenes.scene2d.actions.Actions *.;


public class SceneManagementDemo mengimplementasikan ApplicationListener {
    
    swasta Tahap tahap ;
    swasta Kelompok kelompok ;
    
    @ Override
     public void menciptakan () {        
         tahap = baru Tahap (GDX. Grafis .getWidth (), GDX. Grafis .getHeight (), benar );
        akhir TextureRegion jetTexture = baru TextureRegion ( baru Tekstur ( "data / jet.png" ));
        akhir TextureRegion flameTexture = baru TextureRegion ( baru Tekstur ( "data / flame.png" ));
        
        akhir Aktor jet = baru Aktor () {
             public void draw (Batch batch, mengapung alpha) {
                batch.draw (jetTexture, getX (), getY (), getOriginX (), getOriginY (), getWidth (), getHeight (), 
                        getScaleX () getScaleY () getRotation ());
            }
        };
        jet.setBounds (jet.getX (), jet.getY (), jetTexture.getRegionWidth (), jetTexture.getRegionHeight ());
    
        akhir Aktor api = baru Aktor () {
             public void draw (Batch batch, mengambang alpha) {
                batch.draw (flameTexture, getX (), getY (), getOriginX (), getOriginY (), getWidth (), getHeight (),
                        getScaleX () getScaleY () getRotation ());
            }
        };
        flame.setBounds (0, 0, flameTexture.getRegionWidth (), flameTexture.getRegionHeight ());
        flame.setPosition (jet.getWidth () - 25, 25);
        
        Kelompok = baru Group ();
        Kelompok .addActor (jet);
        Kelompok .addActor (api);
        
        Kelompok .addAction (paralel (moveTo (200,0,5), rotateBy (90,5)));
        
        tahap .addActor ( kelompok );
        
        
    }

    @ Override
     public void buang () {
         tahap .dispose ();
    }

    @ Override
     public void render () {    
        GDX. gl .glClear (GL10. GL_COLOR_BUFFER_BIT );
        Tahap .act (GDX. grafis .getDeltaTime ());
        Tahap .draw ();
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
<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=SceneManagementCompressed.gif" /> 

```
Paket com.me.mygdxgame;

impor com.badlogic.gdx.ApplicationListener;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.graphics.GL10;
impor com.badlogic.gdx.graphics.Texture;
impor com.badlogic.gdx.graphics.g2d.Batch;
impor com.badlogic.gdx.graphics.g2d.TextureRegion;
impor com.badlogic.gdx.scenes.scene2d.Actor;
impor com.badlogic.gdx.scenes.scene2d.InputEvent;
impor com.badlogic.gdx.scenes.scene2d.InputListener;
impor com.badlogic.gdx.scenes.scene2d.Stage;
impor com.badlogic.gdx.scenes.scene2d.Touchable;

impor java.util.Random;

public class SceneManagementDemo mengimplementasikan ApplicationListener {
    
    // Buat Aktor "Jet" yang menampilkan TextureRegion lulus di
     kelas Jet meluas Aktor {
         swasta TextureRegion _texture ;
        
        publik Jet (TextureRegion tekstur) {
             _texture = tekstur;
            setBounds (getX (), getY (), _texture .getRegionWidth (), _texture .getRegionHeight ());
            
            ini .addListener ( baru InputListener () {
                 public boolean Touchdown (InputEvent acara, mengambang x, mengapung y, int pointer, int tombol) {
                    Sistem. out .println ( "Tersentuh" + getName ());
                    setVisible ( palsu );
                    kembali benar ;
                }
            });
        }

        // Melaksanakan bentuk penuh imbang () sehingga kami dapat menangani rotasi dan skala.
        public void draw (Batch batch, mengambang alpha) {
            Batch.Draw ( _Texture , getX (), getY (), GetOriginX (), GetOriginY (), getWidth (), getHeight (),
                    getScaleX () getScaleY () getRotation ());
        }
        
        // hit ini () bukannya memeriksa terhadap kotak berlari, memeriksa lingkaran loncat.
        publik Aktor hit ( mengambang x, mengambang y, boolean terjamah) {
             // Jika Aktor ini tersembunyi atau tersentuh, itu tidak dapat memukul
             jika (! ini .isVisible () || ini .getTouchable () == terjamah. dinonaktifkan )
                 kembali nol ;
            
            // Dapatkan centerpoint lingkaran melompat-lompat, juga dikenal sebagai pusat rect
             mengapung centerX = getWidth () / 2;
            mengapung Centery = getHeight () / 2;
            
            // akar Square m'kay buruk. Dalam "nyata" kode, cukup persegi kedua belah pihak untuk lebih tahan luntur speedy
            // Namun ini adalah yang tepat, unoptimized dan termudah untuk grok persamaan untuk hit dalam lingkaran
            // Anda tentu saja menggunakan kelas Lingkaran LibGDX sebagai gantinya.
            
            // Hitung jari-jari lingkaran
            mengapung radius = ( pelampung ) Math.sqrt (centerX * centerX +
                    Centery * Centery);

            // Dan jarak titik dari pusat lingkaran
             mengapung jarak = ( pelampung ) Math.sqrt (((centerX - x) * (centerX - x))
                    + ((Centery - y) * (Centery - y)));
            
            // Jika jarak kurang dari jari-jari lingkaran, itu adalah hit
             jika (jarak <= jari-jari) kembali ini ;
            
            // Jika tidak, itu isnt
             kembali nol ;
        }
    }
    
    swasta Jet [] jet ;
    swasta Tahap tahap ;
    
    @ Override
     public void menciptakan () {        
         tahap = baru Tahap (GDX. Grafis .getWidth (), GDX. Grafis .getHeight (), benar );
        akhir TextureRegion jetTexture = baru TextureRegion ( baru Tekstur ( "data / jet.png" ));
        
        jet = baru Jet [10];
        
        // Buat / benih nomor acak kami untuk posisi jet acak
         random random = baru Random ();
        
        // Buat 10 objek Jet secara acak di lokasi layar
         untuk ( int i = 0; i <10; i ++) {
             jet [i] = baru Jet (jetTexture);
            
            // Menetapkan posisi jet untuk nilai acak dalam batas-batas layar
             jet [i] .setPosition (random.nextInt (GDX. Grafis .getWidth () - ( int ) jet [i] .getWidth ())
                    , Random.nextInt (. GDX grafis .getHeight () - ( int ) jet [i] .getHeight ()));
            
            // Set nama Jet untuk indeks itu dalam lingkaran
             jet [i] .setName (Integer.toString (i));
            
            // Tambahkan mereka ke tahap
             tahap .addActor ( jet [i]);
        }
        
        GDX. masukan .setInputProcessor ( tahap );
    }

    @ Override
     public void buang () {
         tahap .dispose ();
    }

    @ Override
     public void render () {    
        GDX. gl .glClear (GL10. GL_COLOR_BUFFER_BIT );
        Tahap .act (GDX. grafis .getDeltaTime ());
        Tahap .draw ();
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

<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=SceneManagement2Compressed.gif" /> 

Yang menyenangkan tentang sistem ini adalah pengguna tidak perlu khawatir tentang setiap terjemahan diterapkan untuk itu orang tua atau terjemahan lain yang telah terjadi. Ini juga penting untuk menyadari bahwa ini adalah contoh yang cukup diturunkan. Jika Anda dihapus metode overriden hit (), implementasi standar benar-benar akan bekerja lebih baik. TIDAK perlu menyediakan metode hit () di kelas Aktor berasal Anda kecuali default tidak sesuai dengan kebutuhan Anda. Contoh ini hanyalah untuk menunjukkan bagaimana Scene2D memukul karya deteksi, dan bagaimana menerapkan detektor kustom. Haruskah Anda ingin mengatakan, menerapkan deteksi pixel-sempurna, Anda bisa melakukannya dengan cara ini. Saya berkomentar contoh ini sedikit lebih daripada yang saya lakukan secara teratur, untuk menjelaskan bit saya sudah dipoles. Penjelesan lebih luas kita bisa lihat di laman berikut [Scene Management](http://www.gamefromscratch.com/post/2013/12/11/LibGDX-Tutorial-3C-Scene-management.aspx)

