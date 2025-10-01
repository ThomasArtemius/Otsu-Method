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
![](https://github.com/ThomasArtemius/Otsu-Method/blob/main/Result.png)

## Analysis
![](https://github.com/ThomasArtemius/Otsu-Method/blob/main/histogram_best_metrics.png)
