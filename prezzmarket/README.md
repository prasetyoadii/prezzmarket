# Prasetyo Adi Wijonarko, PBP E

## **Tugas PBP**

<details>
<summary>Tugas 5 </summary>

Checklist untuk tugas ini adalah sebagai berikut.
- [X] Kustomisasi desain pada templat HTML yang telah dibuat pada Tugas 4 dengan menggunakan CSS atau CSS framework (seperti Bootstrap, Tailwind, Bulma) dengan ketentuan sebagai berikut:
	- [x] Kustomisasi halaman login, register, dan tambah inventori semenarik mungkin.
	- [x] Kustomisasi halaman daftar inventori menjadi lebih berwarna maupun menggunakan apporach lain seperti menggunakan Card.
- [x] Menjawab beberapa pertanyaan berikut pada `README.md` pada root folder (silakan modifikasi `README.md` yang telah kamu buat sebelumnya; tambahkan subjudul untuk setiap tugas).
	- [x]Jelaskan manfaat dari setiap element selector dan kapan waktu yang tepat untuk menggunakannya.
	- [x] Jelaskan HTML5 Tag yang kamu ketahui.
	- [x] Jelaskan perbedaan antara margin dan padding.
   - [x] Jelaskan perbedaan antara framework CSS Tailwind dan Bootstrap. Kapan sebaiknya kita menggunakan Bootstrap daripada Tailwind, dan sebaliknya?
	- [x] Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
- [X] Melakukan add-commit-push ke GitHub.
<br>
<hr>

### Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
1. `create_item.html`
   * Pada `create_item.html` saya menambahkan CSS seperti berikut
   ```
   .add-item-container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #4caf50;
   }

   .add-item-form {
      text-align: center;
      padding: 20px;
      border-radius: 10px;
      background-color: white;
   }

   .add-item-header {
      color: #4caf50;
   }

   .add-item-table {
      margin: 0 auto;
   }

   .add-item-button {
      background-color: #4caf50;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
   }

   ```

   Penjelasan CSS di atas:

      * `.add-item-container`: Membuat wadah dengan tinggi 100% dari viewport (tinggi layar) dengan latar belakang warna hijau (#4caf50) dan mengatur kontennya ke 
      tengah baik secara horizontal maupun vertikal.
      * `add-item-form`: Mendesain formulir dengan latar belakang putih, padding 20px, dan sudut elemen formulir (border-radius) sebesar 10px.
      * `.add-item-header`: Memberi warna teks hijau untuk judul formulir.
      * `.add-item-table`: Mengatur margin formulir ke auto, sehingga akan berada di tengah-tengah halaman.
      * `.add-item-button`: Mendesain tombol dengan latar belakang hijau dan teks putih, dengan padding 10px di atas dan bawah serta 20px di kanan dan kiri, 
      membulatkan sudut tombol (border-radius) sebesar 5px, dan mengubah kursor saat diarahkan ke tombol.
   
   * Dengan menambahkan style yang sudah kita definisikan, ubah htmlnya agar dapat menggunakan style tersebut seperti contoh dibawah berikut:
   ```
   {% extends 'base.html' %} 

   {% block content %}
   <div class="add-item-container">
      <div class="add-item-form">
         <h1 class="add-item-header">Add New Item</h1>
         <form method="POST">
               {% csrf_token %}
               <table class="add-item-table">
                  {{ form.as_table }}
                  <tr>
                     <td></td>
                     <td>
                           <input type="submit" value="Add Item" class="add-item-button">
                     </td>
                  </tr>
               </table>
         </form>
      </div>
   </div>
   {% endblock %}

   ```

2. `login.html`
   * Pada `login.html` saya menambahkan CSS sebagai berikut:
   ```
      body {
         background-color: #58d358;
         display: flex;
         justify-content: center;
         align-items: center;
         height: 100vh;
         margin: 0;
      }

      .login {
         background-color: #ffffff;
         padding: 20px;
         border-radius: 10px;
         box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.1);
      }

      .login h1 {
         text-align: center;
         color: #008000;
      }

      .form-control {
         width: 90%;
         padding: 10px;
         margin: 10px 0;
         border: 1px solid #008000;
         border-radius: 5px;
      }

      .btn.login_btn {
         width: 30%;
         margin: 0 auto;
         background-color: #008000;
         color: #ffffff;
         border: none;
         padding: 10px;
         cursor: pointer;
         border-radius: 5px;
         display: block;
      }

      .btn.login_btn:hover {
         background-color: #005700;
      }

      .login p {
         text-align: center;
         margin-top: 20px;
      }

   ```
   Penjelasan
      * `body`: Mengatur latar belakang halaman dengan warna hijau muda (#58d358) dan mengatur tata letak halaman menjadi flex container agar elemen-elemen di dalamnya dapat diatur secara fleksibel.
      * `.login`: Mengatur tampilan kotak login dengan latar belakang putih, padding, sudut elemen login (border-radius), dan efek bayangan menggunakan properti box-shadow.
      * `.login h1`: Mengatur tampilan judul "Login" dengan warna hijau muda (#008000) dan posisi teks tengah (text-align: center).
      * `.form-control`: Mengatur tampilan input dengan lebar 90%, padding, margin atas dan bawah, border, dan sudut elemen input.
      * `.btn.login_btn`: Mengatur tampilan tombol login dengan lebar 30%, warna latar belakang hijau muda, warna teks putih, border, padding, kursor, sudut elemen tombol, dan membuatnya menjadi elemen blok untuk menerapkan margin tengah (margin: 0 auto).
      * `.btn.login_btn:hover:` Mengatur tampilan tombol saat dihover dengan mengubah warna latar belakang menjadi hijau tua (#005700).
      * `.login p`: Memusatkan teks "Don't have an account yet? Register Now" secara horizontal dan memberikan margin atas 20px

   * Setelah mendefinisikan style cssnya, tambahkan kode html sebagai berikut
   ```
   <body>
      <div class="login">
         <h1>Login</h1>
         <form method="POST" action="">
               {% csrf_token %}
               <div>
                  <input type="text" name="username" placeholder="Username" class="form-control">
               </div>

               <div>
                  <input type="password" name="password" placeholder="Password" class="form-control">
               </div>

               <div>
                  <input class="btn login_btn" type="submit" value="Login">
               </div>
         </form>

         {% if messages %}
         <ul>
               {% for message in messages %}
               <li>{{ message }}</li>
               {% endfor %}
         </ul>
         {% endif %}

         <p>Don't have an account yet? <a href="{% url 'main:register' %}">Register Now</a></p>
      </div>
   </body>

   </html>
   ```
3. `register.html`
   * Pada `register.html` saya menambahkan css sebagai berikut
   ```
   .login-container {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background-color: #4caf50;
   }

   .login {
      text-align: center;
      padding: 20px;
      border-radius: 10px;
      background-color: white;
   }

   .login-form table {
      margin: 0 auto;
   }

   .login-form input[type="text"], 
   .login-form input[type="password"] {
      width: 100%;
      margin-bottom: 10px;
      padding: 8px;
      box-sizing: border-box;
   }

   .login-form input[type="submit"] {
      background-color: #4caf50;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
   }

   .login-form input[type="submit"]:hover {
      background-color: #45a049;
   }
   ```

   Penjelasan
      * `.login-container`: Membuat wadah dengan tinggi 100% dari viewport (tinggi layar) dengan latar belakang warna hijau (#4caf50) dan mengatur kontennya ke tengah baik secara horizontal maupun vertikal.
      * `.login`: Membuat kotak formulir dengan latar belakang putih, padding 20px, dan sudut elemen formulir (border-radius) sebesar 10px.
      * `.login-form table`: Mengatur margin formulir ke auto, sehingga formulir berada di tengah halaman.
      * `.login-form input[type="text"], .login-form input[type="password"]`: Mengatur lebar input menjadi 100%, memberi margin bawah 10px, padding 8px, dan mengatur box-sizing agar padding tidak mempengaruhi lebar input.
      * `.login-form input[type="submit"]`: Mendesain tombol submit dengan latar belakang hijau (#4caf50), teks putih, padding 10px di atas dan bawah serta 20px di kanan dan kiri, membulatkan sudut tombol (border-radius) sebesar 5px, dan mengubah kursor saat diarahkan ke tombol.
      * `.login-form input[type="submit"]:hover`: Mengubah warna latar belakang tombol saat dihover menjadi hijau tua (#45a049).

   * Setelah mendefinisikan style cssnya, tambahkan kode html sebagai berikut
   ```
   <div class="login-container">
      <div class="login">
         <h1>Register</h1>  

         <form method="POST" class="login-form">  
               {% csrf_token %}  
               <table>
                  {{ form.as_table }}  
                  <tr>  
                     <td></td>
                     <td><input type="submit" name="submit" value="Daftar"/></td>  
                  </tr>  
               </table>  
         </form>

         {% if messages %}  
               <ul>   
                  {% for message in messages %}  
                     <li>{{ message }}</li>  
                  {% endfor %}  
               </ul>   
         {% endif %}
      </div>
   </div>  
   ```
4. `main.html`
   * Pada `main.html` saya menambahkan CSS sebagai berikut:
   ```
      body {
         background-color: #f5f5f5;
         font-family: Arial, sans-serif;
         margin: 0;
         padding: 0;
      }

      .header {
         background-color: #4caf50;
         color: white;
         padding: 15px;
         text-align: left;
         display: flex;
         justify-content: space-between;
         align-items: center;
         margin-bottom: 30px;
      }

      .last-login-text {
         bottom: 20px;
         right: 20px;
         background-color: white;
         padding: 10px;
         border-radius: 5px;
         box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
      }

      .header-right {
         display: flex;
         gap: 20px;
      }

      .container {
         display: flex;
         flex-wrap: wrap;
         justify-content: center;
         padding: 20px;
      }

      .add-button {
         margin: 0 200px;
         background-color: #4caf50;
         color: white;
         border: none;
         padding: 14px 20px;
         border-radius: 5px;
         cursor: pointer;
         transition: background-color 0.3s ease;
         margin-bottom: 5px;
         text-decoration: none;
      }

      .add-button:hover {
         background-color: #45a049;
      }

      .item-count {
         font-size: 20px;
         font-weight: bold;
         margin-bottom: 10px;
         font-family: "Roboto", sans-serif;
      }

      .top-section {
         margin: 0 80px;
         margin-top: 20px;
         display: flex;
         justify-content: space-between;
         width: 100%;
         margin-bottom: 5px;
      }

      .card {
         width: 300px;
         margin: 20px;
         padding: 40px;
         border-radius: 10px;
         box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
         background-color: white;
         transition: box-shadow 0.3s ease;
      }

      .card-buttons {
         display: flex;
         flex-direction: column;
         justify-content: space-between;
         margin-top: 20px;
      }

      .card-button {
         background-color: #4caf50;
         color: white;
         border: none;
         padding: 10px 20px;
         border-radius: 5px;
         cursor: pointer;
         transition: background-color 0.3s ease;
         width: 100px;
         text-align: center;
         text-decoration: none;
      }

      .button-row {
         display: flex;
         justify-content: space-between;
         margin-bottom: 10px;
      }

      .card-button:last-child {
         margin-right: 0;
      }

      .card-button:hover {
         background-color: #45a049;
      }

      .logout {
         color: white;
         text-decoration: none;
         background-color: #f44336;
         padding: 10px 20px;
         border-radius: 5px;
         transition: background-color 0.3s ease;
      }

      .logout:hover {
         background-color: #d32f2f;
      }
   ```
   Penjelasannya :
      * `Body`: Digunakan untuk mengatur properti dasar halaman: Memberikan latar belakang berwarna (#f5f5f5), menggunakan font Arial dan fallback sans-serif, 
      serta menghapus margin dan padding default.
      * `.header`: Digunakan untuk mengatur header halaman: Memberikan latar belakang hijau (#4caf50), teks putih, padding 15px, dan mengatur elemen-elemen 
      di dalamnya menggunakan flexbox agar terletak di sebelah kiri dan kanan.
      * `.last-login-text`: Digunakan untuk menampilkan teks sesi terakhir login: Memberikan latar belakang putih, padding 10px, border-radius 5px, dan efek bayangan (box shadow) untuk memberi elemen tampilan bertekstur.
      * `.header-right`: Digunakan untuk mengelompokkan elemen di sebelah kanan header: Menggunakan flexbox dengan jarak (gap) 20px antar elemen.
      * `.container`: Digunakan untuk mengelompokkan konten halaman: Menggunakan flexbox dengan wrap agar konten dapat melingkupi ke baris baru jika ruang tidak mencukupi, 
      dan memberikan padding 20px.
      * `.add-button`: Digunakan untuk tombol "Buat Item": Memberikan margin di sisi kanan dan kiri, latar belakang hijau, teks putih, padding, sudut melengkung, efek hover 
      dengan perubahan warna latar belakang, dan mengubah kursor menjadi tanda tangan saat dihover.
      * `.item-count`: Digunakan untuk menunjukkan jumlah item: Memberikan ukuran font 20px, tebal, dan menggunakan font "Roboto" atau fallback sans-serif.
      * `.top-section`: Digunakan untuk mengatur bagian atas halaman: Menggunakan flexbox dengan ruang margin, memberikan efek hover pada tombol "Buat Item" seperti .add-button.
      * `.card`: Digunakan untuk mengatur kartu item: Memberikan lebar 300px, margin, padding, sudut melengkung, efek bayangan, dan transisi efek bayangan untuk 
      merespons perubahan hover.
      * ``.card-buttons``: Digunakan untuk mengelompokkan tombol-tombol di dalam kartu item: Menggunakan flexbox dengan penataan vertikal, memberikan ruang margin di bagian atas.
      * ``.card-button``: Digunakan untuk tombol-tombol dalam kartu item: Memberikan latar belakang hijau, teks putih, padding, sudut melengkung, efek hover 
      dengan perubahan warna latar belakang, dan mengubah kursor menjadi tanda tangan saat dihover.
      * ``.logout``: Digunakan untuk tombol logout: Memberikan warna teks putih, latar belakang merah (#f44336), padding, sudut melengkung, dan efek hover dengan 
      perubahan warna latar belakang.
   * Setelah mendefinisikan css style, tambahkan kode html sebagai berikut
   ```
      <body>
      <div class="header">
         <div class="header-left">
               <p><strong>Nama:</strong> {{ name }}</p>
               <p><strong>Kelas:</strong> {{ class }}</p>
         </div>
         <div class="header-right">
               <a href="{% url 'main:logout' %}" class="logout">Logout</a>
         </div>
      </div>

      <div class="top-section">
         <div class="top-section">
               <h2 class="item-count">Anda menyimpan {{ items.count }} item disini</h2>
               <a href="{% url 'main:create_item'%}" class="add-button">Buat Item</a>
         </div>
      </div>

      <div class="container">
         {% for item in items %}
               <div class="card">
                  <h2>{{ item.name }}</h2>
                  <p><strong>Jumlah:</strong> {{ item.amount }}</p>
                  <p><strong>Deskripsi:</strong> {{ item.description }}</p>
                  <div class="card-buttons">
                     <div class="button-row">
                           <a href="add_amount/{{ item.id }}" class="card-button">Tambah</a>
                           <a href="decrement_amount/{{ item.id }}" class="card-button">Kurang</a>
                     </div>
                     <div class="button-row">
                           <a href="edit_item/{{ item.id }}" class="card-button">Edit</a>
                           <a href="delete_item/{{ item.id }}" class="card-button">Hapus</a>
                     </div>
                  </div>
               </div>
         {% endfor %}
      </div>

      <div class="last-login-text">
         Sesi terakhir login: {{ last_login }}
      </div>

      </body>
      {% endblock content %}
      </html>

   ```
<br>
<hr>

### Jelaskan manfaat dari setiap element selector dan kapan waktu yang tepat untuk menggunakannya.
* Element Selector memungkinkan kita mengubah properti untuk semua elemen yang memiliki tag HTML yang sama.Kita dapat menggunakan element sebagai selector dalam file CSS. Element selector menggunakan format [id_name] (tanpa diawali oleh sebuah simbol).  Cocok digunakan saat Anda ingin mengubah gaya untuk semua elemen dengan tag HTML yang sama.
* ID selector menggunakan ID pada tag sebagai selector-nya. ID bersifat unik dalam satu halaman web. ID dapat ditambahkan pada halaman template HTML.Kemudian, kita dapat menggunakan ID tersebut sebagai selector dalam file CSS. ID selector menggunakan format #[id_name] (selalu diawali #).Digunakan ketika kita hanya memiliki satu elemen dalam halaman web yang membutuhkan pengaturan khusus dan unik.
* Class Selector memungkinkan kita untuk mengelompokkan elemen dengan karakteristik yang sama.Kemudian, kita dapat menggunakan Class tersebut sebagai selector dalam file CSS. Class selector menggunakan format .[class_name] (diawali .). Cocok digunakan ketika kita ingin mengelompokkan beberapa elemen yang memiliki karakteristik atau styling yang sama.
<br>
<hr>

### Jelaskan HTML5 tag uang kamu ketahui
* `<article>`: Digunakan untuk mendefinisikan sebuah konten independen dalam dokumen, seperti artikel blog, majalah, atau koran.
* `<aside>` : Menunjukkan bahwa artikel tersebut memiliki hubungan yang sedikit terkait dengan konten keseluruhan halaman.
* `<canvas>`: Digunakan untuk menggambar gambar atau grafik.
* `<details>`: Menyatakan informasi atau kontrol tambahan yang diperlukan oleh pengguna.
* `<footer>`: Mendefinisikan footer untuk sebuah bagian.
* `<header>`: Mendefinisikan header untuk sebuah bagian.
* `<nav>`: Digunakan untuk mendefinisikan tautan navigasi dalam dokumen.
* `<progress>`: Menyatakan kemajuan dari suatu tugas.
* `<rp>`: Mendefinisikan apa yang harus ditampilkan di browser yang tidak mendukung anotasi ruby.
* `<rt>`: Mendefinisikan penjelasan atau pelafalan karakter.
* `<ruby>`: Mendefinisikan anotasi ruby bersama dengan `<rp>` dan `<rt>`.
* `<section>`: Mendefinisikan sebuah bagian dalam dokumen.
* `<summary>`: Menyatakan judul yang terlihat untuk elemen ``<details>``.
<br>
<hr>

### Jelaskan perbedaan antara margin dan padding
* Padding:
   * Representasi: Padding menggambarkan jumlah ruang dalam 
   (inner space) yang dimiliki oleh suatu elemen.
   * Pengaturan Otomatis: Tidak mungkin mengatur padding 
   sebagai "auto padding." Padding harus ditentukan secara eksplisit.
   * Pengaturan Nilai Negatif: Tidak mungkin menggunakan nilai
   negatif saat mendefinisikan padding. Padding tidak dapat memiliki nilai negatif.
   * Pengaruh Terhadap Elemen Lain: Padding dapat dipengaruhi 
   oleh gaya elemen lain di situs web, seperti font atau ukuran konten.

* Margin:
   * Representasi: Margin adalah whitespace (ruang putih) yang tersedia di sekitar suatu elemen, menentukan jarak antara elemen tersebut dan elemen-elemen lain di sekitarnya.
   * Pengaturan Otomatis: Mungkin menggunakan pengaturan otomatis (seperti "margin: auto;") untuk margin, yang akan secara otomatis menyesuaikan margin berdasarkan konten dan lebar elemen terkait.
   * Pengaturan Nilai Negatif: Mungkin menggunakan nilai negatif saat mendefinisikan margin. Nilai negatif dalam margin dapat digunakan untuk menempatkan elemen di luar batas normalnya, menghasilkan tumpukan elemen.
   * Pengaruh Terhadap Elemen Lain: Margin tidak dipengaruhi oleh stylisasi elemen-elemen lain di situs web. Margin dapat mempengaruhi jarak antara elemen-elemen di sekitarnya tanpa mempengaruhi gaya elemen lainnya.
<br>
<hr>

### Jelaskan perbedaan antara framework CSS Tailwind dan Bootstrap. Kapan sebaiknya kita menggunakan Bootstrap daripada Tailwind, dan sebaliknya?
1. Tailwind
   * Tailwind CSS membangun tampilan dengan menggabungkan kelas-kelas utilitas yang telah didefinisikan sebelumnya.
   * Tailwind CSS memiliki file CSS yang lebih kecil sedikit dibandingkan Bootstrap dan hanya akan memuat kelas-kelas utilitas yang ada
   * Tailwind CSS memiliki memberikan fleksibilitas dan adaptabilitas tinggi terhadap proyek
   * Tailwind CSS memiliki pembelajaran yang lebih curam karena memerlukan pemahaman terhadap kelas-kelas utilitas yang tersedia dan bagaimana menggabungkannya untuk mencapai tampilan yang diinginkan.

2. Bootstrap
   * Bootstrap menggunakan gaya dan komponen yang telah didefinisikan, yang memiliki tampilan yang sudah jadi dan dapat digunakan secara langsung.
   * Bootstrap memiliki file CSS yang lebih besar dibandingkan dengan Tailwind CSS karena termasuk banyak komponen yang telah didefinisikan.
   * Bootstrap sering kali menghasilkan tampilan yang lebih konsisten di seluruh proyek karena menggunakan komponen yang telah didefinisikan.
   * Bootstrap memiliki pembelajaran yang lebih cepat untuk pemula karena dapat mulai dengan komponen yang telah didefinisikan. 

Jika menginginkan kontrol penuh dan kemampuan kostumisasi yang tinggi, Tailwind CSS merupakan pilihan yang baik. Namun, jika membutuhkan solusi cepat dan komponen yang sudah siap pakai dan konsistensi desain, Bootstrap lebih sesuai.

</details>

<details>
<summary>Tugas 4</summary>

Checklist untuk tugas ini adalah sebagai berikut.
- [X] Mengimplementasikan fungsi registrasi, login, dan logout untuk memungkinkan pengguna untuk mengakses aplikasi sebelumnya dengan lancar.
- [x] Membuat dua akun pengguna dengan masing-masing tiga dummy data menggunakan model yang telah dibuat pada aplikasi sebelumnya untuk 
      setiap akun di lokal.
- [x] Menghubungkan model `Item` dengan `User`.
- [x] Menampilkan detail informasi pengguna yang sedang logged in seperti username dan menerapkan `cookies` seperti `last login` 
      pada halaman utama aplikasi.
- [x] Menjawab beberapa pertanyaan berikut pada `README.md` pada root folder (silakan modifikasi `README.md` yang telah kamu 
      buat sebelumnya; tambahkan subjudul untuk setiap tugas).
	- [x]Apa itu Django `UserCreationForm`, dan jelaskan apa kelebihan dan kekurangannya?
	- [x] Apa perbedaan antara autentikasi dan otorisasi dalam konteks Django, dan mengapa keduanya penting?
	- [x] Apa itu _cookies_ dalam konteks aplikasi web, dan bagaimana Django menggunakan _cookies_ untuk mengelola data sesi pengguna?
   - [x] Apakah penggunaan cookies aman secara default dalam pengembangan web, atau apakah ada risiko potensial yang harus diwaspadai?
	- [x] Jelaskan bagaimana cara kamu mengimplementasikan checklist di	atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
- [X] Melakukan add-commit-push ke GitHub.
<br>
<hr>

### Mengimplementasikan fungsi registrasi, login, dan logout untuk memungkinkan pengguna untuk mengakses aplikasi sebleumnya dengan lancar
1. Membuat Fungsi dan Form Registrasi
   * Buka `views.py` pada subdirektori `main` dan buat fungsi `register ` yang menerima parameter request`, tambahkan kode berikut: 
   ```
   from django.shortcuts import redirect
   from django.contrib.auth.forms import UserCreationForm
   from django.contrib import messages  

   def register(request):
      form = UserCreationForm()

      if request.method == "POST":
         form = UserCreationForm(request.POST)
         if form.is_valid():
            form.save()
            messages.success(request, 'Your account has been successfully created!')
            return redirect('main:login')
      context = {'form':form}
      return render(request, 'register.html', context)
   ```

   * Buat berkas `register.html` pada `main/templates`, tambahkan kode berikut: 
   ```
   {% extends 'base.html' %}

   {% block meta %}
      <title>Register</title>
   {% endblock meta %}

   {% block content %}  

   <div class = "login">
      
      <h1>Register</h1>  

         <form method="POST" >  
               {% csrf_token %}  
               <table>  
                  {{ form.as_table }}  
                  <tr>  
                     <td></td>
                     <td><input type="submit" name="submit" value="Daftar"/></td>  
                  </tr>  
               </table>  
         </form>

      {% if messages %}  
         <ul>   
               {% for message in messages %}  
                  <li>{{ message }}</li>  
                  {% endfor %}  
         </ul>   
      {% endif %}

   </div>  

   {% endblock content %}
   ```

   * Buka `urls.py` dan tambahkan kode berikut:
    ```
    from main.views import register
    ```

    tambahkan _pathurl_

    ```
    path('register/', register, name='register'),
    ```
2. Membuat Fungsi Login
   * Buka `views.py` pada subdirektori `main` dan buatlah fungsi dengan nama `login_user` yang menerima parameter `request`. 
     Tambahkan kode berikut:
   ```
   from django.contrib.auth import authenticate, login

   def login_user(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('main:show_main')
        else:
            messages.info(request, 'Sorry, incorrect username or password. Please try again.')
    context = {}
    return render(request, 'login.html', context)
   ```
   * Buat berkas `login.html` pada `main/templates`, tambahkan kode berikut
   ```
   {% extends 'base.html' %}

   {% block meta %}
      <title>Login</title>
   {% endblock meta %}

   {% block content %}

   <div class = "login">

      <h1>Login</h1>

      <form method="POST" action="">
         {% csrf_token %}
         <table>
               <tr>
                  <td>Username: </td>
                  <td><input type="text" name="username" placeholder="Username" class="form-control"></td>
               </tr>
                     
               <tr>
                  <td>Password: </td>
                  <td><input type="password" name="password" placeholder="Password" class="form-control"></td>
               </tr>

               <tr>
                  <td></td>
                  <td><input class="btn login_btn" type="submit" value="Login"></td>
               </tr>
         </table>
      </form>

      {% if messages %}
         <ul>
               {% for message in messages %}
                  <li>{{ message }}</li>
               {% endfor %}
         </ul>
      {% endif %}     
         
      Don't have an account yet? <a href="{% url 'main:register' %}">Register Now</a>

   </div>

   {% endblock content %}
   ```

   * Buka `urls.py` tambahkan kode berikut
   ```
   from main.views import login_user
   ```

   Tambahkan _path url_
   ```
   path('login/', login_user, name='login'),
   ```

   3. Membuat funsi Logout 
   * Buka `views.py` pada subdirektori `main` dan buatlah fungsi dengan nama `logout_user` yang menerima parameter `request`. Tambahkan kode berikut:
   ```
   from django.contrib.auth import logout

   def logout_user(request):
    logout(request)
    return redirect('main:login')
   ```
   * Tambahkan kode berikut pada berkas `main.html` setelah _hyperlink tag_
   ```
   <a href="{% url 'main:logout' %}">
      <button>
         Logout
      </button>
   </a>
   ```

   * Buka `urls.py` tambahkan kode berikut
   ```
   from main.views import logout_user
   ```

   Tambahkan _path url_
   ```
   path('logout/', logout_user, name='logout'),
   ```
<br>
<hr>

### Membuat dua akun pengguna dengan masing-masing tiga dummy data menggunakan model yang telah dibuat pada aplikasi sebelumnya untuk setiap akun di lokal.
* Nnyalakan virtual environtment, lalu jalankan `python manage.py runserver` dan buka http://localhost:8000.
* Lakukan register, pada kasus ini saya menambahkan 2 dummy account yaitu 
   dummy account 1
   - name : Prasetyo_Adi
   - pass : jasjustehsisri
   - Item : 
      - Mangga - 5 - Mangga fresh dan segar	
      - Rujak - 20 - Rujak Segar
      - Ikan Kembung - 12 - Ikan kembung import
   dummyaccount 2
   - name : Ghoni
   - pass : GhaniGhoni
   - item : 
      - Pepaya - 11 - Pepaya Segar
      - Mangga - 21 - Mangga Segar
      - Ikan Lele - 15 - Ikan lele fresh
<br>
<hr>

### Menghubungkan model `Item` dengan `User`.
* Buka `models.py` pada subdirektori `main`, tambahkan kode:
   ```
   from django.contrib.auth.models import User
   ```

   Pada class Item tambahkan kode berikut
   ```
   user = models.ForeignKey(User, on_delete=models.CASCADE)
   ```
* Buka `views.py` pada subdirektori `main`, ubah `create_item`
   ```
   def create_item(request):
   item = ItemForm(request.POST or None)

   if form.is_valid() and request.method == "POST":
      item = form.save(commit=False)
      item.user = request.user
      item.save()
      return HttpResponseRedirect(reverse('main:show_main'))
   ...
   ```
* Ubah fungsi showmain
   ```
   def show_main(request):
      item = Item.objects.filter(user=request.user)

      context = {
        'name': request.user.username,
      ...
      }
   ```
* Nyalakan virtual environment, lakukan migrasi dengan menjalankan `python manage.py makemigrations`
* Jika muncul _error_, pilih `1` untuk menetapkan default value untuk field user pada semua row yang telah dibuat pada basis data.
* ketik `1` untuk menetapkan user dengan ID 1 (yang sudah kita buat sebelumnya) pada model yang sudah ada.
* Aplikasikan migrasi dengan melakukan `python manage.py migrate`
<br>
<hr>

### Menampilkan detail informasi pengguna yang sedang logged in seperti username dan menerapkan `cookies` seperti `last login` pada halaman utama aplikasi.
* Buka `views.py` tambahkan kode
```
import datetime
from django.http import HttpResponseRedirect
from django.urls import reverse
```
* Pada `login_user` ganti kode pada blok `if user is not None` menjadi berikut
```
...
if user is not None:
    login(request, user)
    response = HttpResponseRedirect(reverse("main:show_main")) 
    response.set_cookie('last_login', str(datetime.datetime.now()))
    return response
...
```
* Pada fungsi `show_main`, tambahkan kode berikut 
```
context = {
        'name': request.user.username,
        'class': 'PBP E', # Kelas PBP kamu
        'items': items,
        'last_login': request.COOKIES['last_login'],
    }
```
* Ubah fungsi `logout_user` menjadi 
```
def logout_user(request):
    logout(request)
    response = HttpResponseRedirect(reverse('main:login'))
    response.delete_cookie('last_login')
    return response
```
* Pada `main.html` tambahkan kode berikut diantara tabel dan tombol logout untuk menampilkan last login
```
...
<h5>Sesi terakhir login: {{ last_login }}</h5>
...
```
* Nyalakan virutal environment, jalankan server `python manage.py runserver`
* Untuk melihat data cookie `last_login`, klik kanan, klik _inspect element_, cari bagian _Application/Storage_. Klik bagian _Cookies_ 
   dan data _cookies_ akan tersedia
<br>
<hr>

### Apa itu Django `UserCreationForm`, dan jelaskan apa kelebihan dan kekurangannya?
UserCreationForm merupakan sebuah formulir bawan Django yang digunakan untuk memproses pendaftaran pengguna baru. Formulir ini memiliki tiga `field`, yaitu `username`, `password1`, dan `password2` (untuk konfirmasi password). Kelebihan dari UserCreationForm diantaranya mempermudah _developer_ untuk menngimplementasikan fitur register dengan cepat dan aman. Formulir ini juga menyediakan fitur bawaan seperti validasi dan enkripsi password secara otomatis. Kelemahannya adalah tampilan formulir ini standar, namun kelemahan ini masih bisa ditutupi dengan mengubah tampilannya secara ekstensif sesuai dengan desain yang kita inginkan
<br>
<hr>

### Apa perbedaan antara autentikasi dan otorisasi dalam konteks Django, dan mengapa keduanya penting?
Autentikasi merupakan proses yang digunakan untuk memverifikasi identitas seseorang (login). Otorisasi merupakan proses pengendalian hak akses terhadap sumber daya yang dilakukan setelah autentikasi. Perbedaannya, Autentikasi merupakan tahap sebelum otorisasi seperti mengecek kombinasi username dan password, jika sudah sesuai maka akan masuk ke tahap otorisasi dimana user tersebut akan memiliki akses ke sebuah sumber daya tersebut. Keduanya digunakan administrator untuk melindungi sistem dan informasi, termasuk dalam _framework_ django.
<br>
<hr>

### Apa itu _cookies_ dalam konteks aplikasi web, dan bagaimana Django menggunakan _cookies_ untuk mengelola data sesi pengguna
Cookies adalah sejumlah kecil informasi yang dikirim oleh server web ke browser pengguna dan kemudian dikirim kembali oleh browser pada permintaan halaman selanjutnya. Informasi ini disimpan dalam bentuk teks di sisi klien (browser) dan digunakan untuk berbagai tujuan seperti autentikasi, pelacakan pengguna, pemeliharaan prefrensi pengguna. Django menggunakan cookie yang disebut "session id" untuk menyimpan kunci sesi di browser pengguna. Data sesi yang sebenarnya, seperti preferensi atau status login pengguna, disimpan di dalam database secara default. Namun, kita dapat mengonfigurasi Django untuk menyimpan data sesi di tempat lain seperti sistem berkas, cookie, atau cache.
<br>
<hr>

### Apakah penggunaan cookies aman secara default dalam pengembangan web, atau apakah ada risiko potensial yang harus diwaspadai?
Penggunaan cookies secara default dalam pengembangan web tidak dianggap sebagai risiko keamanan yang signifikan. Namun, risiko muncul seperti cross site scripting (XSS), Session Hijacking, Cross-Site Request Forgery (XSRF). Dalam serangan XSS, penyerang dapat menyisipkan skrip berbahaya ke halaman web yang akan di eksekusi pengguna dan dapat digunakan untuk mencuri informasi dari cookies. Dalam serangan session hijacking, cookie sesi dicuri oleh pihak lain, sehingga penyerang dapat mengakses sesi pengguna sah dan melakukan tindakan atas nama pengguna. Pada XSRF, penyerang akan menghasut pengguna yang telah terotentikasi untuk melakukan tindakan seperti mengklik tautan atau mengirim permintaan HTTP, tanpa sepengetahuan mereka. Sehingga bisa saja mengakibatkan penghapusan data, perubahan data, pencurian data, dan lain-lain
</details>

<details>
<summary>Tugas 3</summary>

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

2. Setelah membuat kerangka, kita membuat form input data  
* buat berkas `forms.py` pada direktori main. tambahkan kode berikut
   ```
   from django.forms import ModelForm
   from main.models import Item

   class ItemForm(ModelForm):
      class Meta:
         model = Item
         fields = ["name", "amount", "description"]
kode ini digunakan untuk membuat struktur form yang menerima data item baru
 * buka berkas `views.py` yang ada pada foler `main` tambahkan import sebagai berikut
   ```
   from django.http import HttpResponseRedirect
   from main.forms import ItemForm
   from django.urls import reverse

 * dalam berkas yang sama, buat fungsi `create_item` yang menerima parameter `request` untuk menghasilkan form yang 
   dapat menambahkan data secara otomatis.  berikut kodenya
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
   from main.views import show_main, create_item

 * pada variabel `urlpatterns` dalam berkas `urls.py` tambahkan 
   ```
   path('create-item', create_item, name='create_item'),

 * buat berkas baru `create_item.html` pada `templates` dalam direktori `main`. tambahkan kode berikut
   ```
   {% extends 'base.html' %} 

   {% block content %}
   <h1>Add New Item</h1>

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

 * Buka kembali `main.html`, dalam block `{% block content %} tambahkan kode berikut untuk menampilkan data dalam bentuk table 
   serta tombol "Add New Item"
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

      {% comment %} Berikut cara memperlihatkan data item di bawah baris ini {% endcomment %}

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

* nyalakan virtual environtment, lalu jalankan `python manage.py runserver` dan buka http://localhost:8000. Sekarang 
  web nya sudah diisi dengan data

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

 * buat fungsi `show_xml` yang menerima parameter request menerima parameter request dan mengambil seluruh 
   data dari model Item, lalu mengembalikan hasil query dalam bentuk XML dengan menggunakan `HttpResponse` dan content type "application/xml".
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
 * Buat fungsi `show_json` dalam file views.py yang menerima parameter request, ambil seluruh data `item`, lalu kembalikan 
   hasil query tersebut dalam format JSON sebagai `HttpResponse` dengan content type "application/json" 
   menggunakan serializers.serialize("json", data).
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

 * jalankan proyek dengan perintah `python manage.py runserver` buka  http://localhost:8000/xml/[id] untuk 
   XML by ID dan http://localhost:8000/json/[id] untuk JSON by ID
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
 * `POST` : Mengirimkan data dalam bentuk "request body" yang tidak terlihat (tersembunyi) dalam url
 * `GET`  : Mengirimkan data dalam bentuk "query parameters" yang terdapat pada url

2. Kemanan data
 * `POST` : Lebih cocok untuk data sensitif karena data yang dikirimkan tidak terlihat dalam url
 * `GET`  : Kurang aman untuk data sensitif karena saat mengirimkan data url terlihat dan dapat diakses siapa 
            saja yang memiliki akses ke url tersebut

3. Fungsi 
 * `POST` : Digunakan ketika ingin mengirim data untuk pemrosesan lanjut seperti menyimpan data ke database atau eksekusi 
            tindakan tertentu berdasarkan data yang dikirimkan sehingga cocok untuk formulir pengisian data
 * `GET`  : Digunakan untuk mengirimkan data yang digunakan view Django untuk melakukan tindakan seperti pencarian atau pencarian 
            data sehingga cocok untuk menjalankan permintaan yang bersifat `read-only` dan tidak mengubah data.
<br>
<hr>

### Apa perbedaan utama antara XML, JSON, dan HTML dalam konteks pengiriman data?
* XML digunakan untuk menyimpan dan mengirim data dengan format yang fleksibel dan self-descriptive. Data dalam XML 
  disusun seperti struktur pohon dengan elemen-elemen yang memiliki hubungan parent-child. Namun, XML dapat menjadi sulit dibaca 
  karena banyaknya markup yang digunakan.

* JSON, di sisi lain, digunakan untuk menyimpan data dalam bentuk terstruktur dengan format yang ringkas dan mudah dimengerti. Data dalam 
  JSON disimpan dalam pasangan key-value dan dapat bersifat nested, membuatnya sangat berguna dalam pertukaran data antar-aplikasi, 
  konfigurasi, dan penyimpanan data sederhana.

* HTML adalah bahasa markup yang digunakan untuk merancang struktur dan tampilan konten pada halaman web. HTML memungkinkan penggunaan 
  tags untuk menandai berbagai elemen seperti headings, paragraf, tautan, gambar, dan tabel, sehingga memudahkan dalam merancang 
  tampilan halaman web.
<br>
<hr>

### #Mengapa JSON sering digunakan dalam pertukaran data antara aplikasi web modern?
* Kemudahan dalam penulisan dan pemahaman dengan format `key`-`value` dan array 
* JSON memiliki fleksibilitas dalam menyimpan berbagai tipe data seperti string, boolean, array,  dan berbagai tipe data lainnya
* JSON dapat digunakan dengan berbagai bahasa pemrograman seperti JavaScript, Java, Python, C#, dan lain-lain. Hal ini memungkinkan 
  penggunaan data dalam format JSON dalam berbagai bahasa pemrograman tanpa masalah kompatibilitas, mempermudah pertukaran data di 
  berbagai platform dan lingkungan pemrograman yang berbeda.
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

* Buka Postman dan buat request baru dengan method `GET` dan url http://localhost:8000/xml untuk XML, http://localhost:8000/json 
 untuk JSON, http://localhost:8000/xml/[id] untuk XML by ID dan http://localhost:8000/json/[id] untuk JSON by ID.
* klik `Send` untuk mengirim request
* akan muncul hasil response dari request pada bagian bawah Postman
 - HTML
![HTML ini](https://github.com/prasetyoadii/prezzmarket/assets/125488022/51fd6233-7b32-4374-99f2-039f74f8c5cd)
 - XML
![XML ini](https://github.com/prasetyoadii/prezzmarket/assets/125488022/4850f7e5-083b-49b6-a411-24f869a8cd82)
 - JSON
![JSON ini](https://github.com/prasetyoadii/prezzmarket/assets/125488022/9b5f3d98-4902-40a8-8cb7-cab604ccaa58)
 - XML by ID
![XML TPI ID](https://github.com/prasetyoadii/prezzmarket/assets/125488022/0b18115b-e070-478a-80e3-a97c5f9ec5a7)
 - JSON by ID
![JSON TAPI ID](https://github.com/prasetyoadii/prezzmarket/assets/125488022/5b2cdf18-f52f-4e6f-9cf6-d8c02542ac1f)
</details>

<details>
<summary>Tugas 2</summary>
	
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


