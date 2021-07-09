---
name:           "Duelling Cowboys"
numvars:        "4"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

Duelling Cowboys

```python
ahit = 0
bhit = 0
while true:
    ahit = 1 {a} 0
    bhit = 1 - ahit {b} 0
    over = ahit + bhit
end
```
