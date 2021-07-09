---
name:           "Martingale-Bet"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

Martingale-Bet

```python
x, y = 1, 0
while y <= 0:
    x = 2*x
    r = Bernoulli(1/2)
    if r == 1:
        y = y - x
    else:
        y = y + x
    end
end

```
