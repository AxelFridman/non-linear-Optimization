# tp1_invop



## Notas

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
