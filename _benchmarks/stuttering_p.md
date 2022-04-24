---
name:           "Stuttering P"
numvars:        "4"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Stuttering P

```python
f = 0
x = -1
y = 1
s = 0
while true:
    u1 = Uniform(0, 2)
    u2 = Uniform(0, 4)
    f = Bernoulli(p)
    x = x + f*u1
    y = y + f*u2
    s = x + y
end
```
