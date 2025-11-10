# Sistem Bantu Wearable untuk Latihan Angkat Beban (Biceps Curl)

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

