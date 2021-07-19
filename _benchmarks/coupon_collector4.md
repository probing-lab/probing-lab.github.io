---
name:           "Coupon Collector 4"
numvars:        "6"
ifthenelse:     "No"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
---

Coupon Collector 4

```python
f = 0
g = 0
a = 0
b = 0
c = 0
d = 0
while true:
   f = Bernoulli(1/2)
   g = Bernoulli(1/2)
   a = a + (1-a)*f*g
   b = b + (1-b)*f*(1-g)
   c = c + (1-c)*(1-f)*g
   d = d + (1-d)*(1-f)*(1-g)
end
```