# Training-IoT-Sample

Repository ini berisi tugas proyek IoT untuk pelatihan di **SMAN Negeri 1 Soreagan**, menggunakan mikrokontroler **Arduino Uno**. Proyek ini berfokus pada pembuatan sistem dengan memanfaatkan berbagai jenis sensor untuk tujuan deteksi dan pemantauan. Setiap sistem dibangun untuk mengembangkan pemahaman lebih lanjut tentang penerapan Internet of Things (IoT).

### Dibuat oleh:
**Aliza Nurfitrian Meizahra**

---

## Deskripsi Proyek

Proyek ini mencakup tiga sistem IoT yang memanfaatkan **Arduino Uno** dan berbagai sensor untuk memantau kondisi lingkungan sekitar dan memberikan respons otomatis berdasarkan deteksi dari sensor yang digunakan.

---

## Jenis-Jenis Sistem dan Sensor yang Digunakan

### 1. Sistem Pendeteksi Gas Bocor
   - **Sensor yang Digunakan**:
     - **Sensor Gas MQ-2**: Untuk mendeteksi kebocoran gas berbahaya seperti metana, propana, dan gas lainnya.
     - **Sensor Suhu DHT22**: Untuk memantau suhu dan kelembapan di sekitar sensor gas.
     - **Buzzer**: Untuk memberi peringatan suara saat gas bocor terdeteksi.
     - **LCD 20x4**: Menampilkan status deteksi gas dan suhu di lingkungan sekitar.

   - **Fungsi**:
     Sistem ini memantau kualitas udara dan memberikan peringatan jika terdeteksi adanya gas bocor yang berbahaya. LCD akan menampilkan informasi suhu dan kelembapan, sementara buzzer akan memberikan alarm saat gas bocor terdeteksi.

---

### 2. Sistem Pendeteksi Pencuri
   - **Sensor yang Digunakan**:
     - **Sensor PIR (Passive Infrared)**: Untuk mendeteksi gerakan manusia di dalam rumah.
     - **Sensor Ultrasonik (HC-SR04)**: Untuk mengukur jarak dan mendeteksi objek yang mendekat di luar rumah.
     - **Buzzer**: Untuk memberi peringatan suara jika gerakan atau objek terlalu dekat terdeteksi.
     - **LED Hijau**: Sebagai indikator bahwa sistem aktif dan bekerja dengan baik.
     - **LCD 20x4**: Menampilkan status deteksi gerakan atau objek yang mendekat.

   - **Fungsi**:
     Sistem ini mengaktifkan alarm dan memberikan informasi visual jika ada gerakan mencurigakan yang terdeteksi oleh sensor PIR atau jika objek terlalu dekat dengan rumah yang terdeteksi oleh sensor ultrasonik.

---

### 3. Sistem Sensor Lampu Pintar
   - **Sensor yang Digunakan**:
     - **Sensor Cahaya (LDR - Light Dependent Resistor)**: Untuk mendeteksi tingkat cahaya di sekitarnya.
     - **Relay**: Untuk mengontrol lampu, menghidupkan atau mematikan lampu berdasarkan tingkat cahaya.
     - **LED**: Sebagai indikator status lampu, apakah menyala atau mati.
   
   - **Fungsi**:
     Sistem ini mengontrol lampu secara otomatis berdasarkan tingkat cahaya di sekitar sensor LDR. Jika cahaya sekitar rendah, maka lampu akan otomatis menyala, dan jika cahaya sudah cukup terang, lampu akan mati. 

---

## Instalasi dan Pengaturan

1. **Persiapan Perangkat Keras**:
   - Gunakan **Arduino Uno** sebagai mikrokontroler.
   - Pasang sensor sesuai dengan pin yang telah ditentukan di setiap proyek.

2. **Perangkat Lunak**:
   - Unduh dan instal **Arduino IDE** dari [situs resmi Arduino](https://www.arduino.cc/en/software).
   - Pastikan untuk menginstal **library** yang diperlukan, seperti:
     - `LiquidCrystal_I2C` untuk LCD I2C
     - `DHT` untuk sensor suhu dan kelembapan DHT22
     - `NewPing` untuk sensor ultrasonik
     - `Relay` untuk mengendalikan perangkat listrik

3. **Menghubungkan Arduino ke Komputer**:
   - Hubungkan Arduino ke komputer menggunakan kabel USB.
   - Pilih port yang sesuai di **Tools > Port** di Arduino IDE.

---

## Penggunaan

- Setelah semua perangkat keras terpasang dan kode dimuat ke dalam Arduino, sistem akan mulai berfungsi sesuai dengan proyek yang telah ditentukan.
- **Sistem Pendeteksi Gas Bocor** akan memberi peringatan suara dan visual jika gas berbahaya terdeteksi.
- **Sistem Pendeteksi Pencuri** akan mengaktifkan alarm jika ada gerakan yang terdeteksi di dalam rumah atau objek yang terlalu dekat.
- **Sistem Sensor Lampu Pintar** akan menghidupkan lampu secara otomatis ketika cahaya di sekitar sensor LDR rendah, dan mematikannya ketika cahaya cukup terang.

---

## Kontribusi

Jika Anda ingin berkontribusi pada proyek ini, Anda dapat:

- Menambahkan sensor atau sistem baru.
- Membantu mengoptimalkan kode.
- Menyediakan ide atau saran perbaikan untuk pengembangan lebih lanjut.

---

## Lisensi

Proyek ini dilisensikan di bawah [MIT License](LICENSE).

---

## Kontak

Jika Anda memiliki pertanyaan atau saran, Anda dapat menghubungi saya melalui email di: **alizahra2403@gmail.com**.

Anda juga dapat mengunjungi profil LinkedIn saya di: [LinkedIn - Aliza Nurfitrian Meizahra](https://www.linkedin.com/in/alizaaaja/)


---

Terima kasih telah menggunakan dan berkontribusi pada proyek ini!
