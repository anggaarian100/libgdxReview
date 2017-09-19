# Part 9: Scene2D Part 1

Pada bagian ini kita akan melihat pada perpustakaan Scene2D. Dan Scene2d sepenuhnya opsional, Pada bagian ini kita akan melihat pada perpustakaan Scene2D. Dan Scene2d sepenuhnya opsional, ada dasarnya grafik adegan adalah struktur data untuk menyimpan barang-barang di dunia pemain. Jadi jika dunia permainan pemain terdiri dari puluhan atau ratusan sprite, mereka sprite disimpan dalam grafik adegan. Selain memegang isi dunia pemain, Scene2D menyediakan sejumlah fungsi yang melakukan pada data tersebut. Hal-hal seperti deteksi hit, menciptakan hirarki antara objek permainan, routing yang input, menciptakan tindakan untuk memanipulasi node dari waktu ke waktu, dll.

Berikut code yang bisa diuji:
```
Paket com.gamefromscratch;

impor com.badlogic.gdx.ApplicationListener;
impor com.badlogic.gdx.Gdx;
impor com.badlogic.gdx.graphics.GL10;
impor com.badlogic.gdx.graphics.Texture;
impor com.badlogic.gdx.graphics.g2d.Batch;
impor com.badlogic.gdx.scenes.scene2d.Actor;
impor com.badlogic.gdx.scenes.scene2d.Stage;

public class SceneDemo mengimplementasikan ApplicationListener {
    
    public class MyActor meluas Aktor {
        Tekstur Tekstur = baru tekstur (. GDX file INTERNAL ( "data / jet.png" ));
        @ Override
         public void draw (Batch batch, mengapung alpha) {
            batch.draw ( tekstur , 0,0);
        }
    }
    
    swasta Tahap tahap ;
    
    @ Override
     public void menciptakan () {        
         tahap = baru Tahap (GDX. Grafis .getWidth (), GDX. Grafis .getHeight (), benar );
        
        MyActor myActor = baru MyActor ();
        Tahap .addActor (myActor);
    }

    @ Override
     public void buang () {
         tahap .dispose ();
    }

    @ Override
     public void render () {    
        GDX. gl .glClear (GL10. GL_COLOR_BUFFER_BIT );
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
<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=image_1032.png" /> 

```
package com.gamefromscratch;

import com.badlogic.gdx.ApplicationListener;
import com.badlogic.gdx.Gdx;
import com.badlogic.gdx.graphics.GL10;
import com.badlogic.gdx.graphics.Texture;
import com.badlogic.gdx.graphics.g2d.Batch;
import com.badlogic.gdx.scenes.scene2d.Actor;
import com.badlogic.gdx.scenes.scene2d.InputEvent;
import com.badlogic.gdx.scenes.scene2d.InputListener;
import com.badlogic.gdx.scenes.scene2d.Stage;
import com.badlogic.gdx.scenes.scene2d.Touchable;

public class SceneDemo2 implements ApplicationListener {
    
    public class MyActor extends Actor {
        Texture texture = new Texture(Gdx.files.internal("data/jet.png"));
        float actorX = 0, actorY = 0;
        public boolean started = false;

        public MyActor(){
            setBounds(actorX,actorY,texture.getWidth(),texture.getHeight());
            addListener(new InputListener(){
                public boolean touchDown (InputEvent event, float x, float y, int pointer, int button) {
                    ((MyActor)event.getTarget()).started = true;
                    return true;
                }
            });
        }
        
        
        @Override
        public void draw(Batch batch, float alpha){
            batch.draw(texture,actorX,actorY);
        }
        
        @Override
        public void act(float delta){
            if(started){
                actorX+=5;
            }
        }
    }
    
    private Stage stage;
    
    @Override
    public void create() {        
        stage = new Stage();
        Gdx.input.setInputProcessor(stage);
        
        MyActor myActor = new MyActor();
        myActor.setTouchable(Touchable.enabled);
        stage.addActor(myActor);
    }

    @Override
    public void dispose() {
    }

    @Override
public void render() {    
    Gdx.gl.glClear(GL10.GL_COLOR_BUFFER_BIT);
    stage.act(Gdx.graphics.getDeltaTime());
    stage.draw();
}

    @Override
    public void resize(int width, int height) {
    }

    @Override
    public void pause() {
    }

    @Override
    public void resume() {
    }
}
```

<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=scene2_thumb.gif" /> 

Scene2D adalah subjek yang cukup besar, jadi pembahasannya menjadi beberapa bagian. Penjelesan lebih luas kita bisa lihat di laman berikut [Scene2D](http://www.gamefromscratch.com/post/2013/11/27/LibGDX-Tutorial-9-Scene2D-Part-1.aspx)
