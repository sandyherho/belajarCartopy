# Cara Cepat Belajar Dasar – Dasar Pemetaan Menggunakan Cartopy

[![forthebadge](https://forthebadge.com/images/badges/cc-0.svg)](https://forthebadge.com) 
[![forthebadge](https://forthebadge.com/images/badges/built-by-hipsters.svg)](https://forthebadge.com)
[![forthebadge made-with-python](http://ForTheBadge.com/images/badges/made-with-python.svg)](https://www.python.org/)

oleh:

[Sandy H.S. Herho](mailto:sandy.herho@igdore.org) 

<p style="text-align:justify">Cartopy merupakan pustaka Python yang digunakan untuk proses pembuatan peta dan ditujukan untuk menggantikan pustaka basemap yang rencananya tidak akan diteruskan pada akhir tahun 2020 ini. Seperti pada basemap, Cartopy juga dijalankan di atas pustaka matplotlib. Cartopy bergantung pada beberapa pustaka Python lainnya seperti geos dan shapely, oleh karena itu instalasi menggunakan pip akan sangat sulit untuk dilakukan pemula. Maka dari itu, pada tutorial ini saya menyarankan kepada para pengguna untuk melakukan instalasi dengan menggunakan <a href="https://docs.conda.io/en/latest/miniconda.html">Miniconda 3</a>. Sesudah melakukan instalasi Miniconda 3, jalankan perintah sebagai berikut di Terminal pengguna masing - masing:</p>

```(bash)
conda install -c conda-forge cartopy
```
<p style="text-align:justify">Selain itu, pembaca juga diharapkan untuk melakukan instalasi pustaka pandas yang digunakan untuk pembacaan data csv pada bagian akhir tutorial singkat ini:</p>

```(bash)
conda install -c anaconda pandas
```

<p style="text-align:justify">Pada tutorial ini, penyusun juga akan menggunakan Jupyter Notebook sebagai lingkungan pengembangannya. Diharapkan pengguna juga menggunakan lingkungan pengembangan yang sama, oleh karena itu, jalankan perintah sebagai berikut di Terminal kalian masing - masing:</p>

```(bash)
conda install -c anaconda jupyter
```

Untuk memulai sesi Jupyter Notebook, jalankan perintah:
```(bash)
jupyter notebook
```

Maka secara otomatis peramban web bawaan kalian akan membuka sesi Jupyter Notebook.

Pada tutorial ini penyusun akan membahas tentang dasar - dasar pemetaan menggunakan Cartopy. Berikut ini susunan materi yang penyusun sampaikan dalam tutorial ini:

1. Membuat peta pertama
2. Sekilas tentang proyeksi peta
3. Menambahkan fitur pada peta
4. Membaca file shp dan menampilkan data geometri negara
5. Menampilkan peta gempa hari ini

Terimakasih kepada: [WCPL ITB](http://weather.meteo.itb.ac.id/) 

![WCPL ITB](wcpl.png)