---
name:           "Hermann-5"
numvars:        "10"
ifthenelse:     "Yes"
infinitesp:     "No"
circdependency: "Yes"
symbolicconst:  "Yes"
contstatesp:    "No"
loopguard:      "(true)"
defective:      "No"
---

Hermann-5

```python
x1 = 1
token1 = 1
x2 = 1
token2 = 1
x3 = 1
token3 = 1
x4 = 1
token4 = 1
x5 = 1
token5 = 1
while true:
    x1o, x2o, x3o, x4o, x5o = x1, x2, x3, x4, x5

    if x1o == x5o:
        x1 = Bernoulli(1/3)
    else:
        x1 = x5o
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

    if x4o == x3o:
        x4 = Bernoulli(1/3)
    else:
        x4 = x3o
    end

    if x5o == x4o:
        x5 = Bernoulli(1/3)
    else:
        x5 = x4o
    end

    if x1 == x5:
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

    if x4 == x3:
        token4 = 1
    else:
        token4 = 0
    end

    if x5 == x4:
        token5 = 1
    else:
        token5 = 0
    end

    numtokens = token1 + token2 + token3 + token4 + token5
end
```
