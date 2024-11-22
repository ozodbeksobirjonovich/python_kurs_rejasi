### 8.1 Modullarni yaratish (Creating Modules)

**Nazariy qism:**
Modul - bu Python dasturining qayta ishlatiladigan qismi. U funksiyalar, klasslar va o'zgaruvchilarni o'z ichiga olgan .py fayl.

**Amaliy misollar:**

```python
# 1. calculator.py - oddiy modul yaratish
def add(x, y):
    """Ikki sonni qo'shish"""
    return x + y

def subtract(x, y):
    """Ikki sonni ayirish"""
    return x - y

PI = 3.14159
E = 2.71828

class Calculator:
    def __init__(self):
        self.result = 0

    def add_number(self, x):
        self.result += x

    def get_result(self):
        return self.result

# 2. Modulni ishlatish
# main.py
import calculator

print(calculator.add(5, 3))       # 8
print(calculator.PI)              # 3.14159

calc = calculator.Calculator()
calc.add_number(10)
print(calc.get_result())          # 10

# 3. Moduldan ma'lum funksiyalarni import qilish
from calculator import add, subtract, PI

print(add(10, 5))                # 15
print(PI)                        # 3.14159
```

### 8.2 Kompilyatsiyalangan python fayllari

**Nazariy qism:**
Python interpretatori .py fayllarni .pyc (Python Compiled) fayllariga kompilyatsiya qiladi. Bu fayllar keyingi ishga tushirishda tezlikni oshiradi.

**Amaliy misollar:**

```python
# 1. Kompilyatsiya jarayonini ko'rish
import py_compile

py_compile.compile('calculator.py')

# 2. Kompilyatsiya vaqtida import
import importlib

# Modulni qayta yuklash
importlib.reload(calculator)

# 3. __pycache__ ni tozalash
import os
import shutil

def clear_pycache():
    if os.path.exists('__pycache__'):
        shutil.rmtree('__pycache__')
```

### 8.3 Modul qidiruv yo'li (Module Search Path)

**Nazariy qism:**
Python modulni import qilganda, uni sys.path ro'yxatidagi joylarda qidiradi.

**Amaliy misollar:**

```python
# 1. Modul qidiruv yo'lini ko'rish
import sys

for path in sys.path:
    print(path)

# 2. Yangi yo'l qo'shish
def add_module_path(path):
    if path not in sys.path:
        sys.path.append(path)

# 3. Modulni dinamik import qilish
import importlib.util

def import_module_from_path(module_name, module_path):
    spec = importlib.util.spec_from_file_location(module_name, module_path)
    module = importlib.util.module_from_spec(spec)
    spec.loader.exec_module(module)
    return module

# Ishlatish
my_module = import_module_from_path("my_module", "/path/to/my_module.py")
```

### 8.4 Paketlar (Packages)

**Nazariy qism:**
Paket - bu modullarni guruhlashtirish uchun ishlatiladigan katalog. U **init**.py faylini va boshqa modullarni o'z ichiga oladi.

**Amaliy misollar:**

```python
# Paket strukturasi
"""
mypackage/
    __init__.py
    module1.py
    module2.py
    subpackage/
        __init__.py
        module3.py
"""

# 1. __init__.py
# mypackage/__init__.py
from .module1 import function1
from .module2 import function2

__all__ = ['function1', 'function2']

# 2. module1.py
# mypackage/module1.py
def function1():
    return "Function 1"

# 3. module2.py
# mypackage/module2.py
def function2():
    return "Function 2"

# Paketni ishlatish
from mypackage import function1, function2
# yoki
import mypackage

# Subpackage bilan ishlash
from mypackage.subpackage import module3
```

### 8.5 Ichki paketlar (Sub-packages)

**Nazariy qism:**
Ichki paketlar - bu paket ichidagi paketlar. Ular katta loyihalarni modullarga ajratishda yordam beradi.

**Amaliy misollar:**

```python
"""
project/
    __init__.py
    database/
        __init__.py
        mysql.py
        postgresql.py
    utils/
        __init__.py
        helpers.py
        validation.py
"""

# 1. database/__init__.py
from .mysql import MySQLConnection
from .postgresql import PostgreSQLConnection

# 2. utils/helpers.py
def format_date(date_string):
    pass

def validate_email(email):
    pass

# 3. Ichki paketlarni import qilish
from project.database import MySQLConnection
from project.utils.helpers import format_date
from project.utils.validation import validate_email

# 4. __all__ ni ishlatish
# database/__init__.py
__all__ = ['MySQLConnection', 'PostgreSQLConnection']

# Endi quyidagicha import qilish mumkin
from project.database import *
```

### 8.6 Paket ichidagi bog'lanishlar (Intra-package References)

**Nazariy qism:**
Paket ichidagi modullar bir-biriga murojaat qilish uchun nisbiy (relative) va absolyut import usullaridan foydalanishi mumkin.

**Amaliy misollar:**

```python
"""
myapp/
    __init__.py
    core/
        __init__.py
        database.py
        models.py
    utils/
        __init__.py
        helpers.py
"""

# 1. Nisbiy import (relative import)
# myapp/core/models.py
from .database import Database  # bir xil papkadan
from ..utils.helpers import format_date  # yuqori papkadan

# 2. Absolyut import
# myapp/core/models.py
from myapp.core.database import Database
from myapp.utils.helpers import format_date

# 3. Umumiy kutubxonalarni import qilish
# myapp/core/__init__.py
from .database import Database
from .models import User, Product

__all__ = ['Database', 'User', 'Product']

# 4. Circular importlardan qochish
# myapp/core/models.py
def get_database():
    from .database import Database  # import funksiya ichida
    return Database()
```

### 8.7 dir() funksiyasi

**Nazariy qism:**
dir() funksiyasi obyektning barcha atributlari va metodlarini ro'yxat ko'rinishida qaytaradi.

**Amaliy misollar:**

```python
# 1. Modul atributlarini ko'rish
import math

# Barcha atributlarni ko'rish
print(dir(math))

# Faqat maxsus bo'lmagan atributlarni ko'rish
attributes = [attr for attr in dir(math)
             if not attr.startswith('__')]
print(attributes)

# 2. Custom klassda dir() ni ishlatish
class MyClass:
    def __init__(self):
        self.x = 1
        self.y = 2

    def method1(self):
        pass

    def method2(self):
        pass

    def __dir__(self):
        """Custom dir() natijasi"""
        return ['x', 'y', 'method1', 'method2']

obj = MyClass()
print(dir(obj))

# 3. Dinamik atributlarni tekshirish
def inspect_object(obj):
    """Obyektning barcha metodlari va atributlarini ko'rsatish"""
    # Metodlar
    methods = [attr for attr in dir(obj)
              if callable(getattr(obj, attr))]
    print("Methods:", methods)

    # Atributlar
    attributes = [attr for attr in dir(obj)
                 if not callable(getattr(obj, attr))]
    print("Attributes:", attributes)
```

### 8.8 Modullarni skript sifatida bajarish

**Nazariy qism:**
Python modullarni skript sifatida ham, modul sifatida ham ishlatish imkonini beradi. Buning uchun `__name__` maxsus o'zgaruvchisidan foydalaniladi.

**Amaliy misollar:**

```python
# utils.py
def process_data(data):
    return data.upper()

def validate_data(data):
    return len(data) > 0

def main():
    """Modul skript sifatida ishga tushganda bajariladigan kod"""
    test_data = "hello world"
    print(f"Processing: {test_data}")
    result = process_data(test_data)
    print(f"Result: {result}")

if __name__ == "__main__":
    main()

# 2. Test funksiyalarini qo'shish
def run_tests():
    """Modul testlari"""
    assert process_data("test") == "TEST"
    assert validate_data("data") == True
    assert validate_data("") == False
    print("All tests passed!")

if __name__ == "__main__":
    import sys
    if len(sys.argv) > 1 and sys.argv[1] == "--test":
        run_tests()
    else:
        main()

# 3. Konfiguratsiya va CLI argumentlar
import argparse

def parse_args():
    parser = argparse.ArgumentParser()
    parser.add_argument("--input", help="Input data")
    parser.add_argument("--test", action="store_true")
    return parser.parse_args()

if __name__ == "__main__":
    args = parse_args()
    if args.test:
        run_tests()
    elif args.input:
        result = process_data(args.input)
        print(result)
    else:
        main()
```

### 8.9 Modullar bilan ishlash - yaxshi amaliyotlar

**Nazariy qism:**
Modullar bilan ishlashda quyidagi tamoyillarga amal qilish tavsiya etiladi:

1. Aniq va tushunarli nomlash
2. Modullarni kichik va fokusli qilish
3. To'g'ri dokumentatsiya
4. Import tartibini saqlash

**Amaliy misollar:**

```python
"""Module for handling database operations.

This module provides a high-level interface for database
operations including connection management and CRUD operations.

Author: Your Name
Version: 1.0.0
"""

import logging
import sqlite3
from typing import Any, Dict, List
from datetime import datetime

# Constants
DEFAULT_DB_PATH = "database.db"
MAX_CONNECTIONS = 5

# Logging setup
logger = logging.getLogger(__name__)

class DatabaseManager:
    """Database connection and operations manager."""

    def __init__(self, db_path: str = DEFAULT_DB_PATH):
        self.db_path = db_path
        self._connection = None

    def connect(self) -> None:
        """Establish database connection."""
        try:
            self._connection = sqlite3.connect(self.db_path)
            logger.info("Database connection established")
        except sqlite3.Error as e:
            logger.error(f"Connection error: {e}")
            raise

    def close(self) -> None:
        """Close database connection."""
        if self._connection:
            self._connection.close()
            logger.info("Database connection closed")

def main():
    """Main function for testing."""
    db = DatabaseManager()
    db.connect()
    # Test operations here
    db.close()

if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO)
    main()
```

Bu formatda modul yaratish quyidagi afzalliklarga ega:

- Aniq dokumentatsiya
- Type hints
- Logging
- Constants
- Tushunarli struktura
- Test imkoniyati
