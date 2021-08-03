# Project 2: Data Analysis [COVID-19 Indonesia Dataset (Analysis)]

Overview:
1. Membuat analisis data dengan python berdasarkan dataset yang berisi data COVID-19 di Indonesia
2. Dataset berasal dari [kaggle.com](https://www.kaggle.com/) dengan nama COVID-19 Indonesia Dataset yang disusun oleh Hendratno yang mengambil data dari beberapa sumber yaitu [situs resmi pemerintah SATGAS COVID-19](https://covid19.go.id/), [Badan Pusat Statistik](https://www.bps.go.id/), dan [Hub InaCOVID-19](https://bnpb-inacovid19.hub.arcgis.com/)
3. Dataset disusun berdasarkan time series atau sususan waktu, tingkat nasional, dan tingkat provinsi, juga beserta data demografi dari lokasi/daerah tersebut
4. Dataset memiliki 37 kolom
   - **'Date'** (Tanggal dilaporkan)
   - **'Location ISO Code'** (Kode lokasi berdasarkan standar ISO)
   - **'Location'** (Nama lokasi)
   - **'New Cases'** (Kasus positif harian)
   - **'New Deaths'** (Kasus kematian harian)
   - **'New Daily Recovered'** (Kasus kesembuhan harian)
   - **'New Active Cases'** (Kasus aktif harian)
   - **'Total Cases'** (Jumlah akumulatif kasus positif sampai waktu terkait)
   - **'Total Deaths'** (Jumlah akumulatif kasus kematian sampai waktu terkait)
   - **'Total Recovered'** (Jumlah akumulatif kasus kesembuhan sampai waktu terkait)
   - **'Total Active Cases'** (Jumlah akumulatif kasus aktif sampai waktu terkait)
   - **'Location Level'** (Tingkat lokasi regional atau nasional)
   - **'City or Regency'** (Nama kota atau wilayah)
   - **'Province'** (Nama provinsi lokasi)
   - **'Country'** (Nama negara lokasi)
   - **'Island'** (Nama pulau utama lokasi)
   - **'Time Zone'** (Zona waktu lokasi)
   - **'Special Status'** (Status istimewa lokasi)
   - **'Total Regencies'** (Jumlah kabupaten dalam lokasi terkait)
   - **'Total Cities'** (Jumlah kota dalam lokasi terkait)
   - **'Total Districts'** (Jumlah kecamatan dalam lokasi terkait)
   - **'Total Urban Village'** (Jumlah pedesaan dalam lokasi terkait)
   - **'Total Rural Village'** (Jumlah perkampungan dalam lokasi terkait)
   - **'Area (km2)'** (Area lokasi dalam kilometer persegi)
   - **'Population'** (Jumlah populasi dalam lokasi terkait)
   - **'Population Density'** (Kepadatan penduduk dalam lokasi terkait, rumus = Population / Area)
   - **'Longitude'** (Garis bujur lokasi)
   - **'Latitude'** (Garis lintang lokasi)
   - **'New Cases per Million'** (Rumus = (New Cases / Population) x 1.000.000)
   - **'Total Cases per Million'** (Rumus = (Total Cases / Population) x 1.000.000)
   - **'Total Deaths per Million'** (Rumus = (Total Deaths / Population) x 1.000.000)
   - **'Case Fatality Rate'** (Rumus = (Total Deaths / Total Cases) x 100)
   - **'Case Recovered Rate'** (Rumus = (Total Recovered / Total Cases) x 100)
   - **'Growth Factor of New Cases'** (Kurang dari 1 artinya menurun, 1 artinya tidak ada perubahan, lebih dari 1 artinya meningkat, rumus = Today New Cases / Yesterday New Cases)
   - **'Growth Factor of New Deaths'** (Kurang dari 1 artinya menurun, 1 artinya tidak ada perubahan, lebih dari 1 artinya meningkat, rumus = Today New Deaths / Yesterday New Deaths)
5. Tahapan dalam menganalisa data yang akan dilakukan terhadap dataset terbagi menjadi tiga tahap
   - Data Preparation
   - Data Wrangling
   - Data Analysis
6. Project menggunakan dataset berasal [kaggle](https://www.kaggle.com/), yang disusun oleh Hendratno.
   - Repository project Github dapat diakses [disini](https://github.com/hibartaufik/Data-Analysis-Covid-in-Indonesia)
   - Dataset dapat diakses [disini](https://www.kaggle.com/hendratno/covid19-indonesia)

## 1. Data Preparation
### 1.1 Import Libraries
Import beberapa library yang dibutuhkan
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```
### 1.2 Import Dataset
Import dataset yang akan digunakan, lalu tampilkan dataset untuk mengecek apakah import berhasil atau tidak
```
df = pd.read_csv('./dataset/covid_19_indonesia_time_series_all.csv')
df.head()
```
![image](https://user-images.githubusercontent.com/74480780/124726805-4bee4080-df38-11eb-8a99-0632f0fdc24e.png)
## 2. Data Wrangling
### 2.1 Memahami Isi Data
Sumber dataset berasal dari kaggle.com, disusun oleh Hendratno. Data disusun berdasarkan time series, baik di tingkat negara (Indonesia), maupun di tingkat provinsi. Data didapatkan dari berbagai sumber yaitu [situs resmi pemerintah SATGAS COVID-19](https://covid19.go.id/), [Badan Pusat Statistik](https://www.bps.go.id/), dan [Hub InaCOVID-19](https://bnpb-inacovid19.hub.arcgis.com/).

Memeriksa dan menemukan data yang bersifat redundant, data yang terduplikasi, dan data NULL yang sekiranya tidak dibutuhkan dalam analisa. Setelah data ditemukan, maka data akan di drop/dibuang agar dataset yang di-analisa lebih rapi dan menghasilkan insight-insight yang lebih akurat. Hal pertama yang dilakukan ialah memahami data dari tiap kolom dengan membaca deskripsi atau summary tiap kolom dari dataset. Untuk dataset yang sedang digunakan, kita dapat mengetahui deskripsi tiap kolom dengan mengakses sumber dataset di [kaggle.com](https://www.kaggle.com/).

### 2.2 Menemukan dan Membuang Data yang Tidak Dibutuhkan
- Memeriksa data tiap kolom
```
df.info()
```
![image](https://user-images.githubusercontent.com/74480780/124795772-9c868d80-df7a-11eb-87cb-bd0a1a2dc444.png)
![image](https://user-images.githubusercontent.com/74480780/124795898-c3dd5a80-df7a-11eb-9218-21e87d89db55.png)
Dataset memiliki 37 kolom, terdiri dari 12 kolom dengan tipe data object/string, 12 kolom dengan tipe data integer, dan 13 kolom dengan tipe data float. Kita juga dapat memeriksa dimensi dataset untuk memastikan jumlah kolom dan baris.
```
df.shape
```
![image](https://user-images.githubusercontent.com/74480780/124796275-2df5ff80-df7b-11eb-9e15-839ef8ea4431.png)
Mengetahui karakteristik data dengan memeriksa jumlah data NULL dalam setiap kolom
```
df.isnull().sum()
```
![image](https://user-images.githubusercontent.com/74480780/124796852-d1471480-df7b-11eb-95ed-e592f8c7243a.png)
![image](https://user-images.githubusercontent.com/74480780/124796942-e91e9880-df7b-11eb-9fb9-80f977cb3ff3.png)
Terlihat dalam beberapa kolom dataset memiliki data NULL, bahkan untuk kolom **'City or Regency'** semua datanya bernilai NULL. Setelah kita memahami isi data dengan membaca deskripsi tiap kolom, kita dapat menetukan kolom mana saja yang tidak terlalu penting dan harus di drop.

- Drop kolom yang dirasa tidak dibutuhkan

Kolom yang akan di drop yaitu **'Location ISO Code'**, **'City or Regency'**, **'Country'**, **'Continent'**, **'Time Zone'**, **'Special Status'**, **'Total Cities'**, **'Total Districts'**, **'Total Regencies'**, **'Total Urban Villages'**, **'Total Rural Villages'**, **'Area (km2)'**, **'New Cases per Million'**, **'Total Cases per Million'**, **'New Deaths per Million'**, **'Total Deaths per Million'**, **'Growth Factor of New Cases'**, dan **'Growth Factor of New Deaths'**.
```
df.drop(['Location ISO Code', 'City or Regency', 'Country', 'Continent', 'Time Zone', 'Special Status', 'Total Cities', 'Total Districts', 'Total Regencies', 'Total Urban Villages', 'Total Rural Villages', 'Area (km2)', 'New Cases per Million', 'Total Cases per Million', 'New Deaths per Million', 'Total Deaths per Million', 'Growth Factor of New Cases', 'Growth Factor of New Deaths'], axis=1, inplace=True)
```

- Ubah tipe data Date menjadi tipe data datetime agar menghindari kesalahan dalam pengurutan time-series untuk visualisasi

```
df['Date'] = pd.to_datetime(df['Date'], format="%m/%d/%Y")
```

Cek untuk melihat perubahan yang sudah dilakukan
```
df.info()
```
![image](https://user-images.githubusercontent.com/74480780/127913832-164d33c1-339d-4aa5-8340-fe2aff324f99.png)

Kini dataset memiliki 19 kolom
## 3. Data Analysis
Melihat korelasi atau hubungan tiap kolom pada dataset
```
# melihat korelasi/hubungan tiap data antar feature
df.corr()
```
![image](https://user-images.githubusercontent.com/74480780/124797820-e96b6380-df7c-11eb-80c3-2912285909af.png)
Agar mudah dipahami, korelasi/hubungan tiap kolom dapat dilihat melalui visualisasi heatmap
```
#visualisasi heatmap hubungan antar feature
mask = np.triu(df.corr())
plt.style.use('seaborn')
fg, ax = plt.subplots(figsize=(18, 7), dpi=200)
sns.heatmap(df.corr(), mask=mask, cmap='Reds', annot=True, linewidths=1)
plt.title('KORELASI TIAP FEATURE', fontweight='bold', fontsize=20)
plt.xticks(rotation=30)
plt.show()
```
![image](https://user-images.githubusercontent.com/74480780/124798163-41a26580-df7d-11eb-809f-7592305e9daf.png)

### 3.1 Q1: Per tanggal berapa kasus baru COVID-19 terbanyak ditemukan dalam satu hari?
A1.1 : Urutan 10 tanggal dengan kasus COVID-19 paling banyak

Filter data berdasarkan kolom **'New Cases'**, lalu tampilkan 10 data dengan jumlah angka kesembuhan terbanyak beserta tanggalnya(kolom **'Date'**). Lalu tampilkan juga kolom **'Location'** untuk menunjukkan bahwa angka **'New Cases'** di-akumulatif tidak dari satu lokasi saja (Akumulatif dari seluruh wilayah di Indonesia per tanggal terkait).
```
top_10_date_new_cases = df.sort_values(by='New Cases', ascending=False, ignore_index=True)[['Date', 'New Cases', 'Location']][:10]
top_10_date_new_cases
```
![image](https://user-images.githubusercontent.com/74480780/125093059-29a52000-e0fc-11eb-9640-14f00cb48efa.png)
Berdasarkan urutan data di atas, kasus COVID-19 paling banyak ditemukan dalam satu hari yaitu pada tanggal 30 Januari 2021 sebanyak 14.518 kasus baru. Hal menariknya yaitu 9 dari 10 tanggal teratas dengan kasus COVID-19 per hari terbanyak berada pada bulan Januari 2021, artinya kasus cenderung naik pada bulan Januari 2021 dan mencapai puncaknya pada akhir bulan.

A1.2 : Visualisasi kenaikan **'New Cases'** berdasarkan urutan 10 tanggal dengan kasus COVID-19 paling banyak per hari
```
# mengakses data dan memasukannya ke dalam list agar dapat di-visualisasikan
x1_2 = list(top_10_date_new_cases.sort_values(by='Date').to_dict()['Date'].values())
y1_2 = list(top_10_date_new_cases.sort_values(by='Date').to_dict()['New Cases'].values())
```
```
plt.style.use('seaborn')
fg, ax = plt.subplots(figsize=(16,6), dpi=200)
sns.lineplot(x=x1_2, y=y1_2, color='blue', marker='o', linewidth=1)
plt.ylim(ymin=12000, ymax=15000)
plt.text(0.64, 0.81, 'Puncak kasus COVID-19 per hari sebanyak 14.518', fontsize=12,transform=fg.transFigure, color='red')
plt.title('Laju Pertumbuhan Kasus COVID-19 Per Tanggal 15 Januari - 6 Februari 2021', fontsize=18, fontweight='bold', pad=40)
plt.xlabel('Tanggal', fontsize=12, fontweight='bold')
plt.ylabel('Jumlah Kasus', fontsize=12, fontweight='bold')
plt.show()
```
![image](https://user-images.githubusercontent.com/74480780/124799193-7a8f0a00-df7e-11eb-9768-98738b5add1d.png)
Berdasarkan visualisasi di atas, pertumbuhan kasus dimulai semenjak pertengahan bulan. Lalu sempat naik turun hingga mencapai kasus minimal pada 23 Januari, namun justru setelah itu peningkatan kasus COVID-19 per hari semakin melonjak hingga mencapai puncaknya pada 30 Januari sebanyak 14.518 kasus per hari.
### 3.2 Q2: Provinsi mana saja yang memiliki kasus baru terbanyak per hari?
A2.1: Urutan 5 provinsi dengan penemuan kasus COVID-19 per hari terbanyak

Filter data dari kolom **'New Cases'**, lalu tampilkan beserta provinsinya(kolom **'Province'**).
```
df_not_ll = df.loc[df['Location Level'] == 'Province'].sort_values(by='New Cases', ascending=False)[['Province', 'New Cases']]
df_not_ll.groupby('Province')[['New Cases']].sum().sort_values(by='New Cases', ascending=False)[:5]
```
![image](https://user-images.githubusercontent.com/74480780/124799935-47994600-df7f-11eb-8c0a-799802d428ec.png)
Provinsi DKI Jakarta memiliki total kasus per hari tertinggi sebanyak 379.204 kasus, Diikuti oleh Jawa Barat, Jawa Tengah, Jawa Timur, dan Kalimantan Timur. Angka ini didapat dengan menjumlahkan kasus per hari dari tiap provinsi, lalu mengurutkan 5 provinsi dengan jumlah kasus per hari tertinggi.

A2.2: Visualisasi perbandingan antar provinsi dengan total penemuan kasus COVID-19 per hari terbanyak
```
a22 = df_not_ll.groupby('Province')[['New Cases']].sum().sort_values(by='New Cases', ascending=False)[:5]
x2_2 = list(a22.to_dict()['New Cases'].keys())
y2_2 = list(a22.to_dict()['New Cases'].values())
```
```
plt.style.use('seaborn')
fg, ax = plt.subplots(figsize=(16,6), dpi=200)
sns.barplot(x=x2_2, y=y2_2, color='blue')
plt.ylim(ymax=450000)
plt.title('Perbandingan Tiap Provinsi dengan Total Penemuan Kasus Baru COVID-19 per Hari', fontsize=18, fontweight='bold', pad=40)
plt.xlabel('Provinsi', fontsize=12, fontweight='bold')
plt.ylabel('Jumlah Kasus', fontsize=12, fontweight='bold')
plt.show()
```
![a22picture](https://user-images.githubusercontent.com/74480780/127914641-df0c39c7-6c0e-4a41-8346-4a0f5ca1aa67.png)


### 3.3 Q3: Pulau mana saja yang memiliki kasus per hari terbanyak? 
A3.1: Pulau dengan jumlah kasus per hari terbanyak

Filter data dari kolom **'New Cases'**, lalu tampilkan beserta pulaunya(kolom **'Island'**).
```
top_islands_new_cases = df.loc[df.Island != None].groupby(['Island'])[['New Cases']].sum().sort_values(by='New Cases', ascending=False)
top_islands_new_cases
```
![image](https://user-images.githubusercontent.com/74480780/124800563-fb9ad100-df7f-11eb-85b9-299c50e22e30.png)

A3.2: Visualisasi perbandingan tiap pulau dengan jumlah kasus per hari terbanyak
```
x3_2 = list(top_islands_new_cases.to_dict()['New Cases'].keys())
y3_2 = list(top_islands_new_cases.to_dict()['New Cases'].values())
```
```
plt.style.use('seaborn')
fg, ax = plt.subplots(figsize=(16,4), dpi=200)
sns.barplot(x=x3_2, y=y3_2, color='blue')
plt.title('Perbandingan Tiap Pulau dengan Total Penemuan Kasus Baru COVID-19 per Hari', fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Pulau', fontsize=12, fontweight='bold')
plt.ylabel('Jumlah Kasus (Juta)', fontsize=12, fontweight='bold')
labels, location = plt.yticks()
plt.yticks(labels, (labels/1000000).astype(float))
plt.show()
```
![image](https://user-images.githubusercontent.com/74480780/124803211-0440d680-df83-11eb-8a36-b292d7a35390.png)
Berdasarkan visualisasi di atas total penemuan kasus COVID-19 per hari berpusat di pulau Jawa menembus hingga 1 juta kasus, perbandingan yang terlihat sangat mencolok jika dibandingkan dengan total penemuan kasus COVID-19 per hari di pulau lain. Hal ini cocok dengan analisa sebelumnya dimana 4 dari 5 provinsi dengan total penemuan kasus COVID-19 per hari terbanyak berada di pulau Jawa.

### 3.4 Q4: Provinsi manakah dengan total rata-rata kesembuhan paling tinggi per hari?
A4.1: Urutan provinsi dengan kesembuhan paling tinggi per hari

Filter data dari kolom **'New Recovered'**, lalu tampilkan beserta provinsinya(kolom **'Island'**).
```
top_province_new_rcvry = df.loc[df['Location Level'] == 'Province'].groupby(['Province'])[['New Recovered']].sum().sort_values(by='New Recovered', ascending=False)
top_province_new_rcvry[:10]
```
![image](https://user-images.githubusercontent.com/74480780/124800952-74019200-df80-11eb-97f0-0619499991e4.png)

A4.2: Visualisasi perbandingan provinsi dengan kesembuhan tertinggi per hari
```
x4_2 = list(top_province_new_rcvry[:10].to_dict()['New Recovered'].keys())
y4_2 = list(top_province_new_rcvry[:10].to_dict()['New Recovered'].values())
```
```
plt.style.use('seaborn')
fg, ax = plt.subplots(figsize=(16,6), dpi=200)
sns.barplot(x=x4_2, y=y4_2, color='blue')
plt.title('Perbandingan Provinsi dengan Total Rata-Rata Kesembuhan Tertinggi per hari', fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Provinsi', fontsize=12, fontweight='bold')
plt.ylabel('Jumlah Kesembuhan', fontsize=12, fontweight='bold')
plt.ylim(ymax=400000)
plt.show()
```
![image](https://user-images.githubusercontent.com/74480780/124801311-e70b0880-df80-11eb-95ea-cce6ec413e6c.png)
Visualisasi di atas menunjukkan bahwa DKI Jakarta unggul dalam angka kesembuhan per hari sebanyak 365.561, hampir dua kali lipat dari provinsi Jawa Barat yang menempati posisi kedua yaitu sebanyak 218.851.

### 3.5 Q5: Time Series Based Visualization in Big Picture
Melihat peningkatan angka kasus baru, kematian, kesembuhan, dan kasus aktif dalam rentan waktu Maret 2020 - Maret 2021
```
fg, ax = plt.subplots(2, 2, figsize=(14, 6), dpi=800, sharex=True)
fg.suptitle("Time Series based Visualization ('New Cases', 'New Deaths', 'New Recovered', 'New Active Cases')", fontsize=18, fontweight='bold')
ax[0, 0].plot(df['Date'] ,df['New Cases'], label='New Cases', color='#0061A8')
ax[0, 0].legend()
ax[1, 0].plot(df['Date'] ,df['New Deaths'], label='New Deaths', color='#F55C47')
ax[1, 0].legend()
ax[0, 1].plot(df['Date'] ,df['New Recovered'], label='New Recovered', color='#4AA96C')
ax[0, 1].legend()
ax[1, 1].plot(df['Date'] ,df['New Active Cases'], label='New Active Cases', color='#F7A440')
ax[1, 1].legend()
plt.show();
```
![q51picture](https://user-images.githubusercontent.com/74480780/127947183-4b622237-203c-4953-9662-33c877e52c6d.png)
