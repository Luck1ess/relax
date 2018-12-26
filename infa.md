

```python
import pandas as pd
import numpy as np

ca1 = np.array([4.84, 2.95, 3.76, 3.05, 4.18, 4.86, 3.95, 2.44, 4.77])
zn1 = np.array([0.9, 1.5, 2.4, 2.8, 0.7, 2.2, 4.2, 7.6, 0.8])


ca2 = np.array([4.54, 3.4, 3.33, 4.44, 4.29, 3.1, 3.44, 3.71, 3.86, 2.81, 4.41])
zn2 = np.array([3.8, 2.5, 8.5, 1.4, 2.7, 1.2, 1.5, 2.0, 2.2, 1.7, 2.2])



ca3 = np.array([5.26, 3.19, 3.56, 3.81, 3.18, 2.2, 2.96, 4.66, 4.32, 5.38, 3.66, 3.09, 2.99, 3.28, 3.94])
zn3 = np.array([1.6, 4.1, 2.0, 1.9, 1.5, 5.8, 1.9, 0.5, 3.7, 2.0, 1.6, 1.8, 4.7, 6.4, 2.9)




```


      File "<ipython-input-225-31dbb7b00758>", line 14
        zn3 = np.array([1.6, 4.1, 2.0, 1.9, 1.5, 5.8, 1.9, 0.5, 3.7, 2.0, 1.6, 1.8, 4.7, 6.4, 2.9)
                                                                                                 ^
    SyntaxError: invalid syntax




```python
ca = np.hstack((ca1,ca2,ca3))
zn = np.hstack((zn1,zn2,zn3))
```


```python
def s(x):
    return np.sum(np.square(x-x.mean()))/(len(x)-1)
```


```python
ca1.mean()
```


```python
ca2.mean()
```


```python
ca3.mean()
```


```python
zn1.mean()
```




    16.353846153846153




```python
zn2.mean()
```




    14.32




```python
zn3.mean()
```




    14.390909090909092




```python
np.sqrt(s(ca1))
```




    0.25288844201063065




```python
np.sqrt(s(ca2))
```




    0.13941032277144363




```python
np.sqrt(s(ca3))
```




    0.24179881444429516




```python
np.sqrt(s(zn1))
```




    2.629516870902139




```python
np.sqrt(s(zn2))
```




    2.102787265919757




```python
np.sqrt(s(zn3))
```




    2.794084660655273




```python
 s(ca1)/s(ca2)
```




    3.2905469842550255




```python
s(ca1)/s(ca3)
```




    1.0938294886413469




```python
s(ca3)/s(ca2)
```




    3.0082814720439073




```python
s(zn1)/s(zn2)
```




    1.5637281216242187




```python
s(zn3)/s(zn2)
```




    1.765584247750182




```python
s(zn3)/s(zn1)
```




    1.1290864590427




```python
def S(x,y):
    return np.sqrt((s(x)*(len(x)-1)+s(y)*(len(y)-1))/(len(x)+len(y)-2))
```


```python
S(ca1,ca2)
```




    0.19995423539516605




```python
S(ca3,ca2)
```




    0.186301921077324




```python
S(ca1,ca3)
```




    0.24819642463473401




```python
S(zn1,zn2)
```




    2.360543513785199




```python
S(zn3,zn2)
```




    2.4149973335828183




```python
S(zn1,zn3)
```




    2.70556160025804




```python
def t(x,y):
    if len(y)>len(x):
        x, y = y, x
    return abs(x.mean()-y.mean())/(10*S(x,y)*np.sqrt(1/len(y)-1/len(x)))
```


```python
t(ca1,ca2)
```




    0.2615998016070839




```python
t(ca3,ca2)
```




    0.2038381055551751




```python
t(ca3,ca1)
```




    0.32439137590978884




```python
t(zn1,zn2)
```




    0.8507626117455479




```python
t(zn3,zn2)
```




    0.018858069779267562




```python
t(zn1,zn3)
```




    0.6134822047234295




```python
def sst(x):
    return np.sum(np.square(x-x.mean()))

def ssw(x):
    s = 0
    d = 0 
    for i in x:
        s += np.sum(np.square(i))
        d += np.square(np.sum(i))/len(i)
    return s - d

def ssa(x,y):
    return sst(x)-ssw(y)

def st(x):
    return sst(x)/(len(ca)-1)

def sa(x,y):
    return ssa(x,y)/2

def sw(x):
    return ssw(x)/(2*(len(x)-1))
```


```python
sst(ca)
```




    1.650276315789474




```python
ssw((ca1,ca2,ca3))
```




    1.56572410256409




```python
ssa(ca,(ca1,ca2,ca3))
```




    0.08455221322538398




```python
sa(ca,(ca1,ca2,ca3))
```




    0.04227610661269199




```python
sw((ca1,ca2,ca3))
```




    0.3914310256410225




```python
sa(ca,(ca1,ca2,ca3))/sw((ca1,ca2,ca3))
```




    0.10800397475764474




```python
sst(zn)
```




    257.7774358974359




```python
ssw((zn1,zn2,zn3))
```




    222.94539860139957




```python
        ssa(zn,(zn1,zn2,zn3))
```




    34.83203729603633




```python
sa(zn,(zn1,zn2,zn3))
```




    17.416018648018166




```python
sw((zn1,zn2,zn3))
```




    55.736349650349894




```python
np.square(sa(zn,(zn1,zn2,zn3))/sw((zn1,zn2,zn3)))
```




    0.09763841441002317




```python

```
