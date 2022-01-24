---
name:           "Random Walk 2D"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Random Walk 2D

```python
h = 0
x = 0
y = 0
while true:
    h = 1 {1/2} 0
    x = x - h {1/2} x + h
    y = y+(1-h) {1/2} y-(1-h)
end
```
