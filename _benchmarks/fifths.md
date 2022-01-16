---
name:           "Fifths"
numvars:        "2"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "Yes"
---

Fifths Model

```python
x, y = 1, 1
while true:
    x, y = (x + y)**5, 2*(x + y)**5 + 1
end
```
