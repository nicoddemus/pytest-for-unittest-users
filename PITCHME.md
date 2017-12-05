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

@title[Me]

![img](assets/images/skipper_action.png)

## Bruno Oliveira

![img](assets/images/github.png) `@nicoddemus`
![img](assets/images/twitter.jpg) https://github.com/nicoddemus

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

`roman7.py`:

```python
def to_roman(n):
    '''convert integer to Roman numeral'''
    ...
    
def from_roman(s):
    '''convert Roman numeral to integer'''
    ...    
```
