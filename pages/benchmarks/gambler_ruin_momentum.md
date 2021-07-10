---
name:           "Gambler Ruin Momentum"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

Gambler Ruin Momentum

```python
xprev = a
x = a
while true:
    z = -1 {p} 1
    tmp = x
    x = 2*x - xprev + z
    xprev = tmp
end
```
