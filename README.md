Regita Maulia Gani
H1D022021
Shift C

# Cara Kerja Login

## Persiapan Koneksi Database
Membuat file koneksi.php, untuk membuat koneksi ke database MySQL yang berisi tabel user dengan field username dan password.

## Penerimaan dan Pemrosesan Data Login
Pada file login.php, data yang diterima dari request login berupa username dan password dalam format JSON. Lalu, password yang diterima akan di-hash dengan MD5 dan dicocokkan dengan data yang ada di database.

## Validasi Login di API
Jika data username dan password yang dikirimkan sesuai dengan data di database, maka API mengembalikan response JSON dengan status_login sebagai "berhasil", bersama username dan token unik. Jika data tidak sesuai, API mengembalikan status_login sebagai "gagal".

## Mengirim Permintaan Login dari Ionic
Pada halaman login, saat pengguna mengklik tombol login, data username dan password dikirim ke API login.php menggunakan method post yang ada di authentication.service.ts.

## Penyimpanan Data Login
Jika API merespon status_login "berhasil", maka AuthenticationService menyimpan token dan username ke dalam penyimpanan lokal (preferences) untuk status autentikasi.
Status isAuthenticated diubah menjadi true, menandakan bahwa pengguna telah berhasil login.

## Pengalihan ke Halaman Home
Setelah login berhasil, pengguna diarahkan secara otomatis ke halaman home.

## Guard untuk Melindungi Rute
Guard authGuard memeriksa status login (isAuthenticated) saat pengguna mencoba mengakses halaman yang membutuhkan login, di sini halaman home.
Jika pengguna belum login, authGuard akan mengalihkan pengguna kembali ke halaman login.

## Auto-login Guard
Guard autoLoginGuard mencegah pengguna yang sudah login untuk kembali ke halaman login.
Jika pengguna yang sudah login mencoba mengakses halaman login, autoLoginGuard akan mengalihkan mereka langsung ke halaman home.

## Logout
Pada saat logout, AuthenticationService menghapus data token dan username dari penyimpanan lokal dan mengubah isAuthenticated menjadi false.
