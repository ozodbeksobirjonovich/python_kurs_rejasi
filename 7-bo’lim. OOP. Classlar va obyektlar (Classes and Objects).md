### 7.1 OOP asoslari va Class tushunchasi

**Nazariy qism:**
Ob'ektga yo'naltirilgan dasturlash (OOP) - bu dasturlash paradigmasi bo'lib, ma'lumotlar va ular ustida bajariladigan amallarni ob'ektlar ko'rinishida ifodalaydi.

**OOP ning asosiy tamoyillari:**

1. Inheritance (Meros olish)
2. Encapsulation (Inkapsulyatsiya)
3. Polymorphism (Polimorfizm)
4. Abstraction (Abstraktsiya)

**Amaliy misollar:**

```python
# 1. Oddiy class yaratish
class Car:
    def __init__(self, name, color):
        self.name = name
        self.color = color

    def get_info(self):
        return f"{self.color} {self.name}"

# 2. Class dan obyekt yaratish
my_car = Car("BMW", "Qora")
print(my_car.get_info())  # Qora BMW

# 3. Class atributlari
class Student:
    university = "MIT"  # Class atributi

    def __init__(self, name):
        self.name = name  # Instance atributi

# 4. Metodlar bilan ishlash
class Calculator:
    def add(self, x, y):
        return x + y

    def multiply(self, x, y):
        return x * y
```

### 7.2 Class yaratish (Creating Classes)

**Nazariy qism:**
Python da class yaratish uchun `class` kalit so'zi ishlatiladi. Classlar atributlar va metodlardan tashkil topadi.

**Amaliy misollar:**

```python
# 1. Constructor bilan class
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            return True
        return False

# 2. Instance va class metodlar
class MathOperations:
    pi = 3.14159

    def __init__(self, value):
        self.value = value

    def square(self):  # Instance metod
        return self.value ** 2

    @classmethod
    def circle_area(cls, radius):  # Class metod
        return cls.pi * radius ** 2

    @staticmethod
    def is_positive(number):  # Static metod
        return number > 0

# 3. Property dekoratori
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, value):
        if not isinstance(value, str):
            raise ValueError("Name must be string")
        self._name = value
```

### 7.3 Konstruktorlar (Constructors)

**Nazariy qism:**
Konstruktor - klassdan obyekt yaratilayotganda avtomatik chaqiriladigan maxsus metod. Python da `__init__` metodi konstruktor vazifasini bajaradi.

**Amaliy misollar:**

```python
# 1. Oddiy konstruktor
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author

# 2. Default qiymatli konstruktor
class Product:
    def __init__(self, name, price=0, quantity=1):
        self.name = name
        self.price = price
        self.quantity = quantity

# 3. Validatsiya bilan konstruktor
class Employee:
    def __init__(self, name, salary):
        if not isinstance(salary, (int, float)):
            raise TypeError("Salary must be a number")
        if salary < 0:
            raise ValueError("Salary cannot be negative")
        self.name = name
        self.salary = salary

# 4. Ko'p parametrli konstruktor
class Rectangle:
    def __init__(self, length, width, color='black', **kwargs):
        self.length = length
        self.width = width
        self.color = color
        self.properties = kwargs
```

### 7.4 Class va obyekt atributlari

**Nazariy qism:**
Python da ikki xil atributlar mavjud:

1. Class atributlari - barcha obyektlar uchun umumiy
2. Obyekt atributlari - har bir obyekt uchun alohida

**Amaliy misollar:**

```python
# 1. Class va obyekt atributlari
class Student:
    school = "Digital One"  # Class atributi

    def __init__(self, name):
        self.name = name    # Obyekt atributi
        self.grades = []    # Obyekt atributi

# 2. Atributlar bilan ishlash
class Counter:
    count = 0  # Class atributi

    def __init__(self):
        Counter.count += 1
        self.id = Counter.count

    @classmethod
    def get_count(cls):
        return cls.count

# 3. Dinamik atributlar
class DynamicClass:
    def __init__(self, **kwargs):
        for key, value in kwargs.items():
            setattr(self, key, value)

    def add_attribute(self, name, value):
        setattr(self, name, value)

# 4. Private atributlar
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private atribut

    def get_balance(self):
        return self.__balance
```

### 7.5 Class va obyekt metodlari

**Nazariy qism:**
Python da uch xil metodlar mavjud:

1. Instance metodlar (self parameter)
2. Class metodlar (@classmethod)
3. Static metodlar (@staticmethod)

**Amaliy misollar:**

```python
class DateTime:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    # Instance metod
    def is_valid_date(self):
        if self.month in [4, 6, 9, 11]:
            return self.day <= 30
        elif self.month == 2:
            return self.day <= 29 if self._is_leap_year() else 28
        else:
            return self.day <= 31

    # Class metod
    @classmethod
    def from_string(cls, date_str):
        year, month, day = map(int, date_str.split('-'))
        return cls(year, month, day)

    # Static metod
    @staticmethod
    def is_weekend(day):
        return day in [6, 7]

    # Private helper metod
    def _is_leap_year(self):
        return self.year % 4 == 0 and (self.year % 100 != 0 or self.year % 400 == 0)

# Metodlarni ishlatish
date = DateTime.from_string("2024-02-15")
print(date.is_valid_date())       # True
print(DateTime.is_weekend(6))     # True
```

### 7.6 Maxsus metodlar (Magic Methods)

**Nazariy qism:**
Magic metodlar - maxsus nomlar bilan belgilangan metodlar bo'lib, Python obyektlarining xatti-harakatlarini boshqaradi.

**Amaliy misollar:**

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    # String reprezentatsiya
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

    def __repr__(self):
        return f"Vector(x={self.x}, y={self.y})"

    # Arifmetik operatorlar
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)

    # Taqqoslash operatorlari
    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __lt__(self, other):
        return (self.x**2 + self.y**2) < (other.x**2 + other.y**2)

    # Uzunlik
    def __len__(self):
        return int((self.x**2 + self.y**2)**0.5)

    # Container metodlari
    def __getitem__(self, key):
        if key == 0:
            return self.x
        elif key == 1:
            return self.y
        raise IndexError("Vector index out of range")

# Ishlatish
v1 = Vector(1, 2)
v2 = Vector(3, 4)
print(v1 + v2)          # Vector(4, 6)
print(v1 < v2)          # True
print(len(v1))          # 2
print(v1[0], v1[1])     # 1 2
```

### 7.7 Obyektlarni taqqoslash (Comparing Objects)

**Nazariy qism:**
Obyektlarni taqqoslash uchun maxsus taqqoslash metodlarini qo'llash kerak. Bu metodlar obyektlarning tenglik va tartib munosabatlarini aniqlaydi.

**Amaliy misollar:**

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius

    def __eq__(self, other):
        if not isinstance(other, Temperature):
            return NotImplemented
        return self.celsius == other.celsius

    def __lt__(self, other):
        if not isinstance(other, Temperature):
            return NotImplemented
        return self.celsius < other.celsius

    def __le__(self, other):
        return self < other or self == other

    def __gt__(self, other):
        return not self <= other

    def __ge__(self, other):
        return not self < other

# Ishlatish
t1 = Temperature(25)
t2 = Temperature(30)
print(t1 < t2)    # True
print(t1 == t2)   # False
print(t1 <= t2)   # True
```

### 7.8 Arifmetik amallar (Arithmetic Operations)

**Nazariy qism:**
Obyektlar ustida arifmetik amallarni bajarish uchun maxsus metodlarni aniqlash kerak.

**Amaliy misollar:**

```python
class Money:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        if isinstance(other, (int, float)):
            return Money(self.amount + other)
        if isinstance(other, Money):
            return Money(self.amount + other.amount)
        return NotImplemented

    def __sub__(self, other):
        if isinstance(other, (int, float)):
            return Money(self.amount - other)
        if isinstance(other, Money):
            return Money(self.amount - other.amount)
        return NotImplemented

    def __mul__(self, other):
        if isinstance(other, (int, float)):
            return Money(self.amount * other)
        return NotImplemented

    def __truediv__(self, other):
        if isinstance(other, (int, float)):
            return Money(self.amount / other)
        return NotImplemented

    def __str__(self):
        return f"${self.amount:.2f}"

# Ishlatish
m1 = Money(100)
m2 = Money(50)
print(m1 + m2)     # $150.00
print(m1 * 2)      # $200.00
print(m1 / 2)      # $50.00
```

### 7.9 Maxsus konteynerlar (Custom Containers)

**Nazariy qism:**
Python da o'z konteyner turlaringizni yaratish uchun maxsus metodlarni aniqlash kerak.

**Amaliy misollar:**

```python
class OrderedList:
    def __init__(self):
        self._items = []

    def add(self, item):
        self._items.append(item)
        self._items.sort()

    def __getitem__(self, index):
        return self._items[index]

    def __setitem__(self, index, value):
        self._items[index] = value
        self._items.sort()

    def __len__(self):
        return len(self._items)

    def __contains__(self, item):
        return item in self._items

    def __iter__(self):
        return iter(self._items)

    def __str__(self):
        return str(self._items)

# Linked List misoli
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        if not self.head:
            self.head = Node(data)
            return

        current = self.head
        while current.next:
            current = current.next
        current.next = Node(data)

    def __iter__(self):
        current = self.head
        while current:
            yield current.data
            current = current.next

    def __len__(self):
        count = 0
        current = self.head
        while current:
            count += 1
            current = current.next
        return count

# Ishlatish
ordered_list = OrderedList()
ordered_list.add(3)
ordered_list.add(1)
ordered_list.add(2)
print(ordered_list)  # [1, 2, 3]

linked_list = LinkedList()
linked_list.append("a")
linked_list.append("b")
linked_list.append("c")
print(list(linked_list))  # ['a', 'b', 'c']
```

### 7.10 Maxfiy a'zolar (Private Members)

**Nazariy qism:**
Python da atribut va metodlarni maxfiy qilish uchun ularning nomini ikki pastki chiziq (__) bilan boshlash kerak.

**Amaliy misollar:**

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.__owner = owner      # private atribut
        self.__balance = balance  # private atribut
        self.__pin = "1234"      # private atribut

    def __validate_pin(self, pin):  # private metod
        return pin == self.__pin

    def get_balance(self, pin):
        if self.__validate_pin(pin):
            return self.__balance
        return "PIN xato"

    def deposit(self, amount, pin):
        if self.__validate_pin(pin):
            self.__balance += amount
            return True
        return False

    def withdraw(self, amount, pin):
        if self.__validate_pin(pin):
            if amount <= self.__balance:
                self.__balance -= amount
                return True
        return False

# Ishlatish
account = BankAccount("John", 1000)
print(account.get_balance("1234"))  # 1000
print(account.get_balance("0000"))  # PIN xato

# Private atributga to'g'ridan-to'g'ri kirish mumkin emas
# print(account.__balance)  # AttributeError
```

### 7.11 Xususiyatlar (Properties)

**Nazariy qism:**
Property - bu atributlarni o'qish va o'zgartirish ustidan nazorat o'rnatish imkonini beruvchi dekorator.

**Amaliy misollar:**

```python
class Temperature:
    def __init__(self):
        self._celsius = 0

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperatura absolut noldan past bo'lishi mumkin emas")
        self._celsius = value

    @property
    def fahrenheit(self):
        return (self.celsius * 9/5) + 32

    @fahrenheit.setter
    def fahrenheit(self, value):
        self.celsius = (value - 32) * 5/9

# Read-only property misoli
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @property
    def area(self):
        return 3.14 * self._radius ** 2

    @property
    def circumference(self):
        return 2 * 3.14 * self._radius

# Ishlatish
temp = Temperature()
temp.celsius = 25
print(temp.fahrenheit)  # 77.0

circle = Circle(5)
print(circle.area)      # 78.5
```

### 7.12 Meros olish (Inheritance)

**Nazariy qism:**
Meros olish - bir klassning xususiyatlarini boshqa klassga o'tkazish mexanizmi.

**Amaliy misollar:**

```python
# 1. Oddiy meros olish
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return f"{self.name} vov-vov deydi"

class Cat(Animal):
    def speak(self):
        return f"{self.name} myau deydi"

# 2. super() funksiyasi bilan
class Vehicle:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def info(self):
        return f"{self.brand} {self.model}"

class Car(Vehicle):
    def __init__(self, brand, model, year):
        super().__init__(brand, model)
        self.year = year

    def info(self):
        return f"{super().info()} ({self.year})"

# 3. Ko'p meroslilik
class Flyable:
    def fly(self):
        return "Flying..."

class Swimmable:
    def swim(self):
        return "Swimming..."

class Duck(Animal, Flyable, Swimmable):
    def speak(self):
        return f"{self.name} quack deydi"

# Ishlatish
dog = Dog("Bobik")
print(dog.speak())      # Bobik vov-vov deydi

car = Car("Toyota", "Camry", 2023)
print(car.info())       # Toyota Camry (2023)

duck = Duck("Donald")
print(duck.speak())     # Donald quack deydi
print(duck.fly())       # Flying...
print(duck.swim())      # Swimming...
```

### 7.13 Obyekt classi (The Object Class)

**Nazariy qism:**
Python da barcha klasslar avtomatik ravishda `object` klassidan meros oladi. Bu klass asosiy metodlarni ta'minlaydi.

**Amaliy misollar:**

```python
class MyClass:
    def __init__(self, value):
        self.value = value

    # object klassining metodlarini qayta yozish
    def __str__(self):
        return f"MyClass({self.value})"

    def __repr__(self):
        return f"MyClass(value={self.value})"

    def __eq__(self, other):
        if not isinstance(other, MyClass):
            return NotImplemented
        return self.value == other.value

    def __hash__(self):
        return hash(self.value)

# Built-in funksiyalar
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    # dir() funksiyasi uchun
    def __dir__(self):
        return ['name', 'age']

    # isinstance() uchun
    def __instancecheck__(self, instance):
        return hasattr(instance, 'name') and hasattr(instance, 'age')

    # len() uchun
    def __len__(self):
        return len(self.name)

# Ishlatish
obj = MyClass(42)
print(str(obj))        # MyClass(42)
print(repr(obj))       # MyClass(value=42)

person = Person("John", 30)
print(dir(person))     # ['name', 'age']
print(len(person))     # 4
```

### 7.14 Metodni qayta belgilash (Method Overriding)

**Nazariy qism:**
Metodni qayta belgilash - voris klasslarda ota-klass metodlarini qayta yozish.

**Amaliy misollar:**

```python
class Shape:
    def __init__(self, color):
        self.color = color

    def area(self):
        raise NotImplementedError("Ushbu metod voris klassda aniqlanishi kerak")

    def info(self):
        return f"{self.__class__.__name__} ({self.color})"

class Rectangle(Shape):
    def __init__(self, color, width, height):
        super().__init__(color)
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def info(self):
        base_info = super().info()
        return f"{base_info}, Yuza: {self.area()}"

class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

# Ishlatish
rect = Rectangle("qizil", 10, 5)
print(rect.info())      # Rectangle (qizil), Yuza: 50

circle = Circle("ko'k", 3)
print(circle.area())    # 28.26
```

### 7.15 Ko'p darajali meros olish (Multi-level Inheritance)

**Nazariy qism:**
Ko'p darajali meros olish - bu klasslarning ketma-ket meros olish zanjirini yaratish.

**Amaliy misollar:**

```python
class Device:
    def __init__(self, brand):
        self.brand = brand

    def info(self):
        return f"Device: {self.brand}"

class Phone(Device):
    def __init__(self, brand, model):
        super().__init__(brand)
        self.model = model

    def info(self):
        return f"{super().info()}, Model: {self.model}"

class SmartPhone(Phone):
    def __init__(self, brand, model, os):
        super().__init__(brand, model)
        self.os = os

    def info(self):
        return f"{super().info()}, OS: {self.os}"

# Ishlatish
iphone = SmartPhone("Apple", "iPhone 13", "iOS")
print(iphone.info())  # Device: Apple, Model: iPhone 13, OS: iOS
```

### 7.16 Ko'p meros olish (Multiple Inheritance)

**Nazariy qism:**
Ko'p meros olish - bir klassga bir nechta klassdan meros olish imkonini beradi.

**Amaliy misollar:**

```python
class Flyable:
    def fly(self):
        return "Flying..."

class Swimmable:
    def swim(self):
        return "Swimming..."

class Walkable:
    def walk(self):
        return "Walking..."

class Duck(Flyable, Swimmable, Walkable):
    def __init__(self, name):
        self.name = name

    def info(self):
        return f"{self.name} can: {self.fly()}, {self.swim()}, {self.walk()}"

class FlyingFish(Flyable, Swimmable):
    def __init__(self, species):
        self.species = species

    def info(self):
        return f"{self.species}: {self.fly()}, {self.swim()}"

# MRO (Method Resolution Order) misoli
class A:
    def method(self):
        return "A method"

class B(A):
    def method(self):
        return "B method"

class C(A):
    def method(self):
        return "C method"

class D(B, C):
    pass

# Ishlatish
duck = Duck("Donald")
print(duck.info())  # Donald can: Flying..., Swimming..., Walking...

fish = FlyingFish("Flying Fish")
print(fish.info())  # Flying Fish: Flying..., Swimming...

# MRO ni tekshirish
d = D()
print(D.__mro__)  # MRO ni ko'rsatadi
print(d.method()) # "B method" (chapdan o'ngga qoidasi)
```

### 7.17 Meros olishning yaxshi misoli

**Nazariy qism:**
Meros olishni to'g'ri qo'llash uchun "is-a" munosabatini tekshirish kerak. Masalan, "Mushuk hayvondir" (Cat is an Animal).

**Amaliy misollar:**

```python
class Account:
    def __init__(self, account_number, balance=0):
        self._account_number = account_number
        self._balance = balance

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            return True
        return False

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance -= amount
            return True
        return False

    def get_balance(self):
        return self._balance

class SavingsAccount(Account):
    def __init__(self, account_number, interest_rate):
        super().__init__(account_number)
        self.interest_rate = interest_rate

    def add_interest(self):
        interest = self._balance * (self.interest_rate / 100)
        self.deposit(interest)
        return interest

class CheckingAccount(Account):
    def __init__(self, account_number, overdraft_limit):
        super().__init__(account_number)
        self.overdraft_limit = overdraft_limit

    def withdraw(self, amount):
        if 0 < amount <= (self._balance + self.overdraft_limit):
            self._balance -= amount
            return True
        return False

# Ishlatish
savings = SavingsAccount("SA001", 5.0)
savings.deposit(1000)
print(savings.add_interest())  # 50.0
print(savings.get_balance())   # 1050.0

checking = CheckingAccount("CA001", 500)
checking.deposit(200)
print(checking.withdraw(600))  # True (overdraft ishlatildi)
print(checking.get_balance()) # -400.0
```

### 7.18 Abstrakt asosiy classlar (Abstract Base Classes)

**Nazariy qism:**
Abstract Base Class (ABC) - bu interfeys yoki shablon vazifasini bajaruvchi klass. Undan to'g'ridan-to'g'ri obyekt yaratib bo'lmaydi.

**Amaliy misollar:**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14 * self.radius

# Abstrakt interfeys misoli
class PaymentProcessor(ABC):
    @abstractmethod
    def process_payment(self, amount):
        pass

    @abstractmethod
    def refund(self, amount):
        pass

class CreditCardProcessor(PaymentProcessor):
    def process_payment(self, amount):
        return f"Processing ${amount} via Credit Card"

    def refund(self, amount):
        return f"Refunding ${amount} to Credit Card"

class PayPalProcessor(PaymentProcessor):
    def process_payment(self, amount):
        return f"Processing ${amount} via PayPal"

    def refund(self, amount):
        return f"Refunding ${amount} to PayPal account"

# Ishlatish
# shape = Shape()  # TypeError: Can't instantiate abstract class

rect = Rectangle(10, 5)
print(rect.area())      # 50
print(rect.perimeter()) # 30

pp = PayPalProcessor()
print(pp.process_payment(100))  # Processing $100 via PayPal
```

### 7.19 Polimorfizm (Polymorphism)

**Nazariy qism:**
Polimorfizm - bu bir xil nomli metodlarning turli klasslarda turlicha ishlash imkoniyati.

**Amaliy misollar:**

```python
# 1. Polimorfizm misollar
class MediaPlayer:
    def play(self, media):
        media.play()

class Video:
    def play(self):
        print("Video ijro etilmoqda...")

class Audio:
    def play(self):
        print("Audio ijro etilmoqda...")

class Image:
    def play(self):
        print("Rasm ko'rsatilmoqda...")

# 2. Duck typing polimorfizm
class DataStore:
    def save_data(self, data, storage):
        storage.save(data)

class FileStorage:
    def save(self, data):
        print(f"Ma'lumot faylga saqlandi: {data}")

class DatabaseStorage:
    def save(self, data):
        print(f"Ma'lumot bazaga saqlandi: {data}")

class CloudStorage:
    def save(self, data):
        print(f"Ma'lumot cloudga saqlandi: {data}")

# Ishlatish
player = MediaPlayer()
player.play(Video())  # Video ijro etilmoqda...
player.play(Audio())  # Audio ijro etilmoqda...
player.play(Image())  # Rasm ko'rsatilmoqda...

store = DataStore()
store.save_data("Hello", FileStorage())      # Ma'lumot faylga saqlandi: Hello
store.save_data("World", DatabaseStorage())  # Ma'lumot bazaga saqlandi: World
store.save_data("!", CloudStorage())         # Ma'lumot cloudga saqlandi: !
```

### 7.20 Duck Typing

**Nazariy qism:**
Duck Typing - bu ob'ektning tipiga emas, balki uning xatti-harakatlariga (metodlariga) qarab ishlash prinsipi.

**Amaliy misollar:**

```python
# 1. Duck typing misoli
class TextProcessor:
    def process_text(self, text_source):
        text = text_source.get_text()
        return text.upper()

class File:
    def get_text(self):
        return "File dan olingan matn"

class Database:
    def get_text(self):
        return "Database dan olingan matn"

class API:
    def get_text(self):
        return "API dan olingan matn"

# 2. Duck typing va validatsiya
class Validator:
    def validate(self, value, validator):
        if hasattr(validator, 'is_valid') and callable(validator.is_valid):
            return validator.is_valid(value)
        raise TypeError("Validator 'is_valid' metodiga ega bo'lishi kerak")

class EmailValidator:
    def is_valid(self, email):
        return '@' in email and '.' in email

class PhoneValidator:
    def is_valid(self, phone):
        return phone.isdigit() and len(phone) == 9

# Ishlatish
processor = TextProcessor()
print(processor.process_text(File()))      # FILE DAN OLINGAN MATN
print(processor.process_text(Database()))  # DATABASE DAN OLINGAN MATN
print(processor.process_text(API()))       # API DAN OLINGAN MATN

validator = Validator()
print(validator.validate("test@example.com", EmailValidator()))  # True
print(validator.validate("123456789", PhoneValidator()))        # True
```

### 7.21 Built-in turlarni kengaytirish

**Nazariy qism:**
Python-ning o'rnatilgan turlarini kengaytirish orqali yangi funksionallikni qo'shish mumkin.

**Amaliy misollar:**

```python
# 1. List kengaytmasi
class UniqueList(list):
    def append(self, item):
        if item not in self:
            super().append(item)

    def extend(self, items):
        for item in items:
            self.append(item)

# 2. Dict kengaytmasi
class DefaultDict(dict):
    def __init__(self, default_value=None):
        super().__init__()
        self.default_value = default_value

    def __missing__(self, key):
        self[key] = self.default_value
        return self.default_value

# 3. String kengaytmasi
class SuperString(str):
    def reverse(self):
        return self[::-1]

    def count_vowels(self):
        return sum(1 for char in self.lower() if char in 'aeiou')

    def count_consonants(self):
        return sum(1 for char in self.lower() if char.isalpha() and char not in 'aeiou')

# Ishlatish
unique_list = UniqueList([1, 2, 3])
unique_list.append(2)  # 2 qo'shilmaydi chunki u allaqachon mavjud
print(unique_list)     # [1, 2, 3]

d = DefaultDict(0)
print(d['noexistent'])  # 0
print(d)               # {'noexistent': 0}

s = SuperString("Hello World")
print(s.reverse())          # dlroW olleH
print(s.count_vowels())     # 3
print(s.count_consonants()) # 7
```

### 7.22 Ma'lumot classlari (Data Classes)

**Nazariy qism:**
Data Classlar - ma'lumotlarni saqlash uchun mo'ljallangan maxsus klasslar. Ular `@dataclass` dekoratori yordamida yaratiladi.

**Amaliy misollar:**

```python
from dataclasses import dataclass, field
from typing import List

# 1. Oddiy data class
@dataclass
class Point:
    x: float
    y: float

# 2. Default qiymatlar bilan
@dataclass
class Rectangle:
    width: float
    height: float = 1.0
    area: float = field(init=False)

    def __post_init__(self):
        self.area = self.width * self.height

# 3. Murakkab data class
@dataclass
class Student:
    name: str
    grades: List[int] = field(default_factory=list)
    average: float = field(init=False)

    def __post_init__(self):
        self.average = sum(self.grades) / len(self.grades) if self.grades else 0

# 4. Immutable data class
@dataclass(frozen=True)
class Configuration:
    host: str
    port: int
    debug: bool = False

# Ishlatish
p = Point(1.0, 2.0)
print(p)  # Point(x=1.0, y=2.0)

rect = Rectangle(10.0, 5.0)
print(rect)  # Rectangle(width=10.0, height=5.0, area=50.0)

student = Student("John", [85, 90, 95])
print(student)  # Student(name='John', grades=[85, 90, 95], average=90.0)

config = Configuration("localhost", 8080)
# config.debug = True  # FrozenInstanceError: can't assign to field 'debug'
```

### 7.23 OOP Best Practices

**Nazariy qism:**
OOP-da eng yaxshi amaliyotlar - bu kodning sifatini oshirish va xatolarni kamaytirish uchun qo'llaniladigan tamoyillar.

**Amaliy misollar:**

```python
# 1. SOLID printsiplari
# Single Responsibility Principle
class UserManager:
    def __init__(self, db):
        self.db = db

    def create_user(self, username, password):
        # Faqat foydalanuvchi yaratish logikasi
        pass

class PasswordHasher:
    @staticmethod
    def hash_password(password):
        # Faqat parolni hashlash logikasi
        pass

# 2. Dependency Injection
class EmailSender:
    def send(self, to, message):
        print(f"Sending email to {to}: {message}")

class UserNotifier:
    def __init__(self, notifier):
        self.notifier = notifier

    def notify(self, user, message):
        self.notifier.send(user.email, message)

# 3. Composition over Inheritance
class Engine:
    def start(self):
        return "Engine started"

class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        return self.engine.start()

# 4. Factory Pattern
class AnimalFactory:
    @staticmethod
    def create_animal(animal_type):
        if animal_type == "dog":
            return Dog()
        elif animal_type == "cat":
            return Cat()
        raise ValueError(f"Unknown animal type: {animal_type}")

# Ishlatish
notifier = UserNotifier(EmailSender())
car = Car()
animal_factory = AnimalFactory()

print(car.start())                    # Engine started
dog = animal_factory.create_animal("dog")
print(dog.speak())                    # Woof!
```

Bu bo'lim OOP ning asosiy konseptsiyalari va ularning Python-dagi implementatsiyasini qamrab oldi. Asosiy mavzular:

1. Klasslar va obyektlar
2. Meros olish va polimorfizm
3. Enkapsulatsiya va abstraktsiya
4. Magic metodlar
5. Data klasslar va best practices

Siz ushbu bilimlarni qo'llab, toza va qayta ishlatiluvchi kod yoza olasiz.
