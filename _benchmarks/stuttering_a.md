---
name:           "Stuttering A"
numvars:        "6"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Stuttering A

```python
v = 0
w = 0
f = 0
x = -1
y = 1
s = 0
while true:
   v = Uniform(1-d, 1+d)
   w = Uniform(2-2*d, 2+2*d)
   f = Bernoulli(3/4)
   x = x + f*v
   y = y + f*w
   s = x + y
end
```
