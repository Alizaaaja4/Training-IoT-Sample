
# Deskripsi Tugas: Sistem Pendeteksi Gas Bocor

Tugas ini bertujuan untuk membuat sistem pendeteksi gas bocor yang menggabungkan pemantauan suhu dan kualitas udara. Sistem ini menggunakan Arduino Uno, sensor suhu DHT22, dan potensiometer sebagai simulasi sensor gas (seperti MQ135). Ketika suhu melebihi batas yang ditentukan atau kualitas udara buruk, sistem akan memberikan peringatan melalui buzzer. Data suhu dan kualitas udara akan ditampilkan pada LCD 20x4.

## Komponen yang Digunakan

- **Sensor DHT22**: Untuk membaca suhu dan kelembapan.
- **LCD 20x4 I2C**: Untuk menampilkan hasil pengukuran suhu, kelembapan, dan status kualitas udara.
- **LED Hijau**: Sebagai indikator bahwa perangkat aktif.
- **Buzzer**: Untuk memberikan peringatan jika kondisi udara atau suhu berbahaya.
- **Potensiometer**: Digunakan untuk mensimulasikan kualitas udara (contoh: sensor MQ135).
- **Arduino Uno**: Sebagai mikrokontroler utama.

## Library yang Digunakan

- `LiquidCrystal_I2C`: Untuk mengontrol LCD I2C.
- `DHT`: Untuk membaca data dari sensor DHT22.

## Langkah-Langkah Merangkai

### 1. **Merangkai Sensor DHT22**:
   - Sambungkan pin VCC ke **VCC** Arduino.
   - Sambungkan pin GND ke **GND** Arduino.
   - Sambungkan pin DATA ke **Pin 2** Arduino (atau pin yang Anda pilih).

   > **Catatan**: Jika ingin meningkatkan kestabilan pembacaan, pasang resistor **4.7 kΩ** atau **10 kΩ** antara pin DATA dan pin VCC.

### 2. **Merangkai LCD 20x4 I2C**:
   - Sambungkan pin VCC ke **VCC** Arduino.
   - Sambungkan pin GND ke **GND** Arduino.
   - Sambungkan pin SDA ke **Pin A4** Arduino.
   - Sambungkan pin SCL ke **Pin A5** Arduino.

### 3. **Merangkai Potensiometer**:
   - Sambungkan pin tengah (wiper) ke **Pin A0** Arduino.
   - Sambungkan satu pin samping ke **5V** Arduino.
   - Sambungkan pin lainnya ke **GND** Arduino.

### 4. **Merangkai LED Hijau dan Buzzer**:
   - Sambungkan pin panjang (anoda) LED ke **Pin 13** Arduino.
   - Sambungkan pin pendek (katoda) LED ke **GND** Arduino.
   - Sambungkan satu pin Buzzer ke **Pin 12** Arduino dan pin lainnya ke **GND**.

   > **Catatan**: LED membutuhkan resistor untuk membatasi arus yang mengalir. Pasang resistor **220 ohm hingga 1 kΩ** di antara pin anoda LED dan pin 13 Arduino.

## Penggunaan Resistor

- **LED Hijau**: 
  - Pasang resistor **220 ohm hingga 1 kΩ** di antara pin anoda LED dan pin 13 Arduino.
  
- **Buzzer Aktif**: 
  - Tidak perlu resistor tambahan karena buzzer aktif sudah memiliki resistor internal.
  
- **Potensiometer**: 
  - Tidak perlu resistor tambahan, karena potensiometer berfungsi sebagai pembagi tegangan.

- **DHT22**: 
  - Tambahkan resistor **4.7 kΩ** atau **10 kΩ** antara pin DATA dan pin VCC untuk kestabilan pembacaan data.

> **Catatan**: Pastikan semua komponen menggunakan koneksi yang benar antara **VCC** dan **GND** pada Arduino. Pilih pin lainnya sesuai kebutuhan, namun sesuaikan dengan kode yang telah diberikan.

## Penjelasan Fungsi Sistem

Sistem ini akan melakukan pemantauan dua parameter: suhu dan kualitas udara. Kualitas udara disimulasikan menggunakan potensiometer, yang akan memberi nilai dalam rentang 0-100. Jika kualitas udara buruk (nilai potensiometer tinggi), atau suhu melebihi batas yang ditentukan, sistem akan memberikan peringatan menggunakan buzzer dan menampilkan status tersebut pada LCD. LCD juga menampilkan suhu dan kualitas udara dalam waktu nyata.

## Sumber Daya

- **Arduino Uno**: Mikrokontroler utama yang digunakan untuk mengendalikan semua komponen dan logika program.
- **Sensor DHT22**: Untuk mendapatkan data suhu dan kelembapan yang dibutuhkan dalam pemantauan kondisi lingkungan.
- **LCD 16x2 I2C**: Untuk menampilkan status suhu dan kualitas udara secara visual.
- **Potensiometer**: Untuk mensimulasikan kualitas udara berdasarkan variabel input yang diberikan.
- **LED Hijau dan Buzzer**: Sebagai indikator visual dan audio untuk memberi tahu status sistem.

## Kode yang Diberikan

```cpp
#include <___> // Nama library LCD I2C, bagian ini perlu diisi
#include <___> //nama library sensor dht, bagian ini perlu diisi

#define Kualitas_Udara ___  // Input kan value batas kualitas udara, bagian ini perlu diisi
#define Batas_Suhu ___     // Input kan value batas suhu, bagian ini perlu diisi

#define DHTPIN __          // Input kan value pin data untuk sensor DHT22, bagian ini perlu diisi
#define DHTTYPE DHT22     // Tipe sensor DHT, bagian ini perlu diisi
#define LED_Hijau __      // Input kan value pin untuk LED indikator IoT ON, bagian ini perlu diisi
#define BUZZER_PIN __     // Input kan value pin untuk Buzzer, bagian ini perlu diisi
#define POT_PIN __        // Input kan value pin untuk Potentiometer yang digunakan untuk mensimulasikan MQ135, bagian ini perlu diisi

DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, __, __); // Input kan ukuran LCD I2C yg digunakan, bagian ini perlu diisi

void setup() {
  Serial.begin(9600);  // Mulai komunikasi serial
  dht.begin();         // Inisialisasi sensor DHT
  lcd.init();          // Inisialisasi LCD
  lcd.backlight();     // Aktifkan lampu latar LCD

  pinMode(LED_Hijau, _____);   // Set pin LED sebagai output, bagian ini perlu diisi
  pinMode(BUZZER_PIN, OUTPUT);  // Set pin buzzer sebagai output

  // LED indikator menyala untuk menunjukkan perangkat aktif
  digitalWrite(LED_Hijau, HIGH);
  lcd.setCursor(0, 0);
  lcd.print("Perangkat Aktif");
  lcd.setCursor(0, 1);
  lcd.print("Sistem Gas Bocor");
  delay(____);  // Tampilkan pesan selama 3 detik, bagian ini perlu diisi
  lcd.clear();
}

void loop() {
  // Membaca suhu dari sensor DHT
  float suhu = dht.readTemperature();
  if (isnan(suhu)) {
    suhu = 0; // Menangani error pembacaan
  }

  // Membaca kualitas udara dari potentiometer (untuk simulasi)
  int kualitas = analogRead(POT_PIN);
  kualitas = map(kualitas, 0, 1023, 0, 100); // Mapping ke skala 0-100

  // Menampilkan suhu dan kualitas udara pada LCD
  lcd.setCursor(0, 0);
  lcd.print("Suhu : ");
  lcd.print(suhu, 1); // 1 desimal untuk suhu
  lcd.print(" C");

  lcd.setCursor(0, 1);
  lcd.print("Kualitas Udara: ");
  lcd.print(kualitas);

  // Cek kondisi gas buruk dan suhu tinggi
  bool gasBuruk = kualitas > Kualitas_Udara;
  bool suhuTinggi = suhu > Batas_Suhu;

  lcd.setCursor(0, 2);
  if (gasBuruk && suhuTinggi) {
    lcd.print("BAHAYA: GAS & SUHU");
    tone(BUZZER_PIN, 1000);  // Bunyikan buzzer pada frekuensi 1000 Hz
  } else if (gasBuruk) {
    lcd.print("Gas Buruk          ");
    ___(BUZZER_PIN);      // Matikan buzzer, bagian ini perlu diisi
  } else if (suhuTinggi) {
    lcd.print("Suhu Tinggi        ");
    noTone(___);      // Matikan buzzer, bagian ini perlu diisi
  } else {
    lcd.print("Kondisi Aman       ");
    noTone(BUZZER_PIN);      // Matikan buzzer
  }

  lcd.setCursor(0, 3);
  lcd.print("Monitoring aktif   ");

  ____(1000); // Update setiap 1 detik, bagian ini perlu diisi
}
```

## Jawaban

- [Sistem Pendeteksi Gas Bocor Wokwi Simulation]()
