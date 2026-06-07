**Nama:** Rizqi Nawaf Putra Rosyadi

**NIM:** 103122430010

**Kelas:** SE-08-02

## Soal
Bukalah repostori kode tugas besarmu dan carilah satu saja design pattern yang digunakan di dalamnya (boleh design pattern apa saja, akan direviu kasus-per-kasus). Sertakan kodenya di tugas ini dan coba jelaskan desainnya.

## Program/Kode
Program Tersedia di [Database.js](Database.js)

## Deskripsi
Singleton Pattern adalah design pattern yang memastikan bahwa sebuah kelas hanya memiliki 1 instance (objek) saja selama program berjalan.
Biasanya digunakan untuk:
1. koneksi database
2. konfigurasi aplikasi
3. logging system
4. cache global

Pada proyek tugas besar ini, saya menggunakan (Node.js/TypeScript backend), Singleton paling umum digunakan pada:
Database Connection (Koneksi DB)
Tujuannya:
1. Menghindari koneksi database dibuat berulang-ulang
2. Menghemat resource
3. Memastikan semua modul memakai koneksi yang sama

Contoh Kode Singleton (Database Connection)
```
class Database {
  static instance;

  constructor() {
    if (Database.instance) {
      return Database.instance;
    }

    this.connection = this.connect();
    Database.instance = this;
  }

  connect() {
    console.log("Membuat koneksi database...");
    return {
      status: "connected",
      time: new Date()
    };
  }

  getConnection() {
    return this.connection;
  }
}

// Pemakaian
const db1 = new Database();
const db2 = new Database();

console.log(db1 === db2); 
// true (hanya 1 instance)

console.log(db1.getConnection());
console.log(db2.getConnection());
```

Cara Kerja Design Pattern Ini
1. Saat new Database() dipanggil pertama kali:
    objek dibuat
    koneksi database dibuat
2. Saat new Database() dipanggil lagi:
    tidak membuat objek baru
    hanya mengembalikan instance lama

Alasan Menggunakan Singleton

1. Menghindari multiple connection ke database
2. Lebih hemat memori dan resource server
3. Menjaga konsistensi data
4. Cocok untuk backend sistem perpustakaan