# Sistem Bantu Wearable untuk Latihan Angkat Beban (Standing Dumbbell Curl)

---

## 📖 Deskripsi Proyek
Proyek ini mengembangkan **sistem bantu wearable** untuk membantu pengguna dalam latihan **standing dumbbell curl**. Sistem menggunakan **sensor MPU6050** untuk membaca data gerakan, lalu mengolahnya dengan algoritma **Random Forest** pada mikrokontroler **ESP32**. Hasil klasifikasi digunakan untuk memberikan **umpan balik real-time** melalui **buzzer**, sehingga pengguna tahu apakah gerakan yang dilakukan sudah benar atau masih salah.

---

## 🎯 Tujuan
- Membantu pengguna menjaga teknik latihan yang benar untuk mencegah cedera.  
- Memberikan umpan balik otomatis tanpa pelatih manusia.  
- Menunjukkan penerapan **Artificial Intelligence (AI)** pada perangkat **wearable IoT**.

---

## ⚙️ Komponen Sistem

| Komponen | Fungsi |
|-----------|---------|
| **MPU6050** | Sensor percepatan dan rotasi (accelerometer & gyroscope). |
| **ESP32** | Prosesor utama yang menjalankan model AI. |
| **TP4056 & Baterai 18650** | Sumber daya perangkat wearable. |
| **Buzzer** | Memberikan umpan balik audio kepada pengguna. |

---

## 🧩 Arsitektur Sistem

Sistem bantu wearable ini terdiri dari **tiga sensor MPU6050**, **mikrokontroler ESP32**, dan **buzzer** sebagai pemberi umpan balik.  
Semua komponen saling terhubung menggunakan **komunikasi nirkabel ESP-NOW**.

### 🔧 Diagram Alur Sistem
```text
[MPU6050 - Pergelangan Tangan] ─┐
                                │
                                ├── (ESP-NOW Wireless Data Transmission)
                                │
[MPU6050 - Lengan Atas] ────────┘
                 ↓
           [ESP32 Master Controller]
                 ↓
        [Random Forest Model (AI)]
                 ↓
           [Buzzer Feedback System]
```


---

## 🧪 Cara Kerja Sistem
1. Sensor MPU6050 membaca data akselerasi dan sudut dari tiga titik tubuh (pergelangan tangan, lengan atas, dada).  
2. Data dikirim ke ESP32 utama melalui **ESP-NOW** (tanpa Wi-Fi).  
3. ESP32 memproses data dengan **model Random Forest** yang telah dilatih.  
4. Jika gerakan benar → buzzer berbunyi.  
   Jika salah → buzzer tidak berbunyi.

---
## 📊 Hasil Pengujian
| Parameter                | Hasil     |
| ------------------------ | --------- |
| Akurasi model (training) | 96.4%     |
| Akurasi sistem wearable  | 95%       |
| Waktu komputasi          | 3.25 ms   |
| Respon sistem            | Real-time |

---

## ⚙️ Instalasi dan Cara Menjalankan

Bagian ini menjelaskan langkah-langkah untuk menyiapkan lingkungan proyek, menjalankan model AI di komputer, dan (opsional) mengimplementasikannya ke perangkat ESP32.

---

### 1. Persiapan Lingkungan Python

#### a. Pastikan Python Terpasang
Pastikan kamu telah menginstal **Python 3.8** atau versi lebih baru.  
Cek versi Python dengan perintah:
```bash
python --version
```

#### b. Clone Repository
Unduh project ke komputer kamu dengan perintah berikut:
```bash
git clone https://github.com/asepzayn/wearable-device-biceps-curl.git
cd ai-wearable-biceps-curl
```

#### c. Install library yang diperlukan
Project ini menggunakan beberapa library Python untuk training dan evaluasi model AI.
Instal semua dependensi dengan:
```bash
pip install -r requirements.txt
```

### 2. Menjalankan Model AI di Komputer

#### a. Masuk ke Folder Sumber Kode
```bash
cd src
```

#### b. Jalankan Script Training Model
```bash
python train_model.py
```

#### c. Hasil Training
Jika berhasil, sistem akan menampilkan akurasi model di terminal seperti:
```yaml
Akurasi Model: 0.964
```
Model yang sudah dilatih akan tersimpan sebagai file:
```bash
src/model_RF.h
```

### 3. Implementasi pada ESP32

#### a. Siapkan Perangkat Keras
- **ESP32** sebagai mikrokontroler utama
- **MPU6050** (sensor akselerometer & giroskop) di 3 titik: pergelangan tangan, lengan atas, dan dada
- **Buzzer** sebagai umpan balik suara
- **TP4056 + Baterai 18650** sebagai sumber daya
- Gunakan komunikasi **ESP-NOW** antar ESP32

#### b. Konversi Model 
Konversi model.pkl agar bisa dijalankan di mikrokontroler, dengan opsi:
- Gunakan TensorFlow Lite for Microcontrollers, atau
- Konversi logika Random Forest menjadi rule-based decision tree sederhana di Arduino IDE.

#### c. Upload Kode ke ESP32
Gunakan Arduino IDE atau Thonny (MicroPython) untuk mengunggah kode. Pastikan semua sensor dan pin terhubung sesuai diagram pada folder "/hardware/"

#### d. Jalankan Sistem
1. Nyalakan perangkat.
2. Gerakkan lengan sesuai latihan standing dumbbell curl.
3. Jika gerakan benar → buzzer berbunyi.
   Jika salah → buzzer diam.
