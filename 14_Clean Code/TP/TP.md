**Nama:** Rizqi Nawaf Putra Rosyadi

**NIM:** 103122430010

**Kelas:** SE-08-02

## Soal
```
Sebagai konteks, fungsi di bawah ini menampilkan rincian pesanan di modal dan jika klik konfirmasi, sistem apa menyimpannya.

function fetchOrderDetails(orderId, token) {
    fetch(`https://example.com/api/order/${orderId}`, {
        headers: {
            'Authorization': token
        }
    })
    .then(response => {
        if (!response.ok) {
            throw new Error('Failed to fetch order details');
        }
        return response.json();
    })
    .then(order => {
        // Display order info
        const modal = document.getElementById('orderModal');
        const detailsDiv = modal.querySelector('#orderDetails');
        detailsDiv.innerHTML = '';

        const header = document.createElement('h3');
        header.textContent = `Order ID: ${order.id}`;
        detailsDiv.appendChild(header);

        const status = document.createElement('p');
        status.textContent = `Status: ${order.status}`;
        detailsDiv.appendChild(status);

        // Show modal
        modal.style.display = 'block';

        // Setup close button
        const closeBtn = modal.querySelector('.close');
        closeBtn.addEventListener('click', () => {
            modal.style.display = 'none';
        });

        // Setup confirm button
        const confirmBtn = modal.querySelector('#confirmOrderBtn');
        if (order.status === 'Delivered') {
            confirmBtn.style.display = 'none';
        } else {
            confirmBtn.addEventListener('click', () => {
                confirmOrder(order.id, token);
            });
        }
    })
    .catch(error => {
        console.error('Error:', error);
    });
}
```

## Program/Kode
Program Tersedia di [index.js](index.js)

## Deskripsi
Pada kode asli, fungsi fetchOrderDetails bertindak sebagai "God Function" atau fungsi yang tahu dan melakukan segalanya. Ini menyalahi prinsip utama Clean Code, yaitu Single Responsibility Principle (SRP)—sebuah fungsi seharusnya hanya memiliki satu alasan untuk berubah dan hanya melakukan satu pekerjaan dengan baik.

Berikut adalah kesalahan kode awal:
Melakukan API Fetching: Mengambil data dari server.
Melakukan Manipulasi DOM secara Masif: Membuat elemen <h3>, <p>, dan mengosongkan HTML.
Mengatur State UI: Mengubah display modal menjadi block atau none.
Mengelola Event Listener: Menempelkan fungsi klik pada tombol close dan confirm.
Jika terjadi perubahan pada struktur HTML modal, kamu terpaksa harus membongkar fungsi fetchOrderDetails yang seharusnya hanya mengurusi data API.

Penjelasan Struktur Kode Baru (Clean Code)
Untuk memperbaikinya, kode tersebut dipecah menjadi 5 fungsi spesifik yang saling bekerja sama:

1. Fungsi fetchOrderDetails (Fokus ke Data)
Tugas: Hanya mengambil data dari API menggunakan fetch.
Fungsi ini sekarang sangat pendek. Begitu data berhasil diambil, ia langsung menyerahkan tugas visual kepada fungsi renderOrderModal. Ia tidak peduli bagaimana cara data tersebut ditampilkan ke layar.

2. Fungsi renderOrderModal (Fokus ke Layout Modal)
Tugas: Menjadi penampung untuk mengatur visual modal. Ia mengosongkan detail lama, memanggil fungsi pembuat elemen, dan menampilkan modal (display = 'block').
fungsi ini seperti membaca daftar tugas (arsitektur tingkat tinggi) tanpa perlu pusing melihat detail cara pembuatan elemen HTML-nya.

3. Fungsi createOrderHeader & createOrderStatus (Fokus ke Komponen)
Tugas: Fungsi kecil yang bertugas membuat dan mengembalikan elemen HTML (<h3> dan <p>) yang sudah diisi teks.
Jika suatu saat ingin mengubah gaya tulisan (misal menambahkan class CSS seperti header.classList.add('text-bold')), saya hanya perlu mengubahnya di fungsi spesifik ini.

4. Fungsi setupModalActionButtons (Fokus ke Interaksi/Event)
Tugas: Mengatur logika tombol-tombol yang ada di dalam modal (Tombol Close dan Tombol Confirm).
Fungsi ini memisahkan logika interaksi pengguna dari logika dekorasi teks. Di sini juga ditambahkan confirmBtn.style.display = 'block' sebagai best practice untuk mengembalikan kondisi tombol jika pesanan yang dibuka berganti-ganti dari status 'Delivered' ke status lainnya.