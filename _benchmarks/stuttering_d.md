---
name:           "Stuttering D"
numvars:        "6"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Stuttering D

```python
v = 0
w = 0
x = Uniform(-9, 7)
y = Uniform(-7, 9)
s = 0
f = 0
while true:
    v = Normal(1, 16/3)
    w = Uniform(-6, 10)
    f = Bernoulli(3/4)
    x = x + f*v
    y = y + f*w
    s = s + x*y
end
```
