# Stellar Luminosity – Regresión lineal y polinomial

## Introducción

Este trabajo lo hice para entender, con calma y de forma práctica, cómo ajustar modelos sencillos a datos astrofísicos. La idea es modelar la luminosidad de estrellas usando su masa y temperatura, sin usar librerías de alto nivel: solo NumPy para calcular y Matplotlib para graficar.

Me enfoqué en dos cosas: 
- que el código sea claro (paso a paso), y 
- que las salidas (gráficas y pérdidas) cuenten una historia coherente sobre cómo mejora el ajuste con entrenamiento y características.

## Qué hay en los notebooks

### 1. **01_part1_linreg_1feature.ipynb** (una sola característica: Masa M)
- Predicción `L_hat = w·M + b` y pérdida MSE.
- Gradientes (derivados a mano), versión no vectorizada y vectorizada.
- Entrenamiento por descenso de gradiente, diferentes tasas de aprendizaje.
- Superficie/contorno de costo y ajuste final sobre los datos.

### 2. **02_part2_polyreg.ipynb** (polinómica + interacción: M y T)
- Ingeniería de características: `X = [M, T_k, M², M·T_k]` donde `T_k = T/1000` para estabilidad.
- Gradientes y entrenamiento vectorizado.
- Comparación de modelos (M1/M2/M3), costo vs interacción `w_MT` y una demo de inferencia.



## Requisitos

- Python 3.x
- NumPy
- Matplotlib

## Cómo lo corrí en mi máquina (Windows)

1. Abrí los notebooks en VS Code/Jupyter.
2. Ejecuté las celdas de arriba hacia abajo (Run All también funciona).
3. Las gráficas salen inline; si algo no converge, bajé `alpha` y aumenté iteraciones.

## AWS SageMaker: Evidencia de Ejecución

**Cómo subí y ejecuté los notebooks en SageMaker (resumen corto):**
- Abrí SageMaker Studio y subí los `.ipynb` (Upload files).
- Abrí cada notebook, seleccioné un kernel de Python (NumPy/Matplotlib) y corrí todas las celdas (Run All).

## Evidencias por sección (galería)

- Notebooks visibles en SageMaker:
![Notebooks abiertos en SageMaker](images/sagemaker-notebooks.png)

### Parte 1 – Regresión lineal (una característica)
- Punto 1:
![Punto 1](images/part1.1.png)
- Punto 2:
![Punto 2](images/parte1.2.png)
- Punto 3:
![Punto 3](images/part1.3.png)
- Punto 4:
![Punto 4](images/parte1.4.png)
- Punto 5:
![Punto 5](images/parte1.5.png)
- Punto 6:
![Punto 6](images/part1.6.png)
- Puntos 7 y 8:
![Puntos 7 y 8](images/parte1.7y1.8.png)
- Punto 9:
![Punto 9](images/parte1.9.png)

### Parte 2 – Polinómica + interacción (masa y temperatura)
- Punto 1:
![Punto 1](images/parte2.1.png)
- Puntos 2 y 3:
![Puntos 2 y 3](images/parte2.2y2.3.png)
- Punto 4 (superficie/curvas de costo):
![Punto 4 – gráfico 1](images/parte2.4.png)
![Punto 4 – gráfico 2](images/parte2.4.2.png)
- Punto 5:
![Punto 5](images/parte2.5.png)
- Punto 6:
![Punto 6](images/parte2.6.png)
- Punto 7:
![Punto 7](images/parte2.7.png)

**Diferencias local vs SageMaker:**
- En local las celdas corren un poco más rápido; en Studio la convergencia tarda unos segundos extra.
- Las superficies 3D pueden tardar más en renderizar en Studio; el resto de gráficas se ven igual.
- Usando un kernel con NumPy y Matplotlib no tuve errores.
- Las pérdidas finales y los parámetros coinciden en ambos entornos.
## Conclusión

- **Modelos**: Con solo masa obtuve un ajuste razonable; al sumar términos polinomiales e interacción con temperatura el modelo captura mejor la tendencia sin complicar el código.
- **Entrenamiento**: Escalar la temperatura en miles y usar un `alpha` pequeño con más iteraciones dio convergencias limpias, sin NaN ni oscilaciones.
- **Evaluación**: La pérdida cae de forma estable y el Predicho vs Real confirma que la interacción `M*T_k` aporta valor; M1 se queda corto, M2/M3 funcionan mejor.
- **Limitaciones**: Son datos sintéticos y el modelo es simple; añadir demasiados términos sin regularización puede llevar a sobreajuste.
- **Próximos pasos**: Normalizar variables, validar con particiones y probar una regularización ligera (L2) hecha a mano en NumPy.

## Información del Proyecto

- **Autor**: Esteban Aguilera Contreras
- **Universidad**: Escuela Colombiana de Ingeniería Julio Garavito
- **Asignatura**: Arquitecturas Empresariales (AREP)


