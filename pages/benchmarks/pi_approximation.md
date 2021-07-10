---
name:           "PI Approximation"
numvars:        "4"
ifthenelse:     "Yes"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
---

PI Approximation

```python
count = 0
while true:
    x = Uniform(0,1)
    y = Uniform(0,1)

    if x**2 + y**2 < 1:
        count = count + 1
    end
end
```
