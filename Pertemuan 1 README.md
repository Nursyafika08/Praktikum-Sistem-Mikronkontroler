Pertemuan 1 - Modul 1: Percabangan dan Perulangan

Nama:Nursyafika  
NIM:H1H024023  

Percobaan 1A - Percabangan

1. Pada kondisi apa program masuk ke blok `if`?
Program masuk ke blok `if` ketika nilai `timeDelay` lebih kecil atau sama dengan 100. Pada kondisi ini, LED sudah mencapai kecepatan kedip maksimum sehingga program memberikan jeda selama 3000 ms, lalu mengembalikan nilai `timeDelay` menjadi 1000.

2. Pada kondisi apa program masuk ke blok `else`?  
Program masuk ke blok `else` ketika nilai `timeDelay` masih lebih besar dari 100. Pada kondisi ini, program akan mengurangi nilai `timeDelay` sebesar 100 agar LED berkedip semakin cepat.

3. Apa fungsi dari perintah `delay(timeDelay)`?  
Perintah `delay(timeDelay)` berfungsi untuk memberikan jeda waktu sesuai nilai variabel `timeDelay`. Semakin besar nilainya, semakin lambat kedipan LED. Semakin kecil nilainya, semakin cepat kedipan LED.

4. Jika program yang dibuat memiliki alur mati → lambat → cepat → reset (mati), ubah menjadi LED tidak langsung reset, tetapi berubah dari cepat → sedang → mati dan berikan penjelasan di setiap baris kode.

Program Modifikasi
```cpp
const int ledPin = 2;
int timeDelay = 1500;
bool mempercepat = true;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(timeDelay);
  digitalWrite(ledPin, LOW);
  delay(timeDelay);

  if (mempercepat) {
    timeDelay -= 100;
    if (timeDelay <= 200) {
      mempercepat = false;
    }
  } else {
    timeDelay += 100;
    if (timeDelay >= 800) {
      digitalWrite(ledPin, LOW);
      delay(2000);
      timeDelay = 1500;
      mempercepat = true;
    }
  }
}

Penjelasan Program

const int ledPin = 2;
Menentukan bahwa LED terhubung pada pin 2.

int timeDelay = 1500;
Menyimpan nilai delay awal sebesar 1500 milidetik.

bool mempercepat = true;
Variabel untuk menandai apakah LED sedang dipercepat.

void setup() {
Bagian program yang dijalankan sekali saat awal.

pinMode(ledPin, OUTPUT);
Mengatur pin LED sebagai output.

void loop() {
Bagian program yang berjalan berulang terus-menerus.

digitalWrite(ledPin, HIGH);
Menyalakan LED.

delay(timeDelay);
Memberi jeda saat LED menyala.

digitalWrite(ledPin, LOW);
Mematikan LED.

delay(timeDelay);
Memberi jeda saat LED mati.

if (mempercepat) {
Mengecek apakah LED sedang dalam fase dipercepat.

timeDelay -= 100;
Mengurangi delay agar kedipan menjadi lebih cepat.

if (timeDelay <= 200) {
Mengecek apakah sudah mencapai batas cepat.

mempercepat = false;
Mengubah kondisi agar LED mulai diperlambat.

} else {
Jika tidak mempercepat, program masuk fase memperlambat.

timeDelay += 100;
Menambah delay agar kedipan menjadi sedang.

if (timeDelay >= 800) {
Mengecek apakah delay sudah mencapai batas sedang.

digitalWrite(ledPin, LOW);
Memastikan LED mati.

delay(2000);
Memberi jeda 2 detik sebelum mengulang siklus.

timeDelay = 1500;
Mengembalikan delay ke nilai awal.

mempercepat = true;
Mengatur agar siklus berikutnya dimulai dari percepatan lagi.


Percobaan 2A - Perulangan

1. Gambarkan rangkaian schematic LED running yang digunakan pada percobaan!
Rangkaian LED running dibuat dengan menghubungkan masing-masing LED ke pin digital Arduino melalui resistor, lalu kaki negatif LED dihubungkan ke GND. Pada percobaan ini, LED dihubungkan ke pin 2, 3, 4, 5, 6, dan 7 Arduino. [GAMBAR SKEMA ADA DI FILE]

2. Jelaskan bagaimana program membuat efek LED berjalan dari kiri ke kanan!
Efek LED berjalan dari kiri ke kanan dibuat menggunakan perulangan for dengan nilai ledPin dari 2 sampai 7. Setiap LED dinyalakan, diberi jeda 200 ms, lalu dimatikan sebelum pindah ke LED berikutnya.

3. Jelaskan bagaimana program membuat LED kembali dari kanan ke kiri!
Efek LED kembali dari kanan ke kiri dibuat menggunakan perulangan for dengan nilai ledPin dari 7 turun sampai 2. Dengan cara ini, urutan nyala LED bergerak ke arah sebaliknya.

4. Buatkan program agar LED menyala tiga LED kanan dan tiga LED kiri secara bergantian dan berikan penjelasan di setiap baris kode!

Program Modifikasi

int timer = 200;
int ledPins[] = {2, 3, 4, 5, 6, 7};

void setup() {
  for (int i = 0; i < 6; i++) {
    pinMode(ledPins[i], OUTPUT);
  }
}

void loop() {
  digitalWrite(ledPins[0], HIGH);
  digitalWrite(ledPins[1], HIGH);
  digitalWrite(ledPins[2], HIGH);
  digitalWrite(ledPins[3], LOW);
  digitalWrite(ledPins[4], LOW);
  digitalWrite(ledPins[5], LOW);
  delay(timer);

  for (int i = 0; i < 6; i++) {
    digitalWrite(ledPins[i], LOW);
  }
  delay(timer);

  digitalWrite(ledPins[0], LOW);
  digitalWrite(ledPins[1], LOW);
  digitalWrite(ledPins[2], LOW);
  digitalWrite(ledPins[3], HIGH);
  digitalWrite(ledPins[4], HIGH);
  digitalWrite(ledPins[5], HIGH);
  delay(timer);

  for (int i = 0; i < 6; i++) {
    digitalWrite(ledPins[i], LOW);
  }
  delay(timer);
}

Penjelasan Program

int timer = 200;
Menentukan lama jeda nyala LED.

int ledPins[] = {2, 3, 4, 5, 6, 7};
Menyimpan daftar pin LED dalam array.

void setup() {
Bagian awal program yang dijalankan sekali.

for (int i = 0; i < 6; i++) {
Perulangan untuk mengatur semua pin LED.

pinMode(ledPins[i], OUTPUT);
Menjadikan setiap pin LED sebagai output.

void loop() {
Bagian program yang diulang terus-menerus.

digitalWrite(ledPins[0], HIGH); sampai digitalWrite(ledPins[2], HIGH);
Menyalakan tiga LED sisi kiri.

digitalWrite(ledPins[3], LOW); sampai digitalWrite(ledPins[5], LOW);
Memastikan tiga LED sisi kanan mati.

delay(timer);
Memberi jeda agar pola terlihat jelas.

for (int i = 0; i < 6; i++) { digitalWrite(ledPins[i], LOW); }
Mematikan semua LED.

digitalWrite(ledPins[3], HIGH); sampai digitalWrite(ledPins[5], HIGH);
Menyalakan tiga LED sisi kanan.

digitalWrite(ledPins[0], LOW); sampai digitalWrite(ledPins[2], LOW);
Memastikan tiga LED sisi kiri mati.

delay(timer);
Memberi jeda sebelum pola diulang lagi.
