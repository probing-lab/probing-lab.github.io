---
name:           "Bees Model"
numvars:        "5"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
---

<b>Mathematical model describing the decision-making process of a swarm of honeybees for selecting one nest-site among many</b>

N.F. Britton, N.R. Franks, S.C. Pratt, T.D. Seeley, Deciding on a new home: how do honeybees agree ?, Proceedings of the Royal Society of London. Series B: Biological Sciences 269 (1498), 1383-1388 (2002)
    [<a href="https://royalsocietypublishing.org/doi/10.1098/rspb.2002.2001">Link</a>]
<p>
\[ \begin{array}{lcl}
X(0) & = & \mathcal{N} (475,5) \\
Y_1(0) & = & \mathcal{U} (350,500) \\
Y_2(0) & = & \mathcal{U} (100,150) \\
Z_1(0) & = & \mathcal{N} (35,1.5) \\
Z_2(0) & = & \mathcal{N} (35,1.5) \\
 &  &  \\
\dot{X} & = & -\beta_1 XY_1 - \beta_2 XY_2 \\
\dot{Y_1} & = & \beta_1 XY_1 -\gamma Y_1 + \delta \beta_1 Y_1 Z_1 + \alpha \beta_1 Y_1 Z_2\\
\dot{Y_2} & = & \beta_2 XY_2 -\gamma Y_2 + \delta \beta_2 Y_2 Z_2 + \alpha \beta_2 Y_2 Z_1\\
\dot{Z_1} & = & \gamma Y_1 - \delta \beta_1 Y_1 Z_1 - \alpha \beta_2 Y_2 Z_1\\
\dot{Z_2} & = & \gamma Y_2 - \delta \beta_2 Y_2 Z_2 - \alpha \beta_1 Y_1 Z_2\\
 &  &  \\
\beta_1 & = & 0.001\\
\beta_2 & = & 0.001\\
\gamma & = & 0.3\\
\delta & = & 0.5\\
\alpha & = & 0.7\\
\end{array}\] 
</p>

<b>Description</b>


Probabilistic Program Computing the Bees Model (Source Code)
```python
x = Normal(475, 5)
y1 = Uniform(350, 400)
y2 = Uniform(100, 150)
z1 = Normal(35, 1.5)
z2 = Normal(35, 1.5)

#c1 = 0.1
#c2 = 0.001
#c3 = 0.3
#c4 = 0.0005
#c5 = 0.0007

while true:
    x, y1, y2, z1, z2 = x + c1*((-c2)*x*y1 - c2*x*y2), y1 + c1*(c2*x*y1 - c3*y1 + c4*y1*z1 + c5*y1*z2), y2 + c1*(c2*x*y2 - c3*y2 + c4*y2*z2 + c5*y2*z1), z1 + c1*(c3*y1 - c4*y1*z1 - c5*y2*z1), z2 + c1*(c3*y2 - c4*y2*z2 - c5*y1*z2)
end
```
