# Python

- [Python](#python)
  - [Python Setup and Infrastructure](#python-setup-and-infrastructure)
    - [Installing venv (and pip too)](#installing-venv-and-pip-too)
    - [Getting it working with PyCharm when installed using Ubuntu Snap](#getting-it-working-with-pycharm-when-installed-using-ubuntu-snap)
    - [Running Python scripts from commandline](#running-python-scripts-from-commandline)
  - [Basic Python Project structure](#basic-python-project-structure)
  - [Virtual Environments](#virtual-environments)
  - [Python Advanced Training - ENV Setup](#python-advanced-training---env-setup)
    - [Environment setup](#environment-setup)
  - [Files and IO](#files-and-io)
    - [Files and Paths](#files-and-paths)
  - [Getting input](#getting-input)
    - [Nice input paradigm](#nice-input-paradigm)
  - [Working with the Operating System](#working-with-the-operating-system)
    - [Calling external commands](#calling-external-commands)
  - [The Quick Python Book Notes](#the-quick-python-book-notes)
    - [Chptr 7 - Dictionaries](#chptr-7---dictionaries)
      - [Keys](#keys)
      - [Examples of using a dictionary](#examples-of-using-a-dictionary)
    - [Chptr 19 - Data Types as Objects](#chptr-19---data-types-as-objects)
      - [Composite](#composite)
    - [Processing - Visual arts with Python](#processing---visual-arts-with-python)
    - [Python main()](#python-main)
  - [Libraries](#libraries)
    - [Reddit PRAW](#reddit-praw)
    - [CSV Reader/Writer](#csv-readerwriter)
    - [Jupyter](#jupyter)
    - [Flask Web Framework](#flask-web-framework)
    - [Notes from Evernote](#notes-from-evernote)
    - [Articles To Read](#articles-to-read)
    - [Lists of Useful Python Links](#lists-of-useful-python-links)
    - [Topics List](#topics-list)
  - [Romain's Book from 1A Python training](#romains-book-from-1a-python-training)
    - [General Notes](#general-notes)
      - [functions](#functions)
      - [method](#method)
      - [documenting functions](#documenting-functions)
      - [Errors](#errors)
      - [Sequences](#sequences)
      - [Sets](#sets)
      - [Strings](#strings)
      - [Refs & Mutable Objs](#refs--mutable-objs)
      - [passing parameters](#passing-parameters)
      - [Modules and Packages](#modules-and-packages)
      - [Package](#package)
      - [import vs direct execution](#import-vs-direct-execution)
  - [Python Advanced Training Notes](#python-advanced-training-notes)
    - [Afternoon Subjects](#afternoon-subjects)
    - [Iterators](#iterators)
      - [Generators - yields and sends](#generators---yields-and-sends)
    - [Testing](#testing)
    - [File Handling](#file-handling)
      - [Example of reading from files](#example-of-reading-from-files)
    - [Context Managers](#context-managers)
    - [Dicts and Tuples](#dicts-and-tuples)
    - [Miscellaneous Topics](#miscellaneous-topics)
  - [Python Tool for HTs](#python-tool-for-hts)
  - [From Original Python Page](#from-original-python-page)
    - [Installing Python](#installing-python)
    - [To install a specific version of python](#to-install-a-specific-version-of-python)
    - [Installing IDLE with MacPorts](#installing-idle-with-macports)
    - [Installing Django](#installing-django)
    - [Running under virtualenv](#running-under-virtualenv)
    - [Articles](#articles)
    - [Working with Python](#working-with-python)
      - [Getting input Python 2 vs 3](#getting-input-python-2-vs-3)
  - [Python Book Topics](#python-book-topics)
    - [Variables and Strings](#variables-and-strings)
    - [Numbers and Maths](#numbers-and-maths)
    - [Operators in Python](#operators-in-python)
    - [int() and float()](#int-and-float)
    - [Comments](#comments)
    - [Other topics to be covered](#other-topics-to-be-covered)
  - [O'Reilly cookbook on python strings](#oreilly-cookbook-on-python-strings)
  - [Slices](#slices)

- Main documentation: <https://docs.python.org/3/tutorial/index.html>
- Book with nice tips:
    <http://book.pythontips.com/en/latest/index.html>
- Style guide from Google -
    <https://google.github.io/styleguide/pyguide.html>

- <https://towardsdatascience.com/the-next-level-of-data-visualization-in-python-dd6e99039d5e?gi=85a98ab749c8>

## Python Setup and Infrastructure

**Running with py, py3 etc.**
TODO - works on win machine in work....


### Virtual Environments

- <https://realpython.com/python-virtual-environments-a-primer/>

#### Venv in production

It seems like venv can be a good thing to use in production environments also to avoid dependencies with other projects and impacting system level packages. 

- [Reddit discussion on venv in prod](https://www.reddit.com/r/Python/comments/2grmnn/virtualenv_on_production/)

#### Installing venv (and pip too)

Command I used was:

- sudo apt install python3-venv python3-pip

### Getting it working with PyCharm when installed using Ubuntu Snap

Below was a recommendation for installing the distutils but once I had
the pip and venv installed from command in section above it was okay.

- <https://superuser.com/questions/1319047/cant-install-virtual-interpreter-in-pycharm-in-linux>

Anaconda - like an environment, includes virtualenv and Spyder - a nice
IDE PyCharm - IntelliJ python IDE - meant to be the best - can modify
virtualenv from within IDE import this -> prints the Python Zen poem :)
PEP8 - style guide, use it!

PEP - Python Enhancement Proposal

### Running Python scripts from commandline

- Use a shebang at the top of the file -

```python
#!/usr/bin/env python3
```

- This format makes it more portable
  - <https://stackoverflow.com/questions/17846908/proper-shebang-for-python-script/17846946>

## Basic Python Project structure

Python-Project dir - setup.py --python-project

1. init.py

## Python Advanced Training - ENV Setup

### Environment setup

```bash
export LD_LIBRARY_PATH=~/anaconda3/lib
export PATH=$PATH:~/anaconda3/bin pip install virtualenv

virtualenv ./ source bin/activate

pip install -e . # (this runs the setup.py)
```

This puts the current directory (.) in site packages (via a egg-link) -e
indicates it's a dev project.

Result is that your package becomes available anywhere in the
virtual-env. Otherwise it would be tricky to import the log_parser from
the tests directory since they are at the same level in the file
hierarchy

## Files and IO

### Files and Paths

Use pathlib instead of os.path:

```python
from pathlib import Path

# WORKING EXAMPLE!!!!!
temp_path = Path.home()
print(temp_path)
file_dc = temp_path # "functional.log"

# Open and read entire file

with file_dc.open() as f:
  print(f.read())

# PathLib allows reading directly without having to explicitly open/close
print(file_dc.read_text())

# MANY USEFUL methods
filename = Path("source_data/text_files/raw_data.txt")

print(filename.name) # prints "raw_data.txt"

print(filename.suffix) # prints "txt"

print(filename.stem) # prints "raw_data"

print(filname.absolute()) # prints full file name + path

if not filename.exists():
  print("Oops, file doesn't exist!")
else:
  print("Yay, the file exists!")

```

- Nice Examples here:
    <https://medium.com/@ageitgey/python-3-quick-tip-the-easy-way-to-deal-with-file-paths-on-windows-mac-and-linux-11a072b58d5f>
- <https://pathlib.readthedocs.io/en/pep428/>
- python3 docs - <https://docs.python.org/3/library/pathlib.html>

## Getting input

### Nice input paradigm

- Instead of reading characters and checking them in "if" for a
    boolean

```python
  do_action = (input('Do you want to continue? (y/n)') == 'y')

  if do_action:
    # Do Stuff
```

## Working with the Operating System

### Calling external commands

- NEVER us "os" module - not portable and requires adaptation per OS
- Instead use "subprocess" module -
    <https://docs.python.org/3/library/subprocess.html#subprocess.check_call>

```python

    # NOT This
    os.system("kdiff3 '{0}' '{1}'".format(actual_file.absolute(), expected_file.absolute()))

    # INSTEAD THIS
    subprocess.check_call(["kdiff3", actual_file.absolute(), expected_file.absolute()])

```

------------------------------------------------------------------------

## The Quick Python Book Notes

- I have hardcopy
- Also available on o reilly -
    <https://learning.oreilly.com/library/view/the-quick-python/9781617294037/>

### Chptr 7 - Dictionaries

- Equivalent of a HashMap - Keys and Values
- Can assign any key
- No ordering

#### Keys

- keys -> any immutable object - Strings, numbers etc.
- Composite key - based on Tuple using immutable values

#### Examples of using a dictionary

```python
y = {} # Creates empty dictionary

y["pi"] = 3.14

y = {'pi':3.14, 'darren': 'person', 'name':'john'}

# Views not lists - TODO what's the difference?
y.keys()
y.values()
y.items() # keys and values

list(y.keys()) # get a list of keys

# Getting things from dictionary:
y["pi"] # test with "pi" in y
otherwise there's an error TODO - look this up again

# or use get()
y.get("pi", "alternative value")

```

### Chptr 19 - Data Types as Objects

#### Composite

- type() -> gives the class as a type object :)
- can check types of primitives ints etc as well as lists and user defined classes
- also
  - isinstance(object, Type)
  - issubclass(object, Type)
- Python uses Duck Typing

### Processing - Visual arts with Python

- <https://py.processing.org/tutorials/gettingstarted/>
- Example of using it: <https://github.com/aaronpenne/generative_art>

### Python main()

When a python program is executed, python interpreter starts executing
code inside it.

- It also sets few implicit variable values, one of them is **name** whose value is set as **main**.
- For python main function, we have to define a function and then use **if name == 'main'** condition to execute this function.
- If the python source file is imported as a module, python interpreter sets the **name** value to module name, so the if condition will return false and main method will not be executed.
- Python provides us flexibility to keep any name for main method, however it's best practice to name it as main() method.

```python
print("Hello")
print("[name value: ", [name)

def main():
  print("python main function")

if [name == 'main':
  main()
```

------------------------------------------------------------------------

## Libraries

### Reddit PRAW

<https://praw.readthedocs.io/en/latest/getting_started/quick_start.html>

### CSV Reader/Writer

<https://docs.python.org/3/library/csv.html>

### Jupyter

<https://jupyter.org/install.html>

### Flask Web Framework

<http://flask.pocoo.org/>

### Pandas & Matplotlib

TODO - but see section below for infos.

### Notes from Evernote

### Articles To Read

- <http://simplyargh.blogspot.fr/2012/04/python-27-django-14-on-bluehost.html>
- <https://medium.com/cs-math/11-things-i-wish-i-knew-about-django-development-before-i-started-my-company-f29f6080c131>
- <https://dbader.org/blog/meaning-of-underscores-in-python>#.

### Lists of Useful Python Links

- Python interview questions but also helpful tutorial -
    <https://www.codementor.io/python/tutorial/essential-python-interview-questions>
      
### Topics List

TODO - get from the book

- Lists, Sets, Tuples
- Dictionaries
- The nice Loops - see A Baffa's Prime Factors Kata for an example

------------------------------------------------------------------------

## Romain's Book from 1A Python training

### General Notes

- None is an Object type in Python, can be used as return value

```python

# + is used for addition but also concatenates Strings, Tuples and Lists
# ** is the power operator

# in - tests if element is in a list, Tuple, Dictionary or substring within a String
# is - identity compare of 2 values

# TRUTH -
#  - most initialized, non empty structures can be true
#  - 0 or empty structures are false

```

#### functions

- pass by reference
- always return a value (by default None)

#### method

- method is a function that's bound to an object
  - e.g. obj.getStuff()

#### documenting functions

- documenting function - if first instruction is a String then it
    becomes a doc for function

```python
def add():
"Blah"

help(add) # "Blah"
```

#### Errors

```python
try:

except IOError as e:
  traceback.print_exc # -> will print stacktrace

# Raising Exceptions ->
raise Exception name()
```

#### Sequences

- Strings
- Tuples - () - immutable
- List - - mutable
- Dictionary - { key : value } - keys must be unique and immutable
- Slicing - s[i:j]
- List comprehensions - way to create lists in Python in a natural way
  - <http://www.secnetix.de/olli/Python/list_comprehensions.hawk>

#### Sets

- Set
- Frozenset

#### Strings

- Strings -> sequences, immutable
- lots of good functions
  - find()
  - replace()
  - capitalize()
  - title()
  - split()
  - join(list)
  - AND more!!!!

#### Refs & Mutable Objs

- dictionaries - can get list of values - in the case of primitives it's a copy but for structures it is a pointer to them.
- Example -> key:value
  - if value is primitive -> list of values can be out of sync if the dictionary changes after the list of values has been extracted - list contains copy of primitives
  - if value is structure e.g. list -> reference to list is always in sync with dict

#### passing parameters

- *args - any # of named parameters
- **kwargs - any # of unnamed parameters

#### Modules and Packages

.py file is a module but not converse

module regroups Python definitions

#### Package

- directory with [init.py
- holds modules & sub-packages

#### import vs direct execution

- [name == '[main' -> this means module is executed
    directly

------------------------------------------------------------------------

## Python Advanced Training Notes

### Afternoon Subjects

------------------------------------------------------------------------

### Iterators

#### Generators - yields and sends

This is now being added to by me separately to the training.

- Generators
  - Intro and examples: <https://wiki.python.org/moin/Generators>
  - Really nice examples:
        <https://www.programiz.com/python-programming/generator>

Generator is a way of simplifying something where we want to produce a
collection of values but there's some logic associated with it. TODO -
add the other benefits -> perf with lazy load etc.

Review dicts, tuples etc. -> see example of printing all fields with
replacing Nones by '-'

### Testing

- Tox framework
  - pip install tox
- flake8 -> applies the PEP 8 style guide and fails if not respected.

### File Handling

- Always use the "with" syntax

``` python
with open(fpath) as f:
```

- never use a raw open since this could leave file handles open in case of errors

```python
f = open(path, r)
```

#### Example of reading from files

- Example of reading to a specific point in a file with a break -
    <https://stackoverflow.com/questions/27135499/read-file-until-specific-line-in-python/41438388>
  - The answers have a couple of nice ways of working with file line
        iterations

```python
# Basic file reading loop with a break from StackOverflow answer
filename = 'somefile.txt'

with open(filename, 'r') as input:

     for line in input:
         if 'indicator' in line:
              break

```

Really nice example of finding the same lines in two files -
<https://stackoverflow.com/questions/19007383/compare-two-different-files-line-by-line-in-python>

```python
with open('some_file_1.txt', 'r') as file1:

      with open('some_file_2.txt', 'r') as file2:
          same = set(file1).intersection(file2)
          # could do diff with .difference() instead of .intersection

same.discard('\\n')

with open('some_output_file.txt', 'w') as file_out:

      for line in same:
          file_out.write(line)

```

### Context Managers

follow on from file handling -> context
managers (i.e. the part after "with") are used everywhere to avoid
cumbersome try/finally structures. Should be used always for file IO,
DBs etc.

### Dicts and Tuples

Dict is not ordered so using tuple is a way of
getting around this -> See log.py for an example of using this to avoid
self.[dict.items()

### Miscellaneous Topics

- <http://mikegrouchy.com/blog/2012/05/be-pythonic-__init__py.html>
- Self explained:
    <https://pythontips.com/2013/08/07/the-self-variable-in-python-explained/>

## Python Tool for HTs

- <https://docs.python.org/3.1/library/zipfile.html#zipinfo-objects> -
    ZipFile handling
- <https://docs.python.org/3.1/library/xml.etree.elementtree.html> -
    XML handling
- <http://www.diveintopython3.net/xml.html> - Tips on using XML
- <http://www.diveintopython3.net/files.html#file-like-objects>

------------------------------------------------------------------------

## From Original Python Page

### Installing Python

Mac Osx has Python installed by default but I installed from MacPorts.

To browse all versions of python provided by Macports, use this command

```bash
$ port search python

python26 @2.6.9 (lang)

      An interpreted, object-oriented programming language

python27 @2.7.6 (lang)

      An interpreted, object-oriented programming language
```

### To install a specific version of python

```bash
port install python24 python27
```

When you install python through Macports, it will auto install the
python_select port. This is a tool for switching among python versions.
To view all the the installed python versions, execute this one

```bash
$ port select --list python

Available versions for python:

    none
    python24
    python25-apple
    python26-apple
    python27 (active)
    python27-apple

```

To set one version as the default one, use port select again

```bash
$ port select --set python python27
Selecting 'python27' for 'python' succeeded. 'python27' is now active.
```

I also installed Pip in order to install Django too

### Installing IDLE with MacPorts

So when I installed python with MacPorts I noticed the Idle version I
had was installed manually and wasn't using the MacPorts version.

In fact, MacPorts installed a version of Idle along with python in the
/Applications/MacPorts/Python 2.7. However the Idle App would not launch
from here.

The issue seemed to be coming from the tkinter port not being installed
along with python. I installed it and all was well!

```bash
sudo port install py27-tkinter
```

### Installing Django

Once Python is installed, using pip I installed the Django package

```bash
sudo pip install Django
```

Useful Link:
<http://truongtx.me/2014/02/25/mac-os-install-python-pip-virtualenv-using-macports/>

The packages were installed /opt/local/Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages/django/bin
but I still had issues with running the django-admin to create the initial project

**Solution:** added the correct library folder to the PATH via the
.profile file in home, but it looks like a better way is to install
virtualenv to isolate the different python installs from each other

```bash
#DC python addition to try to get DJango admin to work (nb - python is already working and django import works in IDLE)
export PATH=/opt/local/Library/Frameworks/Python.framework/Versions/Current/bin:$PATH
#DC finish python
```

### Running under virtualenv

Apparently this is a good idea when you have a few different versions of
python installed.... to be continued

<https://virtualenv.pypa.io/en/latest/>

### Articles

- Tips on Django Development -
    <https://medium.com/cs-math/11-things-i-wish-i-knew-about-django-development-before-i-started-my-company-f29f6080c131>

### Working with Python

Working with Python

#### Getting input Python 2 vs 3

There is an input() function but in python 2 and 3 it is different.

- Python 2 - use raw_input(<prompt_msg>) to accept user input
- Python 3 - use input(<prompt_msg>) to accept user input
  
In Python 2, input() treats the entered input text as python code so a string input would
need to be in quotes to display it for example.

## Python Book Topics

### Variables and Strings

### Numbers and Maths

### Operators in Python

- \+
- \-
- \*
- / - always does floating point division
- \*\* exponentiation
- \% modulo

Can't do arithmetic with Strings, you'll get an error.

### int() and float()

Can make Strings into ints or floats with the functions above. Format is
int(String) or float(String)

### Comments

- Single line comment - #
- block comment - """ to open and """ to finish

### Other topics to be covered

- Boolean and Conditional
- Functions
- Lists
- Dictionaries
- Tuples
- File I/O
- Modules and Packages

------------------------------------------------------------------------

## O'Reilly cookbook on python strings

- <https://learning.oreilly.com/scenarios/python-cookbook-strings/9781492062677/>

```python

import re

#`' PART 1 - Splitting Strings on Any of Multiple Delimiters `'
line = 'asdf fjdk; afed, fkejd,fdsfdd, ffooo'

# Split taking into account multi spaces, ; or , chars
split_string = re.split(r'[;,\\s]\\s\*', line)

print(split_string)

# Split with capture groups in parentheses so the separation chars are taken into account
fields = re.split(r'(;\|,\|\\s)\\s\*', line)
print(fields)

# If you need the split chars later on
values = fields[::2]
delimiters = fields[1::2] + ['']

# Reform the line
final_string = ''.join(v+d for v, d in zip(values, delimiters)) print(values) print(delimiters) print(final_string)

# grouping but without including the capture group
no_capture_group_fields = re.split(r'(?:;\|,\|\\s)\\s\*', line)
print(no_capture_group_fields)

`' PART 2 - Matching Text at the Start or End of a String `'
filename = 'spam.txt' print(filename.endswith('.txt'))
print(filename.startswith('file:'))

url = '<http://www.python.org>' print(url.startswith('http:'))

# Can match one of multiple possibilities
import os
filenames = os.listdir('.')

matching_filenames = [name for name in filenames if name.endswith[^1]]
print(matching_filenames)

result = any(name.endswith('.py') for name in filenames) print(result)

# NB need to pass a tuple not a list or a set
choices = ['http:','ftp:'] url = '<http://www.python.org>'

# url.startswith(choices) - RUNTIME error here
url.startswith(tuple(choices))

```

## Slices

Separate little detour on slices which can be used to cut up lists,
strings, arrays etc

```python
a[start:stop] # items start through stop-1
a[start:] # items start through the rest of the
array a[:stop] # items from the beginning through stop-1
a[:] # a copy of the whole array

# There is also the step value, which can be used with any of the
above: a[start:stop:step] # start through not past stop, by step
```

## Data Visualization - Pandas and Matplotlib

### Really simple example of reading a file into a panda dataframe then plotting it to a file

Shows examples of 
- custom separator
- skipping rows
- skipping whitespace
- giving explicit column names
- specifying a column to be a date

```python
#!/usr/bin/env python3

import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv('data/result.txt',
                 sep='|',
                 skiprows=2,
                 names=['Baseline', 'microsecs_per_iter', 'iter_per_microsecs', 'date'],
                 skipinitialspace=True,
                 parse_dates=['date'])

df.plot(x='date',
        y='iter_per_microsecs',
        kind='line')

plt.savefig('baseline_report.png')
```

### Some links 

- [Pandas docs - reading from types of files & streams](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html)
  - [in particular text/csv](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html)
