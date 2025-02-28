# Oopa - Wordlist Analyzer

## Overview [![PyPI - Version](https://img.shields.io/pypi/v/oopa)](https://pypi.org/project/oopa/)

Oopa is an open source tool for studying password classification through the automated
analysis of wordlists. It is highly modular, allowing
open source contributors to write their own analyzers in Python with minimal
effort and share with others. It supports user-supplied encoding. Output can be
heavily customized.

By design, this project has only one direct dependency and that is prettytable.

## Installation

### From PyPi

This script is distributed on PyPi and can be installed from there.

```bash
pip install oopa
```

### From Source

Alternatively, you can install from source.

```bash
pip install .
````

or simply run the script from the `bin/` directly in the source code.

## Usage

You specify a module with the --analysis argument. Default output is top 10.

    $ oopa --analysis keyword wordlists/phpbb.txt 
    +----------+-------+
    | Keyword  | Count |
    +----------+-------+
    |  phpbb   |  332  |
    |   php    |  127  |
    | password |   89  |
    |  dragon  |   76  |
    |   pass   |   70  |
    |   mike   |   69  |
    |   blue   |   67  |
    |   test   |   66  |
    |  qwerty  |   59  |
    |   alex   |   58  |
    +----------+-------+

You can view the same data in a more parse-friendly format with --greppable.

    $ python oopa.py --analysis keyword wordlists/phpbb.txt --greppable
    #Keyword:Count
    phpbb:332
    php:127
    password:89
    dragon:76
    pass:70
    mike:69
    blue:67
    test:66
    qwerty:59
    alex:58

You can change the number of results with --top.

    $ python oopa.py --analysis length wordlists/phpbb.txt --top 20
    +--------+------------+-------+
    | Length | Percentage | Count |
    +--------+------------+-------+
    |   1    |    0.02    |   32  |
    |   2    |    0.07    |  137  |
    |   3    |    0.42    |  776  |
    |   4    |    2.49    |  4598 |
    |   5    |    4.45    |  8198 |
    |   6    |   22.82    | 42070 |
    |   7    |   17.75    | 32731 |
    |   8    |   30.01    | 55338 |
    |   9    |   10.41    | 19188 |
    |   10   |    6.45    | 11896 |
    |   11   |    2.68    |  4933 |
    |   12   |    1.36    |  2505 |
    |   13   |    0.55    |  1018 |
    |   14   |    0.28    |  515  |
    |   15   |    0.13    |  232  |
    |   16   |    0.07    |  125  |
    |   17   |    0.02    |   36  |
    |   18   |    0.01    |   27  |
    |   19   |    0.0     |   9   |
    |   20   |    0.0     |   8   |
    +--------+------------+-------+

You can change the column sorting is based on with --sort.

    $ python oopa.py --analysis length wordlists/phpbb.txt  --sort Count
    +--------+------------+-------+
    | Length | Percentage | Count |
    +--------+------------+-------+
    |   8    |   30.01    | 55338 |
    |   6    |   22.82    | 42070 |
    |   7    |   17.75    | 32731 |
    |   9    |   10.41    | 19188 |
    |   10   |    6.45    | 11896 |
    |   5    |    4.45    |  8198 |
    |   11   |    2.68    |  4933 |
    |   4    |    2.49    |  4598 |
    |   12   |    1.36    |  2505 |
    |   13   |    0.55    |  1018 |
    +--------+------------+-------+

## Name

OOPA was briefly an acronym, but I soon forgot what it stood for.

## Distribution

Increment version number first in [[setup.py]]

```bash
pip install setuptools wheel twine
python setup.py sdist bdist_wheel
twine upload dist/*
```
