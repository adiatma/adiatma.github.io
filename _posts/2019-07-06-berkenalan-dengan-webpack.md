---
title: Berkenalan dengan webpack
layout: post
author: adiatma
categories: javascript
image: assets/images/webpack.png
---

## Apa itu webpack?

> webpack adalah static module bundler untuk apalikasi javascript modern

Javascript modern membutuhkan beberapa konfigurasi untuk bisa di dukung oleh browser, misalnya [babel](https://babeljs.io/) sebagai javascript `compiler` untuk mengkompilasi javascript modern ke versi yang di dukung oleh browser. Dalam prosesnya webpack akan membundel beberapa module yang saling berkaitan dan akan di generate menjadi satu file atau lebih.

Berikut adalah beberapa konsep utama dari webpack, yang perlu untuk kita pahami:

+ [Entry](#entry)
+ [Output](#output)
+ [Loaders](#loaders)
+ [Plugins](#plugins)
+ [Mode](#mode)

## Entry

Entry adalah sebuah `entry point` atau titik masuk yang menyatakan sebuah direktori atau file yang akan di gunakan untuk di proses lebih lanjut oleh webpack, dengan menggunakan entry kita akan meminta webpack memproses file yang kita definisikan di dalamnya.

Berikut adalah contoh penggunaan entry:

```js
module.exports = {
  entry: './src/index.js',
}
```

Contoh konfigurasi di atas saya akan meminta webpack untuk memproses file yang berada di direktori `./src/index.js` untuk di proses lebih lanjut.

Untuk lebih detail memahami tentang `entry` silahkan cek [disini](https://webpack.js.org/concepts/entry-points/)

## Output

[Output](https://webpack.js.org/concepts/output/) mendifinisikan akhir dari proses kompilasi webpack, dengan menggunakan output kita bisa memodifikasi file dan direktori yang akan menjadi keluarannya.

Berikut adalah contoh penggunaan output:

```js
module.exports = {
  output: {
    filename: 'bundle.js',
  }
}
```

## Loaders

[Loaders](https://webpack.js.org/concepts/loaders/) adalah konfigurasi untuk mengatur pola apa yang akan kita pakai sebagai aturan yang akan di terapkan oleh webpack dalam memproses file javascript.

Berikut adalah contoh penggunaan loaders:

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        loader: 'babel-loader'
      },
    ],
  },
}
```

Dengan contoh konfigurasi di atas, kita meminta webpack untuk memproses file dengan extensi `.js` (file javascript) untuk di proses menggunakan module [babel-loader](https://github.com/babel/babel-loader).

## Plugins

[Plugins](https://webpack.js.org/concepts/plugins/) adalah konfigurasi tambahan untuk manajemen assets dan setup environment di webpack, misalnya kita ingin menambahkan file dengan extensi `.html` yang akan di proses secara bersamaan saat webpack mengkompilasi file javascript.

Berikut adalah contoh penggunaan plugins:

```js
const HTMLWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  plugins: [
    new HTMLWebpackPlugin()
  ]
}
```

Contoh di atas adalah menggunakan library tambahan seperti [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin). yang secara otomatis akan membuat sebuah file `index.html` sebagai assets tambahan.

## Mode

Sejak versi `4.0.0` webpack telah menmbahkan satu konfigurasi baru, yaitu [mode](https://webpack.js.org/configuration/mode/#root). sebagai tambahan untuk menentukan pengaturan konfigurasi berdasarkan mode yang di tentukan.

Berikut adalah contoh penggunaanya:

```js
module.exports = {
  mode: 'development|production',
}
```

## Kesimpulan

Webpack merupakan salah satu `module bundler` populer yang bisa kita gunakan untuk setup projek javascript, dengan berbagai dependency. untuk lebih lanjut silahkan kunjugi dokumentasi [webpack](https://webpack.js.org/concepts/), dan sebelumnya saya juga sudah membuat beberapa video terkait webpack di [youtube](https://www.youtube.com/watch?v=pYEuAZJ1Rkk&list=UUZOeO1elqR4mGVeman6b3SA).