**Nama:** Rizqi Nawaf Putra Rosyadi

**NIM:** 103122430010

**Kelas:** SE-08-02

## Soal
Jelaskan dengan kemampuanmu apa itu event delegation dalam design pattern JavaScript. Tidak ada batas bobot kata dalam menjawab tugas ini, tetapi penilaian akan bergantung dari sepaham apa dan sebagus apa kamu menyajikan jawabanmu.

## Deskripsi
Event Delegation adalah teknik dalam JavaScript di mana kita hanya memasang satu event listener pada parent element, lalu parent tersebut yang akan menangani event dari child-element di dalamnya menggunakan mekanisme event bubbling.

Konsep Dasar
Di DOM (Document Object Model), ketika sebuah event terjadi pada elemen kecil (child), event tersebut akan naik ke atas (bubble) menuju parent, grandparent, hingga document Nah, event delegation memanfaatkan hal ini.

Ilustrasi Sederhana
Misalnya kita punya HTML:
```
<ul id="list">
  <li>Buku</li>
  <li>Pensil</li>
  <li>Penghapus</li>
</ul>
```
Cara lama (tidak efisien)
```
document.querySelectorAll("li").forEach(item => {
  item.addEventListener("click", () => {
    console.log("Item diklik");
  });
});
```

Event Delegation (cara benar):
```
js
document.getElementById("list").addEventListener("click", function(event) {
  if (event.target.tagName === "LI") {
    console.log("Item diklik:", event.target.textContent);
  }
});
```
Cara Kerja Event Delegation
1. Event terjadi di <li>
2. Event naik ke <ul> (parent)
3. Parent menangkap event melalui listener
4. Parent mengecek:
5. siapa target sebenarnya (event.target)
6. Parent menjalankan logic sesuai target

Kenapa ini termasuk Design Pattern?
Event delegation dianggap design pattern karena:
1. Menggunakan strategi pengelolaan event
2. Mengurangi duplikasi kode
3. Mengoptimalkan performa aplikasi
4. Memisahkan tanggung jawab (child tidak perlu handler sendiri)

Kelebihan Event Delegation
1. Lebih efisien
    hanya 1 event listener untuk banyak elemen
2. Cocok untuk elemen dinamis
    elemen baru otomatis ikut “ter-handle”
3. Lebih hemat memori
    tidak membuat banyak listener
4. Lebih mudah maintenance
    logic event terpusat di parent

Kekurangan
1. Harus selalu cek event.target
2. Bisa membingungkan jika struktur DOM kompleks
4. Tidak cocok untuk event yang tidak bubbling (misalnya focus)

Contoh di dunia nyata
Event delegation sering dipakai pada:
1. tombol delete/edit di tabel data
2. list chat / komentar
3. menu dinamis
4. sistem e-commerce (keranjang belanja)

Kesimpulan
Event delegation adalah teknik penting dalam JavaScript yang memanfaatkan event bubbling untuk menangani banyak event melalui satu parent listener, yang membuat kode:
1. lebih ringan
2. lebih scalable
3. lebih mudah dikelola
