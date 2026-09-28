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

5. **Captive Push-Button & Rocker Bar (Sistem Tombol Braun / Cyberdeck):**
   * **Power Button Cap (`Button_Power_Cap`):** Tombol kapsul independen dengan bibir penahan (*retaining lip*) di sisi dalam sasis, menonjol $1.4\text{ mm}$ ke luar dengan 3 micro-ribs vertikal untuk grip jempol.
   * **Volume Rocker Bar (`Button_Volume_Rocker`):** Batang rocker memanjang dengan tumpu pivot di tengah dan 2 plunger terpisah untuk Volume Up & Down, dilengkapi embossed "+" dan "-" serta cekungan ergonomis di tengah.
   * **Mekanisme Drop-In Track:** Tombol dimasukkan dari atas (*slide-in channel*) saat perakitan dan terkunci paten setelah *Front Bezel* dibaut.
6. **Refined SIM Tray Slot & Ejector Funnel:**
   * Lubang akses SIM tray di dinding kanan diubah menjadi profil kapsul halus dengan *trumpet chamfer / finger dish* $45^\circ$ di bibir luar.
   * Dilengkapi corong pemandu pin ejector ($\varnothing 2.8\text{ mm} \to \varnothing 1.4\text{ mm}$) untuk mempermudah mencolok jarum SIM tray tanpa mencakar sasis.
7. **Redesigned Bottom I/O (USB-C & Dual Acoustic Speaker/Mic Stadium Capsules):**
   * **Port USB-C:** Lubang kotak lama digantikan oleh profil **Stadium Capsule ($13.6 \times 6.6\text{ mm}$, $R = 3.3\text{ mm}$)** dengan **$45^\circ$ Trumpet Flare Lead-in ($16.6 \times 8.2\text{ mm}$)**. Mempermudah colok kabel Type-C ber-collar tebal dan mencegah gesekan tajam.
   * **Dual Speaker & Mic Acoustic Ports:** Lubang kisi kotak kiri & kanan digantikan oleh **dua kapsul horizontal ($12.0 \times 3.8\text{ mm}$, $R = 1.9\text{ mm}$)** dengan **$45^\circ$ acoustic flare ($14.4 \times 5.4\text{ mm}$)** yang menjamin transmisi audio/mikrofon jernih tanpa difraksi suara.
   * **Keselarasan Visual:** Seluruh bukaan luar casing (Tombol, SIM tray, USB-C, Speaker) kini menganut bahasa desain kapsul/stadium seragam bergaya Braun/Dieter Rams.
8. **Home Swipe Notch (Bezel Depan Ergonomis):**
   * Cekungan jempol landai (*thumb scoop / scallop*) selebar **$38.0\text{ mm}$** sedalam **$1.4\text{ mm}$** pada bagian tengah bawah *Front Bezel* ($X = -19.0$ s/d $+19.0\text{ mm}$).
   * Menghilangkan ganjalan bibir bezel saat melakukan navigasi usap ke atas (*swipe up gesture*) untuk kembali ke Home screen Android.
9. **Fan Wire Routing Clips / Cable Baffles (Pengaman Kabel Internal):**
   * 2 unit cantelan kabel terintegrasi (*snap-in retention bridges*) pada plafon kompartemen bawah ($X = -6.0\text{ mm}$, $Y = 38.0\text{ mm}$ dan $Y = 92.0\text{ mm}$).
   * Menjepit rapi kabel DC jack dan saklar rocker agar terkunci di dinding kiri dan **tidak bisa bergeser menyentuh baling-baling kipas 3510**.
10. **Redesigned 6 Exhaust Vents (Kisi Pembuangan Kapsul):**
    * 6 lubang pembuangan udara panas di dinding kanan dirombak dari kotak tajam menjadi **Vertical Stadium Capsules ($5.2 \times 8.4\text{ mm}$, $R = 2.6\text{ mm}$)** dengan **$45^\circ$ Trumpet Chamfer ($6.8 \times 10.0\text{ mm}$)**.
    * Aliran udara panas keluar lebih aerodinamis, minim suara desing, dan bebas bridging saat di-print 3D.

---

## 5. Dua Varian Desain Tombol (Opsi A vs Opsi B)

Untuk memberikan fleksibilitas saat mencetak dan merakit, tersedia **dua varian sasis** yang keduanya 100% kompatibel dengan komponen lain (*Bottom Cover*, *Front Bezel*, heatsink SSD, dan dual fan):

| Fitur / Parameter | **Varian Opsi A (Captive Retro Sliders)** | **Varian Opsi B (Compliant Flexure — Print-in-Place)** |
| :--- | :--- | :--- |
| **Konsep** | Tombol mekanik perantara terpisah bergaya Braun / Game Boy | Tombol terintegrasi fleksibel menyatu dengan bodi sasis |
| **File CAD FreeCAD** | `Pixel5_DeckCase.FCStd` | `Pixel5_DeckCase_OptionB.FCStd` |
| **File STL Sasis** | `Pixel5_Main_Chassis.stl` | `Pixel5_Main_Chassis_OptionB.stl` |
| **Part Tambahan** | Perlu cetak `Pixel5_Button_Power.stl` & `Pixel5_Button_Volume.stl` | **NOL part tambahan** (100% monolitik dalam 1 kali print) |
| **Mekanisme Kerja** | Rel vertikal (*drop-in slide track*) dikunci oleh *Front Bezel* | Lengan pegas kantilever (*U-slit flexure blade* $1.4\text{ mm}$, celah $0.8\text{ mm}$) |
| **Kelebihan** | Sensasi klik mekanis sangat presisi, warna tombol bisa kontras | **Sangat simpel, anti-ribet, tidak ada part kecil yang bisa hilang** |

---

## 6. Daftar File Desain & Cetak (Outputs)

| Nama File | Format | Deskripsi |
| :--- | :--- | :--- |
| `Pixel5_DeckCase.FCStd` | FreeCAD Document | Model CAD utama Varian Opsi A (Captive Slider Buttons) |
| `Pixel5_DeckCase_OptionB.FCStd` | FreeCAD Document | Model CAD duplikat Varian Opsi B (Integrated Print-in-Place Buttons) |
| `Pixel5_Main_Chassis.stl` | STL Mesh | Sasis utama Opsi A (dengan track slide-in untuk tombol mandiri) |
| `Pixel5_Main_Chassis_OptionB.stl` | STL Mesh | Sasis utama Opsi B (dengan tombol fleksibel kantilever menyatu) |
| `Pixel5_Bottom_Cover.stl` | STL Mesh | Pelat penutup bawah + 4 kaki terintegrasi + kisi intake (universal A & B) |
| `Pixel5_Front_Bezel.stl` | STL Mesh | Frame bezel penahan layar sentuh depan (universal A & B) |
| `Pixel5_Button_Power.stl` | STL Mesh | Tombol daya mandiri untuk Opsi A (dengan retaining lip & ribs) |
| `Pixel5_Button_Volume.stl` | STL Mesh | Rocker volume mandiri untuk Opsi A (dengan pivot & tactile "+ / -") |
| `Pixel5_DeckCase_Enclosure.step` | STEP AP214 | File assembly STEP universal untuk Varian Opsi A |
| `Pixel5_DeckCase_OptionB.step` | STEP AP214 | File assembly STEP universal untuk Varian Opsi B |

---

## 7. Rekomendasi Cetak 3D & Fabrikasi

* **Bahan Cetak:** Disarankan **PETG** atau **ABS/ASA** karena memiliki ketahanan termal tinggi ($>75^\circ\text{C}$) saat menerima panas continuous dari heatsink, serta elastisitas alami (*springback*) yang sangat baik untuk lengan kantilever Opsi B.
* **Infill & Walls:** Minimal 4 perimeter / wall loops, infill $30–40\%$ (Gyroid / Grid).
* **Hardware Fasteners:**
  * 4x Baut **M3 x 30 mm** (Socket Head Cap Screw).
  * 4x **Brass Threaded Heat-Set Inserts M3** ($\varnothing 4.0–4.2\text{ mm}$, kedalaman $3.0–4.0\text{ mm}$) dipasang pada lubang blind hole di sisi belakang *Front Bezel*.
  * 4x Rubber pad anti-slip $\varnothing 7.0–7.5\text{ mm}$ untuk kaki bawah.
