# Proyek Prediksi Diabetes (Pima Indians Dataset)

## Deskripsi Singkat

Proyek ini bertujuan membangun model *machine learning* untuk memprediksi risiko diabetes pada pasien berdasarkan indikator medis. Fokus utama proyek adalah penerapan *end-to-end data science workflow*, mulai dari eksplorasi data, *data preprocessing* yang ketat, hingga evaluasi dan perbandingan performa beberapa model klasifikasi.

Dataset yang digunakan merupakan dataset medis populer sehingga proyek ini juga berfungsi sebagai studi kasus penerapan *best practice* dalam pemodelan data kesehatan.

---

## Deskripsi Dataset

Dataset yang digunakan adalah **Pima Indians Diabetes Dataset** (`diabetes.csv`). Dataset ini berisi data medis pasien wanita keturunan Pima Indian dengan karakteristik sebagai berikut:

### Fitur Input

* `Pregnancies` : Jumlah kehamilan
* `Glucose` : Kadar glukosa plasma
* `BloodPressure` : Tekanan darah diastolik (mm Hg)
* `SkinThickness` : Ketebalan lipatan kulit trisep (mm)
* `Insulin` : Kadar insulin serum (mu U/ml)
* `BMI` : Body Mass Index (kg/m²)
* `DiabetesPedigreeFunction` : Indikator riwayat genetik diabetes
* `Age` : Usia (tahun)

### Target

* `Outcome`

  * `0` : Tidak Diabetes
  * `1` : Diabetes

---

## Tahapan Preprocessing Data

Berdasarkan notebook **`SF-3_DataCleansing.ipynb`**, preprocessing dilakukan secara komprehensif dengan tahapan berikut:

### 1. Imputasi Missing Values

Beberapa fitur medis (`Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, dan `BMI`) memiliki nilai `0` yang secara medis tidak valid. Nilai tersebut diperlakukan sebagai *missing values* dan ditangani menggunakan:

* **Median Imputation** untuk fitur dengan distribusi relatif simetris
* **KNN Imputation** untuk fitur dengan pola hubungan kompleks antar variabel

### 2. Penanganan Outlier

Outlier dideteksi menggunakan metode **Interquartile Range (IQR)**. Nilai ekstrem kemudian ditangani menggunakan teknik **capping**, yaitu membatasi nilai pada batas minimum dan maksimum yang wajar agar tidak mendistorsi performa model.

### 3. Transformasi Data

Beberapa fitur dengan distribusi miring (*skewed distribution*) ditangani menggunakan **log transformation** untuk mendekati distribusi normal dan meningkatkan stabilitas model.

---

## Model dan Optimasi

Model yang digunakan merupakan model klasifikasi biner dengan fokus pada performa prediksi kelas diabetes.

### Algoritma yang Digunakan

* **Random Forest Classifier**
* **XGBoost Classifier**

### Optimasi Model

* **Hyperparameter tuning** dilakukan menggunakan `GridSearchCV`
* Evaluasi dilakukan pada data validasi untuk memilih kombinasi parameter terbaik

---

## Skenario Pengujian & Metrik Evaluasi

Dataset dibagi menjadi *training set* dan *testing set*. Evaluasi model menggunakan metrik berikut:

* **Accuracy** : Persentase prediksi yang benar
* **Precision** : Ketepatan prediksi positif
* **Recall** : Kemampuan model mendeteksi seluruh kasus diabetes
* **F1-Score** : Rata-rata harmonis antara Precision dan Recall

---

## 📈 Hasil Evaluasi Model

### 🔹 Skenario 1: Menggunakan Seluruh Fitur

#### Random Forest

* **Accuracy** : 0.73

```
precision    recall  f1-score   support

0       0.76      0.84      0.80       100
1       0.64      0.52      0.57        54

accuracy                           0.73       154
```

#### XGBoost

* **Accuracy** : 0.75

```
precision    recall  f1-score   support

0       0.80      0.81      0.81       100
1       0.64      0.63      0.64        54

accuracy                           0.75       154
```

#### XGBoost + GridSearchCV

* **Accuracy** : 0.72

```
precision    recall  f1-score   support

0       0.78      0.80      0.79       100
1       0.61      0.57      0.59        54

accuracy                           0.72       154
```

---

### Skenario 2: Menggunakan Top 5 Fitur Terpenting

#### XGBoost

* **Accuracy** : 0.71

```
Akurasi model XGBoost: 0.7143

Laporan Klasifikasi:
              precision    recall  f1-score   support

           0       0.77      0.80      0.78       100
           1       0.60      0.56      0.58        54

    accuracy                           0.71       154
   macro avg       0.68      0.68      0.68       154
weighted avg       0.71      0.71      0.71       154
```

#### Random Forest

* **Accuracy** : 0.72
```
Akurasi model Random Forest: 0.7208

Laporan Klasifikasi:
              precision    recall  f1-score   support

           0       0.76      0.83      0.79       100
           1       0.62      0.52      0.57        54

    accuracy                           0.72       154
   macro avg       0.69      0.67      0.68       154
weighted avg       0.71      0.72      0.71       154
```

Hasil menunjukkan bahwa reduksi fitur tidak memberikan peningkatan performa signifikan dibandingkan penggunaan seluruh fitur.

---

## Analisis Keberhasilan & Tujuan Bisnis

### Pencapaian Teknis

* Model mencapai akurasi hingga **75%**, menunjukkan performa klasifikasi yang cukup baik
* *Recall* kelas non-diabetes relatif tinggi (>0.80)
* *Recall* kelas diabetes masih moderat (~0.57), menandakan potensi *false negative*

### Nilai Bisnis

Dalam konteks medis, kesalahan *false negative* sangat berisiko. Model ini dapat digunakan sebagai **alat skrining awal** untuk mengidentifikasi pasien berisiko tinggi, namun tetap memerlukan validasi lanjutan oleh tenaga medis profesional.

---

## Rekomendasi Pengembangan Selanjutnya

1. **Menangani Imbalanced Data**

   * Menggunakan SMOTE atau metode *resampling* lainnya untuk meningkatkan *recall* kelas diabetes

2. **Eksplorasi Model Lanjutan**

   * LightGBM, CatBoost, atau stacking ensemble

3. **Feature Engineering**

   * Membuat fitur turunan seperti rasio `Glucose/BMI` atau interaksi antar variabel medis

4. **Evaluasi Tambahan**

   * ROC-AUC dan Precision-Recall Curve untuk analisis lebih mendalam

---


