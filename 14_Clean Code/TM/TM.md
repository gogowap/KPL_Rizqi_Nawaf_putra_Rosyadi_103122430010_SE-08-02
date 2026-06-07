**Nama:** Rizqi Nawaf Putra Rosyadi

**NIM:** 103122430010

**Kelas:** SE-08-02

## Soal
Dari dua kode di bawah ini, mana yang kamu ingin cari masalahnya dan perbaiki di tengah-tengah malam, katakanlah jam 1 malam? Mengapa?
```
function processUser(user) {
  if (user) {
    if (user.isActive) {
      if (user.hasPermission) {
        return doSomething(user)
      }
    }
  }
  return null
}
```
```
function processUser(user) {
  if (!isValidCandidate(user)) return null;
  return doSomething(user);
}

function isValidCandidate(user) {
  return user && user.isActive && user.hasPermission;
}
```
## Deskripsi
Kode 1 (nested & kompleks)
```
function processUser(user) {
  if (user) {
    if (user.isActive) {
      if (user.hasPermission) {
        return doSomething(user)
      }
    }
  }
  return null
}
```
Kode 2 (clean & readable)
```
function processUser(user) {
  if (!isValidCandidate(user)) return null;
  return doSomething(user);
}

function isValidCandidate(user) {
  return user && user.isActive && user.hasPermission;
}
```

Saya akan memilih Kode 2 untuk diperbaiki atau dipelihara di tengah malam (jam 1 malam), karena lebih sesuai dengan prinsip Clean Code.
1. Lebih mudah dibaca (readability tinggi)
Kode 2:
```
if (!isValidCandidate(user)) return null;
``
langsung jelas alurnya tidak perlu membaca nested if satu per satu.
Sedangkan Kode 1 terlalu banyak level indentasi, harus “menelusuri” kondisi bertingkat

2. Kompleksitas rendah
Kode 1 memiliki 3 tingkat nested if, alur eksekusi sulit diprediksi cepat
Kode 2 hanya 1 kondisi utama, logika dipisahkan ke fungsi lain

3. Reusability (bisa dipakai ulang)
```
function isValidCandidate(user)
```
bisa digunakan di tempat lain, tidak mengulang logika validasi

4. Single Responsibility Principle
Kode 2 memisahkan tugas:
processUser() - mengatur proses utama
isValidCandidate() - validasi user
Sedangkan Kode 1 semua logika bercampur dalam satu fungsi

5. Lebih aman untuk debugging malam hari
Saat kondisi darurat:
Kode 1 butuh waktu lama untuk memahami bug
Kode 2 langsung tahu masalah di fungsi validasi

6. Mengurangi risiko error
Nested if seperti ini:
```
if (user) {
  if (user.isActive) {
    if (user.hasPermission)
```

Berpotensi:
1. lupa kondisi null
2. salah blok logika
3. sulit modifikasi tanpa merusak flow