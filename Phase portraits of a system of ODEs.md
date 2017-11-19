**The following content is directly taken from [here](http://kitchingroup.cheme.cmu.edu/blog/2013/02/21/Phase-portraits-of-a-system-of-ODEs/).**

An undamped pendulum with no driving force is described b

![](https://latex.codecogs.com/svg.latex?%24y%5E%5Cprime%20%5E%5Cprime%20&plus;%20%5Csin%28y%29%3D0%24)



We reduce this to standard form of a system of first order ODEs by letting ![](https://latex.codecogs.com/svg.latex?y%5E%5Cprime%20%3D%20y_2) and y2=y′1y2=y1′. This leads to:

y′1=y2y1′=y2

y′2=−sin(y1)y2′=−sin(y1)

The phase portrait is a plot of a vector field which qualitatively shows how the solutions to these equations will go from a given starting point. here is our definition of the differential equations:

To generate the phase portrait, we need to compute the derivatives y′1y1′ and y′2y2′ at t=0t=0 on a grid over the range of values for y1y1 and y2y2 we are interested in. We will plot the derivatives as a vector at each (y1, y2) which will show us the initial direction from each point. We will examine the solutions over the range -2 < y1 < 8, and -2 < y2 < 2 for y2, and create a grid of 20 x 20 points.
```python
import numpy as np
import matplotlib.pyplot as plt

def f(Y, t):
    y1, y2 = Y
    return [y2, -np.sin(y1)]

y1 = np.linspace(-2.0, 8.0, 20)
y2 = np.linspace(-2.0, 2.0, 20)

Y1, Y2 = np.meshgrid(y1, y2)

t = 0

u, v = np.zeros(Y1.shape), np.zeros(Y2.shape)

NI, NJ = Y1.shape

for i in range(NI):
    for j in range(NJ):
        x = Y1[i, j]
        y = Y2[i, j]
        yprime = f([x, y], t)
        u[i,j] = yprime[0]
        v[i,j] = yprime[1]
     

Q = plt.quiver(Y1, Y2, u, v, color='r')

plt.xlabel('$y_1$')
plt.ylabel('$y_2$')
plt.xlim([-2, 8])
plt.ylim([-4, 4])
plt.savefig('images/phase-portrait.png')
```
