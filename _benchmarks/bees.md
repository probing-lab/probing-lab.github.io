---
name:           "Bees"
numvars:        "5"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
---

Bees Model
<p>
\[ \begin{array}{lcr}
\mbox{First number} & x & 8 \\
\mbox{Second number} & y & 15 \\
\mbox{Sum} & x + y & 23 \\
\mbox{Difference} & x - y & -7 \\
\mbox{Product} & xy & 120 \end{array}\] 
</p>

Description


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
