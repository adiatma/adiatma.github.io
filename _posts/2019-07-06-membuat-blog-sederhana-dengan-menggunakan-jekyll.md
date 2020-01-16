---
title: Membuat blog sederhana dengan menggunakan Jekyll
layout: post
author: adiatma
image: assets/images/jekyll.png
categories: jekyll
---

> Transform your plain text into static websites and blogs.
-- jekyll

## Apa itu Jekyll?

Jekyll adalah sebuah site-generator yang dibuat dengan menggunakan [ruby](https://www.ruby-lang.org/id/). Dengan bantuan jekyll kita bisa membuat blog sederhana tanpa menggunakan database, seperti yang tertulis di website official [jekyll](https://jekyllrb.com/), "Transform your plain text into static websites and blogs". kemudian ada tiga point utama yang diperkenalkan yaitu **simple**, **static** dan **blog-aware**.

#### Simple

> No more databases, comment moderation, or pesky updates to install—just your content.

Kita bisa membuat content blog, selayaknya cms seperti wordpress, tanpa menggunakan database.

#### Static

> Markdown, Liquid, HTML & CSS go in. Static sites come out ready for deployment.

Dalam membuat konten kita menggunakan file [markdown](https://id.wikipedia.org/wiki/Markdown) yang kemudian akan di transform oleh jekyll menjadi static HTML.

#### Blog-aware

> Permalinks, categories, pages, posts, and custom layouts are all first-class citizens here.

Fitur selanjutnya adalah customize, kita bisa dengan mudah merubah layout, categori dan halaman.

Okey, let's try, kita akan langsung mencobanya, tetapi sebelumnya ada beberapa hal yang harus di install terlebih dahulu, yaitu:

+ Langkah awal install [ruby](https://www.ruby-lang.org/id/documentation/installation/) di sistem operasi kalian, kemudian jika berhasil cek, dengan menggunakan perintah `ruby -v`.
+ Download dan install [rubygems](https://rubygems.org/pages/download), cek dengan perintah `gem -v`.
+ Langkah terakhir install `gem install bundler jekyll`.

Kemudian ada dua langkah membuat projek dengan jekyll, yaitu dengan menggunakan template bawaan dan yang kedua dengan cara yang manual.

#### Dengan Template Bawaan

Buka terminal atau command line kalian, kemudian ketikan perintah berikut.

```
jekyll new <your_project>
cd <your_project>
jekyll serve // untuk menjalankan server
```

#### Dengan Cara Yang Manual

Buat direktory projek kalian misalnya `blog-jekyll`, kemudian buat satu file dengan nama `index.html` dan simpan di dalam direktory `blog-jekyll`.

Contoh file `index.html` adalah seperti dibawah ini:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

Kemudian selanjutnya buka terminal dan ke direktori project `blog-jekyll` yang tadi sudah dibuat, kemudian ketikan perintah `jekyll build` untuk build file static html, dan tunggu sampai selesai setelah itu ketik `jekyll serve` untuk menjalankan server jekyll.

Okey, sampai tahapan ini kalian sudah berhasil membuat static blog dengan menggunakan jekyll. sekarang tahapannya kita akan mencoba membuat konten yang dinamis, dan kemudian akan kita tampilkan di halaman utama. buatlah direktory `_posts` di dalam projek kalian, kemudian buat konten dengan menggunakan format berikut `YEAR-MONTH-DAY-title.MARKUP` => `2019-07-06-judul-blog.md`. kemudian isikan dengan format [front matter](https://jekyllrb.com/docs/front-matter/), misalnya sebagai berikut.

```
---
layout: post
title: Judul Blog
---

Hello World

Lorem ipsume sit amet dolor
```

Kemudian selanjutnya adalah memodifikasi file `index.html` menjadi seperti berikut.

<img src="{{ site.baseurl }}/assets/images/code-html.png">

Setelah selesai sekarang coba jalankan lagi perintah `jekyll build` kemudian `jekyll serve` untuk menjalankan server, maka konten kalian akan tampil di halaman utama, okey sampai disini kalian sudah berhasil membuat blog dengan jekyll, terimakasih dan sampai jumpa ditulisan berikutnya.