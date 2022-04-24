---
name:           "sum_rnd_series"
numvars:        "2"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Sum Random Series

```python
y = 0
x = 0
while true:
    y = y + 1
    x = x + y {1/2} x
end
```
