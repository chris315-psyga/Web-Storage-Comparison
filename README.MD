Nama : Chris Maruli Siagian
NIM : 2481004

**Eksperimen 1: Persistence Test**
1.	Simpan data dengan Key: testPersist, Value: hello
2.	Tutup browser sepenuhnya (bukan hanya tab)
3.	Buka kembali halaman
4.	Catat: 
o	Cookies: [masih ada / hilang] = Masih ada
o	LocalStorage: [masih ada / hilang] = Masih ada
o	SessionStorage: [masih ada / hilang] = hilang

**Eksperimen 2: Tab Isolation**
1.	Klik "Increment" 5 kali pada Tab Counter
2.	Buka halaman ini di tab baru (copy URL, paste di tab baru)
3.	Catat: Berapa nilai counter di tab baru? = 0
4.	Increment di tab baru 3 kali
5.	Kembali ke tab lama
6.	Catat: Berapa nilai counter di tab lama? = 5
Kesimpulan: SessionStorage adalah tab isolated (tab-shared / tab-isolated)

**Eksperimen 3: Storage Size Comparison**
1.	Buka DevTools > Application > Storage
2.	Lihat quota yang tersedia untuk: 
o	Cookies: 16 KB
o	LocalStorage: 8.00 MB
o	SessionStorage: 8.00 MB

**Eksperimen 4: Decision Quiz**
Selesaikan semua 4 skenario di bagian "Decision Helper" dan catat alasan untuk setiap jawaban.

Skenario 1: User Theme Preference     
User memilih dark mode. Preferensi harus persist.
jawaban
LocalStorage
Benar! LocalStorage cocok untuk preferensi yang harus persist dan tidak perlu dikirim ke server.

Skenario 2: Multi-step Form (Wizard)              
Data form yang hilang jika user tutup tab.
jawaban 
SessionStorage
Benar! SessionStorage perfect untuk data form sementara yang harus hilang saat tab ditutup.

Skenario 3: Session Authentication Token        
Token yang harus dikirim ke server dan dilindungi dari XSS.
jawaban
Cookies(HttpOnly)
Benar! Cookies dengan HttpOnly adalah satu-satunya yang bisa melindungi token dari XSS dan dikirim ke server.

Skenario 4: Shopping Cart (tanpa login)        
Cart yang persist meski browser ditutup, tidak perlu ke server.
jawaban
Benar! LocalStorage cocok untuk shopping cart yang persist tanpa perlu ke server.


**Pertanyaan Refleksi** 
1. **Mengapa session token TIDAK boleh disimpan di LocalStorage?** 
Hal itu dikarenakan localStorage itu bisa diakses oleh JavaScript. Kalau misalnya terjadi serangan XSS maka attacker dapat membaca token tersebut dan menggunakannya untuk mengambil alih sesi pengguna (session hijacking) dan akhirnya tamatlah riwayat pengguna tersebut. Selain itu, data di localStorage itu bersifat persisten dan tidak otomatis kadaluarsa sehingga risikonya lebih besar jika tokennya bocor.

2. **Apa keuntungan SessionStorage untuk multi-step form dibanding LocalStorage?** 
Keuntungannya adalah ruang lingkupnya hanya satu tab dan satu sesi. Jika tapnya ditutup maka data akan otomatis terhapus sehingga ini cocok untuk multi-step form yang datanya hanya relevan selama proses pengisian berlangsung. Hal ini berguna untuk mencegah terjadinya data form yang lama muncul kembali saat user membuka situs di lain waktu.

3. **Jika kamu membuat aplikasi todo list offline-first, storage mana yang akan kamu gunakan dan mengapa?**
Storage yang paling tepat adalah LocalStorage. karena data todo itu harus tetap tersedia meskipun browser ditutup, perangkat offline, atau user membuka ulang aplikasi di lain waktu. Kan nggak lucu ya Kalau misalnya sudah capek capek mengetik panjang lebar kali tinggi kayak buat Novel lalu kemudian waktu keluar dari aplikasi dan saat aplikasinya dibuka kembali dan membuka kembali listnya seketika semua tulisan tersebut hilang tanpa kabar bagaikan ditelan bumi. LocalStorage juga mudah digunakan, cukup untuk menyimpan data sederhana kayak daftar tugas kuliah yang banyaknya bikin kami stress 7 galaksi, dan tidak memerlukan koneksi ke server.