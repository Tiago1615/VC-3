
# Visión por Computador: Práctica 3. Detección y reconocimiento de formas

### Autores

- [@Mauro Gómez Guillén](https://github.com/MGGdesigns)
- [@Santiago Santana Martínez](https://github.com/Tiago1615)

## Tabla de Contenidos

- [Paquetes necesarios](#paquetes-necesarios)
- [Introducción](#introducción)
- [Tareas](#tareas)
  - [Tarea 1](#tarea-1)
    - [Detección de Monedas en Imágenes Estáticas](#detección-de-monedas-en-imágenes-estáticas)
    - [Extra: Demo en vivo](#extra-demo-en-vivo)
    - [Problemas Detectados](#problemas-detectados)
  - [Tarea 2](#tarea-2)
    - [Extracción de Características y Reconocimiento de Partículas](#extracción-de-características-y-reconocimiento-de-partículas)
    - [Carga y Preprocesamiento de Imágenes](#carga-y-preprocesamiento-de-imágenes)
    - [Segmentación de Imágenes](#segmentación-de-imágenes)
    - [Extracción de Características](#extracción-de-características)
    - [Clasificación](#clasificación)
    - [Evaluación](#evaluación)
- [Referencias Bibliográficas](#referencias-bibliográficas)

---

## Paquetes necesarios

- **Librerías**:
  - `opencv-python`
  - `numpy`
  - `matplotlib`
  - `seaborn`
  - `scikit-learn`

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
pip install seaborn
```

```bash
pip install scikit-learn
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

![image](https://github.com/user-attachments/assets/00ba4777-2961-4177-9e5a-2e54a1da1351)

#### Extra: Demo en vivo

- El sistema captura el video desde la cámara en tiempo real y, al presionar la tecla **'1'**, se congela el cuadro para procesarlo.
- Se realiza el mismo procesamiento de imagen (escala de grises, suavizado, bordes y Hough) para identificar monedas.
- El sistema dibuja círculos sobre las monedas detectadas y calcula el número total de monedas, además de sumar el valor de cada una.
- Los resultados se muestran en pantalla.

![image](https://github.com/user-attachments/assets/ac0d97c9-ab41-49d1-97c9-3ffb6db8bbd3)

#### Problemas Detectados

1. **Relación de Escala Inexacta**: El uso de escalas puede generar errores en la detección precisa de las monedas seleccionadas.
2. **Rango de Radios en la Transformada de Hough**: Los valores de radio mínimo y máximo pueden ocasionar falsos positivos.
3. **Dificultad en Condiciones de Iluminación Variables**: La detección de bordes y umbralización depende mucho de las condiciones de iluminación, lo que puede dificultar la precisión en algunas imágenes.

---

### Tarea 2
El objetivo de esta tarea es extraer características geométricas y/o visuales de tres diferentes clases de imágenes de partículas. Basándonos en estas características, desarrollaremos un clasificador simple para identificar y distinguir entre las partículas de cada clase. Evaluaremos el rendimiento de nuestro clasificador utilizando una matriz de confusión para visualizar los aciertos y fallos.

#### Extracción de Características y Reconocimiento de Partículas

- **Carga y Preprocesamiento de Imágenes**:
  - Se cargan tres tipos de imágenes: Fragmentos, Pellets y Alquitrán.
  - Cada imagen se recorta y se normaliza para uniformizar la escala y mejorar la calidad de la detección.

![image](https://github.com/user-attachments/assets/0799c9bd-b3be-4a4e-94c0-4adb76c9e813)

- **Segmentación de Imágenes**:
  - Se aplica un algoritmo de segmentación para identificar posibles partículas en cada imagen. Utilizamos técnicas como la detección de bordes y umbralización adaptativa para mejorar la precisión.

![image](https://github.com/user-attachments/assets/b9623d8f-f5ec-4867-bab6-884dd4af6455)

- **Extracción de Características**:
  - Para cada partícula identificada, calculamos características como el área, perímetro, compacidad y relación de aspecto.

```python
area = cv2.contourArea(contorno)
perimetro = cv2.arcLength(contorno, True)
if area > 0:
  compacidad = (perimetro ** 2) / area
else:
  compacidad = 0
relacion_aspecto = w / h                  #Ancho de la imagen entre su altura
```

- **Clasificación**:
  - Utilizamos las características extraídas para clasificar cada partícula en una de las tres categorías utilizando reglas simples basadas en las propiedades geométricas.

```python
if compacidad < 15 and np.isclose(relacion_aspecto, 1.0, atol=0.1):
  clasificaciones['pellets'] += 1
elif relacion_aspecto > 1.2:
  clasificaciones['fragmentos'] += 1
else:
  clasificaciones['alquitran'] += 1
```

- **Evaluación**:
  - Construimos una matriz de confusión para evaluar cuántas partículas de cada tipo fueron correctamente identificadas versus mal clasificadas.

![image](https://github.com/user-attachments/assets/30be2841-acfa-42b5-aa26-17f73eab524d)

---

## Referencias Bibliográficas

- [Guión de la práctica](https://github.com/otsedom/otsedom.github.io/tree/main/VC/P3)
- [OpenCV dibujo de contornos](https://docs.opencv.org/4.x/d4/d73/tutorial_py_contours_begin.html)
- [OpenCV flags para dibujar contornos](https://docs.opencv.org/4.x/d3/dc0/group__imgproc__shape.html#ga819779b9857cc2f8601e6526a3a5bc71)
- [OpenCV funciones para contornos](https://docs.opencv.org/3.4/dd/d49/tutorial_py_contour_features.html)
- [Documentación matriz de confusión](https://scikit-learn.org/1.5/modules/generated/sklearn.metrics.confusion_matrix.html)
- [Documentación heatmap](https://seaborn.pydata.org/generated/seaborn.heatmap.html)

---
