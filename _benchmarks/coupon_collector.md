---
name:           "Coupon Collector"
numvars:        "3"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
---

Coupon Collector

```python
f = 0
c = 0
d = 0
while true:
   f = 1 {1/2} 0
   c = 1 - f + c*f
   d = d + f - d*f
end
```
