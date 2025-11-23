# Proyek Klasifikasi Gambar: Vegetable Image Dataset

Proyek ini adalah submission akhir untuk klasifikasi gambar sayuran menggunakan Convolutional Neural Network (CNN). Model dilatih untuk mengenali berbagai jenis sayuran dari dataset gambar.

## Informasi Penulis
- **Nama:** Firdaus Khotibul Zickrian
- **Email:** espejodaniel50@gmail.com
- **ID Dicoding:** Firdaus Khotibul Zickrian

## Struktur Proyek
Berikut adalah struktur direktori dari submission ini:

```
submission
├───tfjs_model
| ├───group1-shard1of1.bin
| └───model.json
├───tflite
| ├───model.tflite
| └───label.txt
├───saved_model
| ├───saved_model.pb
| └───variables
├───notebook.ipynb
├───README.md
└───requirements.txt
```

## Dataset
Dataset yang digunakan dalam proyek ini adalah **Vegetable Image Dataset** yang diunduh dari Kaggle.
- **Sumber:** [Kaggle - Vegetable Image Dataset](https://www.kaggle.com/datasets/misrakahmed/vegetable-image-dataset)
- **Struktur Data:** Dataset dibagi menjadi tiga bagian: `train`, `validation`, dan `test`.
- **Preprocessing:**
  - Rescale 1./255
  - Augmentasi data pada training set (Rotation, Width Shift, Height Shift, Zoom, Shear, Horizontal Flip, Brightness).
  - Ukuran gambar diubah menjadi 224x224 piksel.

## Arsitektur Model
Model dibangun menggunakan TensorFlow/Keras dengan arsitektur Sequential CNN:
1. **Input Layer:** (224, 224, 3)
2. **Block 1:** Conv2D (32 filters) + MaxPooling2D
3. **Block 2:** Conv2D (64 filters) + MaxPooling2D
4. **Block 3:** Conv2D (128 filters) + MaxPooling2D
5. **Block 4:** Conv2D (128 filters) + MaxPooling2D
6. **Flatten Layer**
7. **Dense Layer:** 512 units (ReLU) + Dropout (0.5)
8. **Output Layer:** Dense (Softmax) sesuai jumlah kelas.

## Konfigurasi Training
- **Optimizer:** Adam (learning rate = 1e-3)
- **Loss Function:** Categorical Crossentropy
- **Metrics:** Accuracy
- **Callbacks:**
  - `EarlyStopping`: Menghentikan training jika val_loss tidak membaik selama 5 epoch.
  - `ModelCheckpoint`: Menyimpan model terbaik berdasarkan val_accuracy.
  - `ReduceLROnPlateau`: Mengurangi learning rate jika val_loss stagnan.
- **Epochs:** 25

## Evaluasi Model
Model dievaluasi menggunakan data test dengan metrik akurasi dan loss. Visualisasi hasil training (grafik akurasi & loss) serta Confusion Matrix dan Classification Report disertakan dalam notebook untuk analisis performa model.

## Format Model
Model yang telah dilatih diekspor ke dalam tiga format untuk kebutuhan deployment yang berbeda:
1. **SavedModel:** Format standar TensorFlow (`saved_model/`).
2. **TensorFlow Lite (TFLite):** Format ringan untuk perangkat mobile/edge (`tflite/model.tflite`), dilengkapi dengan `label.txt`.
3. **TensorFlow.js (TFJS):** Format untuk deployment berbasis web (`tfjs_model/`).

## Cara Menjalankan
1. Pastikan Python dan pip sudah terinstal.
2. Instal dependencies yang diperlukan:
   ```bash
   pip install -r requirements.txt
   ```
3. Jalankan notebook `Submission_Akhir.ipynb` (atau `notebook.ipynb` jika telah diubah namanya) menggunakan Jupyter Notebook, VS Code, atau Google Colab.
