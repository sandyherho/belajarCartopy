# Menampilkan peta gempa hari ini

<p style="text-align:justify">Sebagai penutup, penyusun akan mengajak sidang pembaca (yang umumnya dari kalangan geosains) untuk melakukan kegiatan pemetaan gempa selama 24 jam terakhir dari data USGS. Diharapkan modul ini akan membantu pembaca untuk mengaplikasikan materi pembelajaran Cartopy pada bidang keilmuannya masing - masing.</p>

<p style="text-align:justify">Untuk memulai proyek mini ini, kita wajib mengimpor tiga buah pustaka Python, yakni: pandas (untuk membaca data tabular), matplotlib (untuk visualisasi), dan Cartopy (untuk pemetaan).</p>


```python
import pandas as pd
import matplotlib
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
```

Selain itu, kita juga perlu mengatur tampilan plot agar tampak lebih estetik.


```python
%matplotlib inline
matplotlib.rcParams['figure.figsize'] = (14,10)
```

Kita membaca data tabular secara *remote* dengan menggunakan pandas.


```python
df = pd.read_csv('http://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/1.0_week.csv')
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>time</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>depth</th>
      <th>mag</th>
      <th>magType</th>
      <th>nst</th>
      <th>gap</th>
      <th>dmin</th>
      <th>rms</th>
      <th>...</th>
      <th>updated</th>
      <th>place</th>
      <th>type</th>
      <th>horizontalError</th>
      <th>depthError</th>
      <th>magError</th>
      <th>magNst</th>
      <th>status</th>
      <th>locationSource</th>
      <th>magSource</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-07-08T04:37:36.100Z</td>
      <td>33.658167</td>
      <td>-116.725333</td>
      <td>15.36</td>
      <td>2.35</td>
      <td>ml</td>
      <td>83.0</td>
      <td>17.00</td>
      <td>0.05368</td>
      <td>0.20</td>
      <td>...</td>
      <td>2020-07-08T04:41:33.997Z</td>
      <td>9km S of Idyllwild, CA</td>
      <td>earthquake</td>
      <td>0.19</td>
      <td>0.37</td>
      <td>0.192</td>
      <td>26.0</td>
      <td>automatic</td>
      <td>ci</td>
      <td>ci</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-07-08T04:37:10.820Z</td>
      <td>36.455833</td>
      <td>-117.953500</td>
      <td>9.83</td>
      <td>1.48</td>
      <td>ml</td>
      <td>14.0</td>
      <td>150.00</td>
      <td>0.10340</td>
      <td>0.22</td>
      <td>...</td>
      <td>2020-07-08T04:47:40.620Z</td>
      <td>18km SE of Lone Pine, CA</td>
      <td>earthquake</td>
      <td>0.60</td>
      <td>1.06</td>
      <td>0.174</td>
      <td>14.0</td>
      <td>automatic</td>
      <td>ci</td>
      <td>ci</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-07-08T04:28:11.830Z</td>
      <td>38.136800</td>
      <td>-117.888200</td>
      <td>9.00</td>
      <td>1.30</td>
      <td>ml</td>
      <td>10.0</td>
      <td>90.21</td>
      <td>0.02300</td>
      <td>0.08</td>
      <td>...</td>
      <td>2020-07-08T04:34:29.366Z</td>
      <td>34 km SE of Mina, Nevada</td>
      <td>earthquake</td>
      <td>NaN</td>
      <td>1.20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>automatic</td>
      <td>nn</td>
      <td>nn</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-07-08T04:14:48.500Z</td>
      <td>38.126200</td>
      <td>-118.094000</td>
      <td>0.30</td>
      <td>2.20</td>
      <td>ml</td>
      <td>24.0</td>
      <td>64.54</td>
      <td>0.03900</td>
      <td>0.23</td>
      <td>...</td>
      <td>2020-07-08T04:29:31.779Z</td>
      <td>29 km S of Mina, Nevada</td>
      <td>earthquake</td>
      <td>NaN</td>
      <td>15.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>automatic</td>
      <td>nn</td>
      <td>nn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-07-08T04:12:46.220Z</td>
      <td>36.261333</td>
      <td>-89.498497</td>
      <td>9.36</td>
      <td>2.36</td>
      <td>md</td>
      <td>26.0</td>
      <td>50.00</td>
      <td>0.16010</td>
      <td>0.21</td>
      <td>...</td>
      <td>2020-07-08T04:18:13.450Z</td>
      <td>0 km WSW of Ridgely, Tennessee</td>
      <td>earthquake</td>
      <td>0.36</td>
      <td>1.47</td>
      <td>0.390</td>
      <td>17.0</td>
      <td>reviewed</td>
      <td>nm</td>
      <td>nm</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>



Karena kolom time belum berupa objek datetime, maka kita perlu melakukan konversi sebagai berikut: 


```python
df['time'] = pd.to_datetime(df['time'])
type(df['time'][1])
```




    pandas._libs.tslibs.timestamps.Timestamp




```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>time</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>depth</th>
      <th>mag</th>
      <th>magType</th>
      <th>nst</th>
      <th>gap</th>
      <th>dmin</th>
      <th>rms</th>
      <th>...</th>
      <th>updated</th>
      <th>place</th>
      <th>type</th>
      <th>horizontalError</th>
      <th>depthError</th>
      <th>magError</th>
      <th>magNst</th>
      <th>status</th>
      <th>locationSource</th>
      <th>magSource</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020-07-08 04:37:36.100000+00:00</td>
      <td>33.658167</td>
      <td>-116.725333</td>
      <td>15.36</td>
      <td>2.35</td>
      <td>ml</td>
      <td>83.0</td>
      <td>17.00</td>
      <td>0.05368</td>
      <td>0.20</td>
      <td>...</td>
      <td>2020-07-08T04:41:33.997Z</td>
      <td>9km S of Idyllwild, CA</td>
      <td>earthquake</td>
      <td>0.19</td>
      <td>0.37</td>
      <td>0.192</td>
      <td>26.0</td>
      <td>automatic</td>
      <td>ci</td>
      <td>ci</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2020-07-08 04:37:10.820000+00:00</td>
      <td>36.455833</td>
      <td>-117.953500</td>
      <td>9.83</td>
      <td>1.48</td>
      <td>ml</td>
      <td>14.0</td>
      <td>150.00</td>
      <td>0.10340</td>
      <td>0.22</td>
      <td>...</td>
      <td>2020-07-08T04:47:40.620Z</td>
      <td>18km SE of Lone Pine, CA</td>
      <td>earthquake</td>
      <td>0.60</td>
      <td>1.06</td>
      <td>0.174</td>
      <td>14.0</td>
      <td>automatic</td>
      <td>ci</td>
      <td>ci</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2020-07-08 04:28:11.830000+00:00</td>
      <td>38.136800</td>
      <td>-117.888200</td>
      <td>9.00</td>
      <td>1.30</td>
      <td>ml</td>
      <td>10.0</td>
      <td>90.21</td>
      <td>0.02300</td>
      <td>0.08</td>
      <td>...</td>
      <td>2020-07-08T04:34:29.366Z</td>
      <td>34 km SE of Mina, Nevada</td>
      <td>earthquake</td>
      <td>NaN</td>
      <td>1.20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>automatic</td>
      <td>nn</td>
      <td>nn</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2020-07-08 04:14:48.500000+00:00</td>
      <td>38.126200</td>
      <td>-118.094000</td>
      <td>0.30</td>
      <td>2.20</td>
      <td>ml</td>
      <td>24.0</td>
      <td>64.54</td>
      <td>0.03900</td>
      <td>0.23</td>
      <td>...</td>
      <td>2020-07-08T04:29:31.779Z</td>
      <td>29 km S of Mina, Nevada</td>
      <td>earthquake</td>
      <td>NaN</td>
      <td>15.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>automatic</td>
      <td>nn</td>
      <td>nn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2020-07-08 04:12:46.220000+00:00</td>
      <td>36.261333</td>
      <td>-89.498497</td>
      <td>9.36</td>
      <td>2.36</td>
      <td>md</td>
      <td>26.0</td>
      <td>50.00</td>
      <td>0.16010</td>
      <td>0.21</td>
      <td>...</td>
      <td>2020-07-08T04:18:13.450Z</td>
      <td>0 km WSW of Ridgely, Tennessee</td>
      <td>earthquake</td>
      <td>0.36</td>
      <td>1.47</td>
      <td>0.390</td>
      <td>17.0</td>
      <td>reviewed</td>
      <td>nm</td>
      <td>nm</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>



<p style="text-align:justify">Untuk mendapatkan data gempa hari ini, kita perlu melakukan operasi <i>masking</i>. Sebagai catatan, Notebook ini dibuat pada tanggal 8 Juli 2020. Oleh karena itu, penyusun akan melakukan <i>masking</i> waktu dari tanggal 7 hingga 8 Juli 2020 (hal ini patut disesuaikan oleh pembaca).</p> 


```python
mask = ((df['time'] >= '2020-07-07') & (df['time'] < '2020-07-08'))
gempaHariIni = df.loc[mask]
gempaHariIni.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>time</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>depth</th>
      <th>mag</th>
      <th>magType</th>
      <th>nst</th>
      <th>gap</th>
      <th>dmin</th>
      <th>rms</th>
      <th>...</th>
      <th>updated</th>
      <th>place</th>
      <th>type</th>
      <th>horizontalError</th>
      <th>depthError</th>
      <th>magError</th>
      <th>magNst</th>
      <th>status</th>
      <th>locationSource</th>
      <th>magSource</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>56</th>
      <td>2020-07-07 23:51:01.840000+00:00</td>
      <td>19.364666</td>
      <td>-155.218506</td>
      <td>-0.19</td>
      <td>1.89</td>
      <td>ml</td>
      <td>19.0</td>
      <td>113.0</td>
      <td>NaN</td>
      <td>0.12</td>
      <td>...</td>
      <td>2020-07-07T23:56:39.490Z</td>
      <td>8 km S of Volcano, Hawaii</td>
      <td>earthquake</td>
      <td>0.33</td>
      <td>0.38</td>
      <td>0.260</td>
      <td>4.0</td>
      <td>automatic</td>
      <td>hv</td>
      <td>hv</td>
    </tr>
    <tr>
      <th>57</th>
      <td>2020-07-07 23:50:59.200000+00:00</td>
      <td>19.355000</td>
      <td>-155.219330</td>
      <td>-0.99</td>
      <td>1.89</td>
      <td>ml</td>
      <td>13.0</td>
      <td>122.0</td>
      <td>NaN</td>
      <td>0.22</td>
      <td>...</td>
      <td>2020-07-07T23:56:32.460Z</td>
      <td>9 km S of Volcano, Hawaii</td>
      <td>earthquake</td>
      <td>0.33</td>
      <td>0.49</td>
      <td>0.260</td>
      <td>4.0</td>
      <td>automatic</td>
      <td>hv</td>
      <td>hv</td>
    </tr>
    <tr>
      <th>58</th>
      <td>2020-07-07 23:49:48.779000+00:00</td>
      <td>63.196800</td>
      <td>-151.112400</td>
      <td>0.00</td>
      <td>1.00</td>
      <td>ml</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.77</td>
      <td>...</td>
      <td>2020-07-07T23:52:51.616Z</td>
      <td>49 km SE of Denali National Park, Alaska</td>
      <td>earthquake</td>
      <td>NaN</td>
      <td>0.50</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>automatic</td>
      <td>ak</td>
      <td>ak</td>
    </tr>
    <tr>
      <th>59</th>
      <td>2020-07-07 23:49:28.655000+00:00</td>
      <td>12.982600</td>
      <td>92.409200</td>
      <td>10.00</td>
      <td>4.60</td>
      <td>mb</td>
      <td>NaN</td>
      <td>84.0</td>
      <td>1.358</td>
      <td>1.21</td>
      <td>...</td>
      <td>2020-07-08T00:19:28.040Z</td>
      <td>145 km NNW of Bamboo Flat, India</td>
      <td>earthquake</td>
      <td>8.70</td>
      <td>1.90</td>
      <td>0.091</td>
      <td>36.0</td>
      <td>reviewed</td>
      <td>us</td>
      <td>us</td>
    </tr>
    <tr>
      <th>60</th>
      <td>2020-07-07 23:31:29.865000+00:00</td>
      <td>63.560000</td>
      <td>-147.489600</td>
      <td>64.70</td>
      <td>1.40</td>
      <td>ml</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.51</td>
      <td>...</td>
      <td>2020-07-07T23:36:07.686Z</td>
      <td>73 km ESE of McKinley Park, Alaska</td>
      <td>earthquake</td>
      <td>NaN</td>
      <td>0.90</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>automatic</td>
      <td>ak</td>
      <td>ak</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>



Kita dapat mengetahui besaran gempa maksimum dan minimum yang terjadi secara global pada hari ini dengan menggunakan perintah sebagai berikut:


```python
print(df[df['mag'] == df['mag'].min()]) # besaran gempa minimum
```

                                     time   latitude   longitude  depth   mag  \
    231  2020-07-07 06:30:21.850000+00:00  33.352000 -116.359833  10.90  0.95   
    260  2020-07-07 03:55:13.260000+00:00  34.126833 -117.478167   5.23  0.95   
    746  2020-07-05 09:58:50.190000+00:00  37.652500 -118.892333   2.60  0.95   
    776  2020-07-05 06:58:02.870000+00:00  33.509167 -116.480000  13.75  0.95   
    880  2020-07-04 21:18:50.110000+00:00  34.465333 -117.966000   8.39  0.95   
    1415 2020-07-03 04:03:31.650000+00:00  53.860333 -166.751167   8.12  0.95   
    1449 2020-07-03 02:08:45.240000+00:00  33.580833 -116.801667   7.10  0.95   
    1586 2020-07-02 17:50:28.090000+00:00  37.461833 -118.727500   4.54  0.95   
    1781 2020-07-02 05:51:54.490000+00:00  33.334500 -116.187333   8.11  0.95   
    
         magType   nst    gap      dmin   rms  ...                   updated  \
    231       ml  34.0   68.0  0.043300  0.23  ...  2020-07-07T06:34:03.667Z   
    260       ml  15.0  123.0  0.097480  0.13  ...  2020-07-07T03:58:59.157Z   
    746       md  19.0   87.0  0.008846  0.08  ...  2020-07-06T17:02:03.770Z   
    776       ml  36.0   63.0  0.064330  0.17  ...  2020-07-06T14:26:40.280Z   
    880       ml  19.0   55.0  0.018550  0.08  ...  2020-07-07T20:34:43.089Z   
    1415      ml   6.0  102.0  0.044930  0.09  ...  2020-07-06T18:12:24.430Z   
    1449      ml  38.0   28.0  0.033880  0.21  ...  2020-07-03T15:07:33.230Z   
    1586      md  15.0  156.0  0.151300  0.03  ...  2020-07-02T18:51:05.078Z   
    1781      ml  29.0  120.0  0.106000  0.24  ...  2020-07-02T05:55:50.184Z   
    
                                      place        type horizontalError  \
    231       11km N of Borrego Springs, CA  earthquake            0.33   
    260              4km NNW of Fontana, CA  earthquake            0.45   
    746        8km ENE of Mammoth Lakes, CA  earthquake            0.38   
    776                19km ESE of Anza, CA  earthquake            0.24   
    880           6km SSE of Littlerock, CA  earthquake            0.14   
    1415  14 km WSW of Dutch Harbor, Alaska  earthquake            0.35   
    1449               12km WNW of Anza, CA  earthquake            0.27   
    1586         12km SSW of Toms Place, CA  earthquake            0.46   
    1781              17km SSW of Oasis, CA  earthquake            0.39   
    
         depthError  magError  magNst     status  locationSource magSource  
    231        0.56     0.158    24.0  automatic              ci        ci  
    260        1.24     0.324    18.0  automatic              ci        ci  
    746        0.29     0.254    15.0   reviewed              nc        nc  
    776        0.45     0.180    28.0   reviewed              ci        ci  
    880        0.25     0.153    13.0   reviewed              ci        ci  
    1415       0.62     0.245     6.0   reviewed              av        av  
    1449       0.74     0.151    27.0   reviewed              ci        ci  
    1586       2.63     0.245    13.0   reviewed              nc        nc  
    1781       1.82     0.124    21.0  automatic              ci        ci  
    
    [9 rows x 22 columns]



```python
print(df[df['mag'] == df['mag'].max()])
```

                                    time  latitude  longitude   depth  mag  \
    328 2020-07-06 22:54:46.856000+00:00   -5.6368   110.6783  528.66  6.6   
    
        magType  nst   gap   dmin   rms  ...                   updated  \
    328     mww  NaN  20.0  1.422  0.92  ...  2020-07-07T23:00:40.068Z   
    
                                place        type horizontalError depthError  \
    328  93 km N of Batang, Indonesia  earthquake             8.3        6.4   
    
         magError  magNst    status  locationSource magSource  
    328     0.068    21.0  reviewed              us        us  
    
    [1 rows x 22 columns]


Sesudah itu, kita akan mengekstraksi data bujur, lintang, dan besaran gempa (dalam skala Richter) dalam bentuk objek *list*:


```python
bujur = list(df['longitude'])
lintang = list(df['latitude'])
besaran = list(df['mag'])
```

<p style="text-align:justify">Kemudian kita akan mengklasifikasikan titik - titik gempa dengan menggunakan warna - warna tertentu (hijau untuk gempa di bawah 3 SR, kuning untuk gempa dengan rentang 3 - 5 SR, dan merah untuk gempa di atas 5 SR) dengan menggunakan fungsi sebagai berikut:</p>


```python
def warna(besaran):
    if besaran < 3.0:
        return 'g'
    elif 3.0 <= besaran < 5.0:
        return 'y'
    else:
        return 'r'
```

Kemudian kita tinggal melakukan pemetaan dengan menggunakan Cartopy:


```python
ax = plt.axes(projection = ccrs.PlateCarree())
ax.coastlines(resolution='50m')
ax.stock_img()

for i in range(len(besaran)):
    warnaEpi = warna(besaran[i])
    plt.scatter(bujur[i], lintang[i], s=besaran[i]*10, c=warnaEpi)

plt.title('Peta gempa bumi global pada 7 - 8 Juli 2020');
```


![png](output_21_0.png)

