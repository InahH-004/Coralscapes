# Coralscapes

🌊 Automated Coral Bleaching Detection Using U-Net Semantic Segmentation📌 

Deskripsi ProyekProyek ini mengimplementasikan model Deep Learning berbasis Citra (Computer Vision) untuk mendeteksi dan mengalkulasi tingkat keparahan pemutihan terumbu karang (coral bleaching severity). Menggunakan skala dataset Coralscapes dari ECEO-EPFL, proyek ini berhasil memetakan wilayah ekosistem bawah laut secara presisi piksel demi piksel (dense semantic segmentation) guna mendukung monitoring konservasi laut secara otomatis.

⚙️ Metodologi & Alur KerjaPipeline Data: Data ditarik langsung via Hugging Face API. 
- Resolusi gambar asli dikonversi menjadi 512 x 512 piksel untuk efisiensi VRAM GPU T4 Google Colab.
- Penyederhanaan Label (Class Re-mapping): Mereduksi 39 kelas bentik asli menjadi 4 kelas esensial: Background (0), Healthy Coral (1), Bleached Coral (2), dan Dead Coral (3) untuk mempercepat konvergensi model.
- Arsitektur Model: Menggunakan arsitektur U-Net dengan tulang punggung (backbone) ResNet34 berbasis Transfer Learning (ImageNet pre-trained weights).
- Strategi Optimasi: * Penanganan class imbalance ekstrem menggunakan Class Weights Loss dengan rasio penalti [0.5, 1.0, 4.0, 8.0]
- Akselerasi latihan menggunakan Mixed Precision Training (AMP FP16).
- Penanganan overfitting menggunakan Model Checkpoint Tracking berbasis Validation Loss terendah.

📊 Hasil & Pencapaian UtamaKondisi Optimal Model: 
Model terbaik berhasil diamankan pada Epoch 2 dengan Validation Loss terendah sebesar 0.9949 sebelum menyentuh tren overfitting.
- Skor Rapor Global: Mencapai mIoU (Mean Intersection over Union) Global sebesar 35.11% dengan Pixel Accuracy validasi sebesar 70.27%.
- Performa per Kelas: Model menunjukkan kemampuan superior dalam memetakan Healthy Coral (IoU: 71.96%) dan berhasil mengeluarkan kelas minoritas krusial dari zona buta, yaitu Dead Coral (IoU: 18.20%) dan Bleached Coral (IoU: 34.56%).
- Output Bisnis: Sistem berhasil mengekstrak metrik keputusan berupa Rasio Pemutihan (Bleaching Ratio) otomatis berdasarkan perbandingan jumlah piksel karang yang stres terhadap total koloni karang yang hidup.
