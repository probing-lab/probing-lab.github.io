---
name:           "Binomial(p)"
numvars:        "2"
ifthenelse:     "no"
infinitesp:     "yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

# Code 

```python
x = 0
while true:
    x = x + 1 {p} x
end
```
