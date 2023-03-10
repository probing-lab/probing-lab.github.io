---
title: Polar
style: fill
color: primary
description: Polar implements a novel static analysis technique to derive higher moments for program variables for a large class of probabilistic loops with potentially uncountable state spaces.
---

<div align="right" style="float:right;margin:50px">
  <a href="https://github.com/probing-lab/polar">
    <img src="../assets/logo/polar-logo.svg" width="300px" alt="Polar logo" />
  </a>
</div>

# Polar

Polar implements a novel static analysis technique to derive higher moments for program variables for a large class
of probabilistic loops with potentially uncountable state spaces.


## Installation

To install Polar, you can do the following steps.

1. Make sure you have python (version &ge; 3.8) and pip installed on your system.
Otherwise install it in your preferred way.

2. Clone the repository:
```
git clone git@github.com:probing-lab/polar.git
cd polar
```

3. Create a virtual environment in the `.venv` directory:
```
pip install --user virtualenv
python -m venv .venv
```

4. Activate the virtual environment:
```
source .venv/bin/activate
```

5. Install the required dependencies:
```
pip install -r requirements.txt
```

## Usage

```
python polar.py benchmarks/polar_paper/illustrating.prob --goals "E(z)"
```

The parameter `goals` takes any expected value of monomials of program variables, for instance `"E(x**2)"`, `"E(t*x**2)"`, etc.
To compute the variance you can pass `"c2(x)"`.
In general, to compute the kth central moment (where k is a natural number), pass `"ck(x)"` to the goals parameter.

For a list of all parameters supported by Polar run:

```
python polar.py --help
```


## Run Tests

You can run the automatic test suite with:

```
python -m unittest
```

To run `flake8`, a tool for style guide enforcement, first install it with:
```
pip install flake8
```

After installation `flake8` can be executed by running:
```
flake8 .
```
