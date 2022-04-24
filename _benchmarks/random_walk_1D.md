---
name:           "Random Walk 1D"
numvars:        "1"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Random Walk 1D

```python
x = 2
while true:
    x = x + 1 {1/2} x - 1
end
```
