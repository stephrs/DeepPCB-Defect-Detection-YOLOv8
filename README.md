# DeepPCB-Defect-Detection-YOLOv8
> Real-time microscopic defect detection pipeline for Printed Circuit Boards (PCB) using YOLOv8-Nano. Built for Automated Optical Inspection (AOI) in smart manufacturing.

# YOLOv8 DeepPCB Defect Detection: Short Term IRIS

![YOLOv8](https://img.shields.io/badge/YOLOv8-Ultralytics-blue)
![Python](https://img.shields.io/badge/Python-3.12-yellow)
![Status](https://img.shields.io/badge/Status-Completed-success)

Proyek ini adalah implementasi *end-to-end Machine Learning pipeline* menggunakan arsitektur **YOLOv8-Nano** untuk mendeteksi anomali/cacat mikroskopis pada *Printed Circuit Boards* (PCB) secara *real-time*. Proyek ini dikembangkan sebagai bagian dari riset otomasi cerdas *Computer Vision* pada lini manufaktur.

## Fitur Utama Pipeline
*notebook* ini dirancang dengan standar industri yang mencakup:
1. **Bipartite Graph & Negative Mining:** Pemetaan otomatis gambar cacat (positif) dan gambar background bersih (negatif) untuk melatih model mengenali *noise* dan mengurangi *False Positives*.
2. **Exploratory Data Analysis (EDA):** Visualisasi ekstraktif berbasis kelas untuk inspeksi *bounding box* secara langsung sebelum pelatihan.
3. **Safe YOLO Format Conversion:** Standardisasi domain gambar menjadi *Grayscale 3-Channel* dan konversi koordinat absolut ke koordinat relatif YOLO secara aman.
4. **Evaluasi Halusinasi Model:** Skrip analisis visual khusus untuk membandingkan fakta (*Ground Truth*) dengan halusinasi/prediksi salah pada area *background*.

## Arsitektur Model YOLO
![Generic YOLO Architecture](images/yolo_generic_architecture.jpg)

*Gambar: Diagram umum arsitektur YOLO (Input -> Backbone -> Neck -> Head) yang menjadi fondasi teknologi dalam proyek ini. Meskipun proyek ini mengimplementasikan YOLOv8, diagram di atas secara akurat menggambarkan alur kerja fundamental model dalam mengekstraksi fitur dan melakukan Dense Prediction.*

## Dataset
Dataset yang digunakan adalah subset **DeepPCB**, yang memuat pasangan gambar PCB berkualitas tinggi (resolusi asli di-*resize* ke 640x640). 
Model mendeteksi 6 kelas cacat:
* `open`
* `short`
* `mousebite`
* `spur`
* `copper`
* `pin-hole`

## Hyperparameter Training
Model dilatih menggunakan akselerator GPU (NVIDIA Tesla T4 di Kaggle) dengan konfigurasi:
* **Model:** YOLOv8 Nano (`yolov8n.pt`)
* **Epochs:** 50
* **Image Size:** 640
* **Batch Size:** 16
* **Waktu Konvergensi:** ~13 Menit

## Hasil Evaluasi (mAP & Metrics)
Berdasarkan agregasi metrik iterasi terminal (50 Epochs):
* Model mencapai akurasi lokalisasi dasar (**mAP@50**) yang nyaris sempurna di angka **98.9%**.
* Presisi kotak ketat (**mAP@50-95**) mencapai **78.4%**.
* Analisis *Confusion Matrix* menunjukkan arsitektur sangat ahli membedakan kelas cacat, meskipun masih terdapat ruang optimasi pada *False Positives* di area latar belakang bersih.

## 🛠️ Cara Penggunaan (How to Run)
1. *Clone repository* ini:
   ```bash
   git clone [https://github.com/stephrs/DeepPCB-Defect-Detection-YOLOv8](https://github.com/stephrs/DeepPCB-Defect-Detection-YOLOv8/edit/main/README.md)
2. Instal pustaka yang dibutuhkan:
   ```bash
   pip install ultralytics opencv-python-headless matplotlib pandas scikit-learn
3. Sesuaikan path dataset pada variabel `INPUT_DIR` di dalam notebook, lalu jalankan sel secara berurutan.


## Kontributor
- Ashif Dyan Armawan (164241040) - IRIS Researcher 2024
- Stephen Richard Sihombing (164251055) - IRIS Researcher 2025
