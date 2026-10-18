======================================================================
README - STUDI KASUS KLASIFIKASI: DIAGNOSIS KANKER PAYUDARA
Breast Cancer Wisconsin (Diagnostic) dengan Machine Learning
======================================================================

1. ISI FOLDER
----------------------------------------------------------------------
- studi_kasus_klasifikasi_kanker_payudara.ipynb : notebook Python (kode
  + penjelasan + hasil eksekusi)
- wdbc_breast_cancer.csv                        : dataset mentah
- readme.txt                                    : berkas ini

2. RINGKASAN KASUS
----------------------------------------------------------------------
Tujuan  : mengklasifikasikan tumor payudara sebagai GANAS (Malignant, M)
          atau JINAK (Benign, B) berdasarkan ciri inti sel dari citra
          Fine Needle Aspirate (FNA).
Jenis   : klasifikasi biner (supervised learning).
Metode  : Logistic Regression, KNN, Decision Tree, SVM (RBF), Random
          Forest; model terbaik (SVM) dituning dengan GridSearchCV.
Hasil   : pada data uji (114 pasien) SVM tuned mencapai akurasi 97,4%,
          precision 100%, recall 92,9%, F1 0,963, ROC-AUC 0,993.

3. DATASET (wdbc_breast_cancer.csv)
----------------------------------------------------------------------
Sumber asli : UCI Machine Learning Repository, "Breast Cancer Wisconsin
              (Diagnostic)", ID 17, lisensi CC BY 4.0
              https://archive.ics.uci.edu/dataset/17/breast-cancer-wisconsin-diagnostic
Pembuat     : William H. Wolberg, W. Nick Street, Olvi L. Mangasarian
              (University of Wisconsin), didonasikan tahun 1995.
Catatan     : CSV ini diekspor dari salinan dataset yang sama di
              scikit-learn (sklearn.datasets.load_breast_cancer), dengan
              label dikembalikan ke format UCI (M/B). Kolom ID pasien
              tidak tersedia pada salinan ini.

Ukuran      : 569 baris (pasien) x 31 kolom
Missing     : tidak ada
Kelas       : B (jinak) = 357 (62,7%) ; M (ganas) = 212 (37,3%)

Kolom:
- diagnosis : label/target. M = ganas, B = jinak.
- 30 fitur numerik, berasal dari 10 ciri inti sel, masing-masing dihitung
  dalam 3 bentuk (mean = rata-rata, error = galat standar, worst = rata-
  rata dari tiga nilai terbesar). Awalan kolom menunjukkan bentuknya:

  Ciri dasar (10)         Arti
  ---------------------   ------------------------------------------
  radius                  rata-rata jarak pusat ke tepi inti sel
  texture                 simpangan baku nilai skala abu-abu
  perimeter               keliling inti sel
  area                    luas inti sel
  smoothness              variasi lokal panjang radius
  compactness             perimeter^2 / area - 1,0
  concavity               tingkat keparahan bagian cekung kontur
  concave_points          jumlah bagian cekung pada kontur
  symmetry                kesimetrisan inti sel
  fractal_dimension       "coastline approximation" - 1

  Contoh nama kolom: mean_radius, radius_error, worst_radius,
  mean_concave_points, worst_texture, dst.

4. ISI NOTEBOOK (.ipynb) - URUTAN BAGIAN
----------------------------------------------------------------------
1. Latar belakang & permasalahan
2. Sumber data & rujukan
   2.1 Penjelasan dataset: gambaran umum, tabel ringkasan (jumlah data,
       target, distribusi kelas), struktur 30 fitur (10 ciri x mean/error/
       worst), kamus data 10 ciri dasar, dan catatan penggunaan; ditutup
       sel kode yang menampilkan kamus nama kolom
3. Metode klasifikasi yang dibandingkan
4. Tahapan penerapan:
   4.1 Import library & muat data mentah
   4.2 Eksplorasi data (EDA): info data, missing value, distribusi
       kelas, statistik deskriptif, boxplot, heatmap korelasi
   4.3 Pra-pemrosesan: M->1, B->0; split 80% latih / 20% uji
       (stratifikasi, random_state=42); StandardScaler di dalam
       Pipeline agar tidak terjadi data leakage
   4.4 Pemodelan: 5 algoritma dibandingkan dengan Stratified 5-Fold CV
   4.5 Tuning hyperparameter SVM (C, gamma, kernel) dengan GridSearchCV
   4.6 Evaluasi akhir pada data uji: accuracy, precision, recall, F1,
       ROC-AUC, classification report, confusion matrix, kurva ROC
   4.7 Interpretasi: permutation importance (10 fitur terpenting)
   4.8 Perbandingan semua model pada data uji + contoh prediksi 5 pasien
5. Hasil, pembahasan, dan manfaat
6. Keterbatasan
7. Daftar pustaka

5. CARA MENJALANKAN
----------------------------------------------------------------------
a. Pastikan Python 3.9+ terpasang, lalu instal library:
     pip install numpy pandas matplotlib seaborn scikit-learn jupyter
b. Letakkan wdbc_breast_cancer.csv SATU FOLDER dengan file .ipynb.
   (Jika CSV tidak ditemukan, notebook otomatis memuat data dari
   scikit-learn.)
c. Jalankan:  jupyter notebook
   Buka file .ipynb, lalu pilih Run > Run All Cells.
   Alternatif: unggah kedua berkas ke Google Colab.
d. Hasil sama setiap dijalankan karena random_state dikunci (42).

6. KETERBATASAN
----------------------------------------------------------------------
- Data hanya 569 pasien dari satu institusi; perlu validasi eksternal.
- Data uji kecil (114), selisih 1 kasus mengubah metrik cukup besar.
- Model bukan pengganti dokter; hanya alat bantu keputusan. Pada data
  uji, 3 dari 42 kasus ganas masih terlewat (false negative).

7. DAFTAR PUSTAKA
----------------------------------------------------------------------
1. Wolberg, W., Mangasarian, O., Street, N., & Street, W. (1995).
   Breast Cancer Wisconsin (Diagnostic) [Dataset]. UCI Machine Learning
   Repository. https://archive.ics.uci.edu/dataset/17/breast-cancer-wisconsin-diagnostic
2. Street, W.N., Wolberg, W.H., & Mangasarian, O.L. (1993). Nuclear
   feature extraction for breast tumor diagnosis. IS&T/SPIE Symposium on
   Electronic Imaging, vol. 1905, hlm. 861-870.
3. Wolberg, W.H., Street, W.N., & Mangasarian, O.L. (1994). Machine
   learning techniques to diagnose breast cancer from fine-needle
   aspirates. Cancer Letters, 77, 163-171.
4. Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in
   Python. Journal of Machine Learning Research, 12, 2825-2830.
