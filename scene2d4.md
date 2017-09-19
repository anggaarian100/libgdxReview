# Part 9: Scene2D Part 4 - UI Skins

Salah satu fitur yang paling menyenangkan dari Scene2D adalah lapisan UI dibangun di atas itu. Scene2D.ui menyediakan serangkaian widget yang membuat menciptakan UI merupakan angin, sesuatu yang sering kurang di perpustakaan pengembangan game. Yang mengatakan, ada satu batu sandungan yang sangat membingungkan sebelum Anda bisa mendapatkan untuk bekerja dengan UI ... Skins.
<br>
Kulit adalah kumpulan file yang pergi bersama-sama untuk membuat antarmuka pengguna.
<br>
Pertama adalah file JSON (JavaScript Object Notation), yang merupakan berbasis JavaScript format penyimpanan data yang populer, seperti cahaya XML. Dalam file JSON Anda menggambarkan berbagai properti dari kulit seperti bagaimana widget akan terlihat. 
<br>
Berikutnya adalah tekstur atlas. Kami melihat menggunakan TexturePacker untuk membuat tekstur atlas kembali tutorial grafis . Tekstur atlas menggambarkan tata letak semua gambar yang membentuk UI Anda. Ini adalah ekstensi file .atlas.
<br>
Seiring dengan atlas tekstur, pemain juga punya gambar yang sebenarnya yang TexturePacker dihasilkan.
<br>
Akhirnya Anda memiliki fnt dan gambar yang terkait. Kami ditutupi font kembali di tutorial Hello World .
<br>
Ini semua bisa tampak cukup menakutkan, terutama mulai dari awal. Untungnya ada kulit termasuk dalam tes LibGDX . File yang Anda tertarik adalah uiskin.atlas, uiskin.json, uiskin.png, default.png dan default.fnt. Cukup download dan menempatkan masing-masing file dalam folder aset / Data Android proyek Anda. Jika Anda men-download dari link Github saya disediakan, pastikan untuk men-download versi RAW setiap file!Berikut code yang bisa diuji:
<br>
Ini adalah berbagai grafis yang masuk ke menciptakan UI. Mari lihat uiskin.json:

```
{
com.badlogic.gdx.graphics.g2d.BitmapFont: {default-font yang: {file: default.fnt}},
com.badlogic.gdx.graphics.Color: {
    hijau: {a: 1, b: 0, g: 1, r: 0},
    putih: {a: 1, b: 1, g: 1, r: 1},
    merah: {a: 1, b: 0, g: 0, r: 1},
    hitam: {a: 1, b: 0, g: 0, r: 0}
},
com.badlogic.gdx.scenes.scene2d.ui.Skin $ TintedDrawable: {
    dialogDim: {Nama: putih, warna: {r: 0, g: 0, b: 0, a: 0,45}}
},
com.badlogic.gdx.scenes.scene2d.ui.Button $ ButtonStyle: {
    default: {bawah: default-round-down, up: default-round},
    beralih: {bawah: default-round-down, diperiksa: default-round-down, up: default-round}
},
com.badlogic.gdx.scenes.scene2d.ui.TextButton $ Tombol Teks Style: {
    default: {bawah: default-round-down, up: default-bulat, huruf: default-font, FONTCOLOR: putih},
    beralih: {bawah: default-round-down, up: default-bulat, diperiksa: default-round-down, huruf: default-font, FONTCOLOR: putih, 
    downFontColor: red}
},
com.badlogic.gdx.scenes.scene2d.ui.ScrollPane $ ScrollPaneStyle: {
    default: {vScroll: default-gulir, hScrollKnob: default-round-besar, latar belakang: default-rect, hScroll: default-scroll, 
    vScrollKnob: default-round-besar}
},
com.badlogic.gdx.scenes.scene2d.ui.SelectBox $ SelectBoxStyle: {
    default: {
        Font: default-font, FONTCOLOR: putih, latar belakang: default-pilih,
        scrollStyle: default,
        listStyle: {font: default-font, seleksi: default-pilih-seleksi}
    }
},
com.badlogic.gdx.scenes.scene2d.ui.SplitPane $ SplitPaneStyle: {
    default-vertikal: {menangani: default-splitpane-vertikal},
    default-horisontal: {menangani: default-splitpane}
},
com.badlogic.gdx.scenes.scene2d.ui.Window $ WindowStyle: {
    default: {titleFont: font default, latar belakang: default window, titleFontColor: putih},
    dialog {titleFont: font default, latar belakang: window Default, titleFontColor: putih, stageBackground: dialogDim}
},
com.badlogic.gdx.scenes.scene2d.ui.Slider $ SliderStyle: {
    default-horisontal: {background: default-slider, tombol: default-slider-knob}
},
com.badlogic.gdx.scenes.scene2d.ui.Label $ LabelStyle: {
    default: {font: default-font, FONTCOLOR: putih}
},
com.badlogic.gdx.scenes.scene2d.ui.TextField $ TextFieldStyle: {
    default: {seleksi: seleksi, latar belakang: textfield, huruf: default-font, FONTCOLOR: putih, kursor: kursor}
},
com.badlogic.gdx.scenes.scene2d.ui.CheckBox $ CheckBoxStyle: {
    default: {checkboxOn: check-on, checkboxOff: check-off, huruf: default-font, FONTCOLOR: putih}
},
com.badlogic.gdx.scenes.scene2d.ui.List $ ListStyle: {
    default: {fontColorUnselected: putih, seleksi: default-rect-pad, fontColorSelected: putih, huruf: default-font yang}
},
com.badlogic.gdx.scenes.scene2d.ui.Touchpad $ TouchpadStyle: {
    default: {background: default-pane, tombol: default-round-besar}
},
com.badlogic.gdx.scenes.scene2d.ui.Tree $ Treestyle: {
    default: {dikurangi: pohon-dikurangi, ditambah: pohon-plus, seleksi: default-pilih-seleksi}
}
}
```

```
Paket com.gamefromscratch;

impor com.badlogic.gdx.ApplicationListener;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.graphics.GL10;
impor com.badlogic.gdx.graphics.g2d.SpriteBatch;
impor com.badlogic.gdx.scenes.scene2d.InputEvent;
impor com.badlogic.gdx.scenes.scene2d.Stage;
impor com.badlogic.gdx.scenes.scene2d.ui.Skin;
impor com.badlogic.gdx.scenes.scene2d.ui.TextButton;
impor com.badlogic.gdx.scenes.scene2d.utils.ClickListener;

public class UIDemo mengimplementasikan ApplicationListener {
     swasta SpriteBatch bets ;
    swasta Kulit kulit ;
    swasta Tahap tahap ;

    @ Override
     public void menciptakan () {        
         bets = baru SpriteBatch ();
        kulit = baru Skin (. GDX file INTERNAL ( "data / uiskin.json" ));
        Tahap = baru Tahap ();

        akhir tombol Tombol text = baru Tombol Text ( "Klik saya" , kulit , "default" );
        
        button.setWidth (200F);
        button.setHeight (20f);
        button.setPosition (. GDX grafis .getWidth () / 2 - 100f, GDX. grafis .getHeight () / 2 - 10F);
        
        button.addListener ( baru ClickListener () {
             @ Override 
             public void diklik (InputEvent acara, mengambang x, mengambang y) {
                button.setText ( "Anda mengklik tombol" );
            }
        });
        
        Tahap .addActor (tombol);
        
        GDX. masukan .setInputProcessor ( tahap );
    }

    @ Override
     public void buang () {
         bets .dispose ();
    }

    @ Override
     public void render () {        
        GDX. gl .glClearColor (1, 1, 1, 1);
        GDX. gl .glClear (GL10. GL_COLOR_BUFFER_BIT );
        
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

<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=image_1067.png" /> 

UI Scene2D adalah topik cukup terlibat, akan menindaklanjuti dengan contoh yang lebih maju tutorial berikutnya.. Penjelesan lebih luas kita bisa lihat di laman berikut [UI Skin](http://www.gamefromscratch.com/post/2013/12/18/LibGDX-Tutorial-9-Scene2D-Part-3-UI-Skins.aspx)
