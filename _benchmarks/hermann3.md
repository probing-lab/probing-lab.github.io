---
name:           "Hermann-3"
numvars:        "7"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
nonpolynomial:  "No"
---

Hermann-3

```python
x1 = 1
token1 = 1
x2 = 1
token2 = 1
x3 = 1
token3 = 1
numtokens = token1 + token2 + token3
while true:
    x1o, x2o, x3o = x1, x2, x3

    if x1o == x3o:
        x1 = Bernoulli(1/3)
    else:
        x1 = x3o
    end

    if x2o == x1o:
        x2 = Bernoulli(1/3)
    else:
        x2 = x1o
    end

    if x3o == x2o:
        x3 = Bernoulli(1/3)
    else:
        x3 = x2o
    end

    if x1 == x3:
        token1 = 1
    else:
        token1 = 0
    end

    if x2 == x1:
        token2 = 1
    else:
        token2 = 0
    end

    if x3 == x2:
        token3 = 1
    else:
        token3 = 0
    end

    numtokens = token1 + token2 + token3
end
```
