---
layout: post
title: Perkenalan React Native
date: 2019-12-08 13:38
category: [ react, mobile, blog]
author: Wahyu Setiawan
tags: [ react, mobile, blog]
summary: 
---


Catatan belajar menggunakan react native dengan 

1. menginstall react native dengan cara menginstall melalui software npm untuk pertama kali kamu install npm yang terdapat dari server

Cata menggunakan ListView di React Native untuk menggunakna list di react native dapat menggunakan cara FlatList dari component React Native. Masukan coding ini didalam React Native yang diperuntukan untuk menampilkan data dari list array kedalam data yang di View Flat List

<FLatList data={} renderItem={(data) => {
    // data == {item : (), index : 0}
    return <View>return dari data {{ data.index }}</View>
}}>

3. Navigation untuk berbagai dari React Native 

untuk mendeteksi suatu dari gesture tab dapat dilakukan dengan menambahkan button atau menambahkan touchable opacity