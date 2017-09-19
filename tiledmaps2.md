# Part 11: Tiled Maps Part 1 - Simple Orthogonal (Top Down) Maps

Pada bagian tutorial ini kita akan melihat memuat peta orthogonal di LibGDX. Orthogonal pada dasarnya berarti “di sudut kanan untuk” yang merupakan cara mewah mengatakan kamera adalah melihat langsung di lokasi kejadian. Kata lain apalagi mewah untuk gaya permainan yang “top down”. Contoh umum termasuk hampir setiap permainan tunggal dari 16Bit generasi konsol seperti Zelda atau MegaMan.
<br>
Salah satu masalah pertama pemain akan menemukan adalah bagaimana pemain membuat peta? Salah satu solusi yang sangat umum adalah Tiled Peta Editor yang untungnya saya baru saja menyelesaikan tutorial tentang!   Tutorial ini mengasumsikan pemain tahu bagaimana untuk menghasilkan file TMX, jadi jika pemain belum pastikan untuk pergi melalui tutorial terkait. Untungnya LibGDX membuatnya sangat mudah untuk bekerja dengan file TMX.
<br>
Hal pertama yang pertama kita perlu menyalin TMX dan setiap / semua file gambar tilemap digunakan untuk folder aset Anda

Sekarang pemainmemiliki peta dan tilesets dalam proyeknya, mari melompat ke kanan dengan kode:
```
Paket com.gamefromscratch;

impor com.badlogic.gdx.ApplicationAdapter;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.Input;
impor com.badlogic.gdx.InputProcessor;
impor com.badlogic.gdx.graphics.GL20;
impor com.badlogic.gdx.graphics.OrthographicCamera;
impor com.badlogic.gdx.graphics.Texture;
impor com.badlogic.gdx.maps.tiled.TiledMap;
impor com.badlogic.gdx.maps.tiled.TiledMapRenderer;
impor com.badlogic.gdx.maps.tiled.TmxMapLoader;
impor com.badlogic.gdx.maps.tiled.renderers.OrthogonalTiledMapRenderer;

public class TiledTest meluas ApplicationAdapter mengimplementasikan InputProcessor {
    Tekstur img ;
    TiledMap tiledMap ;
    OrthographicCamera kamera ;
    TiledMapRenderer tiledMapRenderer ;
    
    @ Override
     public void menciptakan () {
         mengapung w = GDX. grafis .getWidth ();
        mengapung h = GDX. grafis .getHeight ();

        Kamera = baru OrthographicCamera ();
        Kamera .setToOrtho ( palsu , w, h);
        kamera .update ();
        tiledMap = baru TmxMapLoader () beban (. "MyCrappyMap.tmx" );
        tiledMapRenderer = baru OrthogonalTiledMapRenderer ( tiledMap );
        GDX. masukan .setInputProcessor ( ini );
    }

    @ Override
     public void render () {
        GDX. gl .glClearColor (1, 0, 0, 1);
        GDX. gl .glBlendFunc (. GL20 GL_SRC_ALPHA , GL20. GL_ONE_MINUS_SRC_ALPHA );
        GDX. gl .glClear (GL20. GL_COLOR_BUFFER_BIT );
        kamera .update ();
        tiledMapRenderer .setView ( kamera );
        tiledMapRenderer .render ();
    }

    @ Override
     public boolean keyDown ( int keycode) {
         return false ;
    }

    @ Override
     public boolean keyUp ( int keycode) {
         jika (. Keycode == Input.Keys KIRI )
             kamera .translate (-32,0);
        jika (keycode == Input.Keys. KANAN )
             kamera .translate (32,0);
        jika (. keycode == Input.Keys UP )
             kamera .translate (0, -32);
        jika (. keycode == Input.Keys BAWAH )
             kamera .translate (0,32);
        jika (keycode == Input.Keys. NUM_1 )
             tiledMap.getLayers () mendapatkan (0) .setVisible. (! tiledMap .getLayers () mendapatkan (0) .isVisible ().);
        jika (keycode == Input.Keys. NUM_2 )
             tiledMap .getLayers () mendapatkan (1) .setVisible. (! tiledMap .getLayers () mendapatkan (1) .isVisible ().);
        return false ;
    }

    @ Override
     public boolean keyTyped ( Char karakter) {

        return false ;
    }

    @ Override
     public boolean Touchdown ( int screenX, int screenY, int pointer, int tombol) {
         return false ;
    }

    @ Override
     public boolean TouchUp ( int screenX, int screenY, int pointer, int tombol) {
         return false ;
    }

    @ Override
     public boolean touchDragged ( int screenX, int screenY, int pointer) {
         return false ;
    }

    @ Override
     public boolean mouseMoved ( int screenX, int screenY) {
         return false ;
    }

    @ Override
     public boolean menggulir ( int jumlah) {
         return false ;
    }
}
```
<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=image_1202.png" /> 

Hal yang mengesankan di sini adalah bagaimana kode sedikit yang diperlukan untuk mencapai begitu banyak. Singkatnya itu pada dasarnya hanya ini:

```
Kamera = baru OrthographicCamera ();
Kamera .setToOrtho ( palsu , w, h);
kamera .update ();
tiledMap = baru TmxMapLoader () beban (. "MyCrappyMap.tmx" );
tiledMapRenderer = baru OrthogonalTiledMapRenderer ( tiledMap );
```
Pemain membuat OrthographicCamera, set ke dimensi layar dan update () itu. Berikutnya memuat peta menggunakan TmxMapLoader.load () dan menciptakan OrthogonalTiledMapRenderer melintas di peta kita ubin.
<br>
Dalam metode dibuat:
```
kamera .update ();
tiledMapRenderer .setView ( kamera );
tiledMapRenderer . memberikan();
```

Pada dasarnya memperbarui kamera (dalam kasus pindah menggunakan tombol panah), lulus dalam ke TiledMapRenderer dengan setview () dan akhirnya render () peta. Itu dia.
<br>
Seperti yang lihat dalam penangan utama:
```
@ Override
 public boolean keyUp ( int keycode) {
     jika (. Keycode == Input.Keys KIRI )
         kamera .translate (-32,0);
    jika (keycode == Input.Keys. KANAN )
         kamera .translate (32,0);
    jika (. keycode == Input.Keys UP )
         kamera .translate (0, -32);
    jika (. keycode == Input.Keys BAWAH )
         kamera .translate (0,32);
    jika (keycode == Input.Keys. NUM_1 )
         tiledMap .getLayers (). mendapatkan (0) .setVisible (!tiledMap . .getLayers () mendapatkan (0) .isVisible ());
    jika (keycode == Input.Keys. NUM_2 )
         tiledMap .getLayers () mendapatkan (1) .setVisible. (! tiledMap .getLayers () mendapatkan (1) .isVisible ().);
    return false ;
}
```

Jadi pada dasarnya pemain bergerak kiri kamera / kanan / atas / bawah dengan satu ubin setiap kali tombol panah ditekan. Dalam hal 0 atau 1 kunci ditekan kita beralih visibilitas yang lapisan tertentu. Seperti yang dilihat,dapat mengakses lapisan TileMap menggunakan getLayers (). Get () fungsi.. Penjelesan lebih luas kita bisa lihat di laman berikut [Simple Orthogonal (Top Down) Maps](http://www.gamefromscratch.com/post/2014/04/16/LibGDX-Tutorial-11-Tiled-Maps-Part-1-Simple-Orthogonal-Maps.aspx)
