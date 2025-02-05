# Matriz de Fourier 

## ¿Qué es?

Es una matriz cuadrada utilizada para representar la Transformada Discreta de Fourier (DFT) como una operación matricial. Aplicar la DFT a un vector \( x \) es equivalente a multiplicar por la matriz de Fourier:

\[
X = Fx
\]

donde:
- \( x \) es el vector columna de tamaño \( n \), lleno de coeficientes en el dominio del tiempo, es decir, la magnitud de la señal medida. 
- \( F \) es la matriz DFT, una matriz cuadrada de \( n \times n \).
- \( X \) es el vector fila de tamaño \( n \), lleno de coeficientes en el dominio de la frecuencia, de los cuales para conseguir la magnitud y ángulo se debe sacar su magnitud y fase.

La matriz DFT se define como:

\[
F_{k,n} = \frac{1}{\sqrt{N}} e^{-i 2\pi k n / N}
\]

donde:
- \( k, n \) son los índices de fila y columna.
- \( i \) es la unidad imaginaria.
- El factor \( \frac{1}{\sqrt{N}} \) se usa en la versión unitaria.

### Propiedades de la Matriz de Fourier

- **Unitarias**: \( F^H F = I \), donde \( F^H \) es la matriz conjugada transpuesta.
- **Simétrica en frecuencia**: Tiene estructura periódica.
- **Se usa en la FFT**: Aunque la DFT tiene complejidad \( O(N^2) \), la FFT la optimiza a \( O(N \log N) \).

## Cálculo Manual

Partiendo de la base que tenemos en \( x \) los valores de la magnitud de la señal en el tiempo, creamos la matriz de Fourier y multiplicamos. Se puede simplificar el cálculo redefiniendo \( F \) como:

\[
F = \frac{1}{\sqrt{N}}
\begin{bmatrix}
1      & 1      & 1      & \cdots & 1 \\
1      & \omega & \omega^2 & \cdots & \omega^{N-1} \\
1      & \omega^2 & \omega^4 & \cdots & \omega^{2(N-1)} \\
1      & \omega^3 & \omega^6 & \cdots & \omega^{3(N-1)} \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
1      & \omega^{N-1} & \omega^{2(N-1)} & \cdots & \omega^{(N-1)(N-1)}
\end{bmatrix},
\]

donde:

\[
\omega = e^{-\frac{2\pi i}{N}} \quad \text{es la raíz de la unidad.}
\]

## Calcular la DFT en código

```python
import numpy as np

x = np.array([...], dtype=complex) 
N = len(x)

n, k = np.meshgrid(np.arange(N), np.arange(N))
F = np.exp(-2j * np.pi * k * n / N)

X = F @ x  
