# 🛡️ Predictive Digital Twin (PDT) & Dynamic Barrier-based Safety (DBaS) on STM32

**Evaluasi Tengah Semester (ETS) - Pemrograman Kontroler** 👤 **Oleh:** Muhammad Evan Airel Budiasono (NRP: 2042241105)  
🏫 **Institusi:** Departemen Teknik Instrumentasi, Institut Teknologi Sepuluh Nopember (ITS)

---

## 📌 Deskripsi Proyek
Repositori ini memuat implementasi sistem pengaman aktuator otonom berbasis **Predictive Digital Twin (PDT)** dan gerbang logika **Dynamic Barrier-based Safety (DBaS)** pada mikrokontroler **STM32F401CB**. 

Sistem ini didesain sebagai solusi atas kelemahan pengaman *reactive threshold-based* konvensional di industri. Dengan menghitung derivatif diskrit secara *real-time*, mikrokontroler mampu memproyeksikan potensi anomali lonjakan sinyal di masa depan dan melakukan *cut-off* aktuator secara proaktif **sebelum** batas bahaya absolut tersentuh.

## 🚀 Sorotan Teknis (Technical Highlights)
* **Bare-Metal C (HAL):** Dikembangkan murni menggunakan bahasa C dan *Hardware Abstraction Layer* (HAL) untuk efisiensi memori tinggi tanpa membebani siklus CPU.
* **Predictive Algorithm:** Implementasi matematika prediktif linier (`int32_t` dan `uint32_t`) di dalam *loop* utama (*polling*) yang secara instan menghitung nilai tren/derivatif masa depan.
* **Safety Latch Mechanism:** Menghilangkan kelemahan osilasi mekanik (*actuator chattering*) di sekitar titik ambang batas dengan mengunci status aktuator dalam kondisi mati hingga nilai sistem diverifikasi aman secara absolut.
* **Asymmetric Noise Testing:** Divalidasi melalui penyuntikan *AC Noise* asimetris di Proteus pada variasi beban 10% - 100%.

## 📂 Struktur Repositori
Repositori ini disusun secara rapi untuk memudahkan proses evaluasi dan simulasi ulang:

* 📁 **`STM32_Code/`** Berisi *source code* lengkap (C/C++), konfigurasi STM32CubeMX (`.ioc`), dan *project file* Keil µVision 5. Logika utama berada di dalam `Core/Src/main.c`.
* 📁 **`Proteus_Simulation/`** Berisi *file* skematik simulasi perangkat keras Proteus 8 Professional (`.pdsprj`) beserta *file* `.hex` siap pakai untuk mensimulasikan ADC dan respons aktuator (LED).
* 📁 **`Data_and_Plot/`** Berisi *dataset* hasil ekstraksi Virtual Terminal (UART), skrip plotting otomatis, dan hasil visualisasi komparatif menggunakan **GNUPlot 6.0**.

## ⚙️ Cara Menjalankan Simulasi
1. Buka *file* simulasi `.pdsprj` di dalam folder `Proteus_Simulation` menggunakan Proteus 8.xx.
2. Pastikan komponen mikrokontroler STM32F401CB sudah diarahkan ke *file* `.hex` yang disediakan.
3. Tekan **Play** pada Proteus.
4. Putar potensiometer (RV3) secara perlahan (10% - 70%) untuk melihat nilai prediksi yang linier dan status aktuator **"Aman"**.
5. Putar potensiometer dengan **cepat** (simulasi lonjakan anomali) untuk memicu peringatan **"BAHAYA -> CUT-OFF!"** pada Virtual Terminal dan matinya LED aktuator.

---
*Dibuat untuk memenuhi kualifikasi ETS Pemrograman Kontroler (2026).*
