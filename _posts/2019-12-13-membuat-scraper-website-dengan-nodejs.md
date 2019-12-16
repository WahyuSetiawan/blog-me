---
layout: post
title: Cara Membuat Scrape Website Dengan Nodejs
date: 2019-12-13 22:46
category:
author:
tags: []
summary:
---

Untuk membuat website scrape ini dibutuhkan plugin yang membantu dalam scrape data dati website ini. Untuk mendapatkan hasil data dari html, plugin yang digunakan untuk mendapatkan data itu seperti berikut:

1. express
2. request
3. fs
4. cheerio

express digunakan untuk menghandle routing dari website karena inia kan menjadi listen serve pusat 

request digunakan untuk mendapatkan data dari website yang dituju

fs diguankan untuk menyipan data yang dihasilkan dari json request ke file

cheerio digunakan untuk mengambil data berdasarkan component yang terdapat dalam website selayaknya dengan selector pada jquery

untuk pertama kali diperlukan untuk mendapatkan 