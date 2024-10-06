
# Visión por Computador: Práctica 3. Detección y reconocimiento de formas

### Autores

- [@Santiago Santana Martínez](https://github.com/Tiago1615)
- [@Mauro Gómez Guillén](https://github.com/MGGdesigns)

## Tabla de Contenidos

- [Paquetes necesarios](#paquetes-necesarios)
- [Introducción](#introducción)
- [Tareas](#tareas)
  - [Tarea 1](#tarea-1)
    - [Detección de Monedas en Tiempo Real](#deteccion-de-monedas-en-tiempo-real)
    - [Extra: Demo en vivo](#extra-demo-en-vivo)
    - [Problemas Detectados](#problemas-detectados)
  - [Tarea 2](#tarea-2)
- [Referencias Bibliográficas](#referencias-bibliográficas)

---

## Paquetes necesarios

- **Librerías**:
  - `opencv-python`
  - `numpy`
  - `matplotlib`

```bash
pip install opencv-python
```

```bash
pip install numpy
```

```bash
pip install matplotlib
```

```bash
pip install scikit-learn seaborn
```

## Introducción:
El objetivo de esta práctica es adquirir los conocimientos necesarios para extraer información geométrica de los objetos presentes en una imagen.
Pudiendo así, ser capaces de reconocerlos de forma completamente automática.

---

## Tareas

### Tarea 1
A partir de una imagen con monedas no solapadas, identificar interactivamente (haciendo clic) una moneda de un determinado valor. Mostrando la cantidad de monedas de un mismo valor y la cantidad de dinero presente en la imagen.

#### Detección de Monedas en Imágenes Estáticas

- El programa carga una imagen (`MonedasPropias.jpg`) y la convierte a escala de grises.
- Se aplica un suavizado con filtro Gaussiano para reducir el ruido y facilitar la detección de bordes con el algoritmo de Canny.
- Posteriormente, se utiliza la Transformada de Hough para detectar círculos, los cuales representan las posibles monedas.
- El usuario selecciona una moneda con un clic, y el sistema:
  - Determina el valor de la moneda seleccionada.
  - Detecta y cuenta el resto de las monedas.
  - Muestra el número total de monedas y el valor acumulado.

#### Extra: Demo en vivo

- El sistema captura el video desde la cámara en tiempo real y, al presionar la tecla **'1'**, se congela el cuadro para procesarlo.
- Se realiza el mismo procesamiento de imagen (escala de grises, suavizado, bordes y Hough) para identificar monedas.
- El sistema dibuja círculos sobre las monedas detectadas y calcula el número total de monedas, además de sumar el valor de cada una.
- Los resultados se muestran en pantalla.


#### Problemas Detectados

1. **Relación de Escala Inexacta**: El uso de escalas puede generar errores en la detección precisa de las monedas seleccionadas.
2. **Rango de Radios en la Transformada de Hough**: Los valores de radio mínimo y máximo pueden ocasionar falsos positivos.
3. **Dificultad en Condiciones de Iluminación Variables**: La detección de bordes y umbralización depende mucho de las condiciones de iluminación, lo que puede dificultar la precisión en algunas imágenes.

---

### Tarea 2
A partir de tres imágenes, extraer características geométricas y/o visuales e identificar patrones que permitan distinguir las partículas de cada una de las tres clases. Realizando además, una evaluación de los aciertos y fallos mediante una matriz de confusión.

---

## Referencias Bibliográficas

- [Guión de la práctica](https://github.com/otsedom/otsedom.github.io/tree/main/VC/P3)
- [OpenCV dibujo de contornos](https://docs.opencv.org/4.x/d4/d73/tutorial_py_contours_begin.html)
- [OpenCV flags para dibujar contornos](https://docs.opencv.org/4.x/d3/dc0/group__imgproc__shape.html#ga819779b9857cc2f8601e6526a3a5bc71)

---

