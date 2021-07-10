---
name:           "DBN Umbrella"
numvars:        "2"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "No"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
---

DBN Umbrella

```python
rain = Bernoulli(r0)
umbrella = Bernoulli(u0)
while true:
    if rain == 1:
        rain = Bernoulli(r1)
    else:
        rain = Bernoulli(r2)
    end

    if rain == 1:
        umbrella = Bernoulli(u1)
    else:
        umbrella = Bernoulli(u2)
    end
end

```
