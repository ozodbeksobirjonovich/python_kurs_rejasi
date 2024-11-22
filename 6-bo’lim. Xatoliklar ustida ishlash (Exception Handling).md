### 6.1 Xatoliklar (Exceptions)

**Nazariy qism:**
Xatolik (Exception) - bu dastur bajarilishi vaqtida yuzaga keladigan kutilmagan holat. Python xatoliklarni aniqlash va ular bilan ishlash uchun keng imkoniyatlar beradi.

**Asosiy xatolik turlari:**

1. SyntaxError - sintaksis xatolik
2. TypeError - ma'lumot turi xatoligi
3. ValueError - qiymat xatoligi
4. ZeroDivisionError - nolga bo'lish xatoligi
5. FileNotFoundError - fayl topilmadi xatoligi

**Amaliy misollar:**

```python
# 1. SyntaxError
# if True print("Hello")  # Noto'g'ri sintaksis

# 2. TypeError
text = "Hello"
number = 5
# result = text + number  # TypeError: can only concatenate str to str

# 3. ValueError
# number = int("hello")  # ValueError: invalid literal for int()

# 4. ZeroDivisionError
# result = 10 / 0  # ZeroDivisionError: division by zero

# 5. FileNotFoundError
# with open("nonexistent.txt") as file:  # FileNotFoundError
#     content = file.read()

# 6. IndexError
list1 = [1, 2, 3]
# print(list1[5])  # IndexError: list index out of range

# 7. KeyError
dict1 = {"a": 1}
# print(dict1["b"])  # KeyError: 'b'
```

### 6.2 Xatoliklarni boshqarish (Handling Exceptions)

**Nazariy qism:**
Xatoliklarni boshqarish uchun try-except konstruksiyasi ishlatiladi. Bu dasturning xatosiz ishlashini ta'minlaydi.

**Konstruksiya elementlari:**

- try: xatolik yuz berishi mumkin bo'lgan kod
- except: xatolik yuz berganda bajariladigan kod
- else: xatolik yuz bermaganda bajariladigan kod
- finally: har qanday holatda bajariladigan kod

**Amaliy misollar:**

```python
# 1. Oddiy try-except
def safe_divide(a, b):
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        return "Nolga bo'lish mumkin emas"

# 2. Bir nechta except
def convert_to_number(value):
    try:
        number = float(value)
        return number
    except ValueError:
        return "Son emas"
    except TypeError:
        return "Noto'g'ri ma'lumot turi"

# 3. else va finally
def read_file(filename):
    try:
        file = open(filename, 'r')
    except FileNotFoundError:
        print("Fayl topilmadi")
    else:
        content = file.read()
        file.close()
        return content
    finally:
        print("Operatsiya tugadi")

# 4. Xatolik ma'lumotlarini olish
try:
    num = int("abc")
except ValueError as e:
    print(f"Xatolik turi: {type(e)}")
    print(f"Xatolik xabari: {str(e)}")

# 5. Barcha xatoliklarni ushlash
def safe_operation(func):
    try:
        return func()
    except Exception as e:
        return f"Xatolik yuz berdi: {str(e)}"
```

### 6.3 Turli xatoliklarni boshqarish

**Nazariy qism:**
Har xil turdagi xatoliklarni alohida boshqarish mumkin. Bu aniqroq xatolik xabarlarini berish imkonini beradi.

**Amaliy misollar:**

```python
# 1. Har xil xatoliklarni boshqarish
def complex_operation(value):
    try:
        number = float(value)
        result = 100 / number
        values = [1, 2, 3]
        item = values[int(number)]
        return item
    except ValueError:
        return "Qiymat xato (son emas)"
    except ZeroDivisionError:
        return "Nolga bo'lish mumkin emas"
    except IndexError:
        return "Indeks xato"
    except Exception as e:
        return f"Boshqa xatolik: {str(e)}"

# 2. Xatoliklar guruhi
def number_operation(value):
    try:
        result = float(value) + 10
        return result
    except (ValueError, TypeError):
        return "Son kiritilmadi"

# 3. Xatoliklar ierarxiyasi
def file_operations(filename):
    try:
        with open(filename) as f:
            content = f.read()
            number = int(content)
            result = 100 / number
            return result
    except FileNotFoundError:
        return "Fayl topilmadi"
    except ValueError:
        return "Faylda son yo'q"
    except Exception as e:
        return f"Boshqa xatolik: {e}"
```

### 6.4 Tozalash (Cleaning Up)

**Nazariy qism:**
Finally bloki resurslarni to'g'ri yopish va tozalash uchun ishlatiladi.

**Amaliy misollar:**

```python
# 1. Fayl bilan ishlash
def read_and_process_file(filename):
    file = None
    try:
        file = open(filename, 'r')
        content = file.read()
        return content
    except FileNotFoundError:
        return "Fayl topilmadi"
    finally:
        if file:
            file.close()
            print("Fayl yopildi")

# 2. Database bilan ishlash
class DatabaseConnection:
    def connect(self):
        print("Database ulandi")

    def disconnect(self):
        print("Database uzildi")

    def query(self, sql):
        print(f"SQL so'rov: {sql}")

def database_operation():
    db = DatabaseConnection()
    try:
        db.connect()
        db.query("SELECT * FROM users")
    except Exception as e:
        print(f"Xatolik: {e}")
    finally:
        db.disconnect()
```

### 6.5 with operatori (The With Statement)

**Nazariy qism:**
with operatori - context manager protokolini amalga oshiruvchi ob'ektlar bilan ishlash uchun xavfsiz usul. U resurslarni avtomatik yopish/tozalashni ta'minlaydi.

**Amaliy misollar:**

```python
# 1. Fayl bilan ishlash
def read_file_content():
    with open('data.txt', 'r') as file:
        content = file.read()
    return content  # Fayl avtomatik yopiladi

# 2. Bir nechta fayl bilan ishlash
def combine_files():
    with open('file1.txt') as f1, open('file2.txt') as f2:
        content1 = f1.read()
        content2 = f2.read()
        return content1 + content2

# 3. O'z Context Manager'imizni yaratish
class DatabaseConnection:
    def __enter__(self):
        print("Database ulandi")
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Database uzildi")
        if exc_type:
            print(f"Xatolik yuz berdi: {exc_val}")
        return False

# Ishlatish
with DatabaseConnection() as db:
    print("Database bilan ishlaymiz")
    # raise ValueError("Test xatolik")

# 4. contextlib bilan ishlash
from contextlib import contextmanager

@contextmanager
def timer():
    import time
    start = time.time()
    yield
    end = time.time()
    print(f"Bajarilish vaqti: {end - start} sekund")

with timer():
    # Vaqtni o'lchash kerak bo'lgan kod
    sum(range(1000000))
```

### 6.6 Xatoliklarni ko'tarish (Raising Exceptions)

**Nazariy qism:**
Xatoliklarni ko'tarish - dastur mantiqiga ko'ra xatolik yuz berganini bildirish usuli.

**Amaliy misollar:**

```python
# 1. Oddiy xatolikni ko'tarish
def divide(a, b):
    if b == 0:
        raise ValueError("Nolga bo'lish mumkin emas")
    return a / b

# 2. O'z xatolik klassimizni yaratish
class AgeError(Exception):
    """Yosh bilan bog'liq xatoliklar uchun"""
    pass

def verify_age(age):
    if age < 0:
        raise AgeError("Yosh manfiy bo'lishi mumkin emas")
    if age > 150:
        raise AgeError("Yosh juda katta")
    return True

# 3. Xatolikni qayta ko'tarish
def process_data(data):
    try:
        result = complex_calculation(data)
    except ValueError as e:
        print("Xatolik qayta ishlanmoqda...")
        raise  # Xatolikni qayta ko'tarish

# 4. Xatolik zanjirlari
def validate_input(value):
    try:
        if not isinstance(value, str):
            raise TypeError("Qiymat string bo'lishi kerak")
    except TypeError as e:
        raise ValueError("Validatsiya amalga oshmadi") from e
```

### 6.7 Xatoliklarni ko'tarish qiymati

**Nazariy qism:**
Xatoliklarni ko'tarish va ushlab olish jarayoni kompyuter resurslarini talab qiladi. Shuning uchun ulardan oqilona foydalanish kerak.

**Amaliy misollar:**

```python
# 1. Yomon usul (xatoliklar orqali nazorat)
def find_index_bad(lst, value):
    try:
        return lst.index(value)
    except ValueError:
        return -1

# 2. Yaxshi usul (shartlar orqali nazorat)
def find_index_good(lst, value):
    if value in lst:
        return lst.index(value)
    return -1

# 3. Xatoliklar va if/else taqqoslash
import time

# Xatoliklar orqali
def division_with_exceptions(numbers):
    results = []
    for n in numbers:
        try:
            results.append(100/n)
        except ZeroDivisionError:
            results.append(None)
    return results

# Shartlar orqali
def division_with_conditions(numbers):
    results = []
    for n in numbers:
        results.append(100/n if n != 0 else None)
    return results

# Performance test
numbers = [1, 2, 0, 4, 5] * 1000

start = time.time()
division_with_exceptions(numbers)
print(f"Exceptions time: {time.time() - start}")

start = time.time()
division_with_conditions(numbers)
print(f"Conditions time: {time.time() - start}")
```

### 6.8 Exception Handling Best Practices

**Nazariy qism:**
Xatoliklarni boshqarishning eng yaxshi amaliyotlari dastur ishonchliligini oshiradi.

**Amaliy misollar:**

```python
# 1. Aniq xatoliklarni ushlash
def process_file(filename):
    try:
        with open(filename) as f:
            data = f.read()
    except FileNotFoundError:
        logger.error(f"Fayl topilmadi: {filename}")
        raise
    except PermissionError:
        logger.error(f"Faylga kirish huquqi yo'q: {filename}")
        raise
    except Exception as e:
        logger.error(f"Kutilmagan xatolik: {e}")
        raise

# 2. Xatoliklarni login qilish
import logging

logging.basicConfig(
    filename='app.log',
    level=logging.ERROR,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)

def safe_operation():
    try:
        risky_operation()
    except Exception as e:
        logging.error(f"Xatolik yuz berdi: {str(e)}", exc_info=True)
        raise

# 3. Custom Exception klasslari
class ValidationError(Exception):
    def __init__(self, message, errors):
        super().__init__(message)
        self.errors = errors

def validate_user(user_data):
    errors = []
    if 'name' not in user_data:
        errors.append("Ism kiritilmagan")
    if 'age' not in user_data:
        errors.append("Yosh kiritilmagan")

    if errors:
        raise ValidationError("Validatsiya xatosi", errors)

# 4. Clean up resources
class Resource:
    def __init__(self, name):
        self.name = name
        print(f"{name} yaratildi")

    def clean(self):
        print(f"{self.name} tozalandi")

def use_resource():
    resource = None
    try:
        resource = Resource("Test")
        # resurs bilan ishlash
    finally:
        if resource:
            resource.clean()
```
