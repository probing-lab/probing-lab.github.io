---
name:           "Nonlinear Markov Model 2"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
---

Nonlinear Markov Model 2

```python
x, y = 0, 1
while true:
    s = Bernoulli(1/2)
    if s == 0:
        x, y = (4/10)*(x + x*y), (4/10)*((1/3)*x + (2/3)*y + x*y)
    else:
        x, y = (4/10)*(x + y + (2/3)*x*y), (4/10)*(2*y + (2/3)*x*y)
    end
end
```
