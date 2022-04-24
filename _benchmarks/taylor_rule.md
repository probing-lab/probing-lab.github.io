---
name:           "Taylor Rule"
numvars:        "9"
ifthenelse:     "No"
infinitesp:     "Yes"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "Yes"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "Yes"
---

Taylor Rule

```python
ap  = 0.5
ay  = 0.5
y   = 1
y1  = 1
p   = 0.01
p1  = 0.01
i   = 0.02
r   = 0.015
while true:
    dp = Normal (0, 0.01)
    dy = Exponential (100)
    p  = p1
    p1 = p + dp
    y1 = 0.01 + 1.02 * y
    y  = y1 – dy
    ly = log(1 + y)
    ly1= log(1 + y1)
    i  = r + p + ap * (p-p1)+ ay * (ly - ly1)
end
```
