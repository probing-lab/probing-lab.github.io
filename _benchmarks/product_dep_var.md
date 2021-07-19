---
name:           "Product Dep Var"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
---

Product of Dependent Random Variables

```python
f = 0
x = 0
y = 0
p = 0
while true:
    f = Bernoulli(1/2)
    x = x + f
    y = y + 1 - f
    p = x*y
end
```
