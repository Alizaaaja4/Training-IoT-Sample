# Deskripsi Tugas: Sistem Pendeteksi Pencuri 

Tugas ini bertujuan untuk membuat sistem pendeteksi pencuri yang memanfaatkan sensor PIR untuk mendeteksi gerakan di dalam rumah dan sensor ultrasonik untuk mengukur jarak objek di luar rumah. Sistem ini menggunakan **Arduino Uno**, sensor PIR, sensor ultrasonik, LCD 20x4, buzzer, dan LED. Ketika gerakan terdeteksi di dalam rumah atau objek terlalu dekat di luar rumah, sistem akan memberikan peringatan dengan mengaktifkan buzzer, menyalakan LED, dan menampilkan pesan "Pencuri terdeteksi!" pada LCD.

## Komponen yang Digunakan

- **Sensor PIR (Passive Infrared)**: Untuk mendeteksi gerakan di dalam rumah, memberikan sinyal HIGH jika ada gerakan.
- **Sensor Ultrasonik (HC-SR04)**: Untuk mengukur jarak objek di luar rumah dan mendeteksi objek yang terlalu dekat.
- **LCD 20x4 I2C**: Untuk menampilkan status deteksi gerakan dan jarak objek.
- **LED Hijau**: Sebagai indikator bahwa sistem aktif dan berfungsi.
- **Buzzer**: Untuk memberikan peringatan suara ketika gerakan atau objek terdeteksi.
- **Arduino Uno**: Sebagai mikrokontroler utama yang mengendalikan seluruh sistem.

## Library yang Digunakan

- **LiquidCrystal_I2C**: Untuk mengontrol LCD I2C.

## Langkah-Langkah Merangkai

### 1. Merangkai Sensor PIR:
   - Sambungkan pin **VCC** ke **VCC** Arduino.
   - Sambungkan pin **GND** ke **GND** Arduino.
   - Sambungkan pin **OUT** ke **Pin 2** Arduino (atau pin lain sesuai kebutuhan).

### 2. Merangkai Sensor Ultrasonik (HC-SR04):
   - Sambungkan pin **VCC** ke **VCC** Arduino.
   - Sambungkan pin **GND** ke **GND** Arduino.
   - Sambungkan pin **TRIG** ke **Pin 9** Arduino.
   - Sambungkan pin **ECHO** ke **Pin 10** Arduino.

### 3. Merangkai LCD 20x4 I2C:
   - Sambungkan pin **VCC** ke **VCC** Arduino.
   - Sambungkan pin **GND** ke **GND** Arduino.
   - Sambungkan pin **SDA** ke **Pin A4** Arduino.
   - Sambungkan pin **SCL** ke **Pin A5** Arduino.

### 4. Merangkai LED Hijau dan Buzzer:
   - Sambungkan pin panjang (anoda) LED ke **Pin 12** Arduino.
   - Sambungkan pin pendek (katoda) LED ke **GND** Arduino.
   - Sambungkan satu pin **Buzzer** ke **Pin 13** Arduino dan pin lainnya ke **GND**.

   **Catatan**: LED membutuhkan resistor untuk membatasi arus yang mengalir. Pasang resistor 220 ohm hingga 1 kΩ di antara pin anoda LED dan pin 12 Arduino.

## Penjelasan Fungsi Sistem

Sistem ini menggunakan dua sensor utama:

1. **Sensor PIR**: Untuk mendeteksi gerakan di dalam rumah. Ketika ada gerakan, sensor PIR memberikan sinyal HIGH, dan sistem akan mengaktifkan buzzer dan LED sebagai peringatan.
  
2. **Sensor Ultrasonik HC-SR04**: Mengukur jarak objek di luar rumah. Jika jarak objek lebih pendek dari ambang batas yang ditentukan (misalnya 50 cm), sistem akan mengaktifkan buzzer dan LED untuk memberikan peringatan.

Jika salah satu dari kondisi ini terdeteksi, sistem akan memberikan peringatan dengan menyalakan buzzer dan LED, serta menampilkan pesan peringatan, seperti "Pencuri terdeteksi!" di LCD.

## Sumber Daya

- **Arduino Uno**: Mikrokontroler utama yang digunakan untuk mengendalikan semua komponen dan logika program.
- **Sensor PIR**: Untuk mendeteksi gerakan yang mencurigakan di dalam rumah.
- **Sensor Ultrasonik HC-SR04**: Untuk mendeteksi objek yang terlalu dekat di luar rumah.
- **LCD 20x4 I2C**: Untuk menampilkan status sistem secara visual.
- **LED Hijau dan Buzzer**: Sebagai indikator visual dan audio untuk memberi tahu status deteksi.

## Kode Program
```cpp
#include <____>

// Inisialisasi LCD (20 kolom, 4 baris)
LiquidCrystal_I2C lcd(0x27, __, __); // Alamat I2C LCD adalah 0x27, 20 kolom, 4 baris

// Definisikan pin menggunakan #define
#define PIR_PIN __      // Pin PIR sensor untuk mendeteksi gerakan di dalam rumah
#define TRIG_PIN __     // Pin trigger ultrasonic untuk mengukur jarak di luar rumah
#define ECHO_PIN __    // Pin echo ultrasonic untuk mengukur jarak di luar rumah
#define BUZZER_PIN __  // Pin buzzer untuk memberi peringatan
#define LED_PIN __     // Pin LED biasa sebagai indikator status

void setup() {
  // Set pin mode
  pinMode(PIR_PIN, ___);  // Set PIR sensor sebagai input
  pinMode(TRIG_PIN, OUTPUT); // Set pin trigger ultrasonic sebagai output
  ____(ECHO_PIN, INPUT);  // Set pin echo ultrasonic sebagai input
  pinMode(BUZZER_PIN, OUTPUT); // Set pin buzzer sebagai output
  pinMode(LED_PIN, ___);  // Set pin LED sebagai output
  
  // Mulai komunikasi serial
  Serial.begin(9600);  // Menginisialisasi komunikasi serial dengan baud rate 9600
  
  // Inisialisasi LCD
  lcd.init();  // Untuk library yang lebih baru, inisialisasi LCD
  lcd.backlight();  // Menyalakan backlight LCD agar lebih jelas terlihat
  lcd.setCursor(0, 0);  // Set posisi kursor LCD di kolom 0, baris 0
  lcd.print("Sistem Dimulai");  // Menampilkan pesan "Sistem Dimulai" pada LCD
  delay(___);  // Tunggu selama 1 detik
}

___ loop() {
  // Baca sensor PIR untuk mendeteksi gerakan di dalam rumah
  int motion = digitalRead(PIR_PIN);  // Membaca status sensor PIR (HIGH jika ada gerakan)

  // Ukur jarak dengan ultrasonic sensor di luar rumah
  long duration, distance;
  digitalWrite(TRIG_PIN, LOW);  // Set trigger ke LOW
  delayMicroseconds(2);  // Tunggu sejenak
  digitalWrite(TRIG_PIN, HIGH); // Set trigger ke HIGH untuk mengirimkan pulsa
  delayMicroseconds(10); // Tunggu selama 10 mikrodetik
  digitalWrite(TRIG_PIN, LOW);  // Set trigger ke LOW kembali
  duration = pulseIn(ECHO_PIN, HIGH);  // Menghitung durasi pulsa yang dipantulkan
  distance = (duration / 2) / 29.1;  // Menghitung jarak berdasarkan durasi pulsa

  // Menampilkan status pada LCD
  lcd.clear();  // Membersihkan layar LCD
  lcd.____(0, 0);  // Set kursor LCD pada posisi kolom 0, baris 0
  
  // Cek kondisi deteksi gerakan dan jarak
  if (motion == HIGH || distance < 50) {  // Jika ada gerakan di dalam rumah atau objek terlalu dekat di luar rumah
    tone(BUZZER_PIN, 1000);  // Menyalakan buzzer untuk memberi peringatan (frekuensi 1000Hz)
    digitalWrite(LED_PIN, ___);  // Menyalakan LED untuk menunjukkan peringatan
    lcd.print("Pencuri terdeteksi!");  // Menampilkan pesan "Pencuri terdeteksi!" pada LCD
    lcd.setCursor(0, 1);  // Set kursor LCD pada baris kedua
    if (motion == HIGH) {
      lcd.print("Gerakan di dalam rumah!");  // Menampilkan pesan "Gerakan di dalam rumah!" pada LCD
    } else {
      lcd.print("Objek terlalu dekat!");  // Menampilkan pesan "Objek terlalu dekat!" pada LCD
    }
  } else {  // Jika tidak ada gerakan dan jarak aman
    ___(BUZZER_PIN);  // Mematikan buzzer
    digitalWrite(LED_PIN, LOW);  // Mematikan LED
    lcd.print("Sistem Aman");  // Menampilkan pesan "Sistem Aman" pada LCD
    lcd.setCursor(0, 1);  // Set kursor LCD pada baris kedua
    lcd.___("Tidak ada gerakan.");  // Menampilkan pesan "Tidak ada gerakan." pada LCD
  }

  // Delay sebelum loop berikutnya, memberikan waktu untuk pembaruan
  ___(1000);  // Tunggu selama 1 detik sebelum kembali ke awal loop
}


```
## Jawaban

- [Sistem Pendeteksi Maling]()
