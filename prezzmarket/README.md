## Tugas 2 PBP Ganjil 

Checklist untuk tugas ini adalah sebagai berikut.

    - [x] Membuat sebuah proyek django baru.
    - [x] Membuat aplikasi dengan nama main pada proyek tersebut. 
    - [x] Melakukan routing pada proyek agar dapat menjalankan aplikasi main.
    - [x] Membuat model pada aplikasi `main` dengan nama `Item` dan memiliki atribut wajib sebagai berikut.
        + `name` sebagai nama *item* dengan tipe `CharField`.
        + `amount` sebagai jumlah *item* dengan tipe `IntegerField`.
        + `description` sebagai deskripsi *item* dengan tipe `TextField`.
    - [x] Membuat sebuah fungsi pada `views.py` untuk dikembalikan ke dalam sebuah *template* HTML yang menampilkan nama aplikasi serta nama dan kelas kamu.
    - [x] Membuat sebuah *routing* pada `urls.py` aplikasi `main` untuk memetakan fungsi yang telah dibuat pada `views.py`.
    - [x] Melakukan *deployment* ke Adaptable terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.

## Jawaban Pertanyaan-Pertanyaan
**Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekedar mengikuti tutorial)**

**Membuat sebuah proyek django baru**
1. Membuat direktori lokal dan repositori ```prezzmarket```
2. Menghubungkan direkotri lokal dengan repositori
3. Membuat virtual environment (env) python bertujuan untuk mengisolasi depedensi django untuk menghindari konflik depedensi proyek django lainnya. 
   Untuk mengaktifkannya buka direktori tempat env dibuat lalu buka command prompt dan ketik ```env\Scripts\activate.bat```
4. Membuat berkas ```requirements.txt``` lalu menambahkan dependencies sebagai berikut
   ```django```
   ```gunicorn```
   ```whitenoise```
   ```psycopg2-binary```
   ```requests```
   ```urllib3```
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
1. Buat berkas baru bernama ```urls.py``` pada direktori main dengan menambahkan 
   ```from django.urls import path 
   from main.views import show_main

   app_name = 'main'

   urlpatterns = [path('', show_main, name='show_main'),]```
2. Buka ```urls.py``` dalam direktori prezzmarket lalu tambahkan 
   import ```include``` dari ```django urls```:
   ```from django.urls import path, include```
   pada urlpatterns juga tambahkan: 
   ```path('main/', include('main.urls')),```

**Membuat model pada aplikasi `main` dengan nama `Item` dan memiliki atribut wajib yang sudah ditentukan**
1. Buka ```models.py``` pada direktori aplikasi ```main```
2. Isi dengan kode sebagai berikut 
   ```from django.db import models

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
   ```def show_main(request):
    context = {
        'name': 'Prasetyo Adi Wijonarko',
        'class': 'PBP E'
    }

    return render(request, "main.html", context)```

**Membuat sebuah *routing* pada `urls.py` aplikasi `main` untuk memetakan fungsi yang telah dibuat pada `views.py`.**
1. Buka ```urls.py``` pada direktori ```prezzmarket```
2. Tambahkan include :
   ```from django.urls import path, include```
3. Tambahkan ```path('main/',include('main.urls')),``` pada ```urlspatterns```
