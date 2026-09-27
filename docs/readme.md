# Google Pixel 5 - DeckCase 3D Enclosure Specification & Assembly Guide

Dokumentasi teknis perancangan casing 3D printer (*appliance/server/router deck enclosure*) untuk **Google Pixel 5**. Casing ini mengusung arsitektur **2-Tier Compartment** (lantai atas untuk smartphone, lantai bawah untuk modul elektronika & sistem pendingin aktif) dengan sistem penguncian baut M3 dari belakang (*back-fastening*).

---

## 1. Arsitektur Casing (3-Piece Sandwich System)

```text
       [ 1. FRONT RETENTION BEZEL ]  (Tebal 3.0 mm, Lip 1.2 mm menahan kaca)
                   ||
                   \/ (Dudukan HP)
       [ GOOGLE PIXEL 5 PHONE ]      (144.7 x 70.4 x 8.0 mm)
                   ||
                   \/ (Pocket 145.4 x 71.0 x 8.4 mm)
       [ 2. MAIN CHASSIS ]           (Sekat Lantai 2.6 mm + Shroud Kamera + Cavity Bawah 15 mm)
                   ||
                   \/ (Thermal Contact)
       [ HEATSINK SSD & FAN 3510/4010 ] + [ MODUL STEP-DOWN / DC-DC ]
                   ||
                   \/ (Tutup Bawah)
       [ 3. BOTTOM COVER WITH FEET ] (Plat 2.5 mm + 4 Kaki Elevated 6.0 mm + Kisi Intake)
```

---

## 2. Pemetaan Kompartemen & Tata Letak (Rear View Orientation)

Orientasi koordinat dan penempatan komponen dilihat langsung dari **Punggung HP (Tampak Belakang)**:

```text
  Y (mm)
  145.4 +-----------------------[ 71.0 mm ]-----------------------+
        |  [CAMERA SHROUD]       |     [AREA MERAH: HOTSPOT SoC]  |
        |  Window 26.5 x 26.5 mm |     Qualcomm Snapdragon 765G   |
        |  Terisolasi debu       |     Fan 3010 / 3510 / 4010     | <- Tombol Power
  105.0 |  Bibir pelindung +1.5  |     Intake dari kolong bawah   |    (Sisi Kiri)
        +------------------------+--------------------------------+
        |                        |     [SLOT HEATSINK SSD]        |
        |  [KOMPARTEMEN MODUL]   |     Ukuran: 70 x 22 x 4 mm     | <- Tombol Volume
        |  Area Kosong Lega:     |     Sirip vertikal menyalurkan |    (Sisi Kiri)
        |  42 mm (X) x 100 mm (Y)|     aliran udara ke bawah      |
        |  - Stepdown Mini-360   |     Thermal Window Langsung    |
        |  - DC Jack / PD Board  |     nempel ke bodi aluminium   |
        |  - Dummy Batt / BMS    |                                |
   32.0 |  - Jalur kabel         |                                |
        +------------------------+--------------------------------+
        |          [PORT USB-C (13x7 mm) & DUAL SPEAKER]          |
    0.0 +---------------------------------------------------------+
        X = -35.5 mm (Sisi Kiri)       X = 0      X = +35.5 mm (Sisi Kanan)
```

---

## 3. Spesifikasi Maksimal Pendingin (Cooling Dimension Limits)

### A. Area Merah (Hotspot SoC Snapdragon 765G)
* **Koordinat Area:** $X = +6.0\text{ mm}$ s/d $+32.0\text{ mm}$, $Y = 106.0\text{ mm}$ s/d $142.0\text{ mm}$.
* **Ruang Fisik Tersedia:** Lebar $39.4\text{ mm}$ (dari tepi kanan modul kamera ke tepi kanan bodi HP), Tinggi $40.0–42.0\text{ mm}$.
* **Rekomendasi & Batas Maksimal Kipas:**
  * **Fan 3010 ($30 \times 30 \times 10\text{ mm}$):** Sangat lega, clearance aman ke semua dinding.
   * **Dual Fan 3510 ($35 \times 35 \times 10\text{ mm}$ x2) [Model Terpasang di CAD]:**
     * **Fan 1 (Atas):** Tepat di atas hotspot SoC Snapdragon 765G ($Y = 124\text{ mm}$).
     * **Fan 2 (Bawah):** Tepat di atas sirip Heatsink SSD ($Y = 68\text{ mm}$).
     * **Air Plenum Gap:** Sisa celah udara bebas **$4.0\text{ mm}$** ke penutup bawah, mencegah *air choking* dan suara desing turbulen.
   * **Fan 4010 / 4020 ($40 \times 40 \times 10/20\text{ mm}$):** Ukuran maksimal alternatif. Di kompartemen bawah casing (lebar rongga dalam $72.0\text{ mm}$) muat dengan sangat lega.
   * **Blower 4010 (Centrifugal):** Opsi alternatif terbaik untuk meniupkan udara horizontal lurus menyusuri celah sirip heatsink SSD ke arah bawah.

### B. Slot Heatsink SSD M.2 (Area Kuning)
* **Dimensi Heatsink Terpasang:** **$70.0\text{ mm} \times 22.0\text{ mm} \times 4.0\text{ mm}$** (sirip aluminium vertikal).
* **Thermal Window CAD:** Dibuka seluas **$72.0\text{ mm} \times 24.0\text{ mm}$** pada sekat lantai tengah agar heatsink menempel langsung (*direct contact*) ke punggung aluminium Pixel 5 dengan perantara *thermal pad* tipis ($0.5–1.0\text{ mm}$) atau *thermal paste*.
* **Batas Maksimal Dimensi Heatsink:**
  * **Panjang Maksimal:** $72.0\text{ mm}$ (rentang $Y = 32.0$ s/d $104.0\text{ mm}$).
  * **Lebar Maksimal:** $24.0\text{ mm}$ (dapat diekspansi hingga $26.0\text{ mm}$ tanpa mengganggu sensor fingerprint).
  * **Ketebalan Heatsink:** Standar $4.0\text{ mm}$. Dengan kedalaman kompartemen bawah yang diperdalam menjadi **$18.0\text{ mm}$**, heatsink dengan sirip tebal ($6.0–12.0\text{ mm}$) muat dengan leluasa.

---

## 4. Fitur Khusus Enclosure

1. **Dust & Airflow Isolation Camera Shroud:**
   * Dinding selubung (*chimney*) terisolasi dari sekat lantai tengah menembus penutup bawah dengan *aperture* $26.5 \times 26.5\text{ mm}$.
   * Melindungi lensa kamera agar tidak terhalang (*no vignetting*), mencegah lensa tergores meja (bibir shroud $+1.5\text{ mm}$), dan **mencegah debu dari sirkulasi kipas masuk mengotori modul kamera**.
2. **Elevated Standoff Feet (Kaki Kolong 6.0 mm):**
   * 4 kaki silinder terintegrasi pada pelat penutup bawah mengangkat casing setinggi $6.0\text{ mm}$ dari permukaan meja.
   * Menjamin pasokan udara dingin (*fresh air intake*) lancar tanpa terjadi *air starvation*.
   * Dilengkapi cekungan (*recess*) $\varnothing 7.5\text{ mm}$ sedalam $2.5\text{ mm}$ untuk memasang bantalan karet anti-slip (*rubber feet pad*).
3. **Sistem Aliran Udara Terarah (*Wind Tunnel Airflow*):**
   * **Intake:** Kipas menyedot udara dingin dari kolong bawah meja lewat kisi-kisi penutup bawah.
   * **Heat Exchange:** Udara dingin bertekanan ditiupkan langsung ke area SoC dan menyusuri celah sirip vertikal heatsink SSD.
   * **Exhaust:** Udara panas dibuang keluar lewat **5 slot kisi ventilasi ($15 \times 5\text{ mm}$)** di dinding samping kanan, menjauhi kompartemen baterai dan modul elektronika.
4. **Kompartemen Modul Elektronika & Kontrol Daya (Area Kiri):**
   * Ruang kosong bersih seluas $42.0\text{ mm} \times 100.0\text{ mm} \times 15.0\text{ mm}$ di samping kiri heatsink.
   * **DC 12V Barrel Jack (5.5x2.1 mm):** Lubang panel mount $\varnothing 8.2\text{ mm}$ di dinding bawah sisi kiri ($X = -22.0\text{ mm}$, $Z = -18.5\text{ mm}$), sejajar dengan port USB-C.
   * **Fan Mini Toggle Switch:** Lubang saklar tuas $\varnothing 6.2\text{ mm}$ di dinding samping kiri bawah ($Y = 25.0\text{ mm}$, $Z = -18.5\text{ mm}$) untuk kontrol manual on/off kipas.
   * **Dual 1/4"-20 Tripod Mounts (Kuningan Brass Insert):**
     * **Orientasi Landscape:** Lubang insert $\varnothing 8.5\text{ mm} \times 9.0\text{ mm}$ dengan *reinforced internal boss* di dinding samping kiri ($Y = 50.0\text{ mm}$, $Z = -18.5\text{ mm}$) untuk posisi monitor meja / deck horizontal.
     * **Orientasi Portrait:** Lubang insert $\varnothing 8.5\text{ mm} \times 8.0\text{ mm}$ dengan *reinforced boss* di pelat penutup bawah ($X = -12.0\text{ mm}$, $Y = 55.0\text{ mm}$) untuk mounting tripod vertikal.

---

## 5. Daftar File Desain & Cetak (Outputs)

| Nama File | Format | Deskripsi |
| :--- | :--- | :--- |
| `Pixel5_DeckCase.FCStd` | FreeCAD Document | File project CAD 3D parametrik lengkap (FreeCAD v1.1) |
| `Pixel5_Main_Chassis.stl` | STL Mesh | Sasis utama (Pocket HP, Sekat Thermal, Shroud Kamera, Cavity Modul) |
| `Pixel5_Bottom_Cover.stl` | STL Mesh | Pelat penutup bawah + 4 kaki terintegrasi + kisi intake |
| `Pixel5_Front_Bezel.stl` | STL Mesh | Frame bezel penahan layar sentuh depan |
| `Pixel5_DeckCase_Enclosure.step` | STEP AP214 | File CAD universal multi-solid untuk software CAD lain |

---

## 6. Panduan Cetak 3D & Perakitan (Assembly)

* **Bahan Cetak:** Disarankan **PETG** atau **ABS/ASA** karena memiliki ketahanan termal tinggi ($>75^\circ\text{C}$) saat menerima panas continuous dari heatsink.
* **Infill & Walls:** Minimal 4 perimeter / wall loops, infill $30–40\%$ (Gyroid / Grid).
* **Hardware Fasteners:**
  * 4x Baut **M3 x 30 mm** (Socket Head Cap Screw).
  * 4x **Brass Threaded Heat-Set Inserts M3** ($\varnothing 4.0–4.2\text{ mm}$, kedalaman $3.0–4.0\text{ mm}$) dipasang pada lubang blind hole di sisi belakang *Front Bezel*.
  * 4x Rubber pad anti-slip $\varnothing 7.0–7.5\text{ mm}$ untuk kaki bawah.
