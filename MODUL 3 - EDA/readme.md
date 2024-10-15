# <h1 align="center">Laporan Praktikum Modul Exploratory Data Analysis</h1>
<p align="center">Aprianti Ika Larasati</p>

## Dasar Teori

Berikan penjelasan teori terkait materi modul ini dengan bahasa anda sendiri serta susunan yang terstruktur per topiknya.

## Guided 

### 1. [Nama Topik]

```python
def count_outliers_iqr(data):
  Q1 = data.quantile(0.25)
  Q3 = data.quantile(0.75)
  IQR = Q3 - Q1
  lower_bound = Q1 - 1.5 * IQR
  upper_bound = Q3 + 1.5 * IQR
  return ((data < lower_bound) | (data > upper_bound)).sum()
  #ketika data kurang dari batas bawah atau data lebih dari batas atas, maka dilakukan penambahan

# Count outliers in each numerical column
outlier_counts = {}
for col in df.select_dtypes(include=['int64', 'float64']).columns:
  outlier_counts[col] = count_outliers_iqr(df[col])

# Convert the results into a DataFrame form easier viewing
outlier_counts_df = pd.DataFrame(list(outlier_counts.items()),
                                 columns = ['Column', 'Outlier Count'])

# Display the outlier counts DataFrame
outlier_counts_df
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 2. [Nama Topik]

```python
 # melihat proporsi dari setiap label
 df['Outcome'].value_counts()
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 3. [Nama Topik]

```python
# visualisasi dengan count plot
sns.countplot(data = df, y = 'Outcome')
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 4. [Nama Topik]

```python
df.hist(bins = 20, figsize = (15,10), layout = (3, 3),
         color = 'slateblue');
plt.suptitle('Histograms of Pima Indian Diabetes Dataset Features',
             fontsize = 16) 
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 5. [Nama Topik]

```python
# Visualisasi dengan boxplot
def plot_boxplots(data):
  plt.figure(figsize=(15, 10))
  for i, column in enumerate(data.columns[:-1]):
    plt.subplot(3, 3, i+1)
    sns.boxplot(x = 'Outcome', y = column, data = data)
    plt.title(f'Box Plot of {column} by Diabetes Outcome')
  plt.tight_layout()
  plt.show()

plot_boxplots(df)
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 6. [Nama Topik]

```python
# melakukan visualisasi
text = " ".join(review for review in df_text.Text)

def plot_wordcloud(text):
  wordcloud = WordCloud(width = 800, height = 400,
                        background_color = 'white',
                        colormap = 'viridis').generate(text)

  plt.figure(figsize = (10, 5))
  plt.imshow(wordcloud, interpolation = 'bilinear')
  plt.axis('off')
  plt.title("Word Cloud of Reviews", fontsize = 16)
  plt.show()

plot_wordcloud(text)
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 7. [Nama Topik]

```python
# imputasi
imputer = KNNImputer(n_neighbors=5)
df = pd.DataFrame(imputer.fit_transform(df), columns=df.columns)
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 1. [Nama Topik]

```python
print("ini adalah file code guided praktikan")
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 1. [Nama Topik]

```python
print("ini adalah file code guided praktikan")
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 1. [Nama Topik]

```python
print("ini adalah file code guided praktikan")
```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.
## Unguided 

### 1. Imputasi missing value dengan mean, median, dan modus

```python
# cek missing value sebelum imputasi
df.isnull().sum()
```
#### Output:
![image](https://github.com/user-attachments/assets/85a0065d-a8b4-42bf-bb3d-b8f9c2b46d7d)

```python
# Imputasi missing value dengan mean
df_mean = df.fillna(df.mean())

# Imputasi missing value dengan median
df_median = df.fillna(df.median())

# Imputasi missing value dengan modus
df_modus = df.fillna(df.mode().iloc[0])
```

```python
# cek missing value setelah imputasi missing value dengan mean
df_mean.isnull().sum()
```
#### Output:
![image](https://github.com/user-attachments/assets/55781ec0-b8a2-4caf-9b86-5c193e8c1d2c)

Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 2. Cek korelasi antar variabel dengan heatmap

```python
# visualisasi heatmap utk melihat korelasi anatarvariabel
sns.heatmap(df_mean.corr(), annot = True, cmap = 'coolwarm',
            square = True, cbar_kws = {"shrink": .8})
plt.title('Heatmap Korelasi Antar Variabel', fontsize = 16)
plt.show()
```
#### Output:
![image](https://github.com/user-attachments/assets/501ecbe8-5afa-41e1-99f9-2797b26ac334)

Kode di atas digunakan untuk melakukan imputasi missing value dalam dataset 'diabetes' menggunakan mean, median, dan modus

### 3. Lakukan imbalance handling dengan undersampling

```python
# imbalance handling dengan undersampling
x = df_mean.drop('Outcome', axis = 1)
y = df_mean['Outcome']

# memisahkan data menjadi mayoritas dan minoritas
mayoritas = x[y == 0]
minoritas = x[y == 1]

# undersampling pada mayoritas
mayoritas_undersample = resample(mayoritas, replace = False, n_samples = len(minoritas))

# menggabungkan data mayoritas dan minoritas
x_undersample = pd.concat([mayoritas_undersample, minoritas])
y_undersample = np.concatenate([np.zeros(len(mayoritas_undersample)), np.ones(len(minoritas))])
```

Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

### 4. Lakukan scaling dengan robust scaler dan minmax

```python
# sebelum dilakukan scaling
df_mean.head(3)
```
#### Output:
![image](https://github.com/user-attachments/assets/ecb156d6-f5c1-4b47-becc-915bb0d0562a)

```python
# scaling dengan robust scaler
scaler_robust = RobustScaler()
x_robust = scaler_robust.fit_transform(x_undersample)

# scaling dengan minmax scaler
scaler_minmax = MinMaxScaler()
x_minmax = scaler_minmax.fit_transform(x_undersample)
```

```python
# setelah dilakukan scaling dengan robust
pd.DataFrame(x_robust).head(3)
```
#### Output:
![image](https://github.com/user-attachments/assets/1532a84d-d380-42eb-9007-466ccebb8f1b)

```python
# setelah dilakukan scaling dengan minmax
pd.DataFrame(x_minmax).head(3)
```
#### Output:
![image](https://github.com/user-attachments/assets/f9b4c7bf-6d0c-48f3-a82a-a5dfe326d8dd)

Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function print untuk mengeksekusi nya.

## Kesimpulan
Ringkasan dan interpretasi pandangan kalia dari hasil praktikum dan pembelajaran yang didapat[1].

## Referensi
[1] I. Holm, Narrator, and J. Fullerton-Smith, Producer, How to Build a Human [DVD]. London: BBC; 2002.