---
name:           "Binomial(p)"
numvars:        "2"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

Binomial(p)

```python
x = 0
while true:
    x = x + 1 {p} x
end
```
