---
name:           "Eighths"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
nonpolynomial:  "No"
---

Eighths Model

```python
x, y = 1, 1
while true:
    z = Bernoulli(1/2)
    x, y = x**8 + z + z**2 + z**3 + z**4 + z**5 + 1, z + z**2 + z**7 - x**8
end
```
