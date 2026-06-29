# Algoritmos computacionales

## Contenido

| Laboratorio | Tema | Lenguajes y entorno |
| --- | --- | --- |
| `Lab_01` | Interpolación de Newton y Hermite | C++20, Make y CSV |
| `Lab_02` | Interpolación mediante spline cúbico | C++20, Make y CSV |
| `Lab_03` | Interpolación tridimensional | C++20, Make y CSV |
| `Lab_04` | Mínimos cuadrados y aproximación de EDO | C++17, Qt Widgets y Python |
| `Lab_05` | Sistemas no lineales, integral de Laplace y problema de contorno | Python, NumPy y SymPy |

## Laboratorios

### `Lab_01` — Interpolación de Newton y Hermite

Interpolación de funciones tabuladas mediante diferencias divididas. Selección de los nodos próximos al valor de `x`.

- Construcción del polinomio de Newton para un grado configurable.
- Construcción del polinomio de Hermite a partir de valores de la función y de sus derivadas primera y segunda.
- Comparación de Newton y Hermite para configuraciones equivalentes de grado y cantidad de nodos.
- Resolución de ecuaciones mediante interpolación inversa, con intercambio de las variables tabuladas y transformación de las derivadas.
- Resolución del sistema `f(x) = g(x)` mediante interpolación de ambas funciones, cálculo de su diferencia y búsqueda inversa de la raíz.
- Exportación de tablas de diferencias divididas, vectores de nodos y bloques de Hermite en formato CSV.

Formato de entrada:

```csv
x,y,y',y''
```

### `Lab_02` — Spline cúbico

Interpolación por tramos mediante splines cúbicos y resolución del sistema tridiagonal de coeficientes por el método de barrido.

| Condición | Extremo izquierdo | Extremo derecho |
| --- | --- | --- |
| Natural | `S''(x0) = 0` | `S''(xN) = 0` |
| Mixta | `S''(x0) = P3''(x0)` | `S''(xN) = 0` |
| Derivadas estimadas | `S''(x0) = P3''(x0)` | `S''(xN) = P3''(xN)` |

- Cálculo de los coeficientes del spline para cada intervalo.
- Estimación de las derivadas de frontera mediante un polinomio de Newton de tercer grado.
- Selección del tramo que contiene el argumento de interpolación.
- Comparación entre el spline cúbico y el polinomio de Newton de tercer grado.

Formato de entrada:

```csv
x,y
```

### `Lab_03` — Interpolación tridimensional

Interpolación secuencial de una función tabulada sobre una malla regular en los ejes `x`, `y` y `z`.

| Método | Interpolación por ejes |
| --- | --- |
| Newton | Newton en `x`, `y` y `z`, con grados `nx`, `ny` y `nz` |
| Spline | Spline cúbico en `x`, `y` y `z` |
| Mixto | Newton en `x` y spline cúbico en `y` y `z` |

- Lectura de capas bidimensionales asociadas a valores discretos de `z`.
- Selección de una submalla alrededor del punto `(x, y, z)` para la interpolación de Newton.
- Reducción sucesiva del problema tridimensional a interpolaciones bidimensionales y unidimensionales.
- Salida de los resultados de Newton, spline y método mixto.

Datos de ejemplo: [`Lab_03/f.csv`](Lab_03/f.csv), malla `5 × 5 × 5` de la función `f(x, y, z) = x² + y² + z²`.

### `Lab_04` — Mínimos cuadrados y aproximación de EDO

Aplicación Qt para aproximación polinómica ponderada de funciones de una y dos variables y aproximación de un problema de contorno para una ecuación diferencial ordinaria.

- Generación y edición de conjuntos de puntos con pesos individuales o uniformes mediante una interfaz Qt Widgets.
- Aproximación de `y = f(x)` por polinomios de grados seleccionables entre 1 y 10 mediante mínimos cuadrados ponderados.
- Aproximación de `z = f(x, y)` mediante una base de monomios `xⁱyʲ` de grado total configurable.
- Construcción de las ecuaciones normales y resolución del sistema lineal mediante eliminación de Gauss y sustitución regresiva.
- Aproximación del problema de contorno mediante mínimos cuadrados discretos y funciones base de grados 2, 3 y 4.
- Comparación gráfica de las aproximaciones polinómicas y de la solución de la EDO mediante scripts Python ejecutados desde Qt.
- Intercambio de puntos y coeficientes mediante archivos CSV.

Formatos de datos:

```csv
x,y,weight
x,y,z,weight
```

### `Lab_05` — Sistemas no lineales, integración y diferencias finitas

Resolución de tres problemas mediante cálculo simbólico, álgebra lineal, integración numérica y diferencias finitas.

1. Resolución de un sistema de tres ecuaciones no lineales mediante el método de Newton, cálculo simbólico del Jacobiano con SymPy y resolución de los incrementos con NumPy.
2. Cálculo de la integral de Laplace mediante la fórmula de Simpson e inversión de la función integral mediante el método de bisección.
3. Resolución del problema de contorno `y'' = x² + y³`, `y(0) = 1`, `y(1) = 3` mediante una malla de 100 intervalos, diferencias finitas y el método de Newton.

Representación de la solución del problema de contorno con Matplotlib.

## Tecnologías

| Área | Tecnologías |
| --- | --- |
| Desarrollo C++ | C++17, C++20, STL, g++ y Make |
| Interfaz gráfica | Qt Widgets y qmake |
| Cálculo numérico | NumPy, SymPy, SciPy y Boost.Math |
| Visualización | Matplotlib, pandas y Plotly |
| Intercambio de datos | CSV |

## Compilación y ejecución

### `Lab_01`, `Lab_02` y `Lab_03`

Compilación y ejecución desde el directorio del laboratorio:

```bash
cd Lab_01
make release
./app.exe
```

Para `Lab_02` y `Lab_03`, sustituir `Lab_01` por el directorio correspondiente.

Limpieza de artefactos:

```bash
make clean
```

### `Lab_04`

Dependencias de compilación y ejecución:

- compilador con soporte para C++17
- Qt Widgets y qmake
- Python 3.10 y cabeceras de desarrollo
- Boost.Math
- NumPy, pandas, Matplotlib, SciPy y Plotly

Compilación:

```bash
cd Lab_04
qmake Lab_04_ui.pro
make
./Lab_04_ui
```

| Archivo | Configuración |
| --- | --- |
| [`Lab_04/Lab_04_ui.pro`](Lab_04/Lab_04_ui.pro) | Rutas de Python y Boost |
| [`Lab_04/mainwindow.cpp`](Lab_04/mainwindow.cpp) | Rutas de archivos CSV y scripts de visualización |

### `Lab_05`

Dependencias:

```bash
python3 -m pip install numpy sympy scipy matplotlib
```

Ejecución:

```bash
cd Lab_05
python3 main.py
```
