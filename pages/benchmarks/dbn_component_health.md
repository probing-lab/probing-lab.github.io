---
name:           "DBN Component Health"
numvars:        "3"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "No"
contstatesp:    "No"
loopguard:      "(true)"
---

DBN Component Health

```python
health = 0
obs = 0
while true:
    usage = Categorical(1/4, 1/4, 1/4, 1/4)
    if health == 1:
        if usage == 0:
            health = Bernoulli(0.01)
        elif usage == 1:
            health = Bernoulli(0.05)
        elif usage == 2:
            health = Bernoulli(0.1)
        else:
            health = Bernoulli(0.2)
        end
    end
    if health == 1:
        obs = Categorical(0, 0.024, 0.063, 0.418, 0.495)
    else:
        obs = Categorical(0.521, 0.317, 0.112, 0.04, 0.01)
    end
end

```
