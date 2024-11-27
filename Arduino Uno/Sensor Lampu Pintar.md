# Deskripsi Tugas: Sistem Lampu Otomatis 

Tugas ini bertujuan untuk membuat sistem lampu otomatis yang dapat mendeteksi pergerakan menggunakan sensor PIR dan mengontrol lampu di dua ruang: ruang tamu dan ruang belajar. Sistem ini menggunakan Arduino Uno, sensor PIR, dan LED untuk menandakan status lampu di masing-masing ruangan. Sistem akan mengaktifkan atau mematikan lampu berdasarkan pergerakan yang terdeteksi oleh sensor PIR.

## Komponen yang Digunakan

- **Sensor PIR**: Untuk mendeteksi pergerakan manusia.
- **LED ON (indikator perangkat aktif)**: Menunjukkan bahwa perangkat dalam keadaan aktif.
- **LED Ruang Tamu**: Menyala saat ada pergerakan di ruang tamu.
- **LED Ruang Belajar**: Menyala saat ada pergerakan di ruang belajar.
- **Arduino Uno**: Sebagai mikrokontroler utama.

## Library yang Digunakan

- `LiquidCrystal_I2C`: Untuk mengontrol LCD I2C.

## Langkah-Langkah Merangkai

### 1. **Merangkai Sensor PIR**:
   - Sambungkan pin VCC sensor PIR ke **5V** Arduino.
   - Sambungkan pin GND sensor PIR ke **GND** Arduino.
   - Sambungkan pin OUT sensor PIR ke **Pin 2** untuk sensor PIR ruang tamu dan **Pin 4** untuk sensor PIR ruang belajar.

   > **Catatan**: Pastikan sensor PIR terpasang dengan benar agar dapat mendeteksi pergerakan dengan baik.

### 2. **Merangkai LED**:
   - Sambungkan pin panjang (anoda) LED indikator perangkat aktif ke **Pin 13** Arduino dan pin pendek (katoda) LED ke **GND** Arduino.
   - Sambungkan pin panjang (anoda) LED ruang tamu ke **Pin 12** Arduino dan pin pendek (katoda) LED ke **GND** Arduino.
   - Sambungkan pin panjang (anoda) LED ruang belajar ke **Pin 11** Arduino dan pin pendek (katoda) LED ke **GND** Arduino.
   
   > **Catatan**: Pasang resistor **220 ohm** antara pin anoda LED dan pin Arduino untuk membatasi arus yang mengalir.

### 3. **Merangkai LCD 16x2 I2C**:
   - Sambungkan pin VCC ke **VCC** Arduino.
   - Sambungkan pin GND ke **GND** Arduino.
   - Sambungkan pin SDA ke **Pin A4** Arduino.
   - Sambungkan pin SCL ke **Pin A5** Arduino.

## Penggunaan Resistor

- **LED**:
  - Pasang resistor **220 ohm** di antara pin anoda LED dan pin Arduino untuk membatasi arus yang mengalir melalui LED.
  
- **Sensor PIR**: 
  - Sensor PIR sudah memiliki resistor internal, sehingga tidak perlu menambahkan resistor eksternal.

- **LCD 16x2 I2C**:
  - LCD menggunakan komunikasi I2C, sehingga hanya membutuhkan sambungan SDA dan SCL yang benar.

## Penjelasan Fungsi Sistem

Sistem ini akan mendeteksi pergerakan menggunakan dua sensor PIR yang masing-masing terhubung ke ruang tamu dan ruang belajar. Ketika sensor PIR mendeteksi pergerakan, LED di ruang yang bersangkutan akan menyala, menandakan bahwa lampu otomatis menyala. LCD akan menampilkan status ruang tamu dan ruang belajar (ON/OFF) berdasarkan deteksi pergerakan. LED indikator di pin 13 menunjukkan bahwa perangkat sedang aktif.

## Kode yang Diberikan

```cpp
#include <____> // nama library yang diperlukan, misalnya LiquidCrystal_I2C

// Inisialisasi LCD
LiquidCrystal_I2C lcd(0x27, __, __);  // Alamat I2C dan ukuran LCD (misal: 16, 2)

// Pin untuk LED dan sensor PIR
const int pir1Pin = __;  // PIR 1 untuk ruang tamu, bagian ini perlu diisi
const int pir2Pin = __;  // PIR 2 untuk ruang belajar, bagian ini perlu diisi
const int ledIndPin = __;  // LED indikator perangkat aktif, bagian ini perlu diisi
const int ledRuangTamuPin = __;  // LED ruang tamu, bagian ini perlu diisi
const int ledRuangBelajarPin = __;  // LED ruang belajar, bagian ini perlu diisi

// Variabel untuk status PIR
bool _____ = false;  // Status PIR 1, bagian ini perlu diisi
bool pir2Status = ____;  // Status PIR 2, bagian ini perlu diisi

void setup() {
  // Set pin mode
  pinMode(pir1Pin, INPUT);  // Set PIR 1 sebagai input
  pinMode(pir2Pin, ____);  // Set PIR 2 sebagai input, bagian ini perlu diisi
  pinMode(ledIndPin, OUTPUT);  // LED indikator aktif, set sebagai output
  pinMode(ledRuangTamuPin, ____);  // LED ruang tamu, bagian ini perlu diisi
  _____(ledRuangBelajarPin, OUTPUT);  // LED ruang belajar, bagian ini perlu diisi

  // Inisialisasi LCD
  lcd.init();  // Inisialisasi LCD
  lcd.backlight();  // Menyalakan backlight LCD

  // LED indikator menyala untuk menunjukkan perangkat aktif
  digitalWrite(ledIndPin, ___);  // LED indikator aktif, bagian ini perlu diisi dengan HIGH atau LOW

  // Tampilkan pesan awal pada LCD
  lcd.setCursor(0, 0);  // Menempatkan kursor di baris 0, kolom 0
  lcd.print("S.Lampu Otomatis");  // Pesan awal
  delay(____);  // Tampilkan pesan selama beberapa detik, bagian ini perlu diisi (misal 2000 untuk 2 detik)
}

void loop() {
  // Membaca status PIR
  pir1Status = ______(pir1Pin);  // Membaca status PIR 1, bagian ini perlu diisi
  pir2Status = digitalRead(pir2Pin);  // Membaca status PIR 2

  // Lampu ruang tamu (PIR 1)
  if (pir1Status) {
    digitalWrite(ledRuangTamuPin, HIGH);  // Menyalakan LED ruang tamu jika PIR 1 mendeteksi pergerakan
    lcd.setCursor(0, 1);
    lcd.print("Ruang Tamu: ON   ");
  } else {
    digitalWrite(ledRuangTamuPin, LOW);  // Mematikan LED ruang tamu jika PIR 1 tidak mendeteksi pergerakan
    lcd.____(0, 1); // bagian ini perlu diisi
    lcd.print("Ruang Tamu: OFF  ");
  }

  // Lampu ruang belajar (PIR 2)
  if (pir2Status) {
    digitalWrite(ledRuangBelajarPin, HIGH);  // Menyalakan LED ruang belajar jika PIR 2 mendeteksi pergerakan
    lcd.setCursor(0, 2);
    lcd.print("Ruang Belajar: ON");
  } else {
    digitalWrite(ledRuangBelajarPin, LOW);  // Mematikan LED ruang belajar jika PIR 2 tidak mendeteksi pergerakan
    lcd.setCursor(0, 2);
    lcd.print("Ruang Belajar: OFF");
  }

  ____(500);  // Delay sebentar sebelum membaca ulang, bagian ini perlu diisi
}
```
## Jawaban

- [Sistem Lampu Pintar Wokwi Simulation]()
