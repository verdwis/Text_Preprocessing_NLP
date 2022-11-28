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
nltk.download('punkt')
nltk.download('stopwords')
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

Sayangnya, tahap tokenizing tidak sesederhana itu. Dari output kode diatas kita akan mengolah kata “rumah” dan “rumah” sebagai 2 entitas yang berbeda. Permasalahan ini tentunya akan mempengaruhi hasil dari analisa teks itu sendiri. Untuk mengatasi masalah ini kita dapat menggunakan modul dari NLTK yang sudah diinstal sebelumnya.

## Tokenizing kata
Sebuah kalimat atau data dapat dipisah menjadi kata-kata dengan kelas word_tokenize() pada modul NLTK.

```
# impor word_tokenize dari modul nltk
from nltk.tokenize import word_tokenize 
 
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online."
 
tokens = nltk.tokenize.word_tokenize(kalimat.translate(str.maketrans('','',string.punctuation)).lower())
print(tokens)
```

**Output :**

```
['andi', 'kerap', 'melakukan', 'transaksi', 'rutin', 'secara', 'daring', 'atau', 'online']
```


Kita juga bisa mendapatkan informasi frekuensi kemunculan setiap token dengan kelas FreqDist() yang sudah tersedia pada modul NLTK.

```
from nltk.tokenize import word_tokenize
from nltk.probability import FreqDist
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online. Menurut Andi belanja online lebih praktis & murah."
kalimat = kalimat.translate(str.maketrans('','',string.punctuation)).lower()
 
tokens = nltk.tokenize.word_tokenize(kalimat)
kemunculan = nltk.FreqDist(tokens)
print(kemunculan.most_common())
```

**Output :**

```
[('andi', 2), ('online', 2), ('kerap', 1), ('melakukan', 1), ('transaksi', 1), ('rutin', 1), ('secara', 1), ('daring', 1), ('atau', 1), ('menurut', 1), ('belanja', 1), ('lebih', 1), ('praktis', 1), ('murah', 1)]
```

Untuk menggambarkan ke dalam bentuk grafik, kita perlu menginstall library Matplotlib.

```
import matplotlib.pyplot as plt
kemunculan.plot(30,cumulative=False)
plt.show()
```

**Output :**

<img width="384" alt="image" src="https://user-images.githubusercontent.com/101826376/204218882-fc64c6ab-9086-4b6d-9ff2-4d05458300e8.png">


## Tokenizing kalimat
Prinsip yang sama dapat diterapkan untuk memisahkan kalimat pada paragraf. Anda dapat menggunkan kelas sent_tokenize() pada modul NLTK. Saya telah menambahkan kalimat pada contoh seperti dibawah ini :

```
# impor sent_tokenize dari modul nltk
from nltk.tokenize import sent_tokenize
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online. Menurut Andi belanja online lebih praktis & murah."
 
tokens = nltk.tokenize.sent_tokenize(kalimat)
print(tokens)
```

**Output :**

```
['Andi kerap melakukan transaksi rutin secara daring atau online.', 'Menurut Andi belanja online lebih praktis & murah.']
```

# 3. Filtering (Stopword Removal)

Filtering adalah tahap mengambil kata-kata penting dari hasil token dengan menggunakan algoritma stoplist (membuang kata kurang penting) atau wordlist (menyimpan kata penting).

## Filtering dengan NLTK

```
from nltk.tokenize import sent_tokenize, word_tokenize
from nltk.corpus import stopwords
 
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online. Menurut Andi belanja online lebih praktis & murah."
kalimat = kalimat.translate(str.maketrans('','',string.punctuation)).lower()
 
tokens = word_tokenize(kalimat)
listStopword =  set(stopwords.words('indonesian'))
 
removed = []
for t in tokens:
    if t not in listStopword:
        removed.append(t)
 
print(removed)
```

**Output :**

```
['andi', 'kerap', 'transaksi', 'rutin', 'daring', 'online', 'andi', 'belanja', 'online', 'praktis', 'murah']
```

## Filtering dengan sastrawi
Selain untuk stemming, library Sastrawi juga mendukung proses filtering. Kita dapat menggunakan stopWordRemoverFactory dari modul sastrawi.

Untuk melihat daftar stopword yang telah didefinisikan dalam library Sastrawi dapat menggunakan kode berikut :

```
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory
factory = StopWordRemoverFactory()
stopwords = factory.get_stop_words()
print(stopwords)
```

Kode diatas akan menampikan stopword yang tersedia di library Sastrawi. Prosos filtering pada Sastrawi dapat dilihat pada baris kode dibawah :

```
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory
from nltk.tokenize import word_tokenize
factory = StopWordRemoverFactory()
stopword = factory.create_stop_word_remover()
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online. Menurut Andi belanja online lebih praktis & murah."
kalimat = kalimat.translate(str.maketrans('','',string.punctuation)).lower()
stop = stopword.remove(kalimat)
tokens = nltk.tokenize.word_tokenize(stop)
print(tokens)
```

**Output :**

```
['andi', 'kerap', 'transaksi', 'rutin', 'daring', 'online', 'andi', 'belanja', 'online', 'praktis', 'murah']
```

Kita dapat menambah atau mengurangi kata pada daftar stopword sesuai dengan kebutuhan analisa. Pada dasarnya daftar stopword pada library Sastrawi tersimpan di dalam list yang anda lihat disini. Jadi sebenarnya kita tinggal mengubah daftar pada list tersebut. Tetapi hal tersebut bisa menjadi permasalahan apabila pada suatu kasus kita diharuskan menambahkan stopword secara dinamis.


Library Sastrawi dapat mengatasi permasalahan tersebut, perhatikan kode dibawah ini:

```
from Sastrawi.StopWordRemover.StopWordRemoverFactory import StopWordRemoverFactory, StopWordRemover, ArrayDictionary
from nltk.tokenize import word_tokenize 
 

stop_factory = StopWordRemoverFactory().get_stop_words() #load defaul stopword
more_stopword = ['daring', 'online'] #menambahkan stopword
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online. Menurut Andi belanja online lebih praktis & murah."
kalimat = kalimat.translate(str.maketrans('','',string.punctuation)).lower()
data = stop_factory + more_stopword #menggabungkan stopword
 
dictionary = ArrayDictionary(data)
str = StopWordRemover(dictionary)
tokens = nltk.tokenize.word_tokenize(str.remove(kalimat))
 
print(tokens)
```

**Output :**

```
['andi', 'kerap', 'transaksi', 'rutin', 'andi', 'belanja', 'praktis', 'murah']
```

# 4. Stemming
Stemming adalah proses menghilangkan infleksi kata ke bentuk dasarnya, namun bentuk dasar tersebut tidak berarti sama dengan akar kata (root word). Misalnya kata “mendengarkan”, “dengarkan”, “didengarkan” akan ditransformasi menjadi kata “dengar”.

## Stemming dengan NLTK (bahasa inggris)
Ada banyak algoritma yang digunakan untuk stemming. Salah satu algoritma yang tertua dan paling populer adalah algoritma [Porter](https://tartarus.org/martin/PorterStemmer/). Algoritma ini tersedia dalam modul NLTK melalui ```kelasPorterStemmer()```.

```
from nltk.stem import PorterStemmer 
   
ps = PorterStemmer() 
  
kata = ["program", "programs", "programer", "programing", "programers"] 
  
for k in kata: 
    print(k, " : ", ps.stem(k))
```

**Output :**

```
program  :  program
programs  :  program
programer  :  program
programing  :  program
programers  :  program
```

Selain Porter, NLTK juga mendukung algoritma Lancester, WordNet Lemmatizer, dan SnowBall. Sayangnya proses stemming Bahasa Indonesia pada modul NLTK belum didukung.

## Stemming bahasa indonesia menggunakan Python Sastrawi
Proses stemming antara satu bahasa dengan bahasa yang lain tentu berbeda. Contohnya pada teks berbahasa inggris, proses yang diperlukan hanya proses menghilangkan sufiks. Sedangkan pada teks berbahasa Indonesia semua kata imbuhan baik itu sufiks dan prefiks juga dihilangkan.

```
from Sastrawi.Stemmer.StemmerFactory import StemmerFactory
factory = StemmerFactory()
stemmer = factory.create_stemmer()
 
kalimat = "Andi kerap melakukan transaksi rutin secara daring atau online. Menurut Andi belanja online lebih praktis & murah."
hasil = stemmer.stem(kalimat)
print(hasil)
```

**Output :**

```
andi kerap laku transaksi rutin cara daring atau online turut andi belanja online lebih praktis murah
```

# Apakah kita memerlukan semua tahapan pada text preprocessing?
Tidak ada aturan pasti yang membahas setiap tahapan pada text preprocessing. Tentu saja untuk memastikan hasil yang lebih baik dan konsisten semua tahapan harus dilakukan. Untuk memberi gambaran tentang apa yang minimal seharusnya dilakukan, saya telah menguraikan tahapan menjadi harus dilakukan, sebaiknya dilakukan, dan tergantung tugas. Perlu diingat, less is more, anda ingin menjaga pendekatan dengan seindah mungkin. Semakin banyak fitur atau tahapan yang anda tambahkan, semakin banyak pula lapisan yang anda harus kupas.

* **Harus dilakukan** meliputi case folding (dapat tergantung tugas dalam beberapa kasus)

* **Sebaiknya dilakukan** meliputi normalisasi sederhana — misalnya menstandarkan kata yang hampir sama

* **Tergantung tugas** meliputi normalisasi tingkat lanjut — misalnya mengatasi kata yang tidak biasa, stopword removal dan stemming.


# Punutup

Dalam tulisan ini kita telah mengetahui langkah dasar dan praktis pada text preprocessing beserta library yang digunakan dalam python. Selanjutnya hasil dari text preprocessing dapat digunakan untuk analisa NLP yang lebih rumit, contohnya machine translation. Tidak semua kasus membutuhkan level preprocessing yang sama. Dalam beberapa kasus anda bisa menggunakan salah satu tahap dari preprocessing paling sederhana yaitu case folding. Namun semua tahap akan dibutuhkan apabila anda mempunyai dataset dengan level noise sangat tinggi.

Masih ada teknik yang bisa dilakukan pada text preprocessing, tetapi sesuai kata pengantar diatas, tulisan ini hanya mengulas langkah dasar dan praktis dalam text preprocessing.

Selamat mencoba dan bersenang-senang dengan NLP :)

> Baris kode diatas dapat anda temukan di github saya. https://github.com/verydwisetiawa03/Text_Preprocessing_NLP/blob/main/text_Processing_In_NLP.ipynb


# Referensi

1. Python Sastrawi (https://github.com/har07/PySastrawi).
2. Natural Language Toolkit -NLTK (https://www.nltk.org).
3. Matplotlib (https://matplotlib.org).

