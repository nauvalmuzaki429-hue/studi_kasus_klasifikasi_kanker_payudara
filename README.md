# 🩺 Klasifikasi Diagnosis Kanker Payudara dengan Machine Learning

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![License](https://img.shields.io/badge/Dataset-CC%20BY%204.0-green)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/USERNAME/NAMA-REPO/blob/main/studi_kasus_klasifikasi_kanker_payudara.ipynb)

Studi kasus klasifikasi biner untuk menentukan apakah tumor payudara **ganas (Malignant)** atau **jinak (Benign)** berdasarkan ciri inti sel dari citra *Fine Needle Aspirate* (FNA). Tugas individu mata kuliah Machine Learning.

## 📌 Latar Belakang

Penilaian sampel sel secara manual di bawah mikroskop bersifat subjektif dan bergantung pada pengalaman ahli patologi. Model *machine learning* dapat menjadi alat bantu keputusan yang cepat dan konsisten (*second opinion*), **bukan pengganti dokter**.

## 📊 Dataset

| Aspek | Keterangan |
|---|---|
| Nama | Breast Cancer Wisconsin (Diagnostic) |
| Sumber | [UCI Machine Learning Repository (ID 17)](https://archive.ics.uci.edu/dataset/17/breast-cancer-wisconsin-diagnostic) |
| Jumlah data | 569 pasien |
| Fitur | 30 fitur numerik (10 ciri inti sel × mean, error, worst) |
| Target | `diagnosis`: **M** = ganas (212), **B** = jinak (357) |
| Missing value | Tidak ada |
| Lisensi | CC BY 4.0 |

**10 ciri dasar inti sel:** radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, fractal dimension.

> Berkas `wdbc_breast_cancer.csv` diekspor dari salinan dataset yang sama di scikit-learn (`load_breast_cancer`), dengan label dikembalikan ke format UCI (M/B).

## 🗂️ Struktur Repositori

```
├── studi_kasus_klasifikasi_kanker_payudara.ipynb   # notebook utama (kode + penjelasan + hasil)
├── wdbc_breast_cancer.csv                          # dataset mentah
├── readme.txt                                      # penjelasan singkat isi berkas
└── README.md
```

## ⚙️ Tahapan Penerapan

1. Eksplorasi data (EDA): distribusi kelas, statistik, boxplot, heatmap korelasi
2. Pra-pemrosesan: encoding label (M=1, B=0), split 80/20 terstratifikasi, standardisasi di dalam `Pipeline` (mencegah *data leakage*)
3. Pemodelan 5 algoritma dengan Stratified 5-Fold Cross-Validation
4. Tuning hyperparameter SVM dengan `GridSearchCV` (terbaik: `C=10`, kernel RBF, `gamma='scale'`)
5. Evaluasi pada data uji: accuracy, precision, recall, F1, ROC-AUC, confusion matrix
6. Interpretasi fitur dengan *permutation importance*

## 🏆 Hasil (data uji, 114 pasien)

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| **SVM (tuned)** | **0,9737** | **1,0000** | 0,9286 | **0,9630** | 0,9927 |
| SVM (RBF) | 0,9737 | 1,0000 | 0,9286 | 0,9630 | 0,9947 |
| Random Forest | 0,9737 | 1,0000 | 0,9286 | 0,9630 | 0,9944 |
| Logistic Regression | 0,9649 | 0,9750 | 0,9286 | 0,9512 | 0,9960 |
| KNN | 0,9561 | 0,9744 | 0,9048 | 0,9383 | 0,9823 |
| Decision Tree | 0,9211 | 0,9459 | 0,8333 | 0,8861 | 0,9448 |

**Confusion matrix SVM (tuned):** TP = 39, TN = 72, FP = 0, FN = 3.

**Fitur paling berpengaruh:** `worst_texture`, `worst_concavity`, `mean_concavity`.

## 💡 Manfaat

- Memberi *second opinion* yang objektif dan konsisten bagi tenaga medis
- Mempercepat prioritas pemeriksaan saat tenaga ahli terbatas
- Mendukung deteksi dini
- Fitur penting dapat divalidasi dengan pengetahuan patologi

## 🚀 Cara Menjalankan

```bash
git clone https://github.com/USERNAME/NAMA-REPO.git
cd NAMA-REPO
pip install numpy pandas matplotlib seaborn scikit-learn jupyter
jupyter notebook
```

Buka `studi_kasus_klasifikasi_kanker_payudara.ipynb`, lalu pilih **Run → Run All Cells**. Pastikan `wdbc_breast_cancer.csv` berada di folder yang sama. Atau klik badge **Open in Colab** di atas.

## ⚠️ Keterbatasan

- Hanya 569 pasien dari satu institusi, sehingga perlu validasi eksternal
- Data uji kecil (114), satu kasus berbeda mengubah metrik cukup besar
- Pada data uji, 3 dari 42 kasus ganas masih terlewat (*false negative*)
- Untuk tujuan pembelajaran, tidak untuk penggunaan klinis nyata

## 📚 Referensi

1. Wolberg, W., Mangasarian, O., Street, N., & Street, W. (1995). *Breast Cancer Wisconsin (Diagnostic)* [Dataset]. UCI Machine Learning Repository. https://archive.ics.uci.edu/dataset/17/breast-cancer-wisconsin-diagnostic
2. Street, W.N., Wolberg, W.H., & Mangasarian, O.L. (1993). Nuclear feature extraction for breast tumor diagnosis. *IS&T/SPIE Symposium on Electronic Imaging*, 1905, 861–870.
3. Wolberg, W.H., Street, W.N., & Mangasarian, O.L. (1994). Machine learning techniques to diagnose breast cancer from fine-needle aspirates. *Cancer Letters*, 77, 163–171.
4. Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *JMLR*, 12, 2825–2830.

## 👤 Penulis

Nama: **[Nama Anda]** · NIM: **[NIM Anda]** · Mata Kuliah: Machine Learning
