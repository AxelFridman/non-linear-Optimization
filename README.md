# tp1_invop



## Notas

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
