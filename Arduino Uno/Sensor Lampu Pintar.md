# Deskripsi Tugas: Sistem Lampu Otomatis 

Tugas ini bertujuan untuk membuat sistem lampu otomatis yang dapat mendeteksi pergerakan menggunakan sensor PIR di ruang tamu dan mendeteksi intensitas cahaya menggunakan sensor LDR di ruang belajar. Sistem ini menggunakan Arduino Uno, sensor PIR, LDR, dan LED untuk menandakan status lampu di masing-masing ruangan. Sistem akan mengaktifkan atau mematikan lampu berdasarkan pergerakan yang terdeteksi oleh sensor PIR dan tingkat cahaya yang terdeteksi oleh sensor LDR.

## Komponen yang Digunakan

- **Sensor PIR**: Untuk mendeteksi pergerakan manusia di ruang tamu.
- **Sensor LDR**: Untuk mendeteksi tingkat cahaya di ruang belajar.
- **LED ON (indikator perangkat aktif)**: Menunjukkan bahwa perangkat dalam keadaan aktif.
- **LED Ruang Tamu**: Menyala saat ada pergerakan di ruang tamu.
- **LED Ruang Belajar**: Menyala saat intensitas cahaya di ruang belajar rendah (gelap).
- **Arduino Uno**: Sebagai mikrokontroler utama.

## Library yang Digunakan

- `LiquidCrystal_I2C`: Untuk mengontrol LCD I2C.

## Langkah-Langkah Merangkai

### 1. **Merangkai Sensor PIR**:
   - Sambungkan pin VCC sensor PIR ke **5V** Arduino.
   - Sambungkan pin GND sensor PIR ke **GND** Arduino.
   - Sambungkan pin OUT sensor PIR ke **Pin 2** untuk sensor PIR ruang tamu.

### 2. **Merangkai Sensor LDR**:
   - Sambungkan salah satu pin LDR ke **5V** Arduino.
   - Sambungkan pin lainnya ke **Pin A0** Arduino (analog input) dan sambungkan juga ke **GND** melalui resistor 10kΩ untuk pembagian tegangan.

### 3. **Merangkai LED**:
   - Sambungkan pin panjang (anoda) LED indikator perangkat aktif ke **Pin 13** Arduino dan pin pendek (katoda) LED ke **GND** Arduino.
   - Sambungkan pin panjang (anoda) LED ruang tamu ke **Pin 12** Arduino dan pin pendek (katoda) LED ke **GND** Arduino.
   - Sambungkan pin panjang (anoda) LED ruang belajar ke **Pin 11** Arduino dan pin pendek (katoda) LED ke **GND** Arduino.
   
   > **Catatan**: Pasang resistor **220 ohm** antara pin anoda LED dan pin Arduino untuk membatasi arus yang mengalir.

### 4. **Merangkai LCD 16x2 I2C**:
   - Sambungkan pin VCC ke **VCC** Arduino.
   - Sambungkan pin GND ke **GND** Arduino.
   - Sambungkan pin SDA ke **Pin A4** Arduino.
   - Sambungkan pin SCL ke **Pin A5** Arduino.

## Penggunaan Resistor

- **LED**:
  - Pasang resistor **220 ohm** di antara pin anoda LED dan pin Arduino untuk membatasi arus yang mengalir melalui LED.
  
- **Sensor PIR**: 
  - Sensor PIR sudah memiliki resistor internal, sehingga tidak perlu menambahkan resistor eksternal.

- **Sensor LDR**:
  - LDR memerlukan resistor 10kΩ untuk pembagian tegangan pada rangkaian analog.

- **LCD 16x2 I2C**:
  - LCD menggunakan komunikasi I2C, sehingga hanya membutuhkan sambungan SDA dan SCL yang benar.

## Penjelasan Fungsi Sistem

Sistem ini akan mendeteksi pergerakan menggunakan sensor PIR di ruang tamu dan mendeteksi intensitas cahaya menggunakan sensor LDR di ruang belajar. Ketika sensor PIR mendeteksi pergerakan, LED di ruang tamu akan menyala, menandakan bahwa lampu otomatis menyala. Sementara itu, jika sensor LDR mendeteksi kondisi ruang belajar yang gelap, LED ruang belajar akan menyala, menandakan bahwa lampu otomatis menyala. LCD akan menampilkan status ruang tamu dan ruang belajar (ON/OFF) berdasarkan deteksi pergerakan dan cahaya. LED indikator di pin 13 menunjukkan bahwa perangkat sedang aktif.

## Kode yang Diberikan

```cpp
#include <______> // tuliskan

// Inisialisasi LCD
LiquidCrystal_I2C lcd(0x27, __, __);

// Pin untuk LED dan sensor PIR/LDR
#define PIR_PIN __             // PIR untuk ruang tamu
#define LDR_PIN __             // LDR untuk ruang belajar
#define LED_IND_PIN __         // LED indikator perangkat aktif
#define LED_RUANG_TAMU __      // LED ruang tamu
#define LED_RUANG_BELAJAR __   // LED ruang belajar

// Variabel untuk status PIR dan LDR
bool pirStatus = false;        // Status PIR
int ldrValue = 0;              // Nilai pembacaan LDR (0-1023)

void setup() {
  // Set pin mode
  pinMode(PIR_PIN, INPUT);
  pinMode(LDR_PIN, ___);
  pinMode(LED_IND_PIN, OUTPUT);       // LED indikator aktif
  ____(LED_RUANG_TAMU, OUTPUT);   // LED ruang tamu
  pinMode(LED_RUANG_BELAJAR, ____); // LED ruang belajar

  // Inisialisasi LCD
  lcd.init();  // Untuk library yang lebih baru
  lcd.backlight();  // Menyalakan backlight LCD

  // LED indikator menyala untuk menunjukkan perangkat aktif
  digitalWrite(LED_IND_PIN, HIGH);  // Menyalakan LED indikator

  // Tampilkan pesan awal pada LCD
  lcd.setCursor(0, 0);
  lcd.print("S.Lampu Otomatis");
  delay(____);  // Tampilkan pesan selama 2 detik
}

void ___() {
  // Membaca status PIR
  pirStatus = digitalRead(PIR_PIN);

  // Membaca nilai LDR
  ldrValue = analogRead(LDR_PIN);  // Membaca nilai dari LDR (0-1023)

  // Lampu ruang tamu (PIR)
  if (pirStatus) {
    digitalWrite(LED_RUANG_TAMU, ___);  // Menyalakan LED ruang tamu jika PIR mendeteksi pergerakan
    lcd.setCursor(0, 1);
    lcd.print("Ruang Tamu: ON   ");
  } else {
    digitalWrite(LED_RUANG_TAMU, LOW);  // Mematikan LED ruang tamu jika PIR tidak mendeteksi pergerakan
    lcd.setCursor(0, 1);
    lcd.print("Ruang Tamu: OFF  ");
  }

  // Lampu ruang belajar (LDR)
  if (ldrValue <= 400) {  // Jika tingkat cahaya LDR kurang dari atau sama dengan 400 (ruangan gelap)
    digitalWrite(LED_RUANG_BELAJAR, HIGH);  // Menyalakan LED ruang belajar
    lcd.____(0, 2);
    lcd.print("Ruang Belajar: ON ");
  } else {
    digitalWrite(LED_RUANG_BELAJAR, LOW);  // Mematikan LED ruang belajar jika LDR > 400 (ruangan terang)
    lcd.setCursor(0, 2);
    lcd.print("Ruang Belajar: OFF");
  }

  ___(500);  // Delay sebentar sebelum membaca ulang
}

```
## Jawaban

- [Sistem Lampu Pintar Wokwi Simulation]()
