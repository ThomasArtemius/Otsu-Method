# Otsu-Method

## Introduction
![](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Image_otsu%20min.jpg)

Ada 2 cara metode otsu untuk mendapatkan *threshold* yang optimal: memanfaatkan *within-class variance* atau *between-class variance*

Perbedaannya adalah terletak pada pemilihan varians-nya. Pada *within-class* varians, dipilih varians terkecil. Sementara untuk *betwee-class* variance memilih varians terbesar.

### Within-class Variance

$$\sigma_W^2 = W_b\sigma_b^2 + W_f\sigma_f^2$$

Dimana:
- $W_b$ adalah bobot dari *background* dan $W_f$ adalah bobot dari *foreground* (persentase piksel pada masing-masing grup).
- $\sigma_b^2$ adalah varian dari *background* dan $\sigma_f^2$ adalah varian dari *foreground*. Nilai ini merepresentasikan seberapa menyebarnya intensitas piksel dalam grup tersebut.

### Between-class Variance

$$\sigma_B^2 = W_b W_f (\mu_b - \mu_f)^2$$

Dimana:
- $W_b$ dan $W_f$ adalah bobot *background* dan *foreground*.
- $\mu_b$ dan $\mu_f$ adalah rata-rata untuk *background* dan *foreground*
- $(\mu_b - \mu_f)^2$ perbedaan rata-rata dari masing-masing grup. Nilai ini perlu dimaksimalkan.

### Threshold dari kedua metode

Masing-masing akan menghasilkan threshold yang sebenarnya sama tapi beda representasi. Hal ini bisa dijelaskan dengan analogi pagar.\
Katakanlah *Between-class Variance* menunjukan *threshold* adalah 140, sedangkan *Within-class Variance* menunjukan *threshold* adalah 139.

Maksudnya adalah, dalam metode *within-class variance*, nilai 0-139 adalah *background*; dalam *between-class variance*, nilai 140-(seterusnya) adalah *foreground*.

## Otsu Method Process
![](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Otsu_Process%20min.gif)

## Result
![](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Result_Within_Class.png)

### Analisis

Dengan menggunakan *threshold* 140, ditemukan akurasi 83.06% dan IoU 71%. Tapi apakah benar threshold 140 adalah *threshold* terbaik?

## Performa Berdasarkan Akurasi dan IoU

Jika dalam proses segmentasi tidak memiliki *ground truth*, maka menggunakan varian terkecil dari *Within-class variance* sudah cukup. Namun, jika menggunakan *ground truth* maka yang memiliki IoU terbesarlah yang terbaik.

Ada 4 komponen dasar dalam penghitungan akurasi dan IoU:
- **True Positive (TP):** piksel yang dengan tepat memprediksi *foreground*.
- **True Negative (TN):** piksel yang dengan tepat memprediksi *background*.
- **False Positive (FP):** piksel yang tecara tidak tepat diprediksi sebagai *foreground* (*background* dianggap sebagai *foreground*).
- **False Negative (FN):** pikel yang secara tidak tepat diprediksi sebagai *background* (piksel *foreground* dianggap sebagai *background*).

### Akurasi
$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

Akurasi mengukur persentase keseluruhan piksel yang dianggap benar. Dengan begitu, akurasi bisa dianggap sebagai metrik yang kurang tepat, karena jika suatu gambar memiliki *background* yang lebih besar, maka pasti memiliki nilai akurasi yang tinggi.

### IoU
$$\text{IoU} = \frac{\text{Intersection}}{\text{Union}} = \frac{TP}{TP + FP + FN}$$

IoU (Intersection over Union) lebih fokus pada objek (*foreground*) dan tidak akan "terdistorsi" oleh nilai prediksi yang besar dari *background*.

## Hasil Dari Metrik Within-Class Variance, Akurasi, dan IoU

### Within-Class Variance

| Threshold | Within-Class Variance |
|-----------|------------------------|
| 140       | 1123.17                |
| 139       | 1123.32                |
| 141       | 1123.52                |
| 138       | 1123.95                |
| 142       | 1124.36                |

Hasil lengkap bisa dilihat di [sini](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Analysis_Sorted_by_Variance.csv)

### Accuracy
| Threshold | Accuracy |
|-----------|----------|
| 170       | 0.8527   |
| 171       | 0.8527   |
| 172       | 0.8527   |
| 169       | 0.8526   |
| 173       | 0.8526   |

Hasil lengkap bisa dilihat di [sini](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Analysis_Sorted_by_Accuracy.csv)

### IoU
| Threshold | IoU    |
|-----------|--------|
| 177       | 0.7643 |
| 178       | 0.7642 |
| 176       | 0.7642 |
| 179       | 0.7641 |
| 175       | 0.7641 |

Hasil lengkap bisa dilihat di [sini](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Analysis_Sorted_by_IoU.csv)

## Histogram
![](https://github.com/ThomasArtemius/Otsu-Method/blob/main/histogram_best_metrics.png)

Dari hasil penghitungan di atas bisa dilihat bahwa:
- Threshold 140 adalah *threshold* yang memegang nilai *within-class variance* terkecil. Lebih cocok untuk *task* yang tidak memiliki *ground truth*
- Threshold 170 adalah *threshold* yang memegang nilai akurasi tertinggi.
- Threshild 177 adalah *threshold* yang memegang nilai IoU terbaik. Metrik yang cocok jika memiliki ground truth.
