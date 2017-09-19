# Part 8: Audio

LibGDX membuat audio sangat mudah digunakan. LibGDX mendukung 3 format audio: ogg, mp3 dan wav. MP3 adalah format yang terperosok dalam masalah hukum, sedangkan WAV adalah format ukuran file yang agak besar, sehingga OGG sering menjadi pilihan terbaik.

Memuat file-file audio sangat sederhana

```
Sound wavSound = Gdx.audio.newSound(Gdx.files.internal("data/wav.wav"));
Sound oggSound = Gdx.audio.newSound(Gdx.files.internal("data/ogg.ogg"));
Sound mp3Sound = Gdx.audio.newSound(Gdx.files.internal("data/mp3.mp3"));
```

untuk memainkan audionya hanya menggunakan baris code berikut
``` 
wavSound.play (); 
```
Sangat mudah bukan??, untuk lebih lanjut mengenai audio bisa diikuti di laman ini [Audio](http://www.gamefromscratch.com/post/2013/11/19/LibGDX-Tutorial-8-Audio.aspx)
