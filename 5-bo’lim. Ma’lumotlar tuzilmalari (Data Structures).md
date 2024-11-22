### 5.1 Ro'yxatlar (Lists)

**Nazariy qism:**
Ro'yxat - bu tartiblangan, o'zgaruvchan (mutable) ma'lumot turi. U har qanday turdagi ma'lumotlarni o'z ichiga olishi mumkin.

**Asosiy xususiyatlari:**

- O'zgaruvchan (mutable)
- Tartiblangan
- Indekslanadi
- Takrorlanishga ruxsat beradi
- Turli xil ma'lumot turlarini saqlashi mumkin

**Amaliy misollar:**

```python
# 1. Ro'yxat yaratish usullari
sonlar = [1, 2, 3, 4, 5]
ismlar = ["Ali", "Vali", "Gani"]
aralash = [1, "salom", 3.14, True, [1, 2]]

# 2. Ro'yxat metodlari
# Element qo'shish
sonlar.append(6)        # Oxiriga qo'shish
sonlar.insert(0, 0)     # Index bo'yicha qo'shish
sonlar.extend([7, 8])   # Bir nechta element qo'shish

# Element o'chirish
sonlar.remove(3)        # Qiymat bo'yicha o'chirish
del sonlar[0]           # Index bo'yicha o'chirish
oxirgi = sonlar.pop()   # Oxirgi elementni olish va o'chirish

# Ro'yxatni o'zgartirish
sonlar.sort()           # Tartiblash
sonlar.reverse()        # Teskari aylantirish
sonlar.clear()          # Tozalash

# 3. Ro'yxat bilan operatsiyalar
# Kesish (slicing)
raqamlar = [0, 1, 2, 3, 4, 5]
print(raqamlar[1:4])    # [1, 2, 3]
print(raqamlar[::2])    # [0, 2, 4]
print(raqamlar[::-1])   # [5, 4, 3, 2, 1, 0]

# Birlashtirish
list1 = [1, 2]
list2 = [3, 4]
all_numbers = list1 + list2  # [1, 2, 3, 4]

# Ko'paytirish
zeros = [0] * 5  # [0, 0, 0, 0, 0]
```

### 5.2 Elementlarga kirish (Accessing Items)

**Nazariy qism:**
Python ro'yxatlarida elementlarga indeks orqali kirish mumkin. Indekslar 0 dan boshlanadi.

**Asosiy xususiyatlar:**

- Musbat indeks (0 dan)
- Manfiy indeks (-1 dan)
- Slicing (kesish)
- Step (qadam)

**Amaliy misollar:**

```python
# 1. Indeks orqali kirish
numbers = [10, 20, 30, 40, 50]
print(numbers[0])     # 10 (birinchi element)
print(numbers[-1])    # 50 (oxirgi element)
print(numbers[-2])    # 40 (oxiridan ikkinchi)

# 2. Slicing
print(numbers[1:4])   # [20, 30, 40]
print(numbers[:3])    # [10, 20, 30]
print(numbers[2:])    # [30, 40, 50]
print(numbers[:])     # [10, 20, 30, 40, 50] (nusxa olish)

# 3. Qadamlar bilan kesish
print(numbers[::2])   # [10, 30, 50]
print(numbers[::-1])  # [50, 40, 30, 20, 10]

# 4. Elementlarni o'zgartirish
numbers[0] = 100
print(numbers)        # [100, 20, 30, 40, 50]

# Slice orqali o'zgartirish
numbers[1:4] = [200, 300, 400]
print(numbers)        # [100, 200, 300, 400, 50]
```

### 5.3 Ro'yxatni bo'shatish (List Unpacking)

**Nazariy qism:**
Bo'shatish - ro'yxat elementlarini alohida o'zgaruvchilarga ajratish usuli.

**Asosiy xususiyatlar:**

- To'liq bo'shatish
- Qisman bo'shatish
- * operatori orqali bo'shatish
- Bo'shatish bilan almashtirish

**Amaliy misollar:**

```python
# 1. To'liq bo'shatish
numbers = [1, 2, 3]
a, b, c = numbers
print(a, b, c)  # 1 2 3

# 2. * operatori bilan bo'shatish
first, *rest = [1, 2, 3, 4, 5]
print(first)  # 1
print(rest)   # [2, 3, 4, 5]

# O'rtadagi elementlarni olish
first, *middle, last = [1, 2, 3, 4, 5]
print(middle)  # [2, 3, 4]

# 3. Qisman bo'shatish
def get_scores():
    return [98, 95, 89, 92, 96]

highest, *rest, lowest = get_scores()
print(f"Eng yuqori: {highest}")
print(f"Eng past: {lowest}")
print(f"Qolganlar: {rest}")

# 4. Bo'shatish bilan funksiyalar
def process_point(x, y):
    return x + y

point = [3, 4]
result = process_point(*point)
```

### 5.4 Ro'yxatlar bo'ylab tsikllash (Looping over Lists)

**Nazariy qism:**
Python ro'yxatlari bo'ylab yurish uchun bir necha xil usullar mavjud.

**Asosiy usullar:**

1. For loop
2. While loop
3. Enumerate
4. Zip
5. List comprehension

**Amaliy misollar:**

```python
# 1. Oddiy for tsikli
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num)

# 2. Indeks bilan yurish
for i in range(len(numbers)):
    print(f"Index {i}: {numbers[i]}")

# 3. Enumerate ishlatish
for index, value in enumerate(numbers, start=1):
    print(f"{index}-element: {value}")

# 4. Parallel ro'yxatlar bo'ylab yurish
names = ["Ali", "Vali", "Gani"]
ages = [20, 25, 30]
for name, age in zip(names, ages):
    print(f"{name} {age} yoshda")

# 5. While loop
i = 0
while i < len(numbers):
    print(numbers[i])
    i += 1
```

### 5.5 Element qo'shish yoki o'chirish (Adding or Removing Items)

**Nazariy qism:**
Python ro'yxatlarida elementlarni qo'shish va o'chirish uchun turli metodlar mavjud.

**Asosiy metodlar:**

1. append() - oxiriga qo'shish
2. insert() - indeks bo'yicha qo'shish
3. extend() - ro'yxatni kengaytirish
4. remove() - qiymat bo'yicha o'chirish
5. pop() - indeks bo'yicha o'chirish va qaytarish
6. clear() - barcha elementlarni o'chirish

**Amaliy misollar:**

```python
# 1. Elementlarni qo'shish
numbers = [1, 2, 3]
numbers.append(4)           # [1, 2, 3, 4]
numbers.insert(0, 0)       # [0, 1, 2, 3, 4]
numbers.extend([5, 6, 7])  # [0, 1, 2, 3, 4, 5, 6, 7]

# 2. Elementlarni o'chirish
numbers.remove(3)          # Qiymat bo'yicha
last = numbers.pop()       # Oxirgi elementni olish
first = numbers.pop(0)     # Birinchi elementni olish
numbers.clear()            # Ro'yxatni tozalash

# 3. Ro'yxatlarni birlashtirish
list1 = [1, 2]
list2 = [3, 4]
combined = list1 + list2   # [1, 2, 3, 4]

# 4. Ro'yxatni ko'paytirish
zeros = [0] * 5            # [0, 0, 0, 0, 0]
```

### 5.6 Elementlarni topish (Finding Items)

**Nazariy qism:**
Ro'yxatda elementlarni qidirish uchun turli metodlar mavjud.

**Asosiy metodlar:**

1. index() - elementning indeksini topish
2. count() - element sonini hisoblash
3. in operatori - mavjudlikni tekshirish
4. min()/max() - minimum/maximum qiymatlarni topish
5. sorted() - tartiblangan nusxa olish

**Amaliy misollar:**

```python
numbers = [1, 2, 3, 2, 4, 2, 5]

# 1. Element indeksini topish
index = numbers.index(2)        # Birinchi uchragan 2 ning indeksi
print(index)                    # 1

# 2. Element sonini hisoblash
count = numbers.count(2)        # 2 soni necha marta uchragani
print(count)                    # 3

# 3. Mavjudlikni tekshirish
exists = 3 in numbers          # True
not_exists = 6 in numbers      # False

# 4. Min/Max qiymatlarni topish
minimum = min(numbers)         # 1
maximum = max(numbers)         # 5

# 5. Ro'yxatni tartiblash
sorted_numbers = sorted(numbers)            # Yangi ro'yxat
reverse_sorted = sorted(numbers, reverse=True)  # Teskari tartib
```

### 5.7 Ro'yxatlarni tartiblash (Sorting Lists)

**Nazariy qism:**
Python ro'yxatlarni tartiblash uchun ikki xil usulni taqdim etadi: sort() metodi va sorted() funksiyasi.

**Asosiy xususiyatlari:**

- sort() - ro'yxatni o'zini o'zgartiradi
- sorted() - yangi tartiblangan ro'yxat qaytaradi
- key parametri - tartiblash kalitini belgilash
- reverse parametri - teskari tartib

**Amaliy misollar:**

```python
# 1. Oddiy tartiblash
numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
numbers.sort()                  # Ro'yxatni o'zgartiradi
print(numbers)                  # [1, 1, 2, 3, 3, 4, 5, 5, 5, 6, 9]

# 2. Yangi ro'yxat olish
original = [3, 1, 4, 1, 5]
sorted_numbers = sorted(original)  # Yangi ro'yxat qaytaradi
print(original)                   # [3, 1, 4, 1, 5] - o'zgarmaydi

# 3. Teskari tartib
numbers.sort(reverse=True)
print(numbers)                  # [9, 6, 5, 5, 5, 4, 3, 3, 2, 1, 1]

# 4. Key funksiya bilan tartiblash
words = ['banana', 'apple', 'date', 'cherry']
# Uzunlik bo'yicha tartiblash
words.sort(key=len)
print(words)                    # ['date', 'apple', 'banana', 'cherry']

# 5. Murakkab tartiblash
students = [
    {'name': 'Ali', 'grade': 85},
    {'name': 'Vali', 'grade': 92},
    {'name': 'Gani', 'grade': 78}
]
# Ball bo'yicha tartiblash
sorted_students = sorted(students, key=lambda x: x['grade'], reverse=True)
```

### 5.8 Lambda funksiyalari (Lambda Functions)

**Nazariy qism:**
Lambda - bu bir qatorli anonim funksiyalar. Ular oddiy funksiyalarning soddalashtirilgan ko'rinishi.

**Asosiy xususiyatlari:**

- Bir qatorli
- Anonim
- Bir marta ishlatiladigan
- filter(), map(), sort() bilan ishlatish

**Amaliy misollar:**

```python
# 1. Oddiy lambda funksiyalar
square = lambda x: x ** 2
print(square(5))               # 25

sum_two = lambda x, y: x + y
print(sum_two(3, 4))          # 7

# 2. Filter bilan ishlatish
numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)                  # [2, 4, 6]

# 3. Map bilan ishlatish
squares = list(map(lambda x: x ** 2, numbers))
print(squares)                # [1, 4, 9, 16, 25, 36]

# 4. Sort bilan ishlatish
pairs = [(1, 'one'), (2, 'two'), (3, 'three')]
pairs.sort(key=lambda pair: pair[1])  # String bo'yicha tartiblash
print(pairs)

# 5. Conditional lambda
is_even = lambda x: "juft" if x % 2 == 0 else "toq"
print(is_even(4))            # "juft"
```

### 5.9 map() Funksiyasi

**Nazariy qism:**
map() funksiyasi berilgan funksiyani iteratsiya qilinadigan ob'ektning har bir elementiga qo'llaydi va natijalardan yangi map ob'ekt yaratadi.

**Asosiy xususiyatlari:**

- Har bir elementga funksiya qo'llash
- Yangi ob'ekt qaytarish
- Lazy evaluation
- Bir nechta iterable bilan ishlash

**Amaliy misollar:**

```python
# 1. Oddiy map
numbers = [1, 2, 3, 4, 5]
squares = map(lambda x: x**2, numbers)
print(list(squares))  # [1, 4, 9, 16, 25]

# 2. Built-in funksiyalar bilan
numbers_str = ['1', '2', '3', '4']
numbers_int = list(map(int, numbers_str))
print(numbers_int)    # [1, 2, 3, 4]

# 3. Bir nechta ro'yxat bilan ishlash
list1 = [1, 2, 3]
list2 = [10, 20, 30]
sums = list(map(lambda x, y: x + y, list1, list2))
print(sums)          # [11, 22, 33]

# 4. Custom funksiya bilan
def multiply_by_2(x):
    return x * 2

doubled = list(map(multiply_by_2, numbers))
print(doubled)       # [2, 4, 6, 8, 10]
```

### 5.10 filter() Funksiyasi

**Nazariy qism:**
filter() funksiyasi berilgan funksiya True qaytargan elementlarni ajratib oladi.

**Asosiy xususiyatlari:**

- Boolean qaytaruvchi funksiya qo'llash
- Shartga mos kelgan elementlarni saqlash
- Yangi filter ob'ekt qaytarish
- None bilan filtrlash

**Amaliy misollar:**

```python
# 1. Oddiy filtrlash
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)        # [2, 4, 6, 8, 10]

# 2. None bilan filtrlash
values = [0, 1, False, True, None, [], [1, 2]]
valid = list(filter(None, values))
print(valid)        # [1, True, [1, 2]]

# 3. Custom funksiya bilan
def is_positive(x):
    return x > 0

numbers = [-2, -1, 0, 1, 2]
positives = list(filter(is_positive, numbers))
print(positives)    # [1, 2]

# 4. Filter va map birga
numbers = [1, 2, 3, 4, 5, 6]
result = list(map(lambda x: x**2,
                 filter(lambda x: x % 2 == 0, numbers)))
print(result)       # [4, 16, 36]
```

### 5.11 Ro'yxat bilan ifodalar (List Comprehensions)

**Nazariy qism:**
List comprehension - bu ro'yxatni yaratishning qisqa va tushunarli usuli.

**Asosiy xususiyatlari:**

- Qisqa sintaksis
- Filter qo'shish mumkin
- Ichma-ich comprehension
- Generator expression ga o'xshash

**Amaliy misollar:**

```python
# 1. Oddiy comprehension
numbers = [x for x in range(10)]
squares = [x**2 for x in range(10)]

# 2. Shartli comprehension
evens = [x for x in range(10) if x % 2 == 0]
odds = [x for x in range(10) if x % 2 == 1]

# 3. Ichma-ich comprehension
matrix = [[i+j for j in range(3)] for i in range(3)]
print(matrix)  # [[0,1,2], [1,2,3], [2,3,4]]

# 4. Murakkab misollar
words = ['hello', 'world', 'python']
lengths = [len(word) for word in words]

# Dictionary dan ro'yxat
dict1 = {'a': 1, 'b': 2, 'c': 3}
keys = [k for k in dict1.keys()]
values = [v for v in dict1.values()]

# 5. If-else bilan
numbers = [1, 2, 3, 4, 5]
result = ['juft' if x % 2 == 0 else 'toq' for x in numbers]
```

### 5.12 zip() funksiyasi

**Nazariy qism:**
zip() funksiyasi bir nechta iterablelarni parallel ravishda birlashtiradi.

**Asosiy xususiyatlari:**

- Parallel iteratsiya
- Eng qisqa iterable bo'yicha to'xtash
- Yangi zip ob'ekt qaytarish
- Reversible

**Amaliy misollar:**

```python
# 1. Oddiy zip
names = ['Ali', 'Vali', 'Gani']
ages = [20, 25, 30]
zipped = list(zip(names, ages))
print(zipped)  # [('Ali', 20), ('Vali', 25), ('Gani', 30)]

# 2. Unzip (zip ni qaytarish)
names, ages = zip(*zipped)
print(names)  # ('Ali', 'Vali', 'Gani')
print(ages)   # (20, 25, 30)

# 3. Dictionary yaratish
keys = ['a', 'b', 'c']
values = [1, 2, 3]
my_dict = dict(zip(keys, values))
print(my_dict)  # {'a': 1, 'b': 2, 'c': 3}

# 4. Ko'p ro'yxatlar bilan
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
list3 = [True, False, True]
result = list(zip(list1, list2, list3))
print(result)  # [(1, 'a', True), (2, 'b', False), (3, 'c', True)]
```

### 5.13 Stack (To'plam)

**Nazariy qism:**
Stack - LIFO (Last In First Out) prinsipi asosida ishlaydigan ma'lumot tuzilmasi.

**Asosiy operatsiyalar:**

- push - element qo'shish
- pop - element olish
- peek - oxirgi elementni ko'rish
- is_empty - bo'shligini tekshirish

**Amaliy misollar:**

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if not self.is_empty():
            return self.items.pop()

    def peek(self):
        if not self.is_empty():
            return self.items[-1]

    def is_empty(self):
        return len(self.items) == 0

    def size(self):
        return len(self.items)

# Ishlatish
stack = Stack()
stack.push(1)
stack.push(2)
stack.push(3)

print(stack.pop())   # 3
print(stack.peek())  # 2
print(stack.size())  # 2

# Stack qo'llanishi
def is_balanced(text):
    stack = []
    brackets = {')': '(', '}': '{', ']': '['}

    for char in text:
        if char in '({[':
            stack.append(char)
        elif char in ')}]':
            if not stack or stack.pop() != brackets[char]:
                return False

    return len(stack) == 0
```

### 5.14 Queue (Navbat)

**Nazariy qism:**
Queue - FIFO (First In First Out) prinsipi asosida ishlaydigan ma'lumot tuzilmasi.

**Asosiy xususiyatlari:**

- enqueue - element qo'shish
- dequeue - element olish
- front - birinchi elementni ko'rish
- rear - oxirgi elementni ko'rish

**Amaliy misollar:**

```python
from collections import deque

# 1. Oddiy queue
queue = deque()
queue.append(1)      # enqueue
queue.append(2)
queue.append(3)

print(queue.popleft())  # dequeue: 1
print(queue.popleft())  # 2

# 2. Priority Queue
import heapq

class PriorityQueue:
    def __init__(self):
        self.items = []

    def enqueue(self, item, priority):
        heapq.heappush(self.items, (priority, item))

    def dequeue(self):
        return heapq.heappop(self.items)[1] if self.items else None

# 3. Circular Queue
class CircularQueue:
    def __init__(self, size):
        self.size = size
        self.queue = [None] * size
        self.front = self.rear = -1

    def enqueue(self, data):
        if (self.rear + 1) % self.size == self.front:
            print("Queue is full")
        elif self.front == -1:
            self.front = self.rear = 0
            self.queue[self.rear] = data
        else:
            self.rear = (self.rear + 1) % self.size
            self.queue[self.rear] = data
```

### 5.15 Tuplar (Tuples)

**Nazariy qism:**
Tuple - o'zgarmas (immutable) va tartiblangan ma'lumot tuzilmasi.

**Asosiy xususiyatlari:**

- O'zgarmas (immutable)
- Indekslangan
- Ko'p ma'lumot turlarini saqlash
- Listdan tezroq

**Amaliy misollar:**

```python
# 1. Tuple yaratish
point = (10, 20)
coordinates = 10, 20  # qavssiz ham mumkin
single_element = (1,)  # bitta element uchun vergul zarur

# 2. Tuple metodlari
numbers = (1, 2, 2, 3, 4, 2)
print(numbers.count(2))    # 3
print(numbers.index(3))    # 3

# 3. Tuple qo'llanishi
def get_coordinates():
    return (10, 20)

x, y = get_coordinates()  # tuple unpacking

# 4. Named Tuples
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(11, 22)
print(p.x, p.y)      # 11 22

# 5. Tuple vs List
# Tuple listdan xotira kam ishlatadi
import sys
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
print(sys.getsizeof(my_list))    # ko'proq
print(sys.getsizeof(my_tuple))   # kamroq
```

### 5.16 O'zgaruvchilarni almashtirish (Swapping Variables)

**Nazariy qism:**
Python o'zgaruvchilarni almashtirish uchun qulay sintaksisga ega.

**Amaliy misollar:**

```python
# 1. Oddiy almashtirish
a, b = 10, 20
a, b = b, a
print(a, b)  # 20 10

# 2. Ko'p o'zgaruvchilarni almashtirish
x, y, z = 1, 2, 3
x, y, z = z, x, y
print(x, y, z)  # 3 1 2

# 3. List elementlarini almashtirish
lst = [1, 2, 3, 4]
lst[0], lst[-1] = lst[-1], lst[0]
print(lst)  # [4, 2, 3, 1]

# 4. Dictionary qiymatlarini almashtirish
dict1 = {'a': 1, 'b': 2}
dict1['a'], dict1['b'] = dict1['b'], dict1['a']
print(dict1)  # {'a': 2, 'b': 1}

# 5. Without temporary variable
x = 5
y = 10
x = x + y
y = x - y
x = x - y
print(x, y)  # 10 5
```

### 5.17 Massivlar (Arrays)

**Nazariy qism:**
Massivlar bir xil turdagi elementlarni saqlash uchun ishlatiladi. Python da array moduli va NumPy massivlari mavjud.

**Amaliy misollar:**

```python
# 1. Array moduli
from array import array
numbers = array('i', [1, 2, 3, 4, 5])  # i - int

# 2. NumPy arrays
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
print(arr * 2)  # [2 4 6 8 10]

# 3. Multi-dimensional arrays
matrix = np.array([[1, 2, 3],
                  [4, 5, 6],
                  [7, 8, 9]])

# 4. Array operations
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
print(arr1 + arr2)  # [5 7 9]
print(arr1 * arr2)  # [4 10 18]

# 5. Array slicing
arr = np.array([1, 2, 3, 4, 5])
print(arr[1:4])  # [2 3 4]
```

### 5.18 To'plamlar (Sets)

**Nazariy qism:**
Set - bu takrorlanmaydigan va tartiblanmagan ma'lumot tuzilmasi. Asosan elementlarni tekshirish va matematik amallar uchun ishlatiladi.

**Amaliy misollar:**

```python
# 1. Set yaratish
numbers = {1, 2, 3, 4, 5}
fruits = set(['apple', 'banana', 'cherry'])

# 2. Set amallari
set1 = {1, 2, 3}
set2 = {3, 4, 5}
print(set1.union(set2))         # {1, 2, 3, 4, 5}
print(set1.intersection(set2))   # {3}
print(set1.difference(set2))     # {1, 2}
print(set1.symmetric_difference(set2))  # {1, 2, 4, 5}

# 3. Element qo'shish/o'chirish
numbers.add(6)
numbers.remove(1)    # element bo'lmasa xato
numbers.discard(2)   # element bo'lmasa xato bermaydi

# 4. Set comprehension
squares = {x**2 for x in range(5)}
print(squares)  # {0, 1, 4, 9, 16}

# 5. Frozen sets
frozen = frozenset([1, 2, 3])  # o'zgarmas set
```

### 5.19 Lug'atlar (Dictionaries)

**Nazariy qism:**
Dictionary - kalit-qiymat juftliklarini saqlash uchun ishlatiladigan ma'lumot tuzilmasi.

**Amaliy misollar:**

```python
# 1. Dictionary yaratish
person = {
    'name': 'John',
    'age': 30,
    'city': 'New York'
}

# 2. Element qo'shish/o'zgartirish
person['email'] = 'john@example.com'
person['age'] = 31

# 3. Dictionary metodlari
print(person.keys())     # kalitlar
print(person.values())   # qiymatlar
print(person.items())    # juftliklar

# 4. Get metodi
email = person.get('email', 'not found')
phone = person.get('phone', 'not available')

# 5. Dictionary comprehension
squares = {x: x**2 for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# 6. Nested dictionaries
users = {
    'user1': {
        'name': 'John',
        'age': 30
    },
    'user2': {
        'name': 'Jane',
        'age': 25
    }
}
```

### 5.20 Lug'at bilan ifodalar (Dictionary Comprehensions)

**Nazariy qism:**
Dictionary comprehension - lug'atlarni qisqa va aniq yaratish usuli.

**Amaliy misollar:**

```python
# 1. Oddiy dictionary comprehension
numbers = {x: x**2 for x in range(5)}

# 2. Shartli dictionary comprehension
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}

# 3. Ikki ro'yxatdan dictionary
names = ['John', 'Jane', 'Bob']
ages = [30, 25, 35]
people = {name: age for name, age in zip(names, ages)}

# 4. Dictionary transformatsiyasi
original = {'a': 1, 'b': 2, 'c': 3}
squared = {k: v**2 for k, v in original.items()}

# 5. Murakkab misollar
weather = {'Monday': 25, 'Tuesday': 27, 'Wednesday': 23}
status = {day: 'Hot' if temp > 25 else 'Normal'
         for day, temp in weather.items()}
```

### 5.21 Generator ifodalari (Generator Expressions)

**Nazariy qism:**
Generator expressions - xotirada kam joy egallagan holda iterator yaratish usuli.

**Amaliy misollar:**

```python
# 1. Generator expression yaratish
numbers = (x**2 for x in range(1000000))
print(next(numbers))  # 0
print(next(numbers))  # 1

# 2. Generator vs List comprehension
# Generator (xotirada kam joy)
gen = (x for x in range(10))
# List (ko'p joy)
lst = [x for x in range(10)]

# 3. Generator bilan ishlash
sum_squares = sum(x**2 for x in range(10))
print(sum_squares)

# 4. Generator funksiyalar
def fibonacci_gen():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci_gen()
for _ in range(5):
    print(next(fib))  # 0, 1, 1, 2, 3
```

### 5.22 Bo'shatish operatori (Unpacking Operator)

**Nazariy qism:**
Bo'shatish operatori (*) iterablelardagi elementlarni bo'shatish uchun ishlatiladi.

**Amaliy misollar:**

```python
# 1. Ro'yxatni bo'shatish
numbers = [1, 2, 3]
print(*numbers)  # 1 2 3

# 2. Funksiya argumentlari
def sum_three(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
print(sum_three(*numbers))  # 6

# 3. Ro'yxatlarni birlashtirish
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = [*list1, *list2]
print(combined)  # [1, 2, 3, 4, 5, 6]

# 4. Dictionary bo'shatish (**)
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'd': 4}
combined = {**dict1, **dict2}
print(combined)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```

### 5.23 Ma'lumot tuzilmalari xulosa

**Asosiy tushunchalar:**

1. List - o'zgaruvchan, tartiblangan kolleksiya
2. Tuple - o'zgarmas, tartiblangan kolleksiya
3. Set - takrorlanmaydigan elementlar to'plami
4. Dictionary - kalit-qiymat juftliklari
5. Array - bir turdagi elementlar to'plami

**Qachon qaysi tuzilmani ishlatish kerak:**

- List: Elementlar tartibi muhim bo'lganda, elementlar takrorlanishi mumkin bo'lganda
- Tuple: O'zgarmas ma'lumotlar uchun, funksiya qaytarish qiymatlari uchun
- Set: Takrorlanmasligi kerak bo'lgan elementlar uchun, tez qidiruv kerak bo'lganda
- Dictionary: Kalit orqali qiymatga tez kirish kerak bo'lganda
- Array: Katta hajmdagi bir turdagi ma'lumotlar uchun

**Samaradorlik taqqoslash:**

```python
import time

# List vs Set qidiruv tezligi
large_list = list(range(1000000))
large_set = set(range(1000000))

# List qidiruv
start = time.time()
999999 in large_list
print(f"List search: {time.time() - start}")

# Set qidiruv
start = time.time()
999999 in large_set
print(f"Set search: {time.time() - start}")
```
