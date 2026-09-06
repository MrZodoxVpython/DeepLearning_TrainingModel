# CNN CIFAR-10 — Perbandingan Simple CNN dan Residual CNN

Implementasi dan perbandingan dua arsitektur Convolutional Neural Network (CNN) untuk klasifikasi citra **CIFAR-10** menggunakan TensorFlow/Keras.

## Dataset

* **Dataset:** CIFAR-10
* **Jumlah kelas:** 10
* **Data training:** 45.000
* **Data validation:** 5.000
* **Data testing:** 10.000
* **Ukuran citra:** 32 × 32 × 3
* **Framework:** TensorFlow / Keras

## Model

### Model A — Simple CNN

Custom CNN tanpa residual connection yang ditingkatkan kapasitasnya agar mampu memberikan performa yang kompetitif.

* 4 convolutional blocks
* 2 Conv2D per block
* Filter: **32 → 64 → 128 → 256**
* Batch Normalization
* ReLU activation
* MaxPooling2D ×3
* Global Average Pooling
* Dense 128
* Dropout
* L2 Regularization
* Output: Softmax 10 kelas

### Model B — Residual CNN

Custom CNN dengan residual/skip connection untuk membantu aliran gradient dan proses optimasi.

* 3 residual blocks
* 2 Conv2D per block
* Filter: **32 → 64 → 128**
* Batch Normalization
* ReLU activation
* Residual / skip connection
* MaxPooling2D ×3
* Global Average Pooling
* Dropout
* L2 Regularization
* Output: Softmax 10 kelas

## Hyperparameter Utama

| Parameter         |                            Nilai |
| ----------------- | -------------------------------: |
| Epoch             |                           **15** |
| Batch Size        |                          **128** |
| Optimizer         |                         **Adam** |
| Learning Rate     |                        **0.001** |
| Weight Decay / L2 |                       **0.0001** |
| Random Seed       |                           **42** |
| Data Augmentation | Rotation, Shift, Horizontal Flip |

Kedua model menggunakan **hyperparameter training yang sama** agar perbandingan performa tetap fair.

## Hasil Utama

| Metrik        |          Model A |  Model B |
| ------------- | ---------------: | -------: |
| Test Accuracy |       **75.63%** | **≈75%** |
| Parameter     |                — |        — |
| Training Time | **570.29 detik** |        — |

> Parameter dan waktu training Model B diambil langsung dari hasil eksperimen notebook. Nilai tidak dicantumkan di README apabila belum dikonfirmasi dari hasil akhir.

### Model A dengan Dropout

* **Test Accuracy:** 75.63%
* **Test Loss:** 0.8754
* **Training Time:** 570.29 detik (**≈9,50 menit**)

## Ablation Study

Eksperimen tambahan dilakukan pada Model A dengan membandingkan:

* **Model A + Dropout**
* **Model A tanpa Dropout**

Tujuannya untuk melihat pengaruh Dropout terhadap **overfitting**, khususnya melalui perbedaan (*gap*) antara training accuracy dan validation accuracy.

## Kesimpulan

Model A yang telah ditingkatkan dengan **4 convolutional blocks** mampu menghasilkan performa yang kompetitif dan mencapai **75.63% test accuracy**, sedikit lebih tinggi dibandingkan Model B pada eksperimen ini.

Hasil tersebut menunjukkan bahwa **residual connection tidak selalu menjamin akurasi yang lebih tinggi**. Performa CNN dipengaruhi oleh kombinasi kapasitas arsitektur, regularisasi, optimasi, dan karakteristik dataset.

Eksperimen juga menunjukkan pentingnya **Dropout sebagai teknik regularisasi** untuk membantu mengendalikan overfitting.

## Struktur Eksperimen

```text
B.1 Dataset & Setup
B.2 Model Implementation
    ├── Model A — Simple CNN
    └── Model B — Residual CNN
B.3 Experiments & Evaluation
    ├── Training & Validation
    ├── Accuracy & Loss
    ├── Test Accuracy
    ├── Parameter Count
    ├── Training Time
    └── Confusion Matrix
B.4 Ablation Study
    └── Dropout vs Without Dropout
B.5 Analysis & Reflection
```

## Tools

* Python
* TensorFlow / Keras
* NumPy
* Pandas
* Matplotlib
* Seaborn
* Scikit-learn
* Google Colab GPU
