# Part 11: Tiled Maps Part 2 - Adding a Sprite and Dealing with Layers

Sekarang kita ingin menambahkan beberapa karakter untuk itu, secara harfiah. Tergantung pada kebutuhan pemain ini bisa menjadi laughably sederhana atau agak rumit. Mari kita lihat contoh dasar. Ini adalah membangun contoh kode kita sebelumnya dan jika pemain telah bekerja melalui tutorial sebelumnya dalam seri ini, tidak ada yang baru di sini belum.
Berikut code yang bisa diuji:
```
Paket com.gamefromscratch;

impor com.badlogic.gdx.ApplicationAdapter;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.Input;
impor com.badlogic.gdx.InputProcessor;
impor com.badlogic.gdx.graphics.GL20;
impor com.badlogic.gdx.graphics.OrthographicCamera;
impor com.badlogic.gdx.graphics.Texture;
impor com.badlogic.gdx.graphics.g2d.Sprite;
impor com.badlogic.gdx.graphics.g2d.SpriteBatch;
impor com.badlogic.gdx.graphics.g2d.TextureRegion;
impor com.badlogic.gdx.maps.MapLayer;
impor com.badlogic.gdx.maps.objects.TextureMapObject;
imporcom.badlogic.gdx.maps.tiled.TiledMap;
impor com.badlogic.gdx.maps.tiled.TiledMapRenderer;
impor com.badlogic.gdx.maps.tiled.TmxMapLoader;

impor com.badlogic.gdx.math.Vector3;

public class TiledTest meluas ApplicationAdapter mengimplementasikan InputProcessor {
    Tekstur img ;
    TiledMap tiledMap ;
    OrthographicCamera kamera ;
    TiledMapRenderer tiledMapRenderer ;
    SpriteBatch sb ;
    Tekstur tekstur ;
    Sprite sprite ;
    MapLayer objectLayer ;

    Tekstur Daerah wilayah tekstur ;

    @ Override
     public void menciptakan () {
         mengapung w = GDX. grafis .getWidth ();
        mengapung h = GDX. grafis .getHeight ();

        Kamera = baru OrthographicCamera ();
        Kamera .setToOrtho ( palsu , w, h);
        kamera .update ();
        tiledMap = baru TmxMapLoader () beban (. "MyCrappyMap.tmx" );
        tiledMapRenderer = baru OrthogonalTiledMapRendererWithSprites ( tiledMap );
        GDX. masukan .setInputProcessor ( ini );
        Tekstur = baru Tekstur (. GDX file INTERNAL ( "pik.png" ));

        objectLayer = tiledMap . .getLayers () mendapatkan ( "benda" );
        textureRegion = baru TextureRegion ( tekstur , 64,64);

        TextureMapObject TMO = baru TextureMapObject ( textureRegion );
        tmo.setX (0);
        tmo.setY (0);
        objectLayer .getObjects () menambahkan (TMO).;
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
        Vector3 clickCoordinates = baru Vector3 (screenX, screenY, 0);
        Umum Vector3 = kamera .unproject (clickCoordinates);
        Karakter TextureMapObject = (TextureMapObject) tiledMap . .getLayers () mendapatkan ( "benda" ) .getObjects () mendapatkan (0).;
        character.setX (( pelampung .) posisi x );
        character.setY (( pelampung .) posisi y );
        kembali benar ;
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

Banyak metode yang bisa dipakai, preferensi pribadi pemain dan persyaratan permainan pemain. Sendiri, saya menemukan kedua untuk menjadi mungkin yang paling bersih. Tentu saja jika sprite pemain tidak perlu peduli kedalaman ubin sama sekali, pemain dapat mengabaikan semua ini dan hanya menggunakan SpriteBatch di atas dan menyelamatkan diri banyak sakit kepala! Penjelesan lebih luas kita bisa lihat di laman berikut [Adding a Sprite and Dealing with Layers](http://www.gamefromscratch.com/post/2014/05/01/LibGDX-Tutorial-11-Tiled-Maps-Part-2-Adding-a-character-sprite.aspx)

