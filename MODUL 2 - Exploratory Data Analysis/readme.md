# <h1 align="center">Laporan Praktikum Modul Exploratory Data Analysis</h1>
<p align="center">Aprianti Ika Larasati</p>

## Dasar Teori
Exploratory Data Analysis (EDA) memainkan peran penting dalam ilmu data, memberikan wawasan yang berharga untuk mengidentifikasi dan meningkatkan wawasan bisnis yang penting di seluruh organisasi [1]. 
EDA juga dapat secara efektif menunjukkan nilai yang diharapkan dari eksperimen untuk hipotesis tertentu jika dilakukan dengan baik [2].
Tujuan EDA: 
- EDA sangat penting untuk mengungkap wawasan dan pola tersembunyi dalam data, yang sangat penting untuk membuat keputusan bisnis yang tepat dan meningkatkan hasil organisasi [1]
- Ini adalah langkah penting untuk memahami data sebelum menerapkan model statistik atau algoritme pembelajaran mesin, memastikan bahwa data tersebut bersih dan dipahami dengan baik [1]
- EDA membantu dalam mengidentifikasi wawasan bisnis yang penting dan meningkatkan proses pengambilan keputusan di berbagai sektor dengan memberikan pemahaman yang lebih mendalam tentang data [1]
- Hal ini memungkinkan identifikasi pola dan masalah dalam data, yang dapat mengarah pada perumusan hipotesis dan analisis lebih lanjut
- EDA adalah tugas yang menuntut dan memakan waktu yang membutuhkan keterampilan analitis dan pengetahuan domain yang signifikan [3]
- Kemajuan terbaru dalam pembelajaran mesin telah mengarah pada pengembangan sistem yang dapat mengotomatiskan bagian-bagian dari proses EDA, membuatnya lebih efisien dan tidak terlalu banyak membutuhkan tenaga kerja.
- Berbagai alat dan bahasa pemrograman, seperti Python dan R, menyediakan metode untuk melakukan EDA, masing-masing dengan kelebihan dan kekurangannya sendiri
- Sistem dan pustaka baru, seperti DataPrep.EDA, sedang dikembangkan untuk meningkatkan skalabilitas, kegunaan, dan penyesuaian tugas-tugas EDA, sehingga prosesnya lebih mudah diakses oleh para ilmuwan data
- EDA sering kali merupakan proses kolaboratif, dengan para ilmuwan data berbagi temuan mereka melalui buku catatan dan dokumentasi lainnya. Namun, membuat buku catatan EDA yang terdokumentasi dengan baik dapat menjadi rumit [3][5]
- Alat-alat seperti ExplainED dan Diff in the Loop (DITL) membantu dalam memahami dan memvisualisasikan perubahan berulang pada data, meningkatkan aspek kolaboratif dari EDA[3]

## Guided 

### 1. [Nama Topik]

```python
print("ini adalah file code guided praktikan")
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

## Unguided 

### 1. Load data (movie classification)

```python
import pandas as pd
import numpy as np

bf = pd.read_csv('/content/Movie_classification.csv')
bf
```
#### Output:
![image](https://github.com/user-attachments/assets/96a3588f-7c13-46bc-8359-7ca7cdcb4791)

Kode di atas digunakan untuk membaca file csv `Movie_classification.csv` dan menampilkan isi dataset dengan menggunakan library `pandas`. Library `pandas` adalah salah satu library Python yang sangat populer untuk mengolah dan menganalisis data. Sedangkan library `numpy` digunakan untuk mengolah data numerik. Function `read_csv` dari `pandas` digunakan untuk membaca file csv `Movie_classification.csv` lalu disimpan dalam variabel `bf`.

### 2. Cek nilai duplikat

```python
duplicate = bf[bf.duplicated()]
print("Jumlah data duplikat: ", len(duplicate))
```
#### Output:
![image](https://github.com/user-attachments/assets/a7896540-0c0e-4ec6-bea1-d2fe0c942b6a)


Kode di atas digunakan untuk menemukan dan menghitung jumlah data duplikat dalam dataframe `bf`. Pada kode `bf[bf.duplicated()]`, program menggunakan hasil dari function `duplicated()` sebagai mask untuk memilih baris yang duplikat dari dataframe `bf`. Sehingga outputnya hanya baris yang duplikat. Untuk menghitung panjang dari variabel `duplicate`, program menggunakan function `len()`.

### 3. Menemukan null values buat presentase

```python
bf.isna().sum()/len(bf)*100
# jumlah data kosong dibagi panjang datanya dikali 100
```
#### Output:
![image](https://github.com/user-attachments/assets/0ca8e5c8-6bd2-4267-bf3d-fc04f8f70040)


Kode di atas digunakan untuk menghitung presentase missing values atau null values dalam dataframe `bf`. Presentase dihitung dengan jumlah nilai kosong dibagi dengan panjang dataframe, lalu dikali dengan 100. Untuk menghitung jumlah nilai kosong atau missing values, program menggunakan function `bf.isna().sum()`. Sedangkan untuk menghitung panjang dari dataframe `bf` adalah dengan function `len(bf)`.

### 4. Drop missing value berdasarkan baris, kolom, imputasi dengan mean, modus, median

```python
# Drop missing value berdasarkan baris
# Tidak terhapus permanen
bf_dropped_rows = bf.dropna()

# Drop missing value berdasarkan kolom
# Tidak terhapus permanen
bf_dropped_columns = bf.dropna(axis = 1)

# Data yang bertipe float tidak dapat dicari mean, modus, dan mediannya
# Maka perlu dicari tahu apa tipe data dari setiap kolom
print(bf.dtypes)

# Kolom yang memiliki missing value adalah kolom 'Time_taken', maka tipe datanya diganti menjadi numeric
# Kolom 'Time_taken' bersifat float karena terdapat titik.
# Titik diganti dengan kosong dan kolom dikonversi ke tipe numerik
bf['Time_taken'] = pd.to_numeric(bf['Time_taken'].astype(str).str.replace('.', ''), errors='coerce')

# Imputasi dengan mean
bf_imputed_mean = bf.fillna(bf.mean(numeric_only=True))

# Imputasi dengan median
bf_imputed_median = bf.fillna(bf.median(numeric_only=True))

# Imputasi dengan modus
bf_imputed_mode = bf.fillna(bf.mode().iloc[0])

# Memeriksa nilai null setelah imputasi
# Di sini menggunakan data imputasi dengan mean
print(bf_imputed_mean.isnull().sum())
```
#### Output:
![image](https://github.com/user-attachments/assets/4b91e30a-2de7-4fd8-b687-84dca0429b79)
![image](https://github.com/user-attachments/assets/dcf3df37-0911-49d3-8347-e1743143f7cd)


Kode dari program di atas digunakan adalah sebagai berikut:
- Drop missing valu berdasarkan baris menggunakan `bf_dropped_rows = bf.dropna()`.
- Drop missing value berdasarkan kolom dengan menggunakan  `bf_dropped_columns = bf.dropna(axis = 1)`.
- Mengidentifikasi tipe data dengan menggunakan function `dtypes` untuk mengetahui mana data yang numeric, mana data string.
- Mengubah tipe data kolom `Time_taken ` menjadi numerik dengan menghilangkan titik dan mengonversi ke tipe numerik.
- Imputasi dengan mean, median, dan modus. Yaitu mengisi nilai kosong dengan mean, median, atau modus dari setiap kolom.
- Memeriksa null values setelah imputasi untuk memeriksa jumlah nilai kosong setelah imputasi dengan mean, apakah sudha 0 atau tidak?

### 5. Export data ke csv dan excel

```python
bf_imputed_mean.to_csv('Movie_classification_cleaned_mean.csv', index=False)
bf_imputed_mean.to_excel('Movie_classification_cleaned_mean.xlsx', index=False)
```
#### Output:
![image](https://github.com/user-attachments/assets/3cbe9bac-73c8-4c5f-b3a2-4d62e0d990fb)


Kode di atas digunakan untuk menyimpan dataframe `bf_imputed_mean` ke dalam file csv dan excel. Parameter `index=False` digunakan untuk tidak menyertakan indeks dataframe dalam file csv.

## Kesimpulan
Exploratory Data Analysis merupakan bagian tak terpisahkan dari proses sains data, yang memberikan wawasan dan pemahaman penting tentang data. 
Analisis ini memainkan peran penting dalam memfasilitasi pengambilan keputusan yang lebih baik dan memastikan keberhasilan upaya pemodelan selanjutnya. 
Terlepas dari tantangannya, kemajuan dalam otomatisasi dan pengembangan alat membuat EDA menjadi lebih efisien dan mudah diakses, menggarisbawahi pentingnya EDA dalam alur kerja sains data.

## Referensi
[1] A. S. Rao, B. V. Vardhan and H. Shaik, "Role of Exploratory Data Analysis in Data Science," 2021 6th International Conference on Communication and Electronics Systems (ICCES), Coimbatre, India, 2021, pp. 1457-1461, doi: 10.1109/ICCES51350.2021.9488986.

[2] C. Klein, “Exploratory Analysis and the Expected Value of Experimentation,” Philosophy of Science, pp. 1–9, 2023. doi:10.1017/psa.2023.116

[3] Daniel Deutch, Amir Gilad, Tova Milo, and Amit Somech, "ExplainED: explanations for EDA notebooks", Proc. VLDB Endow. 13, 12, 2020, 2917–2920. https://doi.org/10.14778/3415478.3415508

[4] M. - Mambang, “Exploratory Data Analysis of Exact Science and Social Science Learning Content on Digital Platform,” Walisongo Journal of Information Technology, vol. 4, no. 2, pp. 87–94, Nov. 2022, doi: https://doi.org/10.21580/wjit.2022.4.2.12676.

[5] Wang, A., Epperson, W., Deline, R., & Drucker, S. "Diff in the Loop: Supporting Data Comparison in Exploratory Data Analysis," Proceedings of the 2022 CHI Conference on Human Factors in Computing Systems, 2022 https://doi.org/10.1145/3491102.3502123.