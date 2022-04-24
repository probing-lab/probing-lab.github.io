---
name:           "2D Robotic Arm"
numvars:        "9"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "Yes"
---

2D Robotic Arm

```python
x = Normal (0, 0.0025)
y = Normal (0, 0.01)
c = 3.14/180

while true:
    d0  = Uniform (0.98, 1.02)
    t0  = 10 * c * (1 + Uniform (0, 0.0001))
    d1  = Uniform (0.98, 1.02)
    t1  = 60 * c * (1 + Uniform (0, 0.0001))
    d2  = Uniform (0.98, 1.02)
    t2  = 110 * c * (1 + Uniform (0, 0.0001))
    d3  = Uniform (0.98, 1.02)
    t3  = 160 * c * (1 + Uniform (0, 0.0001))
    d4  = Uniform (0.98, 1.02)
    t4  = 140 * c * (1 + Uniform (0, 0.0001))
    d5  = Uniform (0.98, 1.02)
    t5  = 100 * c * (1 + Uniform (0, 0.0001))
    d6  = Uniform (0.98, 1.02)
    t6  = 60 * c * (1 + Uniform (0, 0.0001))
    d7  = Uniform (0.98, 1.02)
    t7  = 20 * c * (1 + Uniform (0, 0.0001))
    d8  = Uniform (0.98, 1.02)
    t8  = 100 * c * (1 + Uniform (0, 0.0001))
    d9  = Uniform (0.98, 1.02)
    t9  = 0
    
    x = x + d0 * cos (t0) + d1 * cos (t1) + d2 * cos (t2) + d3 * cos (t3) + d4 * cos (t4) + d5 * cos (t5) + d6 * cos (t6) + d7 * cos (t7) + d8 * cos (t8) + d9 * cos (t9)
    y = y + d0 * sin (t0) + d1 * sin (t1) + d2 * sin (t2) + d3 * sin (t3) + d4 * sin (t4) + d5 * sin (t5) + d6 * sin (t6) + d7 * sin (t7) + d8 * sin (t8) + d9 * sin (t9)   
end
```
