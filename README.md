
# Images Processing(Just Python, Numpy, Cython)

This proceject is to compare performace of differences filters(Gaussian Filter, Sobel Filter, Median Filter), The main goal is to explore how fundamental image filters work under the hood, including Gaussian blurring, edge detection with Sobel filters, and noise reduction with median filters.



## Overview

This project demonstrates the application of different image processing techniques using pure Python, NumPy, and NumPy with Cython for optimization. The notebook implements three main filters:

- Pure Python (without Numpy)
- NumPy (using matrix operations for optimization)
- NumPy + Cython (optimizing with compiled C functions)

## Dependencies

The project requires the following libraries:

- numpy (for array operations and vectorization)

- cv2 (OpenCV for image handling)

- cython (for performance optimization)


## Requirements
Antes de ejecutar el código, instala las dependencias necesarias con:

```bash
pip install numpy opencv-python matplotlib cython pillow

````

## Local running

``
pip install -r requirements.txt
``


```
import cv2
import numpy as np
import matplotlib.pyplot as plt

## Cargar la imagen en escala de grises
img = cv2.imread("SAPOS.jpg", cv2.IMREAD_GRAYSCALE)
cv2.imshow("Imagen Original", img)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

## #2. Alternativa con Matplotlib

Si `cv2.imshow()` no funciona, usa Matplotlib:

```

plt.imshow(img, cmap='gray')
plt.title("Imagen Original")
plt.axis("off")
plt.show()

```


### Implementations comparation

Three ways of applying filters are compared:

-**Pure Python**: Implementation without optimization.

-**NumPy**: Use of vectorized operations to improve performance.

-**Cython**: Compiled code for maximum efficiency.


### Sobel filter example:

```


sobel_x = np.array([[-1, 0, 1], [-2, 0, 2], [-1, 0, 1]], dtype=np.float32)
sobel_y = np.array([[-1, -2, -1], [ 0,  0,  0], [ 1,  2,  1]], dtype=np.float32)

grad_x = cv2.filter2D(img, cv2.CV_64F, sobel_x)
grad_y = cv2.filter2D(img, cv2.CV_64F, sobel_y)

magnitude = np.sqrt(grad_x**2 + grad_y**2)
magnitude = np.clip(magnitude, 0, 255).astype(np.uint8)

plt.imshow(magnitude, cmap='gray')
plt.title("Detección de Bordes (Sobel)")
plt.axis("off")
plt.show()



```


