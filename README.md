# 🎸 TiKoes 👨🏻

**Tugas - Pemrograman Berbasis Platform - Kelas D**
> **TiKoes** (**T**eknologi **I**nventaris pada album **Koes** Plus) adalah aplikasi *mobile* untuk mengelola penyimpanan berbagai macam album Koes Plus.

<details>
<summary> <b> Tugas 7: Elemen Dasar Flutter </b> </summary>

## *Stateless Widget* dan *Stateful Widget*
Secara singkat,
* **Stateless Widget**: *Widget* yang tidak dapat berubah setelah dibuat.
* **Stateful Widget**: *Widget* yang dapat berubah secara dinamis.

Perbedaan kedua *widget* dapat dilihat pada tabel berikut ini.
| Atribut | Stateless Widgets | Stateful Widgets |
|--|--|--|
| Mutable State | Tidak memiliki *mutable state* | Dapat memiliki *mutable state* |
| Sifat | Statis, tidak merespons peristiwa eksternal | Dinamis, dapat mengubah atribut berdasarkan interaksi *user* atau perubahan data |
| *Rebuild* | Tidak dilakukan | *Rebuild* pada saat *state* diperbarui |
| Kasus Penggunaan | Menampilkan konten statis, seperti teks, ikon, atau gambar | Menangani elemen UI dinamis seperti komponen interaktif |
| Kinerja | Sangat efisien dan ringan | Mungkin memiliki *overhead* sedikit lebih tinggi karena manajemen *state* |
| Kompleksitas Kode | Sederhana | Memerlukan manajemen *state* dan implementasi logika perubahan *state* |
| Fleksibilitas Penggunaan | Cocok untuk komponen yang tidak memerlukan pembaruan yang sering | Penting untuk komponen yang berubah secara teratur |
| Contoh Widget | Teks, Ikon, Gambar | Checkbox, TextField, Slider |

**Widget Life Cycle pada Flutter**:
<p align="center"><img src="https://admin.tops-int.com/storage/media/editor_images/12025.png" width="900"></p>

**Decision Tree**:
<p align="center"><img src="https://admin.tops-int.com/storage/media/editor_images/97441.png" width="900"></p>

## Widget yang Digunakan
| Widget | Fungsi |
|--|--|
| `MyApp` (`MaterialApp`) | Mengonfigurasi aplikasi Flutter secara global serta menentukan tema dan halaman beranda. |
| `Scaffold` | Membuat tata letak dasar aplikasi. |
| `AppBar` | Menampilkan bagian atas aplikasi dengan judul dan latar belakang warna. |
| `Text` | Menampilkan teks dengan format yang sesuai. |
| `SingleChildScrollView`| Wrapper yang memungkinkan konten dapat discroll jika melebihi ukuran layar. |
| `Padding` | Memberikan jarak antara konten dengan tepi layar. |
| `Column` | Menampilkan widget-child secara vertikal. |
| `GridView.count` | Menampilkan item dalam bentuk grid. Mengatur tata letak grid dengan baris dan kolom. |
| `ShopCard` | Custom widget yang menampilkan setiap item dalam grid, termasuk ikon dan teks. |
| `Material` | Memberikan warna latar belakang dan efek responsif saat item di-klik. |
| `InkWell` | Membuat area yang responsif terhadap sentuhan, mendeteksi tindakan seperti ketika item di-klik. |
| `Icon` | Menampilkan ikon yang sesuai dengan setiap item dalam grid. |
| `SnackBar` | Menampilkan pesan sementara atau pemberitahuan di bagian bawah layar ketika item di-klik. |

## Implementasi Tugas
### Membuat Program Flutter Baru
#### *Getting Started with Flutter*
Dalam langkal awal ini, saya pastikan bahwa Flutter sudah ter-*install*. Saya menyiapkan sebuah direktori baru dan menjalankan perintah berikut pada terminal untuk membuat sebuah proyek Flutter baru.
```
flutter create tikoes
cd tikoes
```

#### Merapikan Struktur Proyek
Agar kode proyek mudah dipahami, saya merapikan struktur *file* pada proyek yang dimana hal ini merupakan salah satu bentuk *best practice* dalam pengembangan aplikasi.
1. Membuat file baru `menu.dart` pada `tikoes/lib` dan menambahkan kode berikut.
```dart
import 'package:flutter/material.dart';
```
2. Memindahkan `class MyHomePage ...` dari `main.dart` ke `menu.dart` dan menghapus `class _MyHomePage State ...` di `main.dart`.
3. Terakhir, menambahkan kode berikut pada `main.dart`.
```dart
import 'package:tikoes/menu.dart';
```

### Membuat Tombol Sederhana
#### Menambahkan Teks dan Card
1. Saya mendefinisikan suatu tombol dalam *class* baru seperti berikut ini.
```dart
class AlbumItem {
  final String name;
  final IconData icon;

  AlbumItem(this.name, this.icon);
}
```
2. Pada `menu.dart`, saya menambahkan kode berikut ini dibawah `MyHomePage({Key? key}) : super(key: key);` untuk menambahkan tombol-tombol sederhana.
```dart
final List<AlbumItem> items = [
    AlbumItem("Lihat Item", Icons.checklist),
    AlbumItem("Tambah Item", Icons.add_box_outlined),
    AlbumItem("Logout", Icons.logout),
];
```
3. Saya membuat *class* baru yaitu custom stateless widget seperti kode dibawah ini.
```dart
class AlbumCard extends StatelessWidget {
  final AlbumItem item;

  const AlbumCard(this.item, {super.key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color:Colors.orange.shade600,
      child: InkWell(
        // TODO: Tambahkan snackbar disini!
        child: Container(
          // Container untuk menyimpan Icon dan Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

#### Tampilan Halaman Utama
Untuk menampilkannya, tambahkan kode berikut ini di dalam `class MyHomePage`.
```dart
@override
Widget build(BuildContext context) {
return Scaffold(
    appBar: AppBar(
        title: const Text(
            'Tikoes',
            style: TextStyle(
                color: Colors.white,
                fontWeight: FontWeight.bold
            ),
        ),
        backgroundColor: Colors.orange.shade800,
    ),
    body: SingleChildScrollView(
        // Widget wrapper yang dapat discroll
        child: Padding(
        padding: const EdgeInsets.all(10.0), // Set padding dari halaman
        child: Column(
            // Widget untuk menampilkan children secara vertikal
            children: <Widget>[
            const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Widget Text untuk menampilkan tulisan dengan alignment center dan style yang sesuai
                child: Text(
                'Selamat datang!', // Text yang menandakan toko
                textAlign: TextAlign.center,
                style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                ),
                ),
            ),
            // Grid layout
            GridView.count(
                // Container pada card kita.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((AlbumItem item) {
                // Iterasi untuk setiap item
                return AlbumCard(item);
                }).toList(),
            ),
            ],
        ),
        ),
    ),
    );
}
```

### Memunculkan `Snackbar`
Tambahkan kode berikut ini pada `TODO: Tambahkan snackbar disini` pada `class AlbumCard ...` di `menu.dart`.
```dart
// Area responsive terhadap sentuhan
onTap: () {
    // Memunculkan SnackBar ketika diklik
    ScaffoldMessenger.of(context)
    ..hideCurrentSnackBar()
    ..showSnackBar(SnackBar(
        content: Text("Kamu telah menekan tombol ${item.name}!")));
},
```

Dengan begitu, selesai sudah pembuatan proyek Flutter baru. Saya menjalankan proyek menggunakan Google Chrome dengan perintah berikut ini.
```
flutter run -d chrome
```

## Referensi
* TOPSTECHNOLOGIES - [Mastering Stateless and Stateful Widgets in Flutter & The Best Flutter Course](https://www.tops-int.com/blog/mastering-stateless-and-stateful-widgets-in-flutter-the-best-flutter-course)
* PBP Ganjil 23/24 - [Tutorial 6: Pengantar Flutter](https://pbp-fasilkom-ui.github.io/ganjil-2024/docs/tutorial-6)
* Tim Dosen PBP - Introduction to Dart Programming Language and Flutter Framework dan Layout and Forms

</details>

<details>
<summary> <b> Tugas 8: Flutter Navigation, Layouts, Forms, and Input Elements </b> </summary>

## `Navigator.push()` dan `Navigator.pushReplacement()`
Perbedaan utama antara kedua metode ini terletak pada dampaknya terhadap *route* yang berada di atas *stack*.
* **`push()`** **menambahkan** sebuah *route* baru di atas *route* yang sudah ada di atas *stack*.

Contoh penggunaan `push()` pada tugas:
```dart
if (item.name == "Lihat Album") {
  Navigator.push(
    context, 
    MaterialPageRoute(
      builder: (context) => AlbumListPage(albums: albums,),
    ),
  );
}
```

* **`pushReplacement()`** **menggantikan** *route* yang sudah ada di atas *stack* dengan *route* baru.

Contoh penggunaan `pushReplacement()` pada tugas:
```dart
ListTile(
  leading: const Icon(Icons.home_outlined),
  title: const Text('Halaman Utama'),
  onTap: () {
    Navigator.pushReplacement(
        context,
        MaterialPageRoute(
          builder: (context) => MyHomePage(),
        ));
  },
),
```

## Widget yang Digunakan
| Widget | Fungsi | Penggunaan dalam File |
|--|--|--|
| `Drawer` | Menyediakan menu navigasi | Digunakan dalam `menu.dart` sebagai bagian dari `LeftDrawer` untuk menampilkan menu navigasi disebelah kiri layar. |
| `Form` | Mengelola formulir dan validasi input | Digunakan dalam `albumlist_form.dart` sebagai kerangka formulir untuk menambahkan album baru. |
| `GlobalKey<FormState>` | Kunci global untuk mengidentifikasi dan mengakses status formulir | Digunakan dalam `albumlist_form.dart` untuk mengelola status formulir. |
| `TextFormField` | Menyediakan area input teks | Digunakan dalam `albumlist_form.dart` untuk menerima input pengguna terkait nama, harga, dan deskripsi album. |
| `AlertDialog` | Menampilkan dialog sederhana dengan judul dan konten | Digunakan dalam `albumlist_form.dart` untuk memberikan konfirmasi bahwa album berhasil tersimpan. |
| `ElevatedButton` | Membuat tombol dengan latar belakang berwarna dan memiliki efek *elevate* | Digunakan dalam `albumlist_form.dart` sebagai tombol untuk menyimpan album baru. |


## Elemen Input pada Form
Widget yang digunakan untuk menerima input pada tugas kali ini yaitu `TextFormField`. Alasannya adalah karena `TextFormField` dapat menerima jawaban bebas sesuai pengguna ketik.
Elemen yang digunakan menggunakan widget *form* tersebut yaitu:
* Nama, untuk menerima judul album dari pengguna.
* Harga, untuk menerima harga album dari pengguna.
* Deskripsi, untuk menerima deskripsi album dari pengguna.
* Tautan Gambar, untuk menerima tautan gambar album dari pengguna.

Keempat elemen ini nantinya akan ditampilkan dibagian `Lihat Album`.

## *Clean Architecture* pada Flutter
*Clean Architecture* adalah suatu prinsip dalam pengembangan *app* yang memisahkan kepentingan dalam menciptakan kode yang modular, *scalable*, dan dapat diuji. *Clean Architecture* terdiri dari beberapa *layer*, yaitu:
* Presentation atau UI (`screens`)
Berisi komponen antarmuka pengguna, seperti widget, layar, dan tampilan dan bertanggung jawab untuk menangani interaksi pengguna dan merender antarmuka pengguna.
* Domain (`domain`)
Mengatur logika bagaimana entitas atau elemen dalam aplikasi berinteraksi dan berperilaku.
* Data (`data`)
Bertanggung jawab atas pengambilan dan penyimpanan data. 

Pada tutorial 7, kita diajarkan melakukan *refactoring file*. Menurut saya, ini merupakan penerapan *clean architecture* yaitu dengan melakukan pemisahan *layer* presentasi (`screens`).

## Implementasi Tugas
### Membuat Halaman Formulir
1. Pertama saya membuat berkas baru `albumlist_form.dart` di dalam folder `lib/screens`.
2. Tambahkan kode berikut pada berkas tersebut.
```dart
import 'package:flutter/material.dart';
import 'package:tikoes/widgets/left_drawer.dart';
import 'package:tikoes/data/album_model.dart';

class AlbumFormPage extends StatefulWidget {
    const AlbumFormPage({super.key});

    @override
    State<AlbumFormPage> createState() => _AlbumFormPageState();
}

class _AlbumFormPageState extends State<AlbumFormPage> {
  final _formKey      = GlobalKey<FormState>();   // Handler dari form state, validasi form, dan penyimpanan form
  String _name        = "";
  int    _price       = 0;
  String _description = "";
  String _image       = "";
  @override
  Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          // ...
        ),
        /*
        <!>--- Tambahkan drawer disini ---<!>
        */
        body: Form(     // Wadah untuk beberapa input field widget
          key: _formKey,
          child: SingleChildScrollView(     // Membuat child widget yang dapat di scroll
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: TextFormField(
                    decoration: InputDecoration(
                      hintText: "Nama Album",
                      labelText: "Nama Album",
                      border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(5.0),
                      ),
                    ),
                    onChanged: (String? value) {
                      setState(() {
                        _name = value!;
                      });
                    },
                    /* 
                    Validasi untuk input tidak boleh kosong dan harus 
                    berisi tipe data yang sesuai dengan variabel model
                    */
                    validator: (String? value) {
                      if (value == null || value.isEmpty) {
                        return "Nama tidak boleh kosong!";
                      }
                      return null;
                    },
                  ),
                ),
                /*
                ...
                Input harga, deskripsi, dan tautan gambar
                ...
                */                
                Align(      // Tombol Save
                  alignment: Alignment.bottomCenter,
                  child: Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: ElevatedButton(
                      style: ButtonStyle(
                        backgroundColor:
                            MaterialStateProperty.all(Colors.orange),
                      ),
                      onPressed: () {
                        if (_formKey.currentState!.validate()) {
                          albums.add(Album(_name, _price, _description, _image));
                          // Pop-up jika tombol Save ditekan dan input valid
                          showDialog(
                            context: context,
                            builder: (context) {
                              return AlertDialog(
                                title: const Text('Album berhasil tersimpan'),
                                content: SingleChildScrollView(
                                  child: Column(
                                    crossAxisAlignment:
                                        CrossAxisAlignment.start,
                                    children: [
                                      Text('Nama: $_name'),
                                      Text('Harga: $_price'),
                                      Text('Deskripsi: $_description')
                                    ],
                                  ),
                                ),
                                actions: [
                                  TextButton(
                                    child: const Text('OK'),
                                    onPressed: () {
                                      Navigator.pop(context);
                                    },
                                  ),
                                ],
                              );
                            },
                          );
                          _formKey.currentState!.reset();
                        }
                      },
                      child: const Text(
                        "Save",
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                  ),
                ),
              ]
            ),
          ),
        ),
      );
  }
}
```
3. Terakhir, jangan lupa untuk mengarahkan pengguna ke halaman form ketika menekan tombol `Tambah Album` pada halaman utama. Saya menambahkan kode berikut ini pada fungsi `onTap()` di berkas `lib/widgets/album_card.dart`.
```dart
...
else if (item.name == "Tambah Album") {
  // Melakukan navigasi ke MaterialPageRoute yang mencakup AlbumFormPage.
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => const AlbumFormPage(),
    ),
  );
}
...
```

### Menambahkan Drawer
1. Saya membuat berkas baru `left_drawer.dart` pada folder `lib/widgets`.
2. Tambahkan kode dibawah ini.
```dart
import 'package:flutter/material.dart';
import 'package:tikoes/screens/menu.dart';
import 'package:tikoes/screens/albumlist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.orange,
            ),
            child: Column(
              children: [
                Text(
                  'Tikoes',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text("Catat seluruh albumu di sini!",
                  style: TextStyle(
                    fontSize: 15,
                    color: Colors.white,
                    fontWeight: FontWeight.w100,
                  ),
                  textAlign: TextAlign.center,
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_box_outlined),
            title: const Text('Tambah Produk'),
            // Bagian redirection ke AlbumFormPage
            onTap: () {
              Navigator.pushReplacement(
                context, 
                MaterialPageRoute(builder: (context) => const AlbumFormPage())
              );
            },
          ),
        ],
      ),
    );
  }
}
```

## Referensi
* PBP Ganjil 23/24 - [Tutorial 7: Flutter Navigation, Layouts, Forms, and Input Elements](https://pbp-fasilkom-ui.github.io/ganjil-2024/docs/tutorial-7)
* Tim Dosen PBP - Navigation, Networking, and Integration
* Samra Khan - [Flutter — Clean Architecture](https://medium.com/@samra.sajjad0001/flutter-clean-architecture-5de5e9b8d093)

</details>

# Tugas 9: Integrasi Layanan Web Django dengan Aplikasi Flutter

## Pengambilan Data JSON Tanpa Model
**Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu?**
Ya bisa, kita dapat mengakalinya dengan menggunakan sebuah variabel yang menyimpan sebuah *dictionary* berisi data.

**Apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?**
Tidak, justru model mempermudah kita dalam melakukan pengambilan data karena dengan model kita dapat memastikan suatu objek memiliki semua nilai atribut pada kelas dibanding dengan *dictionary* yang bisa saja kita melewatkan suatu atribut.

## `CookieRequest`
Salah satu *class* pada *package* `pbp_django_auth.dart`.
### Fungsi
Dilihat dari isi *class*-nya, menurut saya, fungsi dari *class* `CookieRequest` ini yaitu:
* Menyediakan fungsi untuk inisialisasi sesi, login, dan logout yang memungkinkan aplikasi untuk melacak status login dan sesi pengguna.
* Cookies berupa informasi sesi tersebut disimpan secara lokal.
* Melakukan permintaan HTTP dengan metode GET dan POST.
### `CookieRequest` pada Semua Komponen Aplikasi
`CookieRequest` perlu dibagikan ke semua komponen di aplikasi Flutter agar status login atau sesi (cookies) **konsisten**. Jadi, jika status login atau sesi diubah dalam suatu komponen atau aplikasi, maka di komponen atau aplikasi lain akan berubah juga.

## Mekanisme Pengambilan Data JSON
Berikut adalah mekanisme pengambilan data dari JSON.
1. **Membuat model kustom**
Manfaatkan website [Quicktype](http://app.quicktype.io/) untuk membuat data JSON yang didapat dari *endpoint* `/json` pada tugas Django.
2. **Menambahkan dependensi HTTP**
Pada proyek Flutter, tambahkan dependensi `http` dan tambahkan kode `<uses-permission android:name="android.permission.INTERNET" />` pada `android/app/src/main/AndroidManifest.xml` untuk memperbolehkan akses internet.
3. **Melakukan Fetch Data**
Pada salah satu *file* `lib/screens` yang ingin melakukan *fetch* data, implementasi fungsi asinkronus dan mengirim permintaan HTTP. Contoh pada tugas kali ini yaitu:
```dart
// Pada album_list.dart
Future<List<Album>> fetchAlbum() async {
  var url = Uri.parse(
      'https://akmal-ramadhan21.pbp.cs.ui.ac.id/get-item/');
  var response = await http.get(
      url,
      headers: {"Content-Type": "application/json"},
  );

  // Melakukan decode response menjadi bentuk json
  var data = jsonDecode(utf8.decode(response.bodyBytes));

  // Melakukan konversi data json menjadi object Album
  List<Album> list_album = [];
  for (var d in data) {
      if (d != null) {
          list_album.add(Album.fromJson(d));
      }
  }
  return list_album;
}
```
4. **Menampilkan Data**
Pada tugas ini, saya menampilkan data menggunakan widget `FutureBuilder` yang dimonitori nilai `future:`. Jadi, ketika fungsi `fetchAlbum()` dipanggil dan sudah selesai melakukan proses, maka `snapshot` akan berisi `list_ablbum` yang di-*return* pada fungsi tersebut. Setelah itu, `snapshot.data` ini akan diolah untuk ditampilkan pada `ListView.builder`.

## Autentikasi
Mekanisme autentikasi pengguna dijelaskan sebagai berikut.
1. Pengguna **memasukkan data akun** yaitu `username` dan `password` pada laman `LoginPage`.
2. Tombol *login* ditekan dan fungsi `login` pada `CookieRequest` terpanggil yang **mengirimkan HTTP *request*** dengan *endpoint* URL proyek Django.
3. Pada Django, **dilakukan autentikasi** seperti `user = authenticate(username=username, password=password)` pada `views.py` milik `authentication`.
4. Setelah itu dicek, **apakah `user is not None` dan `user.is_active:`**?
5. Kembali ke Flutter, jika `request.loggedIn`, **pengguna diarahkan ke `MyHomePage`** dan muncul tampilan selamat datang menggunakan `SnackBar`.

## Widget yang Digunakan
| Widget | Fungsi | Penjelasan Implementasi |
| --| -- | -- |
| `TextField` | Memungkinkan pengguna memasukkan teks | Digunakan untuk memasukkan nama pengguna dan kata sandi. |
| `FutureBuilder` | Membangun widget secara asinkron | Mengelola status loading, error, dan data yang tersedia. |
| `ListView.builder` | Membuat daftar yang dapat discroll  | Menampilkan daftar album yang diambil |
| `Column` | Menyusun komponen secara vertikal | Menyusun secara vertikal detail album, seperti nama, jumlah, dan deskripsi. |
| `SizedBox` | Menambahkan ruang vertikal | Menambahkan ruang di antara berbagai informasi tentang album. |

## Implementasi Tugas
### Membuat Halaman Login dan Mengintegrasikan Sistem Autentikasi Django
Berikut adalah mekanisme saya dalam membuat halaman login.
1. **Siapkan Django App untuk melakukan integrasi autentikasi**
Saya membuat aplikasi `authentication` dan juga meng-*install* *library* `corsheaders`.
2. **Fungsi `login` pada `views.py`** 
Pada aplikasi Django tersebut, saya membuat sebuah fungsi `login` pada `views.py` untuk menangani proses autentikasi login.
3. **Menggunakan *package* `pbp_django_auth`**
Install *package* `pbp_django_auth` dan modifikasi *root* widget untuk menyediakan *instance* `CookieRequest`dengan semua komponen pada proyek di dalam *file* `main.dart`
4. **Membuat `login.dart`**
Buat berkas baru `lib/screens/login.dart` dan isilah kode untuk menampilkan halaman *login* seperti yang sudah diajarkan di Tutorial 8.

### Membuat Model Kustom
Sudah dijelaskan di **Mekanisme Pengambilan Data JSON**. Hasil dari kode tersebut ditulis pada *file* `lib/models/album.dart`.

### Membuat Halaman Daftar Album
Daftar album ditampilkan pada file `lib/screens/album_list.dart` dimana pengambilan datanya sudah dijelaskan di **Mekanisme Pengambilan Data JSON**. Isi dari kode `album_list.dart` mirip dengan Tutorial 8 dengan beberapa perubahan (*routing* dengan halaman detail).

### Membuat Halaman Detail Album
Ketika salah satu album diklik di daftar album, maka pengguna akan diarahkan ke halaman detail pada album tersebut.
Berikut adalah *routing* dari halaman daftar album ke detail album pada `album_list.dart`.
```dart
onTap: () {
  Navigator.push(
    context,
    MaterialPageRoute(
      builder: (context) => AlbumDetailPage(album: snapshot.data![index]),
    ),
  );
},
```
Saya membuat *file* `album_detail.dart` dan berikut adalah kode saya.
```dart
class AlbumDetailPage extends StatelessWidget {
  final Album album;

  const AlbumDetailPage({Key? key, required this.album}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        ...
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          ...
          children: [
            Text(
              'Name: ${album.fields.name}',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 10),
            Text('Amount: ${album.fields.amount}'),
            SizedBox(height: 10),
            Text('Description: ${album.fields.description}'),
          ],
        ),
      ),
    );
  }
}
```

## Referensi
* PBP Ganjil 23/24 - [Tutorial 8: Flutter Networking, Authentication, and Integration](https://pbp-fasilkom-ui.github.io/ganjil-2024/docs/tutorial-8)
* Tim Dosen PBP - Navigation, Networking, and Integration