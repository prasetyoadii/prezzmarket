## Tugas 2 PBP Ganjil 
# Prasetyo Adi Wijonarko, PBP E

Checklist untuk tugas ini adalah sebagai berikut.
- [X] Membuat sebuah proyek django baru.
- [x] Membuat aplikasi dengan nama main pada proyek tersebut. 
- [x] Melakukan routing pada proyek agar dapat menjalankan aplikasi main.
- [x] Membuat model pada aplikasi `main` dengan nama `Item` dan memiliki atribut wajib sebagai berikut.
    + `name` sebagai nama *item* dengan tipe `CharField`.
    + `amount` sebagai jumlah *item* dengan tipe `IntegerField`.
    + `description` sebagai deskripsi *item* dengan tipe `TextField`.
- [x] Membuat sebuah fungsi pada `views.py` untuk dikembalikan ke dalam sebuah *template* HTML yang menampilkan nama aplikasi serta nama dan kelas kamu.
- [x] Membuat sebuah *routing* pada `urls.py` aplikasi `main` untuk memetakan fungsi yang telah dibuat pada `views.py`.
- [x] Melakukan *deployment* ke Adaptable terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.
- [x] Membuat sebuah README.md yang berisi tautan menuju aplikasi Adaptable yang sudah di-deploy, serta jawaban dari beberapa pertanyaan berikut.
 
## Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekedar mengikuti tutorial)

**Membuat sebuah proyek django baru**
1. Membuat direktori lokal dan repositori ```prezzmarket``
2. Menghubungkan direkotri lokal dengan repositori
3. Membuat virtual environment (env) python bertujuan untuk mengisolasi depedensi django untuk menghindari konflik depedensi proyek django lainnya. 
   Untuk mengaktifkannya buka direktori tempat env dibuat lalu buka command prompt dan ketik ```env\Scripts\activate.bat```
4. Membuat berkas ```requirements.txt``` lalu menambahkan dependencies sebagai berikut
   ```
   django
   gunicorn
   whitenoise
   psycopg2-binary
   requests
   urllib3
5. Pasang dependencies dengan perintah ```pip install -r requirements.txt``` dan membuat proyek django bernama ```prezzmarket``` 
   dengan menjalankan perintah ```django-admin startproject prezzmarket .``` (nyalakan terlebih dahulu environtmennya)
6. Ubah ```ALLOWED-HOSTS``` di ```settings.py``` menjadi ```[ * ]```. Step ini bertujuan agar aplikasi dapat diakses secara luas
7. Jalankan server django dengan perintah ```python manage.py runserver```, cek http://localhost:8000 
   jika tidak memunculkan error maka apalikasi berhasil dibuat
8. Tekan ```CTRL + C``` untuk menghentikan server dan jalankan perintah ```deactivate``` untuk menonaktifkan virtual environtment

**Mmebuat aplikasi main pada proyek tersebut**
1. Buka direktori prezzmarket, nyalakan virtual environtment dengan perintah ```env\Scripts\activate.bat```
2. Jalankan perintah ```python manage.py startapp main```
3. Buka ```settings.py``` dalam direktori proyek prezzmarket, tambahkan ```'main'``` pada variabel ```INSTALLED APPS```

**Melakukan routing pada proyek agar dapat menjalankan aplikasi main**
1. Buat berkas baru bernama ```urls.py``` pada direktori ```main``` dan menambahkan 
   ```
   from django.urls import path
   
   from main.views import show_main
   app_name = 'main'
   urlpatterns = [path('', show_main, name='show_main'),]

**Membuat model pada aplikasi `main` dengan nama `Item` dan memiliki atribut wajib yang sudah ditentukan**
1. Buka ```models.py``` pada direktori aplikasi ```main```
2. Isi dengan kode sebagai berikut 
   ```
   from django.db import models
   
   class Product(models.Model):
   name = models.CharField(max_length=255)
   amount = models.IntegerField()
   description = models.TextField()
3. lakukan migrasi model dengan menjalankan perintah ```python manage.py makemigrations``` untuk mencatat perubahan model, 
   lalu terapkan perubahan tersebut ke basis data lokal Anda dengan perintah python manage.py migrate.

**Membuat sebuah fungsi pada `views.py` untuk dikembalikan ke dalam sebuah *template* HTML yang menampilkan nama aplikasi serta nama dan kelas**
1. Buka ```views.py``` dalam direktori aplikasi ```main```
2. Lakukan import ```from django.shortcuts import render```
3. Tambahkan fungsi show_main untuk menampilkan halaman web sesuai permintaan yang diterima pryoek django
   ```
   def show_main(request):
   context = {
        'name': 'Prasetyo Adi Wijonarko',
        'class': 'PBP E'
    }
   return render(request, "main.html", context)
   ```


**Membuat sebuah *routing* pada `urls.py` aplikasi `main` untuk memetakan fungsi yang telah dibuat pada `views.py`.**
1. Buka ```urls.py``` pada direktori ```prezzmarket```
2. Tambahkan include :
   ```from django.urls import path, include```
3. Tambahkan ```path('main/',include('main.urls')),``` pada ```urlspatterns```

**Melakukan *deployment* ke Adaptable terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.**
1. Login Adaptable.io menggunakan akun github, tekan ```New App``` lalu 
   pilih ```Connect an Existing Repository``` lalu pilih ```All Repositories```
2. Pilih ```prezzmarket``` sebagai aplikasi yang ingin di deploy, pilih ```main``` sebagai deployment branch
3. Pilih ```Python App Template``` sebagai template deployment dan ```PostgreSQL``` sebagai tipe basis data
4. Masukkan versi python yang sudah terinstall di device
5. Pada kolom ```Start Command```, masukkan perintah ```python manage.py migrate && gunicorn prezzmarket.wsgi```
6. Masukkan nama App yaitu prezzmarket
7. Centang ```HTTP Listener on PORT``` dan tekan ```Deploy App``` untuk memulai proses deployment aplikasi

## Buatlah bagan yang berisi request client ke web aplikasi berbasis Django beserta responnya dan jelaskan pada bagan tersebut kaitan antara ```urls.py```, ```views.py```, ```models.py```, dan berkas ```html```.
![bagan](https://github.com/prasetyoadii/prezzmarket/assets/125488022/a9d1fc82-8481-4d9e-b747-d766722a3a59)
1. `urls.py` digunakan untuk mengelola routing yang dikirim oleh klien. Django akan mencocokkan URL yang diterima dengan pola URL yang telah didefinisikan dalam `urls.py`, jika cocok akan disematkan pada *template* `HTML`
2. Setelah didefinisikan, `views.py` akan menentukan bagaimana aplikasi akan berlaku. `views.py` mengelola permintaan, mengambil data dari model,melakukan pemrosesan data, kemudian menyiapkan data untuk nantinya ditampilkan ke klien
3. `models.py` berisi definisi model yang merepresentasikan struktur dan hubungan data dalam database. Digunakan untuk berinteraksi dengan database.
4. `template` berkas HTML yang mengatur tampilan antarmuka pengguna


## Jelaskan mengapa kita menggunakan *virtual environment*? Apakah kita tetap dapat membuat aplikasi web berbasis Django tanpa menggunakan *virtual environment*
Virtual environment merupakan sebuah alat yang digunakan untuk menjaga dependensi yang dibutuhkan oleh berbagai proyek Python tetap terisolasi dan terpisah. Dengan menggunakan virtual environment, dapat menjaga dependensi dari berbagi proyek python yang berbeda agar tetap terisolasi dan terpisah.Kita dapat menciptakan lingkungan yang independen, masing-masing sesuai dengan ebutuhan dan depedensi yang kita butuhkan untuk proyek sehingga proyek dapat berjalan baik tanpa konflik depedensi. 

Bisa saja kita membuat proyek Python tanpa menggunakan virtual environment, namun perlu diperhatikan kita harus berhati-hati dalam mengelola dependensi proyek kita untuk menghindari konflik. Misalnya kita membuat proyek A yang membutuhkan versi 1.0 dari pustaka C sedangkan proyek B memerlukan versi 2.0. Tanpa virtual environment, kedua proyek ini akan berbagi instalasi global pustaka X, yang dapat menyebabkan konflik dan masalah dalam menjalankan proyek-proyek tersebut.


## Jelaskan apakah itu MVC, MVT, MVVM dan perbedaan dari ketiganya

**MVC**
MVC atau Model-View-Controller, merupakan desain arsitektur website yang terdiri dari tiga komponen utama yaitu: 
- Model:
  - Bertanggung jawab atas logika bisnis dan data aplikasi.
  - Mengambil, manipulasi, dan berinteraksi dengan data.
  - Mmperbarui tampilan aplikasi.
- View:
  - Mengurus antarmuka pengguna (UI) seperti halaman web atau antarmuka aplikasi.
  - Berkomunikasi dengan pengontrol dan model
  - Mengelola interaksi dengan pengguna.
  - Menyajikan data yang sesuai untuk pengguna
- Controller:
  - Menerima input dari pengguna melalui view/REST
  - Menghubungkan view dengan model.
  - Memproses data dari model dan mengirimkannya ke view untuk ditampilkan.
- **Perbedaan dari MVT (Model-View-Template):** Dalam MVT, peran yang biasanya dimiliki oleh *controller* digantikan oleh *template*. *Template* merupakan file HTML yang digunakan bersama dengan Django Template Language (DTL).
- **Perbedaan dari MVVM (Model-View-ViewModel):** Dalam MVVM, peran *controller* digantikan oleh *ViewModel* yang bertindak sebagai perantara antara *model* dan *view*.

**MVT**
MVT atau Model-View-Template, merupakan pola arsitektur website yang digunakan pada django. Berikut adalah komponennya:
- Model:
  - Bertindak sebagai antarmuka untuk data dalam aplikasi.
  - Menjaga dan mengelola data.
  - Merupakan struktur data logis yang mendasari seluruh aplikasi.
  - Biasanya terhubung dengan database, khususnya database relasional seperti MySql atau Postgres.
- View:
  - Merupakan antarmuka pengguna yang dilihat dalam browser ketika sebuah website dirender.
  - Direpresentasikan oleh HTML, CSS, JavaScript, dan file-file Jinja.
  - Bertanggung jawab atas tampilan visual dari aplikasi.
- Template:
  - Terdiri dari bagian-bagian statis dari output HTML yang diinginkan.
  - Mengandung sintaks khusus yang menggambarkan bagaimana konten dinamis akan dimasukkan.
  - Digunakan untuk menghasilkan tampilan yang akhirnya dilihat oleh pengguna melalui View.
- **Perbedaan dari MVC (Model-View-Controller):** Dalam MVC, peran yang biasanya dimiliki oleh *template* digantikan oleh *controller*. *Controller* bertindak sebagai penghubung antara *view* dan *model*.
- **Perbedaan dari MVVM (Model-View-ViewModel):** Dalam MVVM, peran *template* digantikan oleh *ViewModel* yang berperan sebagai perantara antara *model* dan *view*.

**MVVM**
MVVM atau Model-View-ViewModel, adalah pola arsitektur yang umumnya digunakan dalam pengembangan aplikasi berbasis antarmuka pengguna (UI), termasuk aplikasi mobile dan desktop.  Berikut adalah komponennya:
- Model:
  - Berisi data dasar yang digunakan dalam aplikasi. 
  - Model mengelola data dan aturan bisnis aplikasi, dan seringkali berinteraksi dengan sumber data seperti database atau layanan web.
- View:
  - View dalam MVVM adalah antarmuka grafis yang digunakan oleh pengguna untuk berinteraksi dengan aplikasi. Ini bertanggung jawab untuk menampilkan output dari data yang telah diproses.
  - View dalam MVVM mirip dengan komponen view dalam pola arsitektur MVC
- ViewModel:
  - Memaparkan aliran data yang relevan dengan tampilan (View).
  - Berfungsi sebagai penghubung antara Model dan View.
  - Terdiri dari Model yang diubah menjadi View, dan berisi perintah yang dapat digunakan oleh View untuk mempengaruhi Model.
- **Perbedaan dari MVC (Model-View-Controller):** Dalam MVC, peran *ViewModel* digantikan oleh *controller* yang bertindak sebagai penghubung antara *view* dan *model*.
- **Perbedaan dari MVT (Model-View-Template):** Dalam MVT, peran yang biasanya dimiliki oleh *ViewModel* digantikan oleh *template*. *Template* berperan dalam menyusun tampilan antarmuka pengguna


