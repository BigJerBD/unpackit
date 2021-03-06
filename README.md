PYDARG
======
Toy Project attemting to simplify config management in python
(in the end this was a stupid idea) 


Pydarg is a python simple utility package providing a way to handle
more deeply dictionary parameters of implemented functions


REQUIREMENTS
===========

Require python 3.6+

INSTALLATION
============

Run this command line to fetch the package on Pypi

``` shell
$ pip install pydarg
```

USAGE
============

This package provide a method "dct_arg" used as a decorator

### Basic Usage

without any parameter, dct_arg unpacks the dictionary
argument of function signature

``` python

@dct_arg
def example(foo,bar):
    print(foo,bar)

param = {'foo':'1,'bar':'2','other':3}
example(param)
```

the main advantage of using dct_arg instead of **param
is that it avoid binding extra argument, making it really useful for
handling configuration dictionary having multiple of parameter.

those functions call would also be valid

``` python
example(foo='foo',bar='bar')
example({'foo':'foo_1'},bar='bar)
example({},'foo','bar')
```

It is also possible to override dct_arg's name by using keyword argument.
making this line printing "foo_2" and "bar_2"

``` python
example({'foo':'foo_1','bar:'bar_1},'foo_2,bar='bar_2)
```


### parameters

```python
dct_arg(
    _fct=None, *,
    is_positional=True,
    is_keyword=True,
    name='dct_arg',
    path="",
    fetch_args=None
    ):
```

Where :
- arg_type:

    define what is the type of the dct_arg

    - ArgType.POSITIONAL
    - ArgType.KEY_WORD
    - ArgType.BOTH,

- name

    represent the keyword name of the dct_arg

- path

    if the desired dct_arg is nested you you can specify the path
    with "/"

- fetch_args

    dictionary composed of key representing keyword parameter, and
    the path with "/" to fetch them in the dct_arg


### Examples

**fetch the nested dictionary argument named config**

```python
@dct_arg(name='config,path='child/subchild')
def example(e0, e1):
    print(e1, e0)


example(config={'child': {'subchild': {'e1': 1, 'e0': 0}}})
example({'child': {'subchild': {'e1': 1}}}, e0=0)
```

since by default a dct_arg is a positional keyword
both function call works

**fetch the dct_arg itself as an argument**

```python
@dct_arg(fetch_args={'config': ""})
def example(config, e0):
    pass

example(configuration={'e0': 0})
```
