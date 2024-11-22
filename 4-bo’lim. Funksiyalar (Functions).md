### 4.1 Funksiyalarni ta'riflash (Defining Functions)

**Nazariy qism:**
Funksiya - bu ma'lum vazifani bajaruvchi, qayta ishlatiladigan kod bloki. Funksiyalar dastur kodini tartibli va tushunarli qilishga yordam beradi.

**Funksiya yaratish sintaksisi:**

```python
def funksiya_nomi(parametr1, parametr2, ...):
    """Dokumentatsiya satri (docstring)"""
    # Funksiya tanasi
    return natija
```

**Amaliy misollar:**

```python
# 1. Oddiy funksiya
def salomlash():
    print("Assalomu alaykum!")

salomlash()  # Funksiyani chaqirish

# 2. Parametrli funksiya
def kvadrat(son):
    """Sonning kvadratini qaytaradi"""
    return son ** 2

natija = kvadrat(5)
print(natija)  # 25

# 3. Bir necha parametrli funksiya
def tuliq_ism(ism, familiya):
    """Ism va familiyani birlashtiradi"""
    return f"{ism} {familiya}"

print(tuliq_ism("Anvar", "Aliyev"))  # Anvar Aliyev

# 4. Dokumentatsiyali funksiya
def aylana_yuzi(radius):
    """Aylananing yuzini hisoblaydigan funksiya

    Args:
        radius (float): Aylana radiusi

    Returns:
        float: Aylana yuzi
    """
    import math
    return math.pi * radius ** 2

yordam = help(aylana_yuzi)  # Dokumentatsiyani ko'rish
```

### 4.2 Argumentlar (Arguments)

**Nazariy qism:**
Argumentlar - funksiyaga uzatiladigan qiymatlar. Python da argumentlarning bir necha turi mavjud:

1. Pozitsion argumentlar
2. Kalit so'z argumentlari
3. Standart qiymatli argumentlar
4. O'zgaruvchan argumentlar

**Amaliy misollar:**

```python
# 1. Argumentlar turlari
def talaba_info(ism, yosh, kurs=1, fakultet="AT"):
    """Talaba haqida ma'lumot qaytaruvchi funksiya"""
    return {
        "ism": ism,
        "yosh": yosh,
        "kurs": kurs,
        "fakultet": fakultet
    }

# Pozitsion argumentlar
print(talaba_info("Anvar", 20))

# Kalit so'z argumentlari
print(talaba_info(yosh=19, ism="Botir", kurs=2))

# Argumentlarni aralashtirish
print(talaba_info("Sarvar", yosh=21, fakultet="KIF"))

# 2. Argumentlarni tekshirish
def bolish(a, b):
    """Sonlarni bo'lish funksiyasi"""
    if b == 0:
        return "Nolga bo'lib bo'lmaydi"
    return a / b

# 3. Murakkab argumentlar
def hisoblash(son, amal="+", *sonlar):
    """Ko'p sonlar ustida amal bajarish"""
    natija = son
    for s in sonlar:
        if amal == "+":
            natija += s
        elif amal == "*":
            natija *= s
    return natija
```

### 4.3 Funksiyalar turlari (Types of Functions)

**Nazariy qism:**
Python da funksiyalarning asosiy turlari:

1. Built-in funksiyalar (len, print, type...)
2. Foydalanuvchi funksiyalari
3. Lambda funksiyalar
4. Rekursiv funksiyalar
5. Generator funksiyalar

**Amaliy misollar:**

```python
# 1. Built-in funksiyalar
raqamlar = [1, 2, 3, 4, 5]
print(sum(raqamlar))      # Yig'indi: 15
print(max(raqamlar))      # Maximum: 5
print(sorted(raqamlar, reverse=True))  # Teskari tartiblash

# 2. Lambda funksiyalar
kvadrat = lambda x: x ** 2
print(kvadrat(5))  # 25

sonlar = [1, 2, 3, 4, 5]
juft_sonlar = list(filter(lambda x: x % 2 == 0, sonlar))
print(juft_sonlar)  # [2, 4]

# 3. Rekursiv funksiya
def fibonacci(n):
    """Fibonachchi sonini qaytaruvchi rekursiv funksiya"""
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# 4. Generator funksiya
def son_generator(n):
    """Sonlar generatori"""
    i = 0
    while i < n:
        yield i
        i += 1

# Generator ishlatish
for son in son_generator(5):
    print(son, end=' ')  # 0 1 2 3 4
```

### 4.4 Kalit-so'z argumentlari (Keyword Arguments)

**Nazariy qism:**
Kalit-so'z argumentlari funksiyaga parametrlarni nomlari bilan uzatish imkonini beradi.
Bu kod o'qilishini osonlashtiradi va xatolarni kamaytiradi.

**Amaliy misollar:**

```python
# 1. Kalit-so'z argumentlari bilan funksiya
def talaba_malumot(ism, *, yosh, kurs, fakultet):
    """Faqat kalit-so'z argumentlari qabul qiluvchi funksiya"""
    return f"{ism}, {yosh} yosh, {kurs}-kurs, {fakultet} fakulteti talabasi"

# Faqat kalit-so'z argumentlari bilan chaqirish
print(talaba_malumot("Anvar", yosh=20, kurs=2, fakultet="AT"))

# 2. Aralash argumentlar
def hisobla(a, b, *, operation="add"):
    """Aralash argumentli funksiya"""
    if operation == "add":
        return a + b
    elif operation == "multiply":
        return a * b

print(hisobla(5, 3))                          # 8
print(hisobla(5, 3, operation="multiply"))    # 15

# 3. Funksiya konfiguratsiyasi
def create_user(*, username, password, email, role="user"):
    """Foydalanuvchi yaratish"""
    return {
        "username": username,
        "password": password,
        "email": email,
        "role": role
    }
```

### 4.5 Standart argumentlar (Default Arguments)

**Nazariy qism:**
Standart argumentlar - funksiya parametrlariga oldindan belgilangan qiymatlar.
Agar funksiya chaqirilganda argument berilmasa, standart qiymat ishlatiladi.

**Amaliy misollar:**

```python
# 1. Oddiy standart argumentlar
def salomlash(ism, vaqt="kunduzi"):
    """Salomlashish funksiyasi"""
    if vaqt == "ertalab":
        return f"Xayrli tong, {ism}!"
    elif vaqt == "kechqurun":
        return f"Xayrli kech, {ism}!"
    return f"Salom, {ism}!"

# 2. Murakkab standart qiymatlar
def create_list(element, size=5, fill_with=None):
    """Ro'yxat yaratuvchi funksiya"""
    if fill_with is None:
        return [element] * size
    return [element if i == 0 else fill_with for i in range(size)]

# 3. Xavfli standart qiymatlar
def add_to_list(item, items=[]):  # XAVFLI! O'rniga None ishlating
    items.append(item)
    return items

# To'g'ri versiya
def add_to_list_safe(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

### 4.6 *args

**Nazariy qism:**
*args - funksiyaga o'zgaruvchan miqdordagi pozitsion argumentlarni uzatish imkonini beradi.
Barcha argumentlar tuple ko'rinishida funksiyaga uzatiladi.

**Amaliy misollar:**

```python
# 1. Oddiy *args
def yigindi(*sonlar):
    """Istalgancha sonlar yig'indisini hisoblash"""
    return sum(sonlar)

print(yigindi(1, 2, 3))       # 6
print(yigindi(1, 2, 3, 4, 5)) # 15

# 2. Args va oddiy parametrlar
def talabalar_royxati(kurs, *ismlar):
    """Talabalar ro'yxatini shakllantirish"""
    return f"{kurs}-kurs talabalari: {', '.join(ismlar)}"

print(talabalar_royxati(2, "Ali", "Vali", "Soli"))

# 3. Args bilan ishlash
def max_min(*sonlar):
    """Sonlarning maksimum va minimumini topish"""
    if not sonlar:
        return None, None
    return max(sonlar), min(sonlar)

# 4. Args ni boshqa funksiyaga uzatish
def wrapper(*args):
    """Argumentlarni boshqa funksiyaga uzatish"""
    return yigindi(*args)
```

### 4.7 **kwargs

**Nazariy qism:**
**kwargs - funksiyaga o'zgaruvchan miqdordagi kalit-qiymat juftliklarini uzatish imkonini beradi.
Barcha argumentlar dictionary ko'rinishida funksiyaga uzatiladi.

**Amaliy misollar:**

```python
# 1. Oddiy **kwargs
def print_info(**kwargs):
    """Ma'lumotlarni chiroyli chiqarish"""
    for key, value in kwargs.items():
        print(f"{key.title()}: {value}")

print_info(ism="Anvar", yosh=20, kasb="Dasturchi")

# 2. Kwargs va oddiy parametrlar
def create_person(ism, familiya, **qoshimcha):
    """Shaxs haqida ma'lumot yaratish"""
    person = {
        "ism": ism,
        "familiya": familiya
    }
    person.update(qoshimcha)
    return person

# 3. Kwargs validatsiya
def validate_user(**kwargs):
    """Foydalanuvchi ma'lumotlarini tekshirish"""
    required = {"username", "password", "email"}
    provided = set(kwargs.keys())

    if not required.issubset(provided):
        missing = required - provided
        raise ValueError(f"Quyidagi maydonlar to'ldirilmagan: {missing}")

    return True

# 4. Kwargs bilan konfiguratsiya
def configure_app(**settings):
    """Dastur sozlamalarini o'rnatish"""
    default_settings = {
        "debug": False,
        "port": 8080,
        "host": "localhost"
    }
    default_settings.update(settings)
    return default_settings
```

### 4.8 Mavjudlik (Scope)

**Nazariy qism:**
Python da mavjudlik sohalari:

1. Local scope (lokal)
2. Enclosing scope (o'rab turuvchi)
3. Global scope (global)
4. Built-in scope (o'rnatilgan)

Bu LEGB qoidasi deb ham ataladi.

**Amaliy misollar:**

```python
# 1. Global va lokal o'zgaruvchilar
x = 10  # Global o'zgaruvchi

def outer_function():
    y = 20  # Enclosing o'zgaruvchi

    def inner_function():
        z = 30  # Lokal o'zgaruvchi
        print(f"Lokal z: {z}")
        print(f"Enclosing y: {y}")
        print(f"Global x: {x}")

    inner_function()

# 2. Global keyword
counter = 0

def increment():
    global counter
    counter += 1
    return counter

# 3. Nonlocal keyword
def outer():
    count = 0

    def inner():
        nonlocal count
        count += 1
        return count

    return inner

# 4. Closure misoli
def make_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

# Ishlatish
double = make_multiplier(2)
triple = make_multiplier(3)
```

### 4.9 Nosozliklarni tuzatish (Debugging)

**Nazariy qism:**
Debugging usullari:

1. Print debugging
2. pdb - Python debugger
3. IDE debugger
4. Logging
5. Try-except blocks

**Amaliy misollar:**

```python
# 1. Print debugging
def calculate_discount(price, discount):
    print(f"Kirish qiymatlari: price={price}, discount={discount}")
    if not 0 <= discount <= 100:
        print(f"Noto'g'ri chegirma: {discount}")
        return None

    result = price * (1 - discount/100)
    print(f"Natija: {result}")
    return result

# 2. pdb bilan debugging
import pdb

def complex_calculation(a, b, c):
    pdb.set_trace()  # Debug nuqtasi
    result = a * b / c
    return result

# 3. Logging
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(levelname)s - %(message)s'
)

def process_data(data):
    logging.debug(f"Processing data: {data}")
    try:
        result = data['value'] * 2
        logging.info(f"Success: {result}")
        return result
    except KeyError as e:
        logging.error(f"Error processing data: {e}")
        return None

# 4. Try-except bilan debugging
def divide_numbers(a, b):
    try:
        result = a / b
    except ZeroDivisionError as e:
        print(f"Xato: {e}")
        return None
    except TypeError as e:
        print(f"Xato: {e}")
        return None
    else:
        return result
```

### 4.10 Funksiyalar haqida eslatmalar (Function Guidelines)

**Nazariy qism:**
Funksiyalar yozishning asosiy tamoyillari:

1. SOLID printsiplari
2. DRY (Don't Repeat Yourself)
3. Single Responsibility
4. Clear Documentation
5. Error Handling

**Amaliy misollar:**

```python
# 1. Yaxshi funksiya namunasi
def calculate_area(length: float, width: float) -> float:
    """Calculate the area of a rectangle.

    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle

    Returns:
        float: The area of the rectangle

    Raises:
        ValueError: If length or width is negative
    """
    if length < 0 or width < 0:
        raise ValueError("Length and width must be positive")

    return length * width

# 2. Type hints bilan funksiya
from typing import List, Dict, Optional

def process_user_data(
    user_id: int,
    data: Dict[str, any],
    settings: Optional[Dict] = None
) -> List[Dict]:
    """Process user data with optional settings."""
    result = []
    settings = settings or {}

    # Processing logic here

    return result

# 3. Dekoratorlar bilan funksiya
from functools import wraps
import time

def timing_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end-start:.2f} seconds")
        return result
    return wrapper

@timing_decorator
def slow_function():
    time.sleep(1)
    return "Done"

# 4. Factory pattern
def create_sorter(sort_type: str):
    """Factory function for different sorting strategies."""
    if sort_type == "quick":
        return lambda x: sorted(x)
    elif sort_type == "bubble":
        return lambda x: bubble_sort(x)
    else:
        raise ValueError(f"Unknown sort type: {sort_type}")
```
