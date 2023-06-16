---
name:           "Nagata"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "Yes"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "Yes"
nonpolynomial:  "No"
---

Nagata

```python
while true:
 x,y,z = x - 2*(x*z + y**2)*y - ((x*z+y**2)**2)*z, y + (x*z + y**2)*z, z
end
```
