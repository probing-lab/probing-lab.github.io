---
name:           "Fibonacci Trace"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "Yes"
nonpolynomial:  "No"
---

2D Robotic Arm

```python
while true:
    x, y, z = y, z, 2*y*z - x
end
```
