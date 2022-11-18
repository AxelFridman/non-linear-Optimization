# tp1_invop



## para graficar funciones 
```python 
def plot_fun(f, limites, points=None):
    """
    f : función a graficar
    limites : toma una tupla (x1,x2,y1,y2) de los límites del gráfico: grafica en el dominio [x1,x2] x [y1,y2]
    points : lista de puntos a graficar sobre la superficie; se ingresa como una lista de tuplas (x,y,z) 
    """
    init_notebook_mode(connected=True)

    x = np.linspace(limites[0], limites[1], 1000)
    y = np.linspace(limites[2], limites[3], 1000)
    X, Y = np.meshgrid(x, y)
    Z = f((X, Y))
    data = [go.Surface(x=x, y=y, z=Z)]
    if points is not None:
        for p in points:
            data.append(go.Scatter3d(x=[p[0]], y=[p[1]], z=[p[2]], mode='markers'))
    fig = go.Figure(data=data)
    iplot(fig)

```
```python
%matplotlib notebook

def curvas_nivel(f, limites, levels=10):
    """ 
    Función que grafica curvas de nivel.
    f : es la función a graficar (tiene que ir de R2 en R)
    limites: es una lista o tupla de números: [a,b,c,d]. Va a graficar la función en el cuadrado [a,b] x [c,d]
    levels : cantidad de curvas de nivel a graficar
    """
    plt.figure()
    x = np.linspace(limites[0], limites[1], 1000)
    y = np.linspace(limites[2], limites[3], 1000)
    X, Y = np.meshgrid(x, y)
    Z = f((X, Y))
    plt.contour(X,Y,Z, cmap='plasma', levels=levels)
    plt.tight_layout()
    plt.gca().set_aspect('equal', adjustable='box')
    plt.show()
```
## some functions para quadraticas

gradiente
```python
def metodo_gradiente(A, b, x_0, max_iter, l=None):
  k = 0
  x = x_0
  d = -A @ x_0 - b
  while((k <= max_iter) and (np.linalg.norm(d) > 10e-8)):
    if l == None:
     l = np.random.rand()
    t = l*((d.T @ d)/(d.T @ A @ d))
    x += t*d
    d = -A@x - b
    k += 1  
  return x, k 
```


gradiente conjugado
```python
import numpy as np
def gradiente_conjugado(A, b, x0, kmax=10000, epsilon=1e-8):
    d = -A@x0+b
    x = x0
    k = 0
    recorrido = []
    while (np.linalg.norm(A@x+b)>epsilon and k<kmax):
        t  = - ((A@x+b).T @ d)/(d@A@d)
        recorrido.append(x)
        x  = x + t*d
        beta = (d@A@(A@x+b))/(d@A@d)
        d    = -(A@x+b)+beta*d
        k +=1
    return x, k, recorrido
```
