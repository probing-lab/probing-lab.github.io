---
name:           "Turning Vehicle"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "Yes"
---

Turning Vehicle

```python
v0  = 10
tau = 0.1
K   = -0.5
phi = Normal (   0,  0.01)
v   = Uniform( 6.5,  8.5)
x   = Uniform(-0.1,  0.1)
y   = Uniform(-0.5, -0.3)
while true:
    w1 = Uniform(-0.1, 0.1)
    w2 = Normal(0, 0.01)
    
    x   = x + tau * v * cos (phi)
    y   = y + tau * v * sin (phi)
    v   = v + tau * (K * (v - v0) + w2)
    phi = phi + w2
end
```
