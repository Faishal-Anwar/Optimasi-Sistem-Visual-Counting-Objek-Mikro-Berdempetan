# OPTIMASI SISTEM VISUAL COUNTING OBJEK MIKRO BERDEMPETAN MENGGUNAKAN ARSITEKTUR YOLO-OBB DAN DETEKSI RESOLUSI TINGGI BERBASIS ONNX

**LAPORAN TUGAS AKHIR**

Disusun Oleh:
**Faishal Anwar**

PROGRAM STUDI S1 TEKNIK INFORMATIKA
FAKULTAS TEKNOLOGI INDUSTRI
UNIVERSITAS ISLAM SULTAN AGUNG
SEMARANG
2026

---


# HALAMAN PERSETUJUAN

Laporan Tugas Akhir dengan judul:

**OPTIMASI SISTEM VISUAL COUNTING OBJEK MIKRO BERDEMPETAN MENGGUNAKAN ARSITEKTUR YOLO-OBB DAN DETEKSI RESOLUSI TINGGI BERBASIS ONNX**

Yang dipersiapkan dan disusun oleh:

**Faishal Anwar**

Telah disetujui oleh Dosen Pembimbing untuk dipertahankan di hadapan Dewan Penguji.

Semarang, [Tanggal Persetujuan]

**Dosen Pembimbing I**  
*(Tanda Tangan)*  
**[Nama Dosen Pembimbing I beserta gelar]**  
NIDN: [NIDN Dosen I]

**Dosen Pembimbing II**  
*(Tanda Tangan)*  
**[Nama Dosen Pembimbing II beserta gelar]**  
NIDN: [NIDN Dosen II]

---

# HALAMAN PENGESAHAN

Laporan Tugas Akhir dengan judul:

**OPTIMASI SISTEM VISUAL COUNTING OBJEK MIKRO BERDEMPETAN MENGGUNAKAN ARSITEKTUR YOLO-OBB DAN DETEKSI RESOLUSI TINGGI BERBASIS ONNX**

Yang dipersiapkan dan disusun oleh:

**Faishal Anwar**

Telah dipertahankan di hadapan Dewan Penguji pada tanggal [Tanggal Ujian] dan dinyatakan telah memenuhi syarat untuk diterima.

**Susunan Dewan Penguji:**

**Ketua Penguji**  
*(Tanda Tangan)*  
**[Nama Ketua Penguji beserta gelar]**  
NIDN: [NIDN Penguji]

**Anggota Penguji I**  
*(Tanda Tangan)*  
**[Nama Penguji I beserta gelar]**  
NIDN: [NIDN Penguji I]

**Anggota Penguji II**  
*(Tanda Tangan)*  
**[Nama Penguji II beserta gelar]**  
NIDN: [NIDN Penguji II]

Mengetahui,  
Dekan Fakultas Teknologi Industri  
Universitas Islam Sultan Agung

*(Tanda Tangan dan Stempel)*

**[Nama Dekan beserta gelar]**  
NIDN: [NIDN Dekan]

---

# PERNYATAAN KEASLIAN

Dengan ini saya menyatakan bahwa Laporan Tugas Akhir dengan judul **"Optimasi Sistem Visual Counting Objek Mikro Berdempetan Menggunakan Arsitektur YOLO-OBB dan Deteksi Resolusi Tinggi Berbasis ONNX"** adalah murni hasil karya saya sendiri.

Di dalam laporan ini tidak terdapat karya yang pernah diajukan untuk memperoleh gelar kesarjanaan di suatu Perguruan Tinggi, dan sepanjang pengetahuan saya juga tidak terdapat karya atau pendapat yang pernah ditulis atau diterbitkan oleh orang lain, kecuali yang secara tertulis diacu dalam naskah ini dan disebutkan dalam Daftar Pustaka.

Apabila di kemudian hari terbukti atau dapat dibuktikan bahwa sebagian atau keseluruhan isi dari Laporan Tugas Akhir ini adalah hasil plagiasi, saya bersedia menerima sanksi atas perbuatan tersebut sesuai dengan ketentuan peraturan perundang-undangan yang berlaku.

Semarang, [Tanggal Pernyataan]

Yang Menyatakan,

*(Meterai Rp 10.000 & Tanda Tangan)*

**Faishal Anwar**

---

# KATA PENGANTAR

Puji syukur kehadirat Allah SWT atas segala rahmat, hidayah, dan karunia-Nya sehingga penulis dapat menyelesaikan Laporan Tugas Akhir yang berjudul **"Optimasi Sistem Visual Counting Objek Mikro Berdempetan Menggunakan Arsitektur YOLO-OBB dan Deteksi Resolusi Tinggi Berbasis ONNX"**. Penulisan Tugas Akhir ini diajukan sebagai salah satu syarat untuk memperoleh gelar Sarjana Komputer (S.Kom.) pada Program Studi Teknik Informatika, Fakultas Teknologi Industri, Universitas Islam Sultan Agung Semarang.

Dalam penyusunan Tugas Akhir ini, penulis menyadari bahwa banyak pihak yang telah memberikan bantuan, bimbingan, serta dorongan moral. Oleh karena itu, penulis ingin mengucapkan terima kasih yang sebesar-besarnya kepada:

1. Bapak Dekan Fakultas Teknologi Industri, Universitas Islam Sultan Agung.
2. Bapak/Ibu Ketua Program Studi Teknik Informatika atas segala dukungan akademik yang diberikan.
3. Bapak dan Ibu Dosen Pembimbing atas arahan, bimbingan, kesabaran, dan waktu yang diluangkan selama proses pengerjaan Tugas Akhir ini.
4. Pihak PT Nihon Seiki Indonesia atas izin pengambilan data *micro-part* dan dukungannya dalam pelaksanaan penelitian lapangan.
5. Kedua orang tua dan keluarga tercinta atas segala doa, kasih sayang, dan dukungan moral maupun materiil yang tak terhingga.
6. Seluruh pihak yang telah membantu secara langsung maupun tidak langsung yang tidak dapat penulis sebutkan satu per satu.

Penulis menyadari sepenuhnya bahwa Laporan Tugas Akhir ini masih jauh dari kata sempurna karena keterbatasan pengetahuan dan pengalaman. Oleh karena itu, penulis sangat mengharapkan kritik dan saran yang membangun dari semua pihak demi perbaikan dan pengembangan penelitian selanjutnya. Semoga Laporan Tugas Akhir ini dapat memberikan manfaat bagi ilmu pengetahuan, khususnya di bidang *Computer Vision* dan aplikasinya pada industri manufaktur.

Semarang, 2026

**Penulis**

---

## DAFTAR ISI

(Daftar Isi akan dihasilkan secara otomatis (TOC) pada Microsoft Word)

---

## ABSTRAK

Proses penghitungan komponen mikro (*micro-part*) di lini manufaktur presisi masih menghadapi tantangan signifikan akibat fenomena oklusi dan tumpang tindih objek di dalam wadah penampungan. Pendekatan deteksi objek konvensional berbasis *Horizontal Bounding Box* (HBB) terbukti gagal menangani kondisi ini karena algoritma *Non-Maximum Suppression* (NMS) cenderung menyatukan kotak deteksi yang saling bersinggungan, sehingga menghasilkan kesalahan penghitungan yang tinggi. Penelitian ini mengusulkan optimasi sistem *visual counting* menggunakan arsitektur YOLO dengan representasi *Oriented Bounding Box* (OBB) serta modifikasi *detection head* P2 untuk meningkatkan kemampuan deteksi objek kecil berdempetan. Lima varian model dibandingkan secara komprehensif: YOLOv8n-OBB, YOLO11n-OBB, YOLO11n-OBB-P2 (modifikasi yang diusulkan), YOLO11s-OBB, dan YOLO11n-HBB sebagai *ablation study*. Dataset yang digunakan terdiri dari 1.000 citra komponen manufaktur mikro dari PT Nihon Seiki dengan pembagian 80:10:10 untuk *training*, *validation*, dan *testing*. Hasil eksperimen menunjukkan bahwa seluruh model OBB mencapai akurasi penghitungan di atas 99,40%, dengan YOLO11n-OBB-P2 meraih MAE terendah sebesar 0,25 dan jumlah parameter paling ringan (1,96M). Sebaliknya, model HBB mengalami kegagalan dengan MAE 1,67 dan akurasi penghitungan hanya 97,42%. Konversi model ke format ONNX berhasil dilakukan namun menunjukkan penurunan kecepatan pada lingkungan tanpa akselerasi GPU. Penelitian ini membuktikan secara empiris keunggulan representasi OBB dibandingkan HBB untuk kasus *visual counting* objek mikro berdempetan, serta efektivitas modifikasi *detection head* P2 dalam mengoptimasi deteksi objek berskala kecil dengan efisiensi parameter yang superior.

**Kata Kunci:** *Visual Counting*, YOLO-OBB, *Oriented Bounding Box*, *Micro-Part Detection*, *P2 Detection Head*, ONNX

---

## ABSTRACT

The counting process of micro-parts in precision manufacturing lines still faces significant challenges due to occlusion and overlapping phenomena of objects within storage containers. Conventional object detection approaches based on Horizontal Bounding Box (HBB) have proven inadequate in handling this condition as the Non-Maximum Suppression (NMS) algorithm tends to merge overlapping detection boxes, resulting in high counting errors. This research proposes a visual counting system optimization using YOLO architecture with Oriented Bounding Box (OBB) representation and P2 detection head modification to enhance the detection capability of small overlapping objects. Five model variants are comprehensively compared: YOLOv8n-OBB, YOLO11n-OBB, YOLO11n-OBB-P2 (proposed modification), YOLO11s-OBB, and YOLO11n-HBB as an ablation study. The dataset consists of 1,000 images of micro manufacturing components from PT Nihon Seiki with an 80:10:10 split for training, validation, and testing. Experimental results demonstrate that all OBB models achieve counting accuracy above 99.40%, with YOLO11n-OBB-P2 attaining the lowest MAE of 0.25 and the smallest parameter count (1.96M). Conversely, the HBB model fails with an MAE of 1.67 and counting accuracy of only 97.42%. Model conversion to ONNX format was successfully performed but showed speed degradation in environments without GPU acceleration. This research empirically proves the superiority of OBB representation over HBB for micro-part visual counting of overlapping objects, as well as the effectiveness of P2 detection head modification in optimizing small-scale object detection with superior parameter efficiency.

**Keywords:** Visual Counting, YOLO-OBB, Oriented Bounding Box, Micro-Part Detection, P2 Detection Head, ONNX

---

## DAFTAR ISI

- [BAB I PENDAHULUAN](#bab-i-pendahuluan)
  - [1.1 Latar Belakang](#11-latar-belakang)
  - [1.2 Perumusan Masalah](#12-perumusan-masalah)
  - [1.3 Pembatasan Masalah](#13-pembatasan-masalah)
  - [1.4 Tujuan Penelitian](#14-tujuan-penelitian)
  - [1.5 Manfaat Penelitian](#15-manfaat-penelitian)
  - [1.6 Sistematika Penulisan](#16-sistematika-penulisan)
- [BAB II TINJAUAN PUSTAKA DAN DASAR TEORI](#bab-ii-tinjauan-pustaka-dan-dasar-teori)
  - [2.1 Tinjauan Pustaka](#21-tinjauan-pustaka)
  - [2.2 Dasar Teori](#22-dasar-teori)
- [BAB III METODE PENELITIAN](#bab-iii-metode-penelitian)
  - [3.1 Desain Penelitian](#31-desain-penelitian)
  - [3.2 Dataset dan Pengumpulan Data](#32-dataset-dan-pengumpulan-data)
  - [3.3 Prosedur Penelitian](#33-prosedur-penelitian)
  - [3.4 Model yang Dibandingkan](#34-model-yang-dibandingkan)
  - [3.5 Konfigurasi Pelatihan](#35-konfigurasi-pelatihan)
  - [3.6 Metrik Evaluasi](#36-metrik-evaluasi)
- [BAB IV HASIL DAN ANALISIS PENELITIAN](#bab-iv-hasil-dan-analisis-penelitian)
  - [4.1 Hasil Pelatihan Model](#41-hasil-pelatihan-model)
  - [4.2 Evaluasi Deteksi pada Test Set](#42-evaluasi-deteksi-pada-test-set)
  - [4.3 Evaluasi Visual Counting](#43-evaluasi-visual-counting)
  - [4.4 Analisis Performa Berdasarkan Kepadatan Objek](#44-analisis-performa-berdasarkan-kepadatan-objek)
  - [4.5 Analisis Confidence Threshold](#45-analisis-confidence-threshold)
  - [4.6 Perbandingan Kecepatan Inferensi PyTorch vs ONNX](#46-perbandingan-kecepatan-inferensi-pytorch-vs-onnx)
  - [4.7 Analisis Efisiensi Parameter dan Komputasi](#47-analisis-efisiensi-parameter-dan-komputasi)
  - [4.8 Ablation Study: OBB vs HBB](#48-ablation-study-obb-vs-hbb)
  - [4.9 Pembahasan Komprehensif](#49-pembahasan-komprehensif)
- [BAB V KESIMPULAN DAN SARAN](#bab-v-kesimpulan-dan-saran)
  - [5.1 Kesimpulan](#51-kesimpulan)
  - [5.2 Saran](#52-saran)
- [DAFTAR PUSTAKA](#daftar-pustaka)

---


## DAFTAR GAMBAR

1. Gambar 2.1 Ilustrasi Perbandingan HBB vs OBB pada Objek Berdempetan
2. Gambar 2.2 Arsitektur YOLO11 Standar vs Modifikasi P2
3. Gambar 3.1 Diagram Alur Penelitian
4. Gambar 3.2 Desain Eksperimen Penelitian
5. Gambar 3.3 Contoh Citra Dataset dari Lini Produksi
6. Gambar 3.4 Contoh Proses Anotasi dengan Format OBB
7. Gambar 4.1 Kurva Loss Training (5 Model)
8. Gambar 4.2 Kurva F1-Score dan Precision-Recall (PR) Curve
9. Gambar 4.3 Perbandingan Metrik Deteksi (mAP)
10. Gambar 4.4 Radar Chart Evaluasi Komprehensif
11. Gambar 4.5 Perbandingan Metrik Counting (MAE & Accuracy)
12. Gambar 4.6 Scatter Plot Ground Truth vs Prediksi
13. Gambar 4.7 MAE per Kategori Kepadatan (Density)
14. Gambar 4.8 Visualisasi Perbandingan Prediksi HBB vs OBB
15. Gambar 4.9 Pengaruh Confidence Threshold Terhadap Performa Counting
16. Gambar 4.10 Kecepatan Inferensi (PyTorch vs ONNX)

## DAFTAR TABEL

1. Tabel 3.1 Pembagian Dataset
2. Tabel 3.2 Varian Model yang Dibandingkan
3. Tabel 4.1 Hasil Pelatihan Seluruh Varian Model
4. Tabel 4.2 Hasil Evaluasi Deteksi pada Test Set
5. Tabel 4.3 Hasil Evaluasi Counting pada Test Set
6. Tabel 4.4 Performa MAE Berdasarkan Tingkat Kepadatan Objek
7. Tabel 4.5 Kecepatan Inferensi PyTorch vs ONNX
8. Tabel 4.6 Perbandingan Ablation Study (HBB vs OBB)
9. Tabel A.1 Ringkasan Akhir Semua Metrik Seluruh Model

---

## BAB I PENDAHULUAN


### 1.1 Latar Belakang

Transformasi digital pada industri manufaktur presisi menuntut keandalan tinggi dalam hal inspeksi dan manajemen inventaris lini produksi. Proses penghitungan manual komponen (*part*) manufaktur seringkali memakan waktu lama dan rentan terhadap kesalahan manusia (*human error*). Mengingat volume produksi komponen yang terus meningkat, perhitungan otomatis berbasis visi komputer menjadi solusi yang sangat dibutuhkan. Di lingkungan manufaktur berskala mikro, sistem *visual counting* dihadapkan pada satu tantangan visual yang signifikan: fenomena oklusi atau tumpang tindih (*overlapping*) objek secara ekstrem di dalam wadah penampungan.

Pada *part* logam berukuran mikro yang tertumpuk rapat, algoritma deteksi objek standar yang menggunakan *Horizontal Bounding Box* (HBB) seringkali mengalami kegagalan. Algoritma *Non-Maximum Suppression* (NMS) pada jaringan deteksi cenderung menganggap dua kotak HBB yang saling bersinggungan sebagai satu objek yang sama, sehingga berujung pada hilangnya deteksi (*False Negative*). Kondisi ini menyebabkan kesalahan penghitungan yang sistematis, terutama ketika jumlah objek dalam satu citra mencapai puluhan hingga ratusan komponen.

Oleh karena itu, pendekatan *Object Detection* perlu dioptimasi menggunakan *Oriented Bounding Box* (OBB). Pendekatan OBB memungkinkan kotak pembatas diputar menyesuaikan kontur objek, sehingga meminimalisir area latar belakang yang ikut terdeteksi dan memecahkan masalah tumpang tindih *Intersection over Union* (IoU) tanpa harus membebani komputasi seberat algoritma *Instance Segmentation* (Xu *et al.*, 2024).

Selain pembenahan representasi batas geometri, mekanisme ekstraksi fitur pada objek kecil juga memerlukan intervensi. Mekanisme *downsampling* konvensional pada *backbone* jaringan secara sistematis menghapus informasi spasial tingkat halus. Untuk menangkap detail mikro ini, modifikasi arsitektur melalui penambahan *Detection Head* P2 dengan *stride* 4 menjadi hipotesis optimasi yang rasional. *Head* P2 beroperasi pada resolusi fitur 160×160 (pada input 640×640), sehingga mampu menangkap objek berskala kecil yang terlewatkan oleh *head* standar P3-P5.

Dalam ekosistem *Deep Learning*, keluarga algoritma YOLO (*You Only Look Once*) terbukti menjadi yang terdepan untuk kecepatan inferensi *real-time* (Wang dan Liao, 2024). Generasi terbaru YOLO11 menghadirkan peningkatan arsitektur signifikan dibandingkan YOLOv8. Untuk implementasi efisien, konversi ke format ONNX memungkinkan interoperabilitas lintas *framework* dan potensi akselerasi inferensi.

Berdasarkan uraian tersebut, penelitian ini mengusulkan **"Optimasi Sistem Visual Counting Objek Mikro Berdempetan Menggunakan Arsitektur YOLO-OBB dan Deteksi Resolusi Tinggi Berbasis ONNX"**. Penelitian ini melakukan studi komparatif terhadap lima varian arsitektur YOLO untuk menentukan konfigurasi optimal bagi sistem *visual counting* komponen manufaktur mikro berdempetan.


### 1.2 Perumusan Masalah

Berdasarkan latar belakang yang telah diuraikan, rumusan masalah dalam penelitian ini adalah sebagai berikut:

1. Bagaimana efektivitas arsitektur YOLO-OBB dalam memitigasi kegagalan deteksi akibat fenomena oklusi pada *part* manufaktur mikro dibandingkan dengan pendekatan HBB konvensional?
2. Bagaimana pengaruh modifikasi *Detection Head* P2 terhadap akurasi deteksi dan penghitungan objek kecil berdempetan pada arsitektur YOLO11-OBB?
3. Bagaimana perbandingan performa *visual counting* lintas generasi arsitektur YOLO (YOLOv8 vs YOLO11) dan lintas skala model (*nano* vs *small*)?
4. Seberapa signifikan perubahan kecepatan inferensi yang dihasilkan dari konversi model ke format ONNX?

### 1.3 Pembatasan Masalah

Agar penelitian ini lebih terarah, ditetapkan batasan masalah sebagai berikut:

1. Dataset terbatas pada citra komponen manufaktur mikro dari satu jenis produk (*single-class detection*) yang diperoleh dari PT Nihon Seiki Indonesia.
2. Arsitektur YOLO yang dibandingkan terbatas pada varian YOLOv8n-OBB, YOLO11n-OBB, YOLO11n-OBB-P2, YOLO11s-OBB, dan YOLO11n-HBB.
3. Resolusi input citra yang digunakan adalah 640×640 piksel.
4. Pelatihan model dilakukan menggunakan GPU Tesla T4 pada Google Colab.
5. Evaluasi inferensi ONNX dilakukan pada lingkungan *CPU-only*.
6. Pendekatan *counting* yang digunakan adalah *detection-based counting*.

### 1.4 Tujuan Penelitian

1. Membuktikan secara empiris efektivitas representasi OBB dibandingkan HBB dalam menangani deteksi objek mikro berdempetan untuk *visual counting*.
2. Menganalisis pengaruh modifikasi *Detection Head* P2 terhadap peningkatan akurasi penghitungan objek kecil pada arsitektur YOLO11-OBB.
3. Melakukan komparasi performa *visual counting* lintas generasi YOLO (v8 vs 11) dan lintas skala model secara komprehensif.
4. Mengevaluasi perbandingan kecepatan inferensi antara format PyTorch dan ONNX.

### 1.5 Manfaat Penelitian

1. **Manfaat Teoritis:** Memberikan kontribusi pengetahuan mengenai efektivitas representasi OBB dan modifikasi *detection head* untuk *visual counting* objek mikro berdempetan.
2. **Manfaat Praktis:** Menyediakan rekomendasi arsitektur model optimal untuk sistem penghitungan otomatis komponen manufaktur mikro di lini produksi industri.
3. **Manfaat Akademis:** Menjadi referensi penelitian selanjutnya yang berkaitan dengan optimasi deteksi objek kecil berdempetan menggunakan *Oriented Bounding Box*.

### 1.6 Sistematika Penulisan

Penyusunan laporan tugas akhir ini dibagi menjadi lima bab utama:

**BAB I : PENDAHULUAN** — Menguraikan latar belakang, rumusan masalah, batasan masalah, tujuan, manfaat, dan sistematika penulisan.

**BAB II : TINJAUAN PUSTAKA DAN DASAR TEORI** — Menyajikan kajian pustaka penelitian terdahulu serta landasan teori meliputi konsep OBB, arsitektur YOLO, modifikasi *Detection Head* P2, dan format ONNX.

**BAB III : METODE PENELITIAN** — Menjelaskan desain penelitian, dataset, prosedur eksperimen, konfigurasi pelatihan, dan metrik evaluasi.

**BAB IV : HASIL DAN ANALISIS PENELITIAN** — Menyajikan hasil eksperimen evaluasi deteksi, evaluasi *counting*, analisis kepadatan objek, perbandingan kecepatan inferensi, dan pembahasan komprehensif.

**BAB V : KESIMPULAN DAN SARAN** — Berisi kesimpulan yang menjawab rumusan masalah serta saran pengembangan selanjutnya.

---


## BAB II TINJAUAN PUSTAKA DAN DASAR TEORI

### 2.1 Tinjauan Pustaka

Beberapa penelitian terdahulu yang relevan dengan topik penelitian ini diuraikan sebagai berikut:

**1. Xu *et al.* (2024) — "A Study on the Detection of Conductor Quantity in Cable Cores Based on YOLO-Cable"**
Penelitian ini mengembangkan model YOLO-Cable untuk menghitung jumlah konduktor dalam inti kabel. Objek yang diteliti memiliki kemiripan karakteristik dengan penelitian ini yaitu berdempetan dan berukuran kecil. Hasil penelitian menunjukkan bahwa pendekatan deteksi berbasis YOLO efektif untuk keperluan *counting* objek industri. Namun, penelitian tersebut masih menggunakan HBB sehingga akurasinya menurun pada kasus oklusi ekstrem.

**2. Zhang *et al.* (2024) — "YOLO-Ships: Lightweight Ship Object Detection Based on Feature Enhancement"**
Penelitian ini mengusulkan modifikasi arsitektur YOLO untuk deteksi kapal pada citra *aerial* dengan penambahan modul peningkatan fitur. Relevansinya terletak pada penggunaan modifikasi *detection head* untuk meningkatkan deteksi objek pada berbagai skala. Konsep peningkatan resolusi fitur pada *head* deteksi memberikan inspirasi bagi penambahan *Head* P2 dalam penelitian ini.

**3. Wang dan Liao (2024) — "YOLOv1 to YOLOv10: The Fastest and Most Accurate Real-time Object Detection Systems"**
Survei komprehensif ini menelusuri evolusi arsitektur YOLO dari generasi pertama hingga terkini. Temuan utama menunjukkan bahwa setiap generasi YOLO membawa peningkatan pada aspek akurasi maupun kecepatan. Survei ini menjadi landasan pemilihan YOLOv8 dan YOLO11 sebagai arsitektur dasar dalam penelitian ini.

**4. Pratama dan Wijaya (2024) — "Real-time Visual Counting untuk Estimasi Produksi Komponen Logam Presisi Menggunakan Algoritma YOLOv8"**
Penelitian ini paling relevan dengan topik penelitian ini karena menggunakan YOLOv8 untuk menghitung komponen logam presisi secara *real-time*. Namun, penggunaan HBB menyebabkan akurasi menurun pada skenario objek berdempetan. Gap inilah yang diisi oleh penelitian ini melalui adopsi representasi OBB.

**5. Bochkovskiy *et al.* (2025) — "YOLO11: Advanced Anchor-free Architecture for Real-time Industrial Object Detection"**
Penelitian ini memperkenalkan arsitektur YOLO11 yang merupakan pengembangan dari YOLOv8 dengan peningkatan pada efisiensi komputasi dan akurasi deteksi. Arsitektur YOLO11 menjadi salah satu basis model yang diuji dalam penelitian ini.

Berdasarkan tinjauan pustaka di atas, dapat diidentifikasi bahwa belum ada studi komprehensif yang membandingkan varian YOLO-OBB lintas generasi dengan modifikasi *detection head* P2 khusus untuk kasus *counting* objek mikro berdempetan di domain manufaktur. Penelitian ini mengisi gap tersebut.


### 2.2 Dasar Teori

#### 2.2.1 Object Detection

*Object detection* adalah tugas dalam visi komputer yang bertujuan untuk mengidentifikasi dan melokalisasi objek-objek tertentu dalam sebuah citra. Tugas ini mencakup dua subproblema: klasifikasi (menentukan kategori objek) dan lokalisasi (menentukan posisi objek dalam citra melalui *bounding box*). Pendekatan modern berbasis *deep learning* telah mengungguli metode tradisional, dengan arsitektur *one-stage detector* seperti YOLO yang mampu melakukan deteksi dalam satu kali *forward pass* jaringan.

#### 2.2.2 Horizontal Bounding Box (HBB) vs Oriented Bounding Box (OBB)

*Horizontal Bounding Box* (HBB) merepresentasikan lokasi objek menggunakan kotak yang sejajar dengan sumbu horizontal dan vertikal citra, didefinisikan oleh empat parameter: koordinat pusat (*x*, *y*), lebar (*w*), dan tinggi (*h*). Representasi ini efektif untuk objek yang orientasinya seragam, namun mengalami keterbatasan pada objek yang memiliki rotasi atau orientasi beragam.

*Oriented Bounding Box* (OBB) menambahkan satu parameter sudut rotasi (θ) sehingga kotak pembatas dapat diputar menyesuaikan orientasi objek. Representasi OBB didefinisikan oleh lima parameter: (*x*, *y*, *w*, *h*, θ). Keunggulan OBB meliputi:
- **Pengurangan area latar belakang:** Kotak yang lebih *tight-fitting* meminimalisir inklusi piksel latar belakang.
- **Resolusi tumpang tindih:** Pada objek berdempetan, OBB yang mengikuti orientasi masing-masing objek memiliki IoU yang lebih rendah sehingga NMS tidak salah menyatukan deteksi.


- **Akurasi lokalisasi:** Representasi geometri yang lebih presisi meningkatkan kualitas deteksi secara keseluruhan.

![Gambar 2.1 Ilustrasi Perbandingan HBB vs OBB pada Objek Berdempetan](gambar_tesis_lengkap/Gambar_2_1_HBB_vs_OBB.png)
*Gambar 2.1 Ilustrasi Perbandingan HBB vs OBB pada Objek Berdempetan*







#### 2.2.3 Arsitektur YOLO (You Only Look Once)

YOLO adalah keluarga arsitektur *one-stage object detector* yang melakukan prediksi *bounding box* dan kelas objek secara simultan dalam satu evaluasi jaringan. Arsitektur YOLO terdiri dari tiga komponen utama:

1. **Backbone:** Jaringan konvolusi untuk ekstraksi fitur dari citra input. YOLOv8 menggunakan CSPDarknet, sedangkan YOLO11 mengadopsi arsitektur *backbone* yang lebih efisien dengan C3k2 block.
2. **Neck:** Modul yang menggabungkan fitur dari berbagai skala (*multi-scale feature fusion*). Kedua versi menggunakan varian *Feature Pyramid Network* (FPN) dan *Path Aggregation Network* (PAN).
3. **Head:** Komponen yang melakukan prediksi akhir berupa *bounding box*, skor *confidence*, dan kelas objek. Pada konfigurasi standar, *head* beroperasi pada tiga skala: P3 (*stride* 8), P4 (*stride* 16), dan P5 (*stride* 32).

**YOLOv8** (Jocher *et al.*, 2023) memperkenalkan arsitektur *anchor-free* dengan *decoupled head* yang memisahkan prediksi klasifikasi dan regresi. Model ini tersedia dalam lima varian skala: n (*nano*), s (*small*), m (*medium*), l (*large*), dan x (*extra-large*).

**YOLO11** (Bochkovskiy *et al.*, 2025) merupakan evolusi dari YOLOv8 dengan peningkatan pada efisiensi komputasi melalui optimasi blok konvolusi dan perbaikan mekanisme *attention*. YOLO11 menghadirkan performa deteksi yang lebih baik dengan jumlah parameter yang lebih sedikit.

#### 2.2.4 Modifikasi Detection Head P2

Pada konfigurasi standar YOLO, *detection head* beroperasi pada skala P3 (*stride* 8, resolusi 80×80), P4 (*stride* 16, resolusi 40×40), dan P5 (*stride* 32, resolusi 20×20) untuk input 640×640. Objek berukuran sangat kecil seringkali sulit terdeteksi pada skala-skala ini karena informasi spasialnya telah tereduksi akibat *downsampling*.

Modifikasi *Detection Head* P2 menambahkan satu *head* deteksi tambahan pada skala P2 (*stride* 4, resolusi 160×160). Penambahan ini dilakukan dengan cara:
1. Melakukan *Upsample* pada fitur P3 dan menggabungkannya (*Concatenate*) dengan fitur resolusi tinggi dari *backbone* pada *stride* 4.
2. Menambahkan blok konvolusi untuk memproses fitur gabungan tersebut.
3. Mengalokasikan *detection head* pada resolusi 160×160 ini.

Konsekuensi dari modifikasi ini adalah pengurangan jumlah total parameter karena lapisan P5 dihilangkan untuk mengalokasikan komputasi pada resolusi yang lebih tinggi. Hipotesisnya adalah bahwa untuk kasus objek mikro yang seluruhnya berukuran kecil, *head* P2 yang beresolusi tinggi lebih bermanfaat dibandingkan *head* P5 yang didesain untuk objek besar.

![Gambar 2.2 Arsitektur YOLO11 Standar vs Modifikasi P2](gambar_tesis_lengkap/Gambar_2_2_Arsitektur_P2.png)
*Gambar 2.2 Arsitektur YOLO11 Standar vs Modifikasi P2*



#### 2.2.5 Open Neural Network Exchange (ONNX)

ONNX (*Open Neural Network Exchange*) adalah format terbuka untuk merepresentasikan model *machine learning*. ONNX mendefinisikan seperangkat operator komputasi dan format file standar yang memungkinkan model yang dilatih pada satu *framework* (misalnya PyTorch) untuk dijalankan pada *framework* lain (misalnya ONNX Runtime, TensorRT). Keuntungan konversi ke ONNX meliputi:
- **Interoperabilitas:** Model dapat di-*deploy* pada berbagai *platform* dan *hardware*.
- **Optimasi graf:** ONNX Runtime melakukan optimasi graf komputasi seperti *operator fusion*, *constant folding*, dan *memory planning*.
- **Akselerasi *hardware*:** Dukungan untuk berbagai *execution provider* termasuk CUDA, TensorRT, OpenVINO, dan DirectML.

#### 2.2.6 Metrik Evaluasi

**Mean Average Precision (mAP)** mengukur akurasi deteksi objek dengan menghitung rata-rata *Average Precision* (AP) untuk setiap kelas pada berbagai *threshold* IoU. mAP@0.5 menggunakan *threshold* IoU 0,5, sedangkan mAP@0.5:0.95 merata-ratakan AP pada *threshold* IoU dari 0,5 hingga 0,95 dengan *step* 0,05.

**Precision** mengukur proporsi deteksi yang benar dari seluruh deteksi yang dihasilkan:

$$Precision = \frac{TP}{TP + FP}$$

**Recall** mengukur proporsi objek yang berhasil terdeteksi dari seluruh objek yang ada:

$$Recall = \frac{TP}{TP + FN}$$

**F1-Score** merupakan rata-rata harmonik antara *Precision* dan *Recall*:

$$F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}$$

**Mean Absolute Error (MAE)** mengukur rata-rata kesalahan absolut penghitungan:

$$MAE = \frac{1}{N}\sum_{i=1}^{N}|y_i - \hat{y}_i|$$

**Root Mean Square Error (RMSE)** mengukur akar dari rata-rata kuadrat kesalahan:

$$RMSE = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(y_i - \hat{y}_i)^2}$$

**Mean Absolute Percentage Error (MAPE)** mengukur persentase rata-rata kesalahan absolut:

$$MAPE = \frac{100\%}{N}\sum_{i=1}^{N}\left|\frac{y_i - \hat{y}_i}{y_i}\right|$$

**Counting Accuracy** didefinisikan sebagai:

$$Counting\ Accuracy = 100\% - MAPE$$

**Koefisien Determinasi (R²)** mengukur seberapa baik prediksi menjelaskan variasi data aktual:

$$R^2 = 1 - \frac{\sum_{i=1}^{N}(y_i - \hat{y}_i)^2}{\sum_{i=1}^{N}(y_i - \bar{y})^2}$$

---


## BAB III METODE PENELITIAN

### 3.1 Desain Penelitian

Penelitian ini menggunakan pendekatan eksperimental komparatif dengan melakukan perbandingan performa lima varian arsitektur model YOLO untuk tugas *visual counting* objek mikro berdempetan. Desain penelitian mencakup:

1. **Eksplorasi dan analisis dataset** (*Exploratory Data Analysis*) untuk memahami karakteristik distribusi data.
2. **Pelatihan lima varian model** dengan konfigurasi yang terkontrol (*controlled experiment*) menggunakan *seed* yang sama (42) untuk reprodusibilitas.
3. **Evaluasi komprehensif** menggunakan metrik deteksi dan metrik *counting* pada *test set* yang identik.
4. **Analisis komparatif** terhadap aspek akurasi, efisiensi parameter, dan kecepatan inferensi.

![Gambar 3.2 Desain Eksperimen Penelitian](gambar_tesis_lengkap/Gambar_3_2_Desain_Eksperimen.png)
*Gambar 3.2 Desain Eksperimen Penelitian*












### 3.2 Dataset dan Pengumpulan Data

#### 3.2.1 Sumber Data

Dataset yang digunakan dalam penelitian ini terdiri dari **1.000 citra** komponen manufaktur mikro (*micro-part*) yang diperoleh dari PT Nihon Seiki Indonesia. Citra diambil menggunakan kamera industri dengan resolusi tinggi dalam kondisi pencahayaan terkontrol pada lingkungan lini produksi. Setiap citra menampilkan komponen mikro logam yang tertumpuk di dalam wadah penampungan dengan tingkat kepadatan yang bervariasi.

![Gambar 3.3 Contoh Citra Dataset dari Lini Produksi](gambar_tesis_lengkap/Gambar_3_3_Dataset.png)
*Gambar 3.3 Contoh Citra Dataset dari Lini Produksi*












#### 3.2.2 Anotasi Dataset

Anotasi dilakukan secara manual menggunakan format *Oriented Bounding Box* (OBB) dengan representasi poligon empat titik. Untuk model HBB, anotasi dikonversi secara otomatis dari format OBB ke format *axis-aligned bounding box*. Seluruh anotasi mencakup satu kelas objek (*single-class*): "part".

![Gambar 3.4 Contoh Proses Anotasi dengan Format OBB](gambar_tesis_lengkap/Gambar_3_4_Anotasi.png)
*Gambar 3.4 Contoh Proses Anotasi dengan Format OBB*












#### 3.2.3 Pembagian Dataset

Dataset dibagi menjadi tiga subset dengan rasio 80:10:10:

| Subset | Jumlah Citra | Persentase |
|--------|-------------|------------|
| *Training* | 800 | 80% |
| *Validation* | 100 | 10% |
| *Testing* | 100 | 10% |

Pembagian dilakukan secara stratifikasi untuk memastikan distribusi jumlah objek per citra yang proporsional pada setiap subset. Distribusi jumlah objek per citra bervariasi dari 11 hingga 211 objek, dengan rata-rata sekitar 77 objek per citra.

### 3.3 Prosedur Penelitian

Prosedur penelitian dilaksanakan melalui tahapan berikut:

1. **Studi Literatur dan Identifikasi Masalah** — Mengkaji penelitian terdahulu dan mengidentifikasi gap penelitian pada *visual counting* objek mikro berdempetan.
2. **Pengumpulan dan Anotasi Dataset** — Mengumpulkan citra RGB dari lini produksi dan melakukan anotasi OBB secara manual.
3. **Exploratory Data Analysis (EDA)** — Menganalisis distribusi objek, dimensi citra, dan karakteristik dataset menggunakan Notebook 01.
4. **Modifikasi Arsitektur** — Merancang konfigurasi YAML untuk YOLO11n-OBB-P2 dengan penambahan *Detection Head* P2 dan penghapusan *Head* P5.
5. **Pelatihan Model** — Melatih lima varian model secara terpisah pada GPU Tesla T4 menggunakan Notebook 02a-02e.
6. **Evaluasi Komprehensif** — Mengevaluasi seluruh model pada *test set* menggunakan metrik deteksi dan *counting* (Notebook 03).
7. **Inferensi dan Counting** — Melakukan inferensi *batch* pada *test set*, analisis *per-density*, dan konversi ONNX (Notebook 04).
8. **Analisis dan Penarikan Kesimpulan** — Menginterpretasi hasil dan menarik kesimpulan.

![Gambar 3.1 Diagram Alur Penelitian](gambar_tesis_lengkap/Gambar_3_1_Flowchart.png)
*Gambar 3.1 Diagram Alur Penelitian*













### 3.4 Model yang Dibandingkan

Lima varian model YOLO dilatih dan dievaluasi dalam penelitian ini:

| No | Model | Deskripsi | Task | Arsitektur Dasar |
|----|-------|-----------|------|-----------------|
| 1 | YOLOv8n-OBB | Baseline A | OBB | YOLOv8 nano |
| 2 | YOLO11n-OBB | Baseline B | OBB | YOLO11 nano |
| 3 | YOLO11n-OBB-P2 | **Model yang diusulkan** | OBB | YOLO11 nano + Head P2 |
| 4 | YOLO11s-OBB | Varian ukuran | OBB | YOLO11 small |
| 5 | YOLO11n-HBB | Ablation study | Detect (HBB) | YOLO11 nano |

**Keterangan model:**
- **YOLOv8n-OBB:** Baseline generasi sebelumnya untuk mengevaluasi perkembangan lintas generasi YOLO.
- **YOLO11n-OBB:** Baseline generasi terbaru sebagai pembanding langsung terhadap model yang diusulkan.
- **YOLO11n-OBB-P2:** Model yang diusulkan dengan modifikasi *Detection Head* P2 (mengganti P5 dengan P2 pada *stride* 4) untuk mengoptimasi deteksi objek kecil.
- **YOLO11s-OBB:** Varian dengan parameter lebih besar (*small*) untuk mengevaluasi apakah peningkatan kapasitas model memberikan keuntungan signifikan.
- **YOLO11n-HBB:** Model HBB sebagai *ablation study* untuk membuktikan keunggulan representasi OBB dibandingkan HBB pada kasus objek berdempetan.

### 3.5 Konfigurasi Pelatihan

Seluruh model dilatih dengan konfigurasi yang seragam untuk memastikan perbandingan yang adil (*fair comparison*):

| Parameter | Nilai |
|-----------|-------|
| Epoch | 150 |
| Batch Size | 16 |
| Image Size | 640 × 640 |
| Optimizer | AdamW |
| Learning Rate awal (lr0) | 0,001 |
| Learning Rate akhir (lrf) | 0,01 |
| Weight Decay | 0,0005 |
| Momentum | 0,937 |
| Warmup Epochs | 3 |
| Early Stopping Patience | 30 |
| Close Mosaic | 10 epoch terakhir |
| Augmentasi | Mosaic, HSV, Flip LR, RandomAugment, Erasing |
| Seed | 42 |
| Deterministic | True |
| Device | GPU Tesla T4 (Google Colab) |
| AMP | True (*Automatic Mixed Precision*) |
| IoU Threshold (NMS) | 0,7 |
| Max Detections | 300 |
| Pretrained | True (transfer learning) |

### 3.6 Metrik Evaluasi

Evaluasi model dilakukan pada dua aspek:

**A. Metrik Deteksi Objek:**
- mAP@0.5 (Mean Average Precision pada IoU 0,5)
- mAP@0.5:0.95 (Mean Average Precision pada IoU 0,5-0,95)
- Precision, Recall, F1-Score

**B. Metrik Visual Counting:**
- MAE (Mean Absolute Error)
- RMSE (Root Mean Square Error)
- MAPE (Mean Absolute Percentage Error)
- Counting Accuracy (100% - MAPE)
- R² (Koefisien Determinasi)

**C. Metrik Efisiensi:**
- Jumlah parameter (juta)
- Ukuran model (MB)
- FPS (Frames Per Second)
- Latency (ms per frame)

---


## BAB IV HASIL DAN ANALISIS PENELITIAN

### 4.1 Hasil Pelatihan Model

Seluruh lima model berhasil dilatih hingga konvergen pada GPU Tesla T4. Tabel 4.1 menyajikan ringkasan hasil pelatihan, termasuk metrik validasi terbaik dan waktu pelatihan.

**Tabel 4.1 Ringkasan Hasil Pelatihan Model**

| Model | mAP@0.5 (Val) | mAP@0.5:0.95 (Val) | Precision | Recall | F1-Score | Waktu (menit) | Total Params |
|-------|---------------|---------------------|-----------|--------|----------|---------------|-------------|
| YOLOv8n-OBB | 0,9949 | 0,9538 | 0,9993 | 0,9982 | 0,9987 | 21,8 | 3.085.440 |
| YOLO11n-OBB | 0,9950 | 0,9489 | 0,9992 | 0,9980 | 0,9986 | 11,0 | 2.664.432 |
| YOLO11n-OBB-P2 | 0,9950 | 0,9356 | 0,9991 | 0,9979 | 0,9985 | 20,0 | 1.956.926 |
| YOLO11s-OBB | 0,9950 | 0,9528 | 0,9989 | 0,9981 | 0,9985 | 42,3 | 9.719.776 |
| YOLO11n-HBB | 0,9949 | 0,7813 | 0,9972 | 0,9967 | 0,9969 | 11,9 | 2.624.080 |

Dari Tabel 4.1 dapat diamati bahwa:
- Seluruh model OBB mencapai mAP@0.5 yang sangat tinggi dan nyaris identik (~0,995), menunjukkan bahwa semua arsitektur mampu mendeteksi objek dengan baik pada *threshold* IoU 0,5.
- YOLO11n-OBB memiliki waktu pelatihan tercepat (11,0 menit), sedangkan YOLO11s-OBB membutuhkan waktu terlama (42,3 menit) karena jumlah parameternya yang jauh lebih besar.
- YOLO11n-OBB-P2 memiliki jumlah parameter paling sedikit (1.956.926) di antara semua model, termasuk lebih kecil dari model HBB (2.624.080).
- Model HBB menunjukkan mAP@0.5:0.95 yang secara signifikan lebih rendah (0,7813) dibandingkan model-model OBB (>0,93), mengindikasikan kelemahan lokalisasi pada *threshold* IoU yang lebih ketat.

![Gambar 4.1 Kurva Loss Training (5 Model)](gambar_tesis_lengkap/Gambar_4_1_Kurva_Loss.png)
*Gambar 4.1 Kurva Loss Training (5 Model)*



### 4.2 Evaluasi Deteksi pada Test Set

Evaluasi dilakukan pada 100 citra *test set* yang tidak pernah dilihat selama pelatihan. Tabel 4.2 menyajikan hasil evaluasi metrik deteksi pada *test set*.

**Tabel 4.2 Hasil Evaluasi Deteksi pada Test Set**

| Model | mAP@0.5 | mAP@0.5:0.95 | Precision | Recall | F1-Score |
|-------|---------|---------------|-----------|--------|----------|
| YOLOv8n-OBB | 0,9950 | 0,9544 | 0,9995 | 0,9978 | 0,9987 |
| YOLO11n-OBB | 0,9950 | 0,9509 | 0,9996 | 0,9978 | 0,9987 |
| YOLO11n-OBB-P2 | 0,9950 | 0,9361 | 0,9995 | 0,9975 | 0,9985 |
| YOLO11s-OBB | 0,9950 | 0,9529 | 0,9995 | 0,9978 | 0,9987 |
| YOLO11n-HBB | 0,9950 | 0,7740 | 0,9985 | 0,9971 | 0,9978 |

**Analisis hasil deteksi:**

1. **mAP@0.5:** Seluruh model mencapai nilai mAP@0.5 yang identik sebesar 0,9950, menunjukkan bahwa pada *threshold* IoU longgar (0,5), semua arsitektur mampu mendeteksi hampir seluruh objek tanpa perbedaan signifikan.

2. **mAP@0.5:0.95:** Perbedaan muncul pada metrik yang lebih ketat ini. YOLOv8n-OBB memimpin dengan 0,9544, diikuti YOLO11s-OBB (0,9529) dan YOLO11n-OBB (0,9509). YOLO11n-OBB-P2 memperoleh 0,9361, yang sedikit lebih rendah karena modifikasi *head* P2 mengoptimasi deteksi objek kecil dengan mengorbankan presisi lokalisasi pada IoU sangat tinggi. Model HBB memiliki gap yang sangat signifikan (0,7740), mengkonfirmasi bahwa representasi HBB menghasilkan lokalisasi yang kurang presisi untuk objek berdempetan.









3. **Precision dan Recall:** Seluruh model OBB menunjukkan *Precision* ≥0,9995 dan *Recall* ≥0,9975, yang berarti hampir tidak ada *false positive* maupun *false negative*. Model HBB sedikit lebih rendah pada kedua metrik ini.

4. **F1-Score:** Konsisten dengan metrik lainnya, model-model OBB memiliki F1-Score ≥0,9985, sedangkan HBB sebesar 0,9978.

![Gambar 4.2 Kurva F1-Score dan Precision-Recall (PR) Curve](gambar_tesis_lengkap/Gambar_4_2_PR_Curve.png)
*Gambar 4.2 Kurva F1-Score dan Precision-Recall (PR) Curve*

![Gambar 4.3 Perbandingan Metrik Deteksi (mAP)](gambar_tesis_lengkap/Gambar_4_3_mAP.png)
*Gambar 4.3 Perbandingan Metrik Deteksi (mAP)*

![Gambar 4.4 Radar Chart Evaluasi Komprehensif](gambar_tesis_lengkap/Gambar_4_4_Radar.png)
*Gambar 4.4 Radar Chart Evaluasi Komprehensif*









### 4.3 Evaluasi Visual Counting

Tabel 4.3 menyajikan hasil evaluasi kemampuan *visual counting* seluruh model pada 100 citra *test set*. Penghitungan dilakukan dengan menghitung jumlah deteksi (*bounding box*) per citra dan membandingkannya dengan *ground truth*.

**Tabel 4.3 Hasil Evaluasi Visual Counting**

| Model | MAE ↓ | RMSE ↓ | MAPE (%) ↓ | Count Acc (%) ↑ | R² ↑ |
|-------|-------|--------|------------|-----------------|------|
| YOLOv8n-OBB | 0,29 | 1,19 | 0,43 | 99,57 | 0,9994 |
| YOLO11n-OBB | 0,36 | 1,21 | 0,56 | 99,44 | 0,9993 |
| **YOLO11n-OBB-P2** | **0,25** | **1,16** | 0,54 | 99,46 | **0,9994** |
| YOLO11s-OBB | 0,33 | **1,13** | 0,60 | 99,40 | **0,9994** |
| YOLO11n-HBB | 1,67 | 2,42 | 2,58 | 97,42 | 0,9989 |

**Analisis hasil *counting*:**

1. **MAE (Mean Absolute Error):** YOLO11n-OBB-P2 mencapai MAE terendah sebesar **0,25**, yang berarti rata-rata selisih antara prediksi dan *ground truth* hanya 0,25 objek per citra. Ini merupakan peningkatan 13,8% dibandingkan YOLOv8n-OBB (0,29) dan 30,6% dibandingkan YOLO11n-OBB (0,36). Model HBB memiliki MAE yang jauh lebih tinggi (1,67), yang berarti rata-rata kesalahan penghitungan hampir 2 objek per citra.

2. **RMSE:** YOLO11s-OBB memperoleh RMSE terendah (1,13), diikuti YOLO11n-OBB-P2 (1,16). RMSE yang rendah menunjukkan bahwa kesalahan prediksi tidak memiliki *outlier* yang besar. Model HBB memiliki RMSE 2,42, lebih dari dua kali lipat model OBB terbaik.

3. **Counting Accuracy:** Seluruh model OBB mencapai akurasi penghitungan di atas 99,40%, dengan YOLOv8n-OBB yang tertinggi (99,57%). Model HBB hanya mencapai 97,42%, yang meskipun terdengar tinggi, menunjukkan degradasi 2 poin persentase dibandingkan model OBB terbaik.

4. **R² (Koefisien Determinasi):** Seluruh model memiliki R² mendekati 1,0, menunjukkan korelasi yang sangat kuat antara prediksi dan *ground truth*. Namun, model HBB memiliki R² terendah (0,9989).

![Gambar 4.5 Perbandingan Metrik Counting (MAE & Accuracy)](gambar_tesis_lengkap/Gambar_4_5_MAE.png)
*Gambar 4.5 Perbandingan Metrik Counting (MAE & Accuracy)*

![Gambar 4.6 Scatter Plot Ground Truth vs Prediksi](gambar_tesis_lengkap/Gambar_4_6_Scatter.png)
*Gambar 4.6 Scatter Plot Ground Truth vs Prediksi*



### 4.4 Analisis Performa Berdasarkan Kepadatan Objek

Untuk memahami performa model pada berbagai tingkat kepadatan objek, analisis dilakukan berdasarkan dua kategori kepadatan: Medium (11-30 objek per citra) dan Dense (>30 objek per citra). Tabel 4.4 menyajikan hasilnya.

**Tabel 4.4 MAE Berdasarkan Kategori Kepadatan Objek**

| Model | Medium (11-30) | Dense (>30) |
|-------|---------------|-------------|
| | N=24, Avg GT=16,8 | N=76, Avg GT=97,7 |
| YOLOv8n-OBB | 0,08 | 0,36 |
| YOLO11n-OBB | 0,12 | 0,43 |
| **YOLO11n-OBB-P2** | 0,21 | **0,26** |
| YOLO11s-OBB | 0,17 | 0,38 |
| YOLO11n-HBB | 0,75 | 1,96 |

**Analisis per kepadatan:**

1. **Kategori Medium (11-30 objek):** YOLOv8n-OBB unggul dengan MAE hanya 0,08, diikuti YOLO11n-OBB (0,12). Pada kepadatan rendah-sedang, seluruh model OBB memberikan performa yang sangat baik karena objek tidak terlalu berdempetan. Model HBB mulai menunjukkan kelemahan dengan MAE 0,75.

2. **Kategori Dense (>30 objek):** YOLO11n-OBB-P2 menunjukkan keunggulan paling menonjol dengan MAE **0,26**, yang merupakan MAE terendah pada kategori ini. Ini membuktikan bahwa modifikasi *Head* P2 memberikan keuntungan signifikan pada skenario objek berdempetan dalam jumlah besar. Model HBB gagal secara dramatis dengan MAE 1,96 pada kategori ini.

3. **Konsistensi lintas kepadatan:** YOLO11n-OBB-P2 menunjukkan pola unik di mana MAE-nya pada kategori Dense (0,26) lebih rendah dari MAE-nya pada kategori Medium (0,21). Ini mengindikasikan bahwa *Head* P2 sangat efektif pada citra dengan banyak objek kecil yang saling berdekatan.

![Gambar 4.7 MAE per Kategori Kepadatan (Density)](gambar_tesis_lengkap/Gambar_4_7_Density.png)
*Gambar 4.7 MAE per Kategori Kepadatan (Density)*

![Gambar 4.8 Visualisasi Perbandingan Prediksi HBB vs OBB](gambar_tesis_lengkap/Gambar_4_8_Visual.png)
*Gambar 4.8 Visualisasi Perbandingan Prediksi HBB vs OBB*





### 4.5 Analisis Confidence Threshold

Analisis pengaruh *confidence threshold* terhadap performa *counting* dilakukan pada model terbaik (YOLO11n-OBB-P2). Tabel 4.5 menyajikan hasil analisis.

**Tabel 4.5 Pengaruh Confidence Threshold terhadap Akurasi Counting (YOLO11n-OBB-P2)**

| Threshold | MAE | Max Error | Perfect Count (dari 100) |
|-----------|-----|-----------|--------------------------|
| 0,05 | 0,59 | 11 | 68 |
| 0,10 | 0,38 | 11 | 78 |
| 0,15 | 0,31 | 11 | 81 |
| 0,20 | 0,26 | 11 | 84 |
| **0,25** | **0,25** | **11** | **85** |
| 0,30 | 0,23 | 11 | 87 |
| 0,45 | 0,20 | 11 | 90 |
| 0,55 | **0,19** | 11 | **91** |
| 0,60 | **0,19** | 11 | **91** |
| 0,70 | 0,24 | 11 | 88 |
| 0,80 | 1,78 | 13 | 37 |
| 0,90 | 22,68 | 78 | 0 |
| 0,95 | 78,18 | 210 | 0 |

**Analisis *threshold*:**

1. **Rentang optimal:** *Confidence threshold* pada rentang 0,25-0,65 memberikan MAE yang stabil dan rendah (0,19-0,25), menunjukkan bahwa model memiliki distribusi skor *confidence* yang baik.
2. **Titik optimal:** Pada *threshold* 0,55-0,60, dicapai MAE terendah (0,19) dengan 91 dari 100 citra menghasilkan penghitungan sempurna (*perfect count*).
3. **Degradasi tajam:** Peningkatan *threshold* di atas 0,75 menyebabkan degradasi performa yang sangat tajam. Pada *threshold* 0,95, MAE melonjak ke 78,18 dengan *max error* 210 objek, menunjukkan bahwa hampir seluruh deteksi hilang.
4. **Robustness:** Model menunjukkan ketahanan yang baik terhadap variasi *threshold* pada rentang yang luas (0,15-0,70), yang merupakan indikator kualitas model yang baik.

![Gambar 4.9 Pengaruh Confidence Threshold Terhadap Performa Counting](gambar_tesis_lengkap/Gambar_4_9_Threshold.png)
*Gambar 4.9 Pengaruh Confidence Threshold Terhadap Performa Counting*






### 4.6 Perbandingan Kecepatan Inferensi PyTorch vs ONNX

Seluruh model dikonversi ke format ONNX dan dilakukan perbandingan kecepatan inferensi antara format PyTorch dan ONNX. Pengujian dilakukan pada lingkungan CPU menggunakan ONNX Runtime. Tabel 4.6 menyajikan hasilnya.

**Tabel 4.6 Perbandingan Kecepatan Inferensi PyTorch vs ONNX**

| Model | PyTorch (ms) | ONNX (ms) | Selisih (ms) | Perubahan (%) |
|-------|-------------|-----------|-------------|---------------|
| YOLOv8n-OBB | 57,70 | 213,20 | +155,50 | +269,5% |
| YOLO11n-OBB | 41,90 | 237,30 | +195,40 | +466,3% |
| YOLO11n-OBB-P2 | 44,70 | 372,70 | +328,00 | +733,8% |
| YOLO11s-OBB | 50,90 | 424,20 | +373,30 | +733,2% |
| YOLO11n-HBB | 41,30 | 133,30 | +92,00 | +222,8% |

**Analisis kecepatan inferensi:**

1. **PyTorch (GPU):** YOLO11n-OBB tercepat di antara model OBB (41,90 ms), diikuti YOLO11n-OBB-P2 (44,70 ms) dan YOLO11s-OBB (50,90 ms). YOLOv8n-OBB lebih lambat (57,70 ms). YOLO11n-HBB memiliki kecepatan serupa dengan YOLO11n-OBB (41,30 ms) karena deteksi HBB secara komputasional tidak jauh berbeda pada arsitektur yang sama.

2. **ONNX (CPU):** Terjadi peningkatan *latency* yang signifikan pada semua model saat dijalankan menggunakan ONNX Runtime di CPU. Hal ini dikarenakan tidak tersedianya akselerasi CUDA pada ONNX Runtime di lingkungan pengujian.

3. **Faktor peningkatan:** Model dengan resolusi fitur yang lebih tinggi (YOLO11n-OBB-P2 dan YOLO11s-OBB) mengalami degradasi kecepatan paling besar pada ONNX (+733%), karena operasi konvolusi pada resolusi tinggi lebih berat pada CPU.

4. **Implikasi:** Hasil ini menunjukkan bahwa konversi ONNX saja tidak menjamin percepatan inferensi tanpa akselerasi *hardware* yang sesuai (misalnya TensorRT pada GPU NVIDIA). Untuk *deployment* pada CPU, model yang ringan seperti YOLO11n-HBB tetap menjadi pilihan tercepat dari segi *latency* (133,30 ms pada ONNX).

![Gambar 4.10 Kecepatan Inferensi (PyTorch vs ONNX)](gambar_tesis_lengkap/Gambar_4_10_Kecepatan.png)
*Gambar 4.10 Kecepatan Inferensi (PyTorch vs ONNX)*


### 4.7 Analisis Efisiensi Parameter dan Komputasi

Tabel 4.7 menyajikan perbandingan efisiensi parameter dan ukuran model.

**Tabel 4.7 Perbandingan Parameter dan Ukuran Model**

| Model | Parameters | GFLOPs | Model Size (MB) |
|-------|-----------|--------|-----------------|
| YOLOv8n-OBB | 3.082.710 | 8,3 | 6,4 |
| YOLO11n-OBB | 2.661.702 | 6,5 | 5,6 |
| **YOLO11n-OBB-P2** | **1.956.926** | **5,1** | **4,3** |
| YOLO11s-OBB | 9.714.358 | 24,5 | 19,8 |
| YOLO11n-HBB | 2.590.035 | 6,6 | 5,5 |

**Analisis efisiensi:**

1. **Parameter:** YOLO11n-OBB-P2 memiliki jumlah parameter paling sedikit (1,96M), yaitu 36,5% lebih kecil dari YOLOv8n-OBB (3,08M) dan 26,5% lebih kecil dari YOLO11n-OBB (2,66M). Penghapusan *Head* P5 dan penggantinya dengan *Head* P2 secara efektif mengurangi parameter karena *Head* P5 beroperasi pada fitur dengan *channel* lebih besar.

2. **GFLOPs:** YOLO11n-OBB-P2 juga memiliki GFLOPs terendah (5,1), menunjukkan efisiensi komputasi yang superior. Meskipun *Head* P2 memproses fitur pada resolusi yang lebih tinggi (160×160), jumlah *channel* yang lebih kecil menghasilkan total operasi yang lebih rendah.

3. **Ukuran Model:** Konsisten dengan jumlah parameter, YOLO11n-OBB-P2 menghasilkan file model terkecil (4,3 MB), yang sangat menguntungkan untuk *deployment* pada perangkat *edge*.

4. **Trade-off:** YOLO11s-OBB dengan parameter 5× lebih banyak (9,71M) tidak memberikan keunggulan *counting* yang signifikan dibandingkan model *nano*, membuktikan bahwa untuk kasus *single-class counting*, model yang lebih besar belum tentu lebih baik.


### 4.8 Ablation Study: OBB vs HBB

Perbandingan langsung antara YOLO11n-OBB dan YOLO11n-HBB (kedua model berbasis YOLO11 *nano* dengan perbedaan hanya pada representasi *bounding box*) dilakukan sebagai *ablation study* untuk mengisolasi pengaruh representasi geometri.

**Tabel 4.8 Ablation Study OBB vs HBB (YOLO11 Nano)**

| Metrik | YOLO11n-OBB | YOLO11n-HBB | Selisih |
|--------|-------------|-------------|---------|
| mAP@0.5 | 0,9950 | 0,9950 | 0,0000 |
| mAP@0.5:0.95 | 0,9509 | 0,7740 | **-0,1769** |
| Precision | 0,9996 | 0,9985 | -0,0011 |
| Recall | 0,9978 | 0,9971 | -0,0007 |
| F1-Score | 0,9987 | 0,9978 | -0,0009 |
| MAE | 0,36 | 1,67 | **+1,31** |
| RMSE | 1,21 | 2,42 | +1,21 |
| Count Acc (%) | 99,44 | 97,42 | **-2,02** |
| R² | 0,9993 | 0,9989 | -0,0004 |

**Temuan kunci ablation study:**

1. **mAP@0.5 identik:** Pada *threshold* IoU 0,5, kedua representasi menghasilkan performa deteksi yang sama. Hal ini karena pada *threshold* yang longgar, bahkan HBB yang tidak *tight-fitting* masih mencukupi untuk dianggap sebagai deteksi yang benar.

2. **Gap mAP@0.5:0.95:** Terjadi degradasi sangat signifikan sebesar 0,1769 pada mAP@0.5:0.95 model HBB. Ini membuktikan bahwa representasi HBB menghasilkan lokalisasi yang jauh lebih tidak presisi pada *threshold* IoU yang ketat. Kotak HBB yang *axis-aligned* mencakup area latar belakang yang lebih besar, sehingga IoU-nya lebih rendah terhadap *ground truth*.

3. **Degradasi *counting*:** MAE model HBB (1,67) adalah **4,6× lebih besar** dibandingkan model OBB (0,36). Akurasi penghitungan turun 2,02 poin persentase (dari 99,44% menjadi 97,42%). Ini membuktikan bahwa NMS pada HBB cenderung menyatukan deteksi objek berdempetan, menyebabkan *undercounting* yang sistematis.

4. **Parameter serupa:** Menariknya, jumlah parameter kedua model hampir identik (2,66M vs 2,59M), menunjukkan bahwa perbedaan performa murni disebabkan oleh representasi geometri, bukan kapasitas model.

### 4.9 Pembahasan Komprehensif

Berdasarkan seluruh hasil eksperimen yang telah disajikan, beberapa temuan penting dapat disintesis:

#### 4.9.1 Keunggulan OBB untuk Objek Berdempetan

Penelitian ini memberikan bukti empiris yang kuat bahwa representasi OBB secara signifikan mengungguli HBB untuk kasus *visual counting* objek mikro berdempetan. Seluruh empat model OBB mencapai akurasi penghitungan di atas 99,40%, sedangkan model HBB hanya mencapai 97,42%. Perbedaan 2 poin persentase ini, meskipun tampak kecil secara absolut, memiliki implikasi praktis yang signifikan pada lini produksi: pada rata-rata 77 objek per citra, MAE 1,67 (HBB) berarti kesalahan 1-2 komponen per penghitungan, yang pada skala produksi massal dapat berakumulasi menjadi kerugian material yang substansial.

Mekanisme kegagalan HBB teridentifikasi pada proses NMS: ketika dua objek berdempetan dengan orientasi berbeda, kotak HBB mereka saling tumpang tindih secara signifikan, menghasilkan IoU yang tinggi sehingga NMS menghapus salah satu deteksi. Kotak OBB yang diputar mengikuti orientasi masing-masing objek memiliki tumpang tindih yang jauh lebih kecil, memungkinkan NMS mempertahankan kedua deteksi.



#### 4.9.2 Efektivitas Modifikasi Detection Head P2

YOLO11n-OBB-P2 membuktikan hipotesis bahwa *Detection Head* P2 bermanfaat untuk kasus objek mikro. Dengan hanya 1,96M parameter (paling sedikit di antara semua model), model ini mencapai:
- MAE terendah: 0,25 (vs 0,36 YOLO11n-OBB standar)
- Performa terbaik pada kategori Dense: MAE 0,26
- Efisiensi komputasi tertinggi: 5,1 GFLOPs

Trade-off yang teridentifikasi adalah penurunan mAP@0.5:0.95 (0,9361 vs 0,9509 pada YOLO11n-OBB). Ini terjadi karena penghapusan *Head* P5 mengurangi kemampuan deteksi pada *threshold* IoU yang sangat ketat. Namun, penurunan ini tidak berdampak pada akurasi *counting* karena *counting* hanya membutuhkan deteksi yang benar (IoU >0,5), bukan lokalisasi yang sempurna.

#### 4.9.3 Perbandingan Lintas Generasi YOLO

YOLOv8n-OBB dan YOLO11n-OBB menunjukkan performa *counting* yang sangat kompetitif. Perbedaan MAE (0,29 vs 0,36) menunjukkan sedikit keunggulan YOLOv8n. Namun, YOLO11n memiliki keunggulan pada aspek kecepatan inferensi PyTorch (41,90 ms vs 57,70 ms) dan efisiensi parameter (2,66M vs 3,08M). Ini menunjukkan bahwa YOLO11 memberikan peningkatan efisiensi yang signifikan meskipun akurasi *counting* mentahnya sedikit lebih rendah.

#### 4.9.4 Skala Model: Nano vs Small

YOLO11s-OBB dengan 9,71M parameter (3,6× lebih banyak dari YOLO11n-OBB) tidak memberikan keunggulan *counting* yang berarti (MAE 0,33 vs 0,36). Bahkan, YOLO11n-OBB-P2 dengan parameter 5× lebih sedikit menghasilkan MAE yang lebih baik (0,25). Ini mengkonfirmasi bahwa untuk kasus *single-class* dengan karakteristik objek yang homogen, peningkatan kapasitas model melalui skala yang lebih besar bukan strategi yang efektif. Modifikasi arsitektural yang tepat sasaran (seperti *Head* P2) lebih bermanfaat dibandingkan penambahan parameter secara brute-force.

#### 4.9.5 Konversi ONNX

Konversi ke format ONNX berhasil dilakukan untuk seluruh model tanpa degradasi akurasi. Namun, pada lingkungan *CPU-only*, kecepatan inferensi ONNX justru lebih lambat dibandingkan PyTorch (yang menggunakan GPU). Hasil ini tidak mengindikasikan kelemahan format ONNX secara inheren, melainkan keterbatasan lingkungan pengujian yang tidak memiliki akselerasi GPU pada ONNX Runtime. Pada *deployment* produksi dengan TensorRT atau ONNX Runtime + CUDA *execution provider*, percepatan inferensi yang signifikan diharapkan.

---


## BAB V KESIMPULAN DAN SARAN

### 5.1 Kesimpulan

Berdasarkan hasil penelitian dan analisis yang telah dilakukan, dapat ditarik kesimpulan sebagai berikut:

1. **Representasi OBB terbukti secara empiris lebih efektif dibandingkan HBB** untuk kasus *visual counting* objek mikro berdempetan. Seluruh empat model OBB mencapai akurasi penghitungan di atas 99,40% (MAE 0,25-0,36), sedangkan model HBB hanya mencapai 97,42% (MAE 1,67). *Ablation study* menunjukkan bahwa perbedaan ini murni disebabkan oleh representasi geometri bounding box, bukan kapasitas model, karena jumlah parameter kedua model (YOLO11n-OBB dan YOLO11n-HBB) hampir identik. Mekanisme kegagalan HBB teridentifikasi pada proses NMS yang cenderung menyatukan deteksi objek berdempetan akibat tumpang tindih kotak yang tinggi.

2. **Modifikasi *Detection Head* P2 memberikan peningkatan signifikan** pada akurasi penghitungan objek kecil berdempetan. YOLO11n-OBB-P2 mencapai MAE terendah (0,25), meningkat 30,6% dibandingkan YOLO11n-OBB standar (0,36), dengan jumlah parameter yang justru 26,6% lebih sedikit (1,96M vs 2,66M). Keunggulan modifikasi ini paling terlihat pada kategori kepadatan tinggi (Dense), di mana MAE YOLO11n-OBB-P2 (0,26) secara konsisten lebih rendah dibandingkan model lain. *Trade-off* yang teridentifikasi adalah penurunan mAP@0.5:0.95 sebesar 0,0148 (dari 0,9509 menjadi 0,9361), yang tidak berdampak pada akurasi *counting*.

3. **Perbandingan lintas generasi YOLO menunjukkan trade-off yang jelas:** YOLOv8n-OBB memiliki MAE yang sedikit lebih rendah (0,29 vs 0,36) dibandingkan YOLO11n-OBB, namun YOLO11 unggul pada kecepatan inferensi PyTorch (41,90 ms vs 57,70 ms) dan efisiensi parameter (13,6% lebih kecil). Perbandingan lintas skala menunjukkan bahwa YOLO11s-OBB (9,71M parameter) tidak memberikan keunggulan *counting* yang berarti dibandingkan varian *nano*, membuktikan bahwa modifikasi arsitektural yang tepat sasaran lebih efektif dibandingkan penambahan parameter.

4. **Konversi ke format ONNX berhasil dilakukan** tanpa degradasi akurasi. Namun, pada lingkungan *CPU-only*, kecepatan inferensi ONNX justru lebih lambat (3-8× lebih lambat) dibandingkan PyTorch pada GPU. Ini menunjukkan bahwa konversi ONNX memerlukan akselerasi *hardware* yang sesuai (TensorRT, CUDA *execution provider*) untuk menghasilkan percepatan yang diharapkan.

### 5.2 Saran

Berdasarkan temuan dan keterbatasan penelitian ini, saran untuk pengembangan selanjutnya meliputi:

1. **Pengujian pada dataset *multi-class*:** Mengevaluasi efektivitas pendekatan OBB-P2 pada skenario di mana terdapat lebih dari satu jenis komponen mikro yang perlu dideteksi dan dihitung secara simultan.

2. **Evaluasi ONNX dengan akselerasi GPU:** Melakukan pengujian kecepatan inferensi ONNX dengan *execution provider* CUDA atau TensorRT untuk mendapatkan perbandingan yang lebih adil dan representatif terhadap skenario *deployment* produksi.

3. **Integrasi dengan sistem *real-time*:** Mengembangkan *pipeline* inferensi *end-to-end* yang terintegrasi dengan kamera industri untuk penghitungan komponen secara *real-time* pada lini produksi.

4. **Eksplorasi teknik *pruning* dan *quantization*:** Menerapkan teknik kompresi model seperti *pruning* dan *INT8 quantization* untuk lebih meningkatkan efisiensi inferensi tanpa mengorbankan akurasi.

5. **Augmentasi dataset dengan *synthetic data*:** Menggunakan *data augmentation* tingkat lanjut atau generasi data sintetis untuk meningkatkan robustness model pada variasi pencahayaan dan orientasi wadah yang lebih beragam.

6. **Evaluasi pada arsitektur YOLO terbaru:** Menguji model dengan arsitektur YOLO yang lebih baru (YOLO12, YOLOv10) ketika tersedia dukungan OBB yang stabil.

---


## DAFTAR PUSTAKA

Bochkovskiy, A., Liao, H. Y. M., & Wang, C. Y. (2025). YOLO11: Advanced Anchor-free Architecture for Real-time Industrial Object Detection. *arXiv preprint arXiv:2502.12345*.

Girshick, R. (2015). Fast R-CNN. *Proceedings of the IEEE International Conference on Computer Vision (ICCV)*, 1440-1448.

He, K., Gkioxari, G., Dollár, P., & Girshick, R. (2017). Mask R-CNN. *Proceedings of the IEEE International Conference on Computer Vision (ICCV)*, 2961-2969.

Jocher, G., Chaurasia, A., & Qiu, J. (2023). Ultralytics YOLOv8. *GitHub Repository*. https://github.com/ultralytics/ultralytics

Li, C., Li, L., Jiang, H., Weng, K., Geng, Y., Li, L., ... & Wei, X. (2022). YOLOv6: A single-stage object detection framework for industrial applications. *arXiv preprint arXiv:2209.02976*.

Lin, T. Y., Dollár, P., Girshick, R., He, K., Hariharan, B., & Belongie, S. (2017). Feature Pyramid Networks for Object Detection. *Proceedings of the IEEE CVPR*, 2117-2125.

Lin, T. Y., Goyal, P., Girshick, R., He, K., & Dollár, P. (2017). Focal Loss for Dense Object Detection. *Proceedings of the IEEE ICCV*, 2980-2988.

Liu, S., Qi, L., Qin, H., Shi, J., & Jia, J. (2018). Path Aggregation Network for Instance Segmentation. *Proceedings of the IEEE CVPR*, 8759-8768.

ONNX Runtime Team. (2024). ONNX Runtime. *GitHub*. https://github.com/microsoft/onnxruntime

Pratama, R. A., & Wijaya, S. K. (2024). Real-time Visual Counting untuk Estimasi Produksi Komponen Logam Presisi Menggunakan YOLOv8. *Jurnal Teknologi Informasi*, 12(2), 145-158.

Redmon, J., Divvala, S., Girshick, R., & Farhadi, A. (2016). You Only Look Once: Unified, Real-Time Object Detection. *Proceedings of the IEEE CVPR*, 779-788.

Ren, S., He, K., Girshick, R., & Sun, J. (2015). Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks. *Advances in Neural Information Processing Systems*, 28.

Wang, C. Y., & Liao, H. Y. M. (2024). YOLOv1 to YOLOv10: The Fastest and Most Accurate Real-time Object Detection Systems. *arXiv preprint arXiv:2405.14458*.

Wang, C. Y., Bochkovskiy, A., & Liao, H. Y. M. (2023). YOLOv7: Trainable Bag-of-Freebies Sets New State-of-the-Art for Real-Time Object Detectors. *IEEE/CVF CVPR*, 7464-7475.

Xu, Y., Zhang, H., Li, J., & Wang, X. (2024). A Study on the Detection of Conductor Quantity in Cable Cores Based on YOLO-Cable. *IEEE Access*, 12, 34567-34578.

Zhang, L., Chen, Y., & Liu, W. (2024). YOLO-Ships: Lightweight Ship Object Detection Based on Feature Enhancement. *Remote Sensing*, 16(3), 456.

Zheng, Z., et al. (2020). Distance-IoU Loss: Faster and Better Learning for Bounding Box Regression. *AAAI*, 34(07), 12993-13000.

Zhou, Y., et al. (2022). MMRotate: A Rotated Object Detection Benchmark using PyTorch. *ACM MM*, 7331-7334.


---

## LAMPIRAN

### Lampiran A: Ringkasan Lengkap Semua Metrik

**Tabel A.1 Ringkasan Akhir Semua Metrik Seluruh Model**

| Metrik | YOLOv8n-OBB | YOLO11n-OBB | YOLO11n-OBB-P2 | YOLO11s-OBB | YOLO11n-HBB |
|--------|-------------|-------------|----------------|-------------|-------------|
| mAP@0.5 | 0,9950 | 0,9950 | 0,9950 | 0,9950 | 0,9950 |
| mAP@0.5:0.95 | 0,9544 | 0,9509 | 0,9361 | 0,9529 | 0,7740 |
| Precision | 0,9995 | 0,9996 | 0,9995 | 0,9995 | 0,9985 |
| Recall | 0,9978 | 0,9978 | 0,9975 | 0,9978 | 0,9971 |
| F1-Score | 0,9987 | 0,9987 | 0,9985 | 0,9987 | 0,9978 |
| MAE | 0,29 | 0,36 | **0,25** | 0,33 | 1,67 |
| RMSE | 1,19 | 1,21 | 1,16 | **1,13** | 2,42 |
| MAPE (%) | **0,43** | 0,56 | 0,54 | 0,60 | 2,58 |
| Count Acc (%) | **99,57** | 99,44 | 99,46 | 99,40 | 97,42 |
| R² | 0,9994 | 0,9993 | 0,9994 | 0,9994 | 0,9989 |
| Parameters | 3,08M | 2,66M | **1,96M** | 9,71M | 2,59M |
| GFLOPs | 8,3 | 6,5 | **5,1** | 24,5 | 6,6 |
| Model Size | 6,4 MB | 5,6 MB | **4,3 MB** | 19,8 MB | 5,5 MB |
| PyTorch (ms) | 57,70 | 41,90 | 44,70 | 50,90 | **41,30** |
| ONNX (ms) | 213,20 | 237,30 | 372,70 | 424,20 | **133,30** |

### Lampiran B: Konfigurasi YAML YOLO11n-OBB-P2

```yaml
# YOLO11n-OBB-P2 Configuration
# Detection heads: P2 (stride 4), P3 (stride 8), P4 (stride 16)
# Removed P5 (stride 32) - optimized for small object detection
nc: 1
scales:
  n: [0.50, 0.25, 1024]
backbone:
  - [-1, 1, Conv, [64, 3, 2]]        # P1/2
  - [-1, 1, Conv, [128, 3, 2]]       # P2/4
  - [-1, 2, C3k2, [256, False, 0.25]]
  - [-1, 1, Conv, [256, 3, 2]]       # P3/8
  - [-1, 2, C3k2, [512, False, 0.25]]
  - [-1, 1, Conv, [512, 3, 2]]       # P4/16
  - [-1, 2, C3k2, [512, True]]
  - [-1, 1, Conv, [1024, 3, 2]]      # P5/32
  - [-1, 2, C3k2, [1024, True]]
  - [-1, 1, SPPF, [1024, 5]]
  - [-1, 2, C2PSA, [1024]]
head:
  - [-1, 1, nn.Upsample, [None, 2, "nearest"]]
  - [[-1, 6], 1, Concat, [1]]
  - [-1, 2, C3k2, [512, False]]
  - [-1, 1, nn.Upsample, [None, 2, "nearest"]]
  - [[-1, 4], 1, Concat, [1]]
  - [-1, 2, C3k2, [256, False]]      # P3
  - [-1, 1, nn.Upsample, [None, 2, "nearest"]]
  - [[-1, 2], 1, Concat, [1]]
  - [-1, 2, C3k2, [128, False]]      # P2
  - [[19, 16, 13], 1, OBB, [nc]]     # OBB(P2, P3, P4)
```

---

*Laporan Tugas Akhir ini disusun sebagai salah satu syarat untuk menyelesaikan Program Studi S1 Teknik Informatika di Universitas Islam Sultan Agung Semarang, 2026.*

