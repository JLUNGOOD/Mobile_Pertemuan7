# Pertemuan_7

Nama : Alwan Alawi

Kelas : TI-3A

Absen : 09


# Praktikum 1: Membangun Layout di Flutter

### Langkah 1: Buat Project Baru
Buatlah sebuah project flutter baru dengan nama layout_flutter. Atau sesuaikan style laporan praktikum yang Anda buat.

### Langkah 2: Buka file lib/main.dart
Buka file main.dart lalu ganti dengan kode berikut. Isi nama dan NIM Anda di text title.
```
import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter layout: Alwan Alawi 2141720178',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Flutter layout demo'),
        ),
        body: const Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}

```
### Langkah 3: Identifikasi layout diagram
Langkah pertama adalah memecah tata letak menjadi elemen dasarnya:

- Identifikasi baris dan kolom.
- Apakah tata letaknya menyertakan kisi-kisi (grid)?
- Apakah ada elemen yang tumpang tindih?
- Apakah UI memerlukan tab?
- Perhatikan area yang memerlukan alignment, padding, atau borders.
  
### Langkah 4: Implementasi title row
Pertama, Anda akan membuat kolom bagian kiri pada judul. Tambahkan kode berikut di bagian atas metode build() di dalam kelas MyApp:
```
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter layout: Alwan Alawi 2141720178',
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Flutter layout demo'),
        ),
        body: ListView(
          children: [
            buildTitleSection(),
          ],
        ),
      ),
    );
  }

  Widget buildTitleSection() {
    return Container(
      padding: const EdgeInsets.all(16.0),
      child: Row(
        children: [
          Expanded(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Container(
                  padding: const EdgeInsets.only(bottom: 8.0),
                  child: const Text(
                    'Telaga Sarangan',
                    style: TextStyle(
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                ),
                Text(
                  'Magetan, Jawa Timur, Indonesia',
                  style: TextStyle(
                    color: Colors.grey[500],
                  ),
                ),
              ],
            ),
          ),
          Icon(
            Icons.star,
            color: Colors.purple[500],
          ),
          const Text('41'),
        ],
      ),
    );
  }
}

```
Output:

![image](https://github.com/JLUNGOOD/Mobile_Pertemuan7/assets/106043734/f74bd71a-ae0a-48e1-97b2-6e318e8f200a)

# Praktikum 2: Implementasi button row

### Langkah 1: Buat method Column _buildButtonColumn
Bagian tombol berisi 3 kolom yang menggunakan tata letak yang sama—sebuah ikon di atas baris teks. Kolom pada baris ini diberi jarak yang sama, dan teks serta ikon diberi warna primer.

Karena kode untuk membangun setiap kolom hampir sama, buatlah metode pembantu pribadi bernama buildButtonColumn(), yang mempunyai parameter warna, Icon dan Text, sehingga dapat mengembalikan kolom dengan widgetnya sesuai dengan warna tertentu.
```
Column _buildButtonColumn(Color color, IconData icon, String label) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(icon, color: color),
        Container(
          margin: const EdgeInsets.only(top: 8),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12,
              fontWeight: FontWeight.w400,
              color: color,
            ),
          ),
        ),
      ],
    );

```

### Langkah 2: Buat widget buttonSection
Buat Fungsi untuk menambahkan ikon langsung ke kolom. Teks berada di dalam Container dengan margin hanya di bagian atas, yang memisahkan teks dari ikon.

Bangun baris yang berisi kolom-kolom ini dengan memanggil fungsi dan set warna, Icon, dan teks khusus melalui parameter ke kolom tersebut. Sejajarkan kolom di sepanjang sumbu utama menggunakan MainAxisAlignment.spaceEvenly untuk mengatur ruang kosong secara merata sebelum, di antara, dan setelah setiap kolom. Tambahkan kode berikut tepat di bawah deklarasi titleSection di dalam metode build():
```
Widget buildButtonSection(Color color) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        _buildButtonColumn(color, Icons.call, 'CALL'),
        _buildButtonColumn(color, Icons.near_me, 'ROUTE'),
        _buildButtonColumn(color, Icons.share, 'SHARE'),
      ],
    );
  }
```
### Langkah 3: Tambah button section ke body
Tambahkan variabel buttonSection ke dalam body seperti berikut:
```
body: ListView(
          children: [
            buildTitleSection(),
            buildButtonSection(color)
          ],
```

Output:

![image](https://github.com/JLUNGOOD/Mobile_Pertemuan7/assets/106043734/1e493c51-a775-4855-b0e8-9a9408ae5d20)

# Praktikum 3: Implementasi text section

### Langkah 1: Buat widget textSection
Tentukan bagian teks sebagai variabel. Masukkan teks ke dalam Container dan tambahkan padding di sepanjang setiap tepinya. Tambahkan kode berikut tepat di bawah deklarasi buttonSection:
```
Widget buildTextSection() {
    return Container(
      padding: const EdgeInsets.all(32),
      child: const Text(
        'Telaga Sarangan, juga dikenal sebagai Telaga Pasir adalah telaga alami yang berada di ketinggian 1.200 meter di atas permukaan laut'
        'dan terletak di lereng Gunung Lawu,Kecamatan Plaosan, Kabupaten Magetan, Jawa Timur.Telaga ini berjarak sekitar 16 kilometer arah barat Kota Magetan.' 
        'Telaga ini luasnya sekitar 30 hektare dan berkedalaman 28 meter.Dengan suhu udara antara 15 hingga 20 derajat Celsius.'
        'Telaga Sarangan mampu menarik ratusan ribu pengunjung setiap tahunnya. Telaga Sarangan adalah objek wisata andalan Kabupaten Magetan' 
        'Di sekeliling telaga terdapat dua hotel berbintang, 43 hotel kelas melati, dan 18 pondok wisata.Di samping puluhan kios cendera mata,'
        'pengunjung dapat pula menikmati indahnya Sarangan dengan berkuda mengitari telaga,atau mengendarai kapal cepat.Fasilitas objek wisata lainnya'
        'pun tersedia,misalnya rumah makan, tempat bermain,pasar wisata,tempat parkir,tempat ibadah,dan taman.',
        softWrap: true,
      ),
    );
  }
```
Dengan memberi nilai softWrap = true, baris teks akan memenuhi lebar kolom sebelum membungkusnya pada batas kata.

### Langkah 2: Tambahkan variabel text section ke body
Tambahkan widget variabel textSection ke dalam body seperti berikut:
```
body: ListView(
          children: [
            buildTitleSection(),
            buildButtonSection(color),
            buildTextSection()
          ],
```

Output:

![image](https://github.com/JLUNGOOD/Mobile_Pertemuan7/assets/106043734/d960df52-ad69-4883-b397-4ee5be3b638f)


# Praktikum 4: Implementasi image section
### Langkah 1: Siapkan aset gambar
Anda dapat mencari gambar di internet yang ingin ditampilkan. Buatlah folder images di root project layout_flutter. Masukkan file gambar tersebut ke folder images, lalu set nama file tersebut ke file pubspec.yaml seperti berikut:
```
flutter:
  assets:
    - sarangan.jpeg
```
### Langkah 2: Tambahkan gambar ke body
Tambahkan aset gambar ke dalam body seperti berikut:
```
children: [
              Image.asset(
              'images/sarangan.jpeg',
              width: 600,
              height: 300,
              fit: BoxFit.cover,
            ),
```

BoxFit.cover memberi tahu kerangka kerja bahwa gambar harus sekecil mungkin tetapi menutupi seluruh kotak rendernya.

### Langkah 3: Terakhir, ubah menjadi ListView
Pada langkah terakhir ini, atur semua elemen dalam ListView, bukan Column, karena ListView mendukung scroll yang dinamis saat aplikasi dijalankan pada perangkat yang resolusinya lebih kecil.
```
 body: ListView(
          children: [
              Image.asset(
```

Output:

![image](https://github.com/JLUNGOOD/Mobile_Pertemuan7/assets/106043734/06f0ba84-db91-43da-8eed-012e6fbcb222)


