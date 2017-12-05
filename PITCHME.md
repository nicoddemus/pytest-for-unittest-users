@title[Quick pytest for unittest users]

# Quick <span class="gold">pytest</span> intro

### A quick introduction to `pytest` for `unittest` users.

Very basic! Really, for people who don't know pytest at all yet.

---

@title[What]

* Dive Into Python 3: www.diveintopython3.net
* Let's use `pytest` instead of `unittest` for the example on chapter 6.

![img](assets/images/pytest1.png)


---

@title[Start]

Fork and clone the repository:

https://github.com/nicoddemus/pytest-for-unittest-users



---

@title[venv]

Create a virtual environment:

```
$ python3 -m venv .env
$ source activate .env
```

---

@title[Run it]

```
$ python romantest7.py
...........
----------------------------------------------------------------------
Ran 11 tests in 0.027s

OK
```

All set!

---

@title[roman7.py]

`roman7.py`

```python
def to_roman(n):
    '''convert integer to Roman numeral'''
    ...
    
def from_roman(s):
    '''convert Roman numeral to integer'''
    ...    
```

---

@title[romantest7.py::KnownValues]

`romantest7.py::KnownValues`

```python
class KnownValues(unittest.TestCase):
    known_values = ( (1, 'I'),
                     (2, 'II'),
                      ...
                     (3999, 'MMMCMXCIX'))

    def test_to_roman_known_values(self):
        '''to_roman should give known result with known input'''
        for integer, numeral in self.known_values:
            result = roman7.to_roman(integer)
            self.assertEqual(numeral, result)
```

---

@title[romantest7.py::ToRomanBadInput]


`romantest7.py::ToRomanBadInput`

```python
class ToRomanBadInput(unittest.TestCase):
    def test_too_large(self):
        '''to_roman should fail with large input'''
        self.assertRaises(roman7.OutOfRangeError, roman7.to_roman, 4000)
```

---

@title[romantest7.py::FromRomanBadInput]

`romantest7.py::FromRomanBadInput`

```python
class FromRomanBadInput(unittest.TestCase):
    def test_too_many_repeated_numerals(self):
        '''from_roman should fail with too many repeated numerals'''
        for s in ('MMMM', 'DD', 'CCCC', 'LL', 'XXXX', 'VV', 'IIII'):
            self.assertRaises(roman7.InvalidRomanNumeralError, roman7.from_roman, s)
```


---

@title[romantest7.py::RoundtripCheck]

`romantest7.py::RoundtripCheck`

```python
class RoundtripCheck(unittest.TestCase):
    def test_roundtrip(self):
        '''from_roman(to_roman(n))==n for all n'''
        for integer in range(1, 4000):
            numeral = roman7.to_roman(integer)
            result = roman7.from_roman(numeral)
            self.assertEqual(integer, result)
```


---

@title[How pytest?]

"How can I use pytest?"


---

@title[pip install]

```
$ pip install pytest
```


---

@title[Run pytest]

```
$ pytest romantest7.py
======================== test session starts ========================
platform win32 -- Python 3.6.3, pytest-3.3.0, py-1.5.2, pluggy-0.6.0
rootdir: X:\pytest-for-unittest-users, inifile:
collected 11 items

romantest7.py ...........                                      [100%]

===================== 11 passed in 0.06 seconds =====================
```

*Not pictured: colors!*


---

@title[Easy to start]

### Easy to start

* `pytest` can run `unittest`-based tests out of the box 99% of the time.
* Use `pytest` as a runner and enjoy its features for new tests.
* Convert old-tests to pytest-style as you go, at your own pace.


---

@title[pytest-style]

### pytest-style, you say? 

* You can use plain `assert` statements, no need to remember `self.assert*` functions;
* Tests can be simple functions!


---

@title[Convert RoundtripCheck pt1]

Let's convert `RoundtripCheck` then. 

```python
class RoundtripCheck(unittest.TestCase):
    def test_roundtrip(self):
        '''from_roman(to_roman(n))==n for all n'''
        for integer in range(1, 4000):
            numeral = roman7.to_roman(integer)
            result = roman7.from_roman(numeral)
            self.assertEqual(integer, result)
```


---

@title[Convert RoundtripCheck pt2]

**Get rid of the class (and self):** 

```python
def test_roundtrip(self):
    '''from_roman(to_roman(n))==n for all n'''
    for integer in range(1, 4000):
        numeral = roman7.to_roman(integer)
        result = roman7.from_roman(numeral)
        self.assertEqual(integer, result)
```  

(You can have test methods in classes, you just don't *have* to)


---

@title[Convert RoundtripCheck pt3]

**Change self.assertEqual to an assert** 

```python
def test_roundtrip():
    '''from_roman(to_roman(n))==n for all n'''
    for integer in range(1, 4000):
        numeral = roman7.to_roman(integer)
        result = roman7.from_roman(numeral)
        assert integer == result
```

---

@title[Convert RoundtripCheck pt4]

**It still passes of course:** 

```
$ pytest romantest7.py
======================== test session starts ========================
platform win32 -- Python 3.6.3, pytest-3.3.0, py-1.5.2, pluggy-0.6.0
rootdir: X:\pytest-for-unittest-users, inifile:
collected 11 items

romantest7.py ...........                                      [100%]

===================== 11 passed in 0.06 seconds =====================
```

*Not pictured: colors!*

---

@title[Convert RoundtripCheck pt5]

Notice that is perfectly fine to have mixed pytest-style tests and
unittest-style tests in the same test suite.

---

@title[Wait, plain asserts?]

What if an assertion fails?


---

@title[yes, plain asserts]

If an assertion fails, you still get a nice error message:

```python
def test_roundtrip():
    '''from_roman(to_roman(n))==n for all n'''
    for integer in range(1, 4000):
        numeral = roman7.to_roman(integer)
        result = roman7.from_roman(numeral) + 1  # oh oh
        assert integer == result
```

---

@title[yes, plain asserts pt2]

If an assertion fails, you still get a nice error message:

```
============================= FAILURES ==============================
__________________________ test_roundtrip ___________________________

    def test_roundtrip():
        '''from_roman(to_roman(n))==n for all n'''
        for integer in range(1, 4000):
            numeral = roman7.to_roman(integer)
            result = roman7.from_roman(numeral) + 1  # oh oh
>           assert integer == result
E           assert 1 == 2

romantest7.py:124: AssertionError
================ 1 failed, 10 passed in 0.06 seconds ================
```

*Not pictured: colors!*

---

@title[Me]


![img](assets/images/portrait11.jpg)

## Bruno Oliveira

<span align="left">
**GitHub:** https://github.com/nicoddemus
<br>
**Twitter:** `@nicoddemus`
</span> 
