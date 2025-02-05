# Matriz de Fourier 

## ¿Qué es?

Es una matriz cuadrada utilizada para representar la Transformada Discreta de Fourier (DFT) como una operación matricial. Aplicar la DFT a un vector $ x $ es equivalente a multiplicar por la matriz de Fourier:

X = Fx

donde:
- x es el vector columna de tamaño n, lleno de coeficientes en el dominio del tiempo, es decir, la magnitud de la señal medida. 
- F es la matriz DFT, una matriz cuadrada de n por n.
- X es el vector fila de tamaño n, lleno de coeficientes en el dominio de la frecuencia, de los cuales para conseguir la magnitud y ángulo se debe sacar su magnitud y fase.

La matriz DFT se define como:

F_k,n = 1/sqrt(N) e^(-i 2\pi k n / N)

donde:
- k, n son los índices de fila y columna.
- i es la unidad imaginaria.
- El factor 1/sqrt(N) se usa para conservar la unidad.

### Propiedades de la Matriz de Fourier

- **Unitarias**: F^H F = I , donde F^H es la matriz conjugada transpuesta.
- **Simétrica en frecuencia**: Tiene estructura periódica.
- **Se usa en la FFT**: Aunque la DFT tiene complejidad O(N^2), la FFT la optimiza a O(N log N).

## Cálculo Manual

Partiendo de la base que tenemos en \( x \) los valores de la magnitud de la señal en el tiempo, creamos la matriz de Fourier y multiplicamos. Se puede simplificar el cálculo redefiniendo \( F \) como se ve en la [imagen de Wikipedia](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTCqWoqoIa5dAKzpO0c3R8sEkWqjbJKk6oFyA&s), donde omega = e^(-2pi *i/N)

## Calcular en Código

```python
import numpy as np

x = np.array([...], dtype=complex) 
N = len(x)

n, k = np.meshgrid(np.arange(N), np.arange(N))
F = np.exp(-2j * np.pi * k * n / N)

X = F @ x  
```
