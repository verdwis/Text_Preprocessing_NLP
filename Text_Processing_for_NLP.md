# **Text Pre Processing dalam Teknik Pengolahan Data Teks**

Untuk mencapai tujuan penelitian serta dapat memecahkan suatu permasalahan diperlukan tahapan-tahapan salah satunya teknik pengolahan data. Tanpa adanya proses pengolahan data, data tidak berarti apa-apa bagi organisasi maupun perusahaan manapun atau bagi penelitian apapun. Untuk itu, diperlukan teknik pengolahan data untuk menemukan makna dibalik data-data tersebut. Pengolahan data dapat diterapkan untuk berbagai real case ataupun study case salah satunya yang akan kita bahas adalah untuk text mining khususnya dalam tahapan text preprocessing.

## Pengantar Singkat : Text Preprocessing

Pada natural language processing (NLP), informasi yang akan digali berisi data-data yang strukturnya “sembarang” atau tidak terstruktur. Oleh karena itu, diperlukan proses pengubahan bentuk menjadi data yang terstruktur untuk kebutuhan lebih lanjut (sentiment analysis, topic modelling, dll).


## Persiapan : Library yang dibutuhkan
Salah satu keunggulan python adalah mendukung banyak open-source library. Ada banyak library python yang dapat digunakan untuk melakukan dan mengimplementasikan masalah dalam NLP.

## Natural Language Toolkit (NLTK)
Natural Language Toolkit atau disingkat NLTK, adalah libray python untuk bekerja dengan permodelan teks. NLTK menyediakan alat yang baik mempersiapkan teks sebelum digunakan pada machine learning atau algoritma deep learning. Cara termudah untuk menginstall NLTK adalah menggunakan “pip” pada command line/terminal.

```
!pip install nltk
```

Langkah pertama yang perlu anda lakukan setelah menginstall NLTK adalah mengunduh paket NLTK.

```
import nltk
nltk.download()
```

Dokumentasi lengkap dari NLTK dapat anda baca [disini](https://www.nltk.org).

## Python Sastrawi (Stemming Bahasa Indonesia)
Python Sastrawi adalah pengembangan dari proyek PHP Sastrawi. Python Sastrawi merupakan library sederhana yang dapat mengubah kata berimbuhan bahasa Indonesia menjadi bentuk dasarnya. Sastrawi juga dapat diinstal melalui “!pip”.

```
!pip install PySastrawi
```

Penggunaan Python Sastrawi sangat sederhana seperti baris kode dibawah ini :

```
# import StemmerFactory class
from Sastrawi.Stemmer.StemmerFactory import StemmerFactory

# create stemmer
factory = StemmerFactory()
stemmer = factory.create_stemmer()

# stemming process
sentence = 'Perekonomian Indonesia sedang dalam pertumbuhan yang membanggakan'
output   = stemmer.stem(sentence)

print(output)
```
**Output:**
```
ekonomi indonesia sedang dalam tumbuh yang bangga
```

Dokumentasi lengkap dari Python Sastrawi dapat anda baca [disini](https://github.com/har07/PySastrawi).

## 1. Case folding
Case folding adalah salah satu bentuk text preprocessing yang paling sederhana dan efektif meskipun sering diabaikan. Tujuan dari case folding untuk mengubah semua huruf dalam dokumen menjadi huruf kecil.

Ada beberapa cara yang dapat digunakan dalam tahap case folding, anda dapat menggunakan beberapa atau menggunakan semuanya, tergantung pada tugas yang diberikan.

### Mengubah text menjadi lowercase
Salah satu contoh pentingnya penggunaan lower case adalah untuk mesin pencarian. Bayangkan anda sedang mencari dokumen yang mengandung “indonesia” namun tidak ada hasil yang muncul karena “indonesia” di indeks sebagai “INDONESIA”. Siapa yang harus kita salahkan? U.I. designer yang mengatur user interface atau developer yang mengatur sistem dalam indeks pencarian?

Contoh dibawah menunjukan bagaimana python mengubah teks menjadi lowercase :

```
kalimat = "Berikut ini adalah 5 negara dengan pendidikan terbaik di dunia adalah Korea Selatan, Jepang, Singapura, Hong Kong, dan Finlandia."
lower_case = kalimat.lower()
print(lower_case)
```

**Output :**

```
berikut ini adalah 5 negara dengan pendidikan terbaik di dunia adalah korea selatan, jepang, singapura, hong kong, dan finlandia.
```

### Menghapus angka
Hapuslah angka jika tidak relevan dengan apa yang akan anda analisa, contohnya seperti nomor rumah, nomor telepon, dll. Regular expression (regex) dapat digunakan untuk menghapus karakter angka. Python memiliki modulre untuk melakukan hal – hal yang berkaitan dengan regex.

Contoh dibawah menunjukan bagaimana python menghapus angka dalam sebuah kalimat :

```
import re # impor modul regular expression
kalimat = "Berikut ini adalah 5 negara dengan pendidikan terbaik di dunia adalah Korea Selatan, Jepang, Singapura, Hong Kong, dan Finlandia."
hasil = re.sub(r"\d+", "", kalimat)
print(hasil)
```

**Output :**

```
Berikut ini adalah  negara dengan pendidikan terbaik di dunia adalah Korea Selatan, Jepang, Singapura, Hong Kong, dan Finlandia.
```

### Menghapus tanda baca
Sama halnya dengan angka, tanda baca dalam kalimat tidak memiliki pengaruh pada text preprocessing. Menghapus tanda baca seperti [!”#$%&’()*+,-./:;<=>?@[\]^_`{|}~] dapat dilakukan di pyhton seperti dibawah ini :

```
import string
kalimat = "Ini &adalah [contoh] kalimat? {dengan} tanda. baca?!!"
hasil = kalimat.translate(str.maketrans("","", string.punctuation))
print(hasil)
```

**Output :**


```
Ini adalah contoh kalimat dengan tanda baca
```

## Menghapus whitepace (karakter kosong)
Untuk menghapus spasi di awal dan akhir, anda dapat menggunakan fungsi strip()pada pyhton. Perhatikan kode dibawah ini :

```
kalimat = " \t ini kalimat contoh\t "
hasil = kalimat.strip()
print(hasil)
```

**Output :**


```
ini kalimat contoh
```

## 2. Tokenizing
Tokenizing adalah proses pemisahan teks menjadi potongan-potongan yang disebut sebagai token untuk kemudian di analisa. Kata, angka, simbol, tanda baca dan entitas penting lainnya dapat dianggap sebagai token. Didalam NLP, token diartikan sebagai “kata” meskipun tokenize juga dapat dilakukan pada paragraf maupun kalimat.

Fungsi split()pada pyhton dapat digunakan untuk memisahkan teks. Perhatikan contoh dibawah ini :

```
kalimat = "rumah idaman adalah rumah yang bersih"
pisah = kalimat.split()
print(pisah)
```
**Output :**

```
['rumah', 'idaman', 'adalah', 'rumah', 'yang', 'bersih']
```

https://ksnugroho.medium.com/dasar-text-preprocessing-dengan-python-a4fa52608ffe
