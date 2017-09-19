# Part 17: VIEWPORTS

Sebelumnya kita melihat bagaimana menggunakan kamera dengan LibGDX untuk menghilangkan perbedaan resolusi sehingga tidak lagi menggunakan koordinat pixel. LibGDX menerapkan konsep Viewports, yang dapat dianggap sebagai pengkodean setara dengan tombol aspek di layar, yang mengontrol bagaimana konten non-asli diskalakan untuk ditampilkan di layar.

Ada beberapa macam Viewports:

* ExtendViewport
* FillViewport
* FitViewport
* StretchViewport
* ScreenViewport

Tentu saja kita bisa mewarisi Viewport dan membuatnya sendiri.

Berikut adalah kode untuk membuat FillViewport:

```
package com.gamefromscratch;

import com.badlogic.gdx.ApplicationAdapter;
import com.badlogic.gdx.Gdx;
import com.badlogic.gdx.graphics.GL20;
import com.badlogic.gdx.graphics.OrthographicCamera;
import com.badlogic.gdx.graphics.Texture;
import com.badlogic.gdx.graphics.g2d.Sprite;
import com.badlogic.gdx.graphics.g2d.SpriteBatch;
import com.badlogic.gdx.utils.viewport.FillViewport;
import com.badlogic.gdx.utils.viewport.Viewport;

public class ViewportDemo extends ApplicationAdapter {
   SpriteBatch batch;
   Sprite aspectRatios;
   OrthographicCamera camera;
   Viewport viewport;

   @Override
   public void create () {
      batch = new SpriteBatch();
      aspectRatios = new Sprite(new Texture(Gdx.files.internal("Aspect.jpg")));
      aspectRatios.setPosition(0,0);
      aspectRatios.setSize(100,100);

      camera = new OrthographicCamera();
      viewport = new FillViewport(100,100,camera);
      viewport.apply();

      camera.position.set(camera.viewportWidth/2,camera.viewportHeight/2,0);
   }

   @Override
   public void render () {

      camera.update();
      Gdx.gl.glClearColor(1, 0, 0, 1);
      Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT);

      batch.setProjectionMatrix(camera.combined);
      batch.begin();
      aspectRatios.draw(batch);
      batch.end();
   }

   @Override
   public void dispose(){
      aspectRatios.getTexture().dispose();
   }

   @Override
   public void resize(int width, int height){
      viewport.update(width,height);
      camera.position.set(camera.viewportWidth/2,camera.viewportHeight/2,0);
   }
}
```
FillViewPort akan selalu mengisi viewport, meski itu berarti harus memotong bagian gambar.

![image](https://user-images.githubusercontent.com/30854454/30584344-9f714c96-9d53-11e7-9a97-7d7cacf8a8ed.png)

untuk mengetahui lebih lanjut mengenai ViewPorts, bisa mengunjungi alamat ini
http://www.gamefromscratch.com/post/2014/12/09/LibGDX-Tutorial-Part-17-Viewports.aspx
