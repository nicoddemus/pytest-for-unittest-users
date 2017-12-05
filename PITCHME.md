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
python3 -m venv .env
source activate .env
```

---

@title[Run it]

```
python romantest7.py
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
import roman7
import unittest

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

    def test_from_roman_known_values(self):
        '''from_roman should give known result with known input'''
        for integer, numeral in self.known_values:
            result = roman7.from_roman(numeral)
            self.assertEqual(integer, result)
```

---

@title[romantest7.py::ToRomanBadInput]


## `romantest7.py::ToRomanBadInput`

```python
class ToRomanBadInput(unittest.TestCase):
    def test_too_large(self):
        '''to_roman should fail with large input'''
        self.assertRaises(roman7.OutOfRangeError, roman7.to_roman, 4000)

    def test_zero(self):
        '''to_roman should fail with 0 input'''
        self.assertRaises(roman7.OutOfRangeError, roman7.to_roman, 0)

    def test_negative(self):
        '''to_roman should fail with negative input'''
        self.assertRaises(roman7.OutOfRangeError, roman7.to_roman, -1)

    def test_non_integer(self):
        '''to_roman should fail with non-integer input'''
        self.assertRaises(roman7.NotIntegerError, roman7.to_roman, 0.5)
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

    def test_repeated_pairs(self):
        '''from_roman should fail with repeated pairs of numerals'''
        for s in ('CMCM', 'CDCD', 'XCXC', 'XLXL', 'IXIX', 'IVIV'):
            self.assertRaises(roman7.InvalidRomanNumeralError, roman7.from_roman, s)

    def test_malformed_antecedents(self):
        '''from_roman should fail with malformed antecedents'''
        for s in ('IIMXCC', 'VX', 'DCM', 'CMM', 'IXIV',
                  'MCMC', 'XCX', 'IVI', 'LM', 'LD', 'LC'):
            self.assertRaises(roman7.InvalidRomanNumeralError, roman7.from_roman, s)

    def test_non_string(self):
        '''from_roman should fail with non-string input'''
        self.assertRaises(roman7.InvalidRomanNumeralError, roman7.from_roman, 1)
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

@title[Me]


![img](assets/images/portrait11.jpg)

## Bruno Oliveira

<span align="left">
**GitHub:** https://github.com/nicoddemus
<br>
**Twitter:** `@nicoddemus`
</span> 
