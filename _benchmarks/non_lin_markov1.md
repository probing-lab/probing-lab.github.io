---
name:           "Nonlinear Markov Model 1"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
---

Nonlinear Markov Model 1

```python
while true:
    s = Bernoulli(1/2)
    if s == 0:
        x, y = x + x*y, (1/3)*x + (2/3)*y + (x*y)
    else:
        x, y = x + y + (2/3)*x*y, 2*y + (2/3)*(x*y)
    end
end
```
