# Prasetyo Adi Wijonarko, PBP E

<details>
<summary>Tugas 3</summary>
# Tugas 3 Pemrograman Berbasis Platform
<br>
<hr>

Checklist untuk tugas ini adalah sebagai berikut.
- [X] Membuat input `form` untuk menambahkan objek model pada app sebelumnya.
- [x] Tambahkan 5 fungsi `views` untuk melihat objek yang sudah ditambahkan dalam format HTML, XML, JSON, XML by ID, dan JSON by ID.
- [x] Membuat routing URL untuk masing-masing `views` yang telah ditambahkan pada poin 2.
- [x] Menjawab beberapa pertanyaan berikut pada README.md pada root folder.
	- [x] Apa perbedaan antara form POST dan form GET dalam Django?
	- [x] Apa perbedaan utama antara XML, JSON, dan HTML dalam konteks pengiriman data?
	- [x] Mengapa JSON sering digunakan dalam pertukaran data antara aplikasi web modern?
	- [x] Jelaskan bagaimana cara kamu mengimplementasikan checklist di	atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
- [X] Mengakses kelima URL di poin 2 menggunakan Postman, membuat screenshot dari hasil akses URL pada Postman, dan menambahkannya ke dalam `README.md.`
- [X] Melakukan add-commit-push ke GitHub.

### Membuat input `form` untuk menambahkan objek model pada app sebelumnya.
1. sebelum membuat form, kita perlu membuat kerangka views dari situs web kita. berikut ini adalah caranya 
 * membuat folder `templates` pada root folder, buat berkas `base.html` dan isi dengan kode berikut
   ```
{% load static %}
   <!DOCTYPE html>
   <html lang="en">
      <head>
         <meta charset="UTF-8" />
         <meta
               name="viewport"
               content="width=device-width, initial-scale=1.0"
         />
         {% block meta %}
         {% endblock meta %}
      </head>

      <body>
         {% block content %}
         {% endblock content %}
      </body>
   </html>

* pada variabel `TEMPLATES` pada `settings.py` dalam direktori `prezzmarket` tambahkan kode berikut 
   ```...
   TEMPLATES = [
      {
         'BACKEND': 'django.template.backends.django.DjangoTemplates',
         'DIRS': [BASE_DIR / 'templates'], # Tambahkan kode ini
         'APP_DIRS': True,
         ...
      }
   ]
   ...

   kode tersebut berguna untuk mendeteksi `base.html` sebagai berkas template
 * buka berkas `main.html` yang ada pada `templates` direktori `main`, ubah kodenya menjadi seperti berikut 
   ```
{% extends 'base.html' %}

{% block content %}
    <html>
    <head>
    </head>
    <body>
    <h1>Selamat datang di Prezzmarket</h1>

    <p><strong>Nama:</strong> {{ name }}</p>
    <p><strong>Kelas:</strong> {{ class }}
{% endblock content %}
kode tersebut menggunakan `base.html` sebagai template utama

2. Setelah membaut kerangka, kita membuat form input data  
* buat berkas `forms.py` pada direktori main. tambahkan kode berikut
   ```
from django.forms import ModelForm
from main.models import Item

class ItemForm(ModelForm):
    class Meta:
        model = Item
        fields = ["name", "amount", "description"]

kode ini digunakan untuk membuat struktur form yang menerima data produk baru
 * buka berkas `views.py` yang ada pada foler `main` tambahkan import sebagai berikut
   ```
from django.http import HttpResponseRedirect
from main.forms import ItemForm
from django.urls import reverse

 * dalam berkas yang sama, buat fungsi `create_item` yang menerima parameter `request` untuk menghasilkan form yang dapat menambahkan data secara otomatis.  berikut kodenya
   ```
def create_item(request):
    form = ItemForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        form.save()
        return HttpResponseRedirect(reverse('main:show_main'))

    context = {'form': form}
    return render(request, "create_item.html", context)

 * ubah fungsi `show main` yang sudah ada menjadi berikut 
   ```
def show_main(request):
    items = Item.objects.all()

    context = {
        'name': 'Prasetyo Adi Wijonarko', # Nama kamu
        'class': 'PBP E', # Kelas PBP kamu
        'items': items
    }

    return render(request, "main.html", context)

 * buka `urls.py` pada folder `main` dan tambahkan import 
   ```
from main.views import show_main, create_product

 * pada cariabel `urlpatterns` dalam berkas `urls.py` tambahkan 
   ```
    path('create-item', create_item, name='create_item'),

 * buat berkas baru `create_product.html` pada `templates` dalam direktori `main`. tambahkan kode berikut
   ```
{% extends 'base.html' %} 

{% block content %}
<h1>Add New Product</h1>

<form method="POST">
    {% csrf_token %}
    <table>
        {{ form.as_table }}
        <tr>
            <td></td>
            <td>
                <input type="submit" value="Add Item"/>
            </td>
        </tr>
    </table>
</form>

{% endblock %}

 * buka kembali `main.html`, dalam block `{% block content %} tambahkan kode berikut untuk menampilkan data dalam bentuk table serta tombol "Add New Product"
   ```
...
<table>
    <h4>Anda menyimpan {{ items.count }} item disini</h4>
    <tr>
        <th>Name</th>
        <th>Price</th>
        <th>Description</th>
        <th>Date Added</th>
    </tr>

    {% comment %} Berikut cara memperlihatkan data produk di bawah baris ini {% endcomment %}

    {% for item in items %}
            <tr>
                <td>{{item.name}}</td>
                <td>{{item.amount}}</td>
                <td>{{item.description}}</td>
                <td>{{item.date_added}}</td>
            </tr>
        {% endfor %}
    </table>

    <br />

    <a href="{% url 'main:create_item' %}">
        <button>
            Add New Item
        </button>
    </a>

{% endblock content %}

* nyalakan virtual environtment, lalu jalankan `python manage.py runserver` dan buka http://localhost:8000. Sekarang web nya sudah diisi dengan data

<br>
<hr>

### Tambahkan 5 fungsi `views` untuk melihat objek yang sudah ditambahkan dalam format HTML, XML, JSON, XML by ID, dan JSON by ID.
1. Mengembalikan data dalam bentuk HTML
 * pada `views.py` pada folder `main`, lengkapi `show_main` seperti kode berikut
   ```
   def show_main(request):
    items = Item.objects.all()

    context = {
        'name': 'Prasetyo Adi Wijonarko', # Nama kamu
        'class': 'PBP E', # Kelas PBP kamu
        'items': items
    }

    return render(request, "main.html", context)

2. Mengembalikan data dalam bentuk XML
 * buka `views.py` pada folder `main`, tambahkan import 
   ```
   from django.http import HttpResponse
   from django.core import serializers

 * buat fungsi `show_xml` yang menerima parameter request menerima parameter request dan mengambil seluruh data dari model Product, lalu mengembalikan hasil query dalam bentuk XML dengan menggunakan `HttpResponse` dan content type "application/xml".
   ```
   def show_xml(request):
      data = Item.objects.all()
      return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

 * buka `buka urls.py` pada folder `main`, tambahkan import
   ```
   from main.views import show_main, create_item, show_xml 
 * pada variabel `urlpatterns` tambahkan path url untuk mengakses fungsi yang sudah diimport tadi
   ```
   path('xml/', show_xml, name='show_xml'), 

 * jalankan proyek dengan perintah `python manage.py runserver` dan buka  http://localhost:8000/xml 

3. Mengembalikan data dalam bentuk JSON
 * Buat fungsi `show_json` dalam file views.py yang menerima parameter request, ambil seluruh data `product`, lalu kembalikan hasil query       tersebut dalam format JSON sebagai `HttpResponse` dengan content type "application/json" menggunakan serializers.serialize("json", data).
   ```
   def show_json(request):
      data = Item.objects.all()
      return HttpResponse(serializers.serialize("json", data), content_type="application/json")

 * buka `urls.py` pada folder `main`, tambahkan import
   ```
   from main.views import show_main, create_item, show_xml, show_json

 * tambahkan path url ke dalam `urlpatterns`
   ```
   path('json/', show_json, name='show_json'), 

4. Mengembalikan data berdasarkan ID dalam bentuk XML dan JSON
 * buka `views.py` pada folder `main` dan buat fungsi `show_xml_by_id` dan `show_json_by_id`. berikut adalah kodenya
 - XML by ID
   ```
   def show_xml_by_id(request, id):
      data = Item.objects.filter(pk=id)
      return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

 - JSON by ID
   ```
   def show_json_by_id(request, id):
      data = Item.objects.filter(pk=id)
      return HttpResponse(serializers.serialize("json", data), content_type="app)

 * buka `urls.py` pada folder `main`, tambahkan import
   ```
   from main.views import show_main, create_item, show_xml, show_json, show_xml_by_id, show_json_by_id 

 * tambahkan path url ke dalam `urlpatterns`
   ```
   path('xml/<int:id>/', show_xml_by_id, name='show_xml_by_id'),
   path('json/<int:id>/', show_json_by_id, name='show_json_by_id'), 

 * jalankan proyek dengan perintah `python manage.py runserver` buka  http://localhost:8000/xml/[id] untuk XML by ID dan http://localhost:8000/json/[id] untuk JSON by ID

<br>
<hr>

### Membuat routing URL untuk masing-masing views yang telah ditambahkan pada poin 2.
 * kita akan mengubah routing dari `main/` menjadi `/`. nyalakan virtual environment 
   ```
   env\Scripts\activate.bat

 * buka `urls.py` pada folder `prezzmarket` ubah path `main/` menjadi ' ' pada `urlpatterns`
   ```
   path('', include('main.urls')),

 * jalankan server dengan perintah `python manage.py runserver` dan buka http://localhost:8000/ 
<br>
<hr>

### Apa perbedaan antara form `POST` dan form `GET` dalam Django?
1. Pengiriman Data
 * `POST` : mengirimkan data dalam bentuk "request body" yang tidak terlihat (tersembunyi) dalam url
 * `GET` : Mengirimkan data dalam bentuk "query parameters" yang terdapat pada url

2. Kemanan data
 * `POST` : lebih cocok untuk data sensitif karena data yang dikirimkan tidak terlihat dalam url
 * `GET` : Kurang aman untuk data sensitif karena saat mengirimkan data url terlihat dan dapat diakses siapa saja yang memiliki akses ke url tersebut

3. Fungsi 
 * `POST` : Digunakan ketika ingin mengirim data untuk pemrosesan lanjut seperti menyimpan data ke database atau eksekusi tindakan tertentu berdasarkan data yang dikirimkan sehingga cocok untuk formulir pengisian data
 * `GET` : Digunakan untuk mengirimkan data yang digunakan view Django untuk melakukan tindakan seperti pencarian atau pencarian data sehingga cocok untuk menjalankan permintaan yang bersifat `read-only` dan tidak mengubah data.
<br>
<hr>

### Apa perbedaan utama antara XML, JSON, dan HTML dalam konteks pengiriman data?
* XML digunakan untuk menyimpan dan mengirim data dengan format yang fleksibel dan self-descriptive. Data dalam XML disusun seperti struktur pohon dengan elemen-elemen yang memiliki hubungan parent-child. Namun, XML dapat menjadi sulit dibaca karena banyaknya markup yang digunakan.

* JSON, di sisi lain, digunakan untuk menyimpan data dalam bentuk terstruktur dengan format yang ringkas dan mudah dimengerti. Data dalam JSON disimpan dalam pasangan key-value dan dapat bersifat nested, membuatnya sangat berguna dalam pertukaran data antar-aplikasi, konfigurasi, dan penyimpanan data sederhana.

* HTML adalah bahasa markup yang digunakan untuk merancang struktur dan tampilan konten pada halaman web. HTML memungkinkan penggunaan tags untuk menandai berbagai elemen seperti headings, paragraf, tautan, gambar, dan tabel, sehingga memudahkan dalam merancang tampilan halaman web.
<br>
<hr>

### #Mengapa JSON sering digunakan dalam pertukaran data antara aplikasi web modern?
* Kemudahan dalam penulisan dan pemahaman dengan format `key`-`value` dan array 
* JSON memiliki fleksibilitas dalam menyimpan berbagai tipe data seperti string, boolean, array,  dan berbagai tipe data lainnya
* JSON dapat digunakan dengan berbagai bahasa pemrograman seperti JavaScript, Java, Python, C#, dan lain-lain. Hal ini memungkinkan penggunaan data dalam format JSON dalam berbagai bahasa pemrograman tanpa masalah kompatibilitas, mempermudah pertukaran data di berbagai platform dan lingkungan pemrograman yang berbeda.
* Mudah dikonversi ke JavaScript dan sebaliknya sehingga sangat bermanfaat bagi pengembang web dalam pemrosesan data.
<br>
<hr>


### Mengakses kelima URL di poin 2 menggunakan Postman, membuat screenshot dari hasil akses URL pada Postman, dan menambahkannya ke dalam `README.md.`
* nyalakan virtual environtment dengan perintah 
   ```
   env\Scripts\activate.bat

* jalankan perintah 
   ```
   python manage.py runserver

* Buka Postman dan buat request baru dengan method `GET` dan url http://localhost:8000/xml untuk XML, http://localhost:8000/json untuk JSON, http://localhost:8000/xml/[id] untuk XML by ID dan http://localhost:8000/json/[id] untuk JSON by ID.
* klik `Send` untuk mengirim request
* akan muncul hasil response dari request pada bagian bawah Postman
 - HTML

 - XML

 - JSON

 - XML by ID

 - JSON by ID
<br>
<hr>

## Tugas 2 PBP Ganjil 
<details>
<summary>Tugas 2</summary>
<br>
<hr>

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


