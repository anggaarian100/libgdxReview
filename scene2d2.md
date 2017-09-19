# Part 9: Scene2D Part 2 - Actions

Pada bagian kedua dari tutorial LibGDX Scene2D yaitu Actions. Actions adalah cara mudah dan benar-benar opsional untuk mendapatkan Aktor permainan Anda untuk “melakukan hal-hal”.

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
impor com.badlogic.gdx.scenes.scene2d.actions.MoveToAction;


public class SceneDemo3 mengimplementasikan ApplicationListener {
    
    public class MyActor meluas Aktor {
        Tekstur Tekstur = baru tekstur (. GDX file INTERNAL ( "data / jet.png" ));
        public boolean mulai = palsu ;

        publik MyActor () {
            setBounds (getX () getY (), tekstur .getWidth (), tekstur .getHeight ());
        }
        
        @ Override
         public void draw (Batch batch, mengapung alpha) {
            batch.draw ( tekstur , ini .getX (), getY ());
        }
    }
    swasta Tahap tahap ;
    
    @ Override
     public void menciptakan () {        
         tahap = baru Tahap ();
        GDX. masukan .setInputProcessor ( tahap );
        
        MyActor myActor = baru MyActor ();
        
        MoveToAction moveAction = baru MoveToAction ();
        moveAction.setPosition (300F, 0f);
        moveAction.setDuration (10F);
        myActor.addAction (moveAction);
        
        Tahap .addActor (myActor);
    }

    @ Override
     public void buang () {
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
<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=MoveToActionReduced.gif" /> 

Banyak dari kode ini adalah daur ulang dari contoh Scene2D sebelumnya, jadi ini pembahasan bagian baru, yang berada dalam fungsi buat ():

```
@ Override
 public void menciptakan () {        
     tahap = baru Tahap ();
    GDX. masukan .setInputProcessor ( tahap );
    
    MyActor myActor = baru MyActor ();
    
    MoveToAction moveAction = baru MoveToAction ();
    moveAction.setPosition (300F, 0f);
    moveAction.setDuration (10F);
    myActor.addAction (moveAction);
    
    Tahap .addActor (myActor);
}
```
Di sini dibuat MoveToAction, yang bergerak Aktor melekat pada posisi tertentu dari waktu ke waktu.

```
@ Override
 public void tindakan ( pelampung delta) {
     untuk (Iterator <Action> iter = ini .getActions () iterator ();. Iter.hasNext ();) {
        iter.next () tindakan (delta).;
    }
}
```
Jika menjalankan lebih dari satu tindakan seperti:

```
MoveToAction moveAction = baru MoveToAction ();
RotateToAction rotateAction = baru RotateToAction ();
ScaleToAction scaleAction = baru ScaleToAction ();

moveAction.setPosition (300F, 0f);
moveAction.setDuration (5f);
rotateAction.setRotation (90f);
rotateAction.setDuration (5f);
scaleAction.setScale (0.5f);
scaleAction.setDuration (5f);

myActor.addAction (moveAction);
myActor.addAction (rotateAction);
myActor.addAction (scaleAction);

Tahap .addActor (myActor);
```

<img align="middle" src="http://www.gamefromscratch.com/image.axd?picture=RotateScaleMoveActionReduced.gif" /> 

Sebuah tindakan Runnable hanya menjalankan kode tertentu dalam metode run saat, um, jalankan. Itu saja untuk Actions. Cukup sederhana, namun dapat dengan mudah dirantai untuk membuat interaksi yang sangat kompleks. Penjelesan lebih luas kita bisa lihat di laman berikut [Actions](http://www.gamefromscratch.com/post/2013/12/09/LibGDX-Tutorial-9-Scene2D-Part-2-Actions.aspx)

