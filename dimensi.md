# Google Pixel 5 - Technical Dimensions & 3D Print Enclosure Specs

Dokumentasi referensi dimensi bodi, posisi port/I/O, rekonsiliasi hasil ukur fisik (caliper), serta parameter toleransi cetak (*clearance gap*) untuk perancangan casing 3D printer (router/server appliance).

---

## 1. Spesifikasi Bodi Utama (Nominal vs CAD Bay)

* **Sistem Koordinat (Origin):** 
  * `X = 0`: Titik tengah bodi (Centerline horizontal).
  * `Y = 0`: Tepi bodi paling bawah (Bottom edge).
  * `Z = 0`: Permukaan layar depan (Front glass surface).

| Sumbu / Fitur | Ukuran Nominal (Pabrik) | Toleransi FDM (+Gap) | Rekomendasi CAD Pocket |
| :--- | :--- | :--- | :--- |
| **Panjang (Tinggi / Y)** | 144.7 mm | +0.7 mm | **145.4 mm** |
| **Lebar (X)** | 70.4 mm | +0.6 mm | **71.0 mm** |
| **Tebal Bodi (Z)** | 8.0 mm | +0.4 mm | **8.4 mm** |
| **Radius Sudut (Corner)** | ~R10.5 mm | Offset bodi | **R10.8 mm** |
| **Tepi Belakang (Rear Edge Fillet)** | ~R2.5 mm | Sesuai kurva bodi | Chamfer / Fillet R2.8 mm |

---

## 2. Pemetaan Fitur & Rekonsiliasi Pengukuran

Semua pengukuran posisi sumbu Y dihitung dari **bawah (Bottom Edge, Y=0)** agar sejajar dengan port I/O utama.

### A. Sisi Kanan (Right Flank - Tombol Daya & Volume)
* **Power Button:**
  * Ukuran Fisik: `3.0 mm (Z) x 10.0 mm (Y)`
  * Posisi Y: `Y = 99.7 mm s/d 109.7 mm` (Jarak dari tepi atas: ~35.0 mm).
  * **Rekomendasi Cutout CAD:** Lubang slot terbuka lebar `14.0 mm (Y) x 6.0 mm (Z)` (rentang `Y = 97.5 mm s/d 111.5 mm`).
* **Volume Rocker:**
  * Ukuran Fisik: `3.0 mm (Z) x 20.0 mm (Y)`
  * Posisi Y: `Y = 70.0 mm s/d 90.0 mm` (Jarak dari tepi atas: ~54.7 mm).
  * **Rekomendasi Cutout CAD:** Lubang slot terbuka lebar `24.0 mm (Y) x 6.0 mm (Z)` (rentang `Y = 68.0 mm s/d 92.0 mm`).

---

### B. Sisi Bawah (Bottom Flank - USB-C & Speaker)
* **USB-C Port:**
  * Posisi: Center simetris di `X = 0` (jarak ke sisi kiri & kanan masing-masing 31.2 mm).
  * Dimensi Bodi Port Internal: `8.0 mm (X) x 3.0 mm (Z)`.
  * **Rekomendasi Cutout CAD (Outer Plug Clearance):** Minimal **`13.0 mm (X) x 7.0 mm (Z)`**.  
    *(Penting: Kepala overmold colokan kabel USB-C umumnya setebal 5.5–6.5 mm dan selebar 11–12 mm. Ukuran 8x3 mm hanya cukup untuk lubang port, bukan kepala kabel).*
* **Speaker & Mic Grille (Kiri & Kanan USB-C):**
  * Posisi: Simetris, berjarak ~7.0 mm dari tepi luar lubang USB-C bawaan.
  * Ukuran Fisik Tiap Grille: `10.0 mm (X) x 1.0 mm (Z)`.
  * **Rekomendasi CAD:** Slot kisi ventilasi `12.0 mm x 3.0 mm` per sisi (bisa dimanfaatkan sebagai intake/exhaust udara bawah).

---

### C. Sisi Kiri (Left Flank - SIM Tray)
* **SIM Card Tray:**
  * Ukuran Fisik: `12.0 mm (Y) x 3.0 mm (Z)`
  * Posisi Y: Rentang `Y = 35.0 mm s/d 47.0 mm` (Jarak ke tepi atas: ~97.7 mm).
  * **Rekomendasi Cutout CAD:** Slot selebar `16.0 mm (Y) x 4.5 mm (Z)` + lubang pin ejector tembus diameter `1.5 mm` jika case dirancang modular tanpa harus melepas HP.

---

### D. Punggung Bodi (Rear Panel - Modul Kamera & Sensor)
*(Orientasi perspektif: Melihat punggung HP langsung)*

* **Camera Island (Bump Kamera):**
  * Bentuk: Persegi rounded edge `25.0 mm x 25.0 mm`, tonjolan keluar ~`1.1 mm`.
  * Posisi: Pojok kiri atas punggung.
    * Offset tepi atas: `6.0 mm`
    * Offset tepi kiri: `6.0 mm`
    * Sisa jarak ke tepi kanan: `~39.4 mm`
  * **Rekomendasi CAD Pocket:** Rongga berukuran **`27.0 mm x 27.0 mm`** dengan kedalaman minimal **`1.3 mm`** agar bodi HP dapat bertumpu rata (*flat flush*) tanpa membuat motherboard melengkung saat dibaut.
* **Fingerprint Sensor:**
  * Bentuk: Lingkaran diameter `10.0 mm`, cekungan ke dalam ~`0.6 mm`.
  * Posisi Center: Tepat di sumbu simetris `X = 0`, jarak dari tepi atas ~`34.0 mm` (`Y = ~100.7 mm`).
  * **Rekomendasi Desain Router/Appliance:** **Ditutup penuh** oleh kompartemen modul/baterai belakang. Gunakan unlock bypass/ADB/scrcpy untuk operasional.
* **Thermal Hotspot Area (Posisi SoC Snapdragon 765G):**
  * Terletak di punggung HP, **persis di sebelah kanan modul kamera (persepsi belakang)**, sekitar `X = +5 mm s/d +25 mm` dan `Y = 95 mm s/d 130 mm`.
  * **Catatan Cooling:** Posisi kipas blower 4010/4020 atau heatsink pad wajib diarahkan tepat pada zona koordinat ini.

---

## 3. Checklist Aturan Pemodelan 3D Enclosure

1. **Front Bezel Retention:**
   * Buat bibir penahan tepi kaca depan selebar `1.2 mm` di sekeliling frame dengan ketebalan bibir `1.5 mm` agar HP terkunci rapat dari depan.
2. **Mounting Hardware:**
   * Gunakan lubang untuk **Brass Threaded Heat-Set Inserts M3** (diameter lubang cetak `4.0–4.2 mm`, kedalaman `5.0 mm`) di 4 sudut luar enclosure untuk menyatukan frame depan dan sasis kompartemen belakang.
3. **Penyusutan Filamen (Shrinkage Allowance):**
   * Jika mencetak dengan **PETG**, gunakan skala `100.2%` – `100.4%`.
   * Jika mencetak dengan **ABS/ASA**, perhitungkan penyusutan `0.6% – 0.8%` pada slicer.

   ===========================================================================
1. TAMPAK BELAKANG (REAR VIEW) - PEMETAAN HARDWARE & TITIK PANAS (SoC)
===========================================================================
Skala dimensi bodi: 144.7 mm x 70.4 mm x 8.0 mm
Origin (0,0) di sudut kiri-bawah (persepsi melihat langsung punggung HP)

 Y (mm)
  144.7 +-----------------------[ 70.4 mm ]-----------------------+
        |  (R10.5 Corner Fillet)                 (Top Mic Cutout) |
  138.7 |  +--------------------+                                 |
        |  |  [CAMERA ISLAND]   |     *** THERMAL ZONE ***        | <- Posisi Power
        |  |  25 x 25 mm        |     (SoC SD765G Hotspot)        |    (Sisi Kanan)
        |  |  (Bump +1.1mm)     |     Area Heatsink / Fan 4010    |    Y: 99.7 - 109.7
  113.7 |  +--------------------+                                 |
        |    Jarak kiri: 6.0 mm          (O) FINGERPRINT          |
  100.7 |                                Diameter 10mm            |
        |                               (Tengah: X=35.2)          | <- Posisi Volume
        |                                                         |    (Sisi Kanan)
        |                                                         |    Y: 70.0 - 90.0
   80.0 |                                                         |
        |                                                         |
        |                                                         |
   47.0 |  [SIM TRAY]                                             |
        |  12 x 3 mm                                              |
   35.0 |  Y: 35.0 - 47.0                                         |
        |                                                         |
        |                                                         |
    0.0 +---------------------------------------------------------+
        X=0 mm                                                  X=70.4 mm


===========================================================================
2. TAMPAK SISI (PROFIL TEPI KANAN, KIRI, & BAWAH)
===========================================================================

[SISI KANAN - TOMBOL FISIK]
Top                                                                     Bottom
 +--------------+-----------+----------------+--------------------------+
 | Offset 35.0  | POWER     | Jarak: 9.7 mm  | VOLUME ROCKER            | Sisa ke bawah:
 | (Fillet R10) | 10 x 3 mm |                | 20 x 3 mm                | 70.0 mm
 +--------------+-----------+----------------+--------------------------+
 Y=144.7        Y=109.7     Y=99.7           Y=90.0                     Y=0.0

[SISI KIRI - SLOT AKSES SIM]
Top                                                                     Bottom
 +-------------------------------------------+------------+-------------+
 | Offset ke atas: 97.7 mm                   | SIM TRAY   | Sisa bawah: |
 |                                           | 12 x 3 mm  | 35.0 mm     |
 +-------------------------------------------+------------+-------------+
 Y=144.7                                     Y=47.0       Y=35.0        Y=0.0

[SISI BAWAH - PORT & GRILLE]
Tebal Z = 8.0 mm (CAD Pocket Z = 8.4 mm)
 +----------------------------------------------------------------------+
 |           Left Spk          USB-C PORT           Right Spk           |
 |          [==========]      [============]       [==========]         |
 |   <--- 14 mm --->   <-7mm-> <---13 mm---> <-7mm->   <--- 14 mm --->  |
 +----------------------------------------------------------------------+
 X=0 mm (Tepi Kiri)              X=35.2 mm (Center)             X=70.4 mm (Tepi Kanan)
 (Catatan: Cutout USB-C dibuat 13 x 7 mm untuk clearance overmold kabel)


===========================================================================
3. ARSITEKTUR CASING 2-PART (EXPLODED CAD ASSEMBLY VIEW)
===========================================================================

       [1. FRONT RETENTION FRAME]
       +=========================================+
       | (o) Baut M3                         (o) |
       |   +---------------------------------+   |
       |   |      LAYAR TETAP TERBUKA        |   | <- Bezel penahan kaca
       |   |       (Full Touchscreen)        |   |    depan (lip 1.2 mm)
       |   +---------------------------------+   |
       | (o) Baut M3                         (o) |
       +=========================================+
                           ||
                           \/ (Dudukan HP)
       +-----------------------------------------+
       |             GOOGLE PIXEL 5              |
       |         144.7 x 70.4 x 8.0 mm           |
       +-----------------------------------------+
                           ||
                           \/ (Pocket bodi 145.4 x 71.0 x 8.4 mm)
       [2. REAR BACKPACK CHASSIS (Tebal +30 s/d 35 mm)]
       +=========================================+
       | [H] Threaded Brass Insert M3        [H] |
       | +-------------------------------------+ |
       | |  POCKET KAMERA (Rongga 27 x 27 mm)  | |
       | +-------------------------------------+ |
       | |  COOLING BAY: FAN 4010 / 4020       | | <- Posisikan tepat di
       | |  Kisi-kisi exhaust buang panas SoC  | |    atas area motherboard
       | +-------------------------------------+ |
       | |  MODUL & BATTERY COMPARTMENT        | |
       | |  - Slot 18650 / Baterai LiPo        | | <- Ruang bebas modul &
       | |  - TP4056 BMS / 5V DC-DC Converter  | |    routing kabel
       | |  - Cutout RJ45 / USB-C Splitter Hub | |
       | +-------------------------------------+ |
       | [H]                                 [H] |
       +=========================================+