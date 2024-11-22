### 3.1 Taqqoslash operatorlari (Comparison Operators)

**Nazariy qism:**
Taqqoslash operatorlari qiymatlarni solishtirish va mantiqiy natija olish uchun ishlatiladi.

**Asosiy operatorlar:**

| Operator | Ma'nosi | Misol |
| --- | --- | --- |
| `==` | Tenglik | `5 == 5` → `True` |
| `!=` | Teng emaslik | `5 != 3` → `True` |
| `>` | Katta | `5 > 3` → `True` |
| `<` | Kichik | `3 < 5` → `True` |
| `>=` | Katta yoki teng | `5 >= 5` → `True` |
| `<=` | Kichik yoki teng | `3 <= 5` → `True` |

**Amaliy misollar:**

```python
# 1. Sonlarni solishtirish
x = 10
y = 20
print(f"{x} == {y}: {x == y}")  # False
print(f"{x} != {y}: {x != y}")  # True

# 2. Satrlarni solishtirish
ism1 = "Ali"
ism2 = "ali"
print(f"{ism1} == {ism2}: {ism1 == ism2}")  # False
print(f"{ism1.lower()} == {ism2.lower()}: {ism1.lower() == ism2.lower()}")  # True

# 3. Murakkab solishtirishlar
son = 15
print(f"{son} in range(10, 20): {son in range(10, 20)}")  # True
print(f"'a' in 'salom': {'a' in 'salom'}")  # True

# 4. Objektlarni solishtirish
list1 = [1, 2, 3]
list2 = [1, 2, 3]
print(f"list1 == list2: {list1 == list2}")  # True
print(f"list1 is list2: {list1 is list2}")  # False
```

### 3.2 Shartli ifodalar (Conditional Statements)

**Nazariy qism:**
Shartli ifodalar - dastur oqimini boshqarish uchun ishlatiladigan asosiy konstruksiyalar.

**Asosiy konstruksiyalar:**

- if
- elif
- else

**Amaliy misollar:**

```python
# 1. Oddiy if-else
yosh = int(input("Yoshingizni kiriting: "))

if yosh >= 18:
    print("Siz ovoz bera olasiz")
else:
    print("Siz hali ovoz bera olmaysiz")

# 2. if-elif-else zanjiri
baho = int(input("Bahoni kiriting (0-100): "))

if baho >= 90:
    natija = "A"
elif baho >= 80:
    natija = "B"
elif baho >= 70:
    natija = "C"
elif baho >= 60:
    natija = "D"
else:
    natija = "F"

print(f"Sizning bahoyingiz: {natija}")

# 3. Ichma-ich shartlar
login = input("Login: ")
parol = input("Parol: ")

if login == "admin":
    if parol == "12345":
        print("Tizimga xush kelibsiz, Admin!")
    else:
        print("Noto'g'ri parol")
else:
    print("Bunday foydalanuvchi mavjud emas")
```

### 3.3 Ternary operator

**Nazariy qism:**
Ternary operator - bu bir qatorli shartli ifoda bo'lib, if-else konstruksiyasining qisqa shakli.

**Sintaksis:**

```python
natija = agar_true if shart else agar_false

```

**Amaliy misollar:**

```python
# 1. Oddiy ternary operator
yosh = 20
status = "voyaga yetgan" if yosh >= 18 else "voyaga yetmagan"
print(status)  # voyaga yetgan

# 2. Funksiyalar bilan
def tekshir(son):
    return "juft" if son % 2 == 0 else "toq"

print(tekshir(4))  # juft
print(tekshir(7))  # toq

# 3. Murakkab ifodalar
x = 5
y = 10
katta = x if x > y else y
print(f"Katta son: {katta}")

# 4. Ichma-ich ternary
bal = 85
natija = "a'lo" if bal >= 90 else ("yaxshi" if bal >= 70 else "qoniqarli")
print(natija)  # yaxshi
```

### 3.4 Mantiqiy operatorlar (Logical Operators)

**Nazariy qism:**
Mantiqiy operatorlar bir nechta shartlarni birlashtirish uchun ishlatiladi.

**Asosiy operatorlar:**

- and - barcha shartlar true bo'lishi kerak
- or - kamida bitta shart true bo'lishi kerak
- not - shartni teskarisiga o'zgartiradi

**Amaliy misollar:**

```python
# 1. Asosiy mantiqiy operatorlar
yosh = 25
maosh = 5000000

if yosh >= 18 and maosh >= 3000000:
    print("Kredit olishingiz mumkin")

# 2. Murakkab shartlar
login = "admin"
parol = "12345"
active = True

if (login == "admin" and parol == "12345") and not active:
    print("Akkaunt bloklangan")
elif login == "admin" and parol == "12345":
    print("Xush kelibsiz")
else:
    print("Login yoki parol xato")

# 3. or operatori
ball = 85
sport = True

if ball >= 90 or sport:
    print("Siz stipendiya olasiz")

# 4. Murakkab mantiqiy ifodalar
son = 15
if son > 0 and son < 100 and son % 3 == 0:
    print(f"{son} - 0 dan 100 gacha bo'lgan 3 ga bo'linadigan son")
```

### 3.5 Qisqa tutashuvni baholash (Short-circuit Evaluation)

**Nazariy qism:**
Short-circuit evaluation - bu mantiqiy operatorlarning optimallashtirilgan baholanishi.

**Qoidalar:**

- and: Agar birinchi shart False bo'lsa, ikkinchisi tekshirilmaydi
- or: Agar birinchi shart True bo'lsa, ikkinchisi tekshirilmaydi

**Amaliy misollar:**

```python
# 1. and bilan short-circuit
def tekshir_parol():
    print("Parol tekshirilmoqda...")
    return False

def tekshir_login():
    print("Login tekshirilmoqda...")
    return True

print("Login va parol:", tekshir_login() and tekshir_parol())

# 2. or bilan short-circuit
x = 5
y = 0
natija = (x != 0) and (y/x > 0)  # 0 ga bo'lish xatosi yuz bermaydi

# 3. Xatolardan himoyalanish
royxat = []
if len(royxat) > 0 and royxat[0] == "start":
    print("Dastur boshlandi")

# 4. Cache bilan ishlash
cache = None
def qimmat_operatsiya():
    print("Qimmat operatsiya bajarilmoqda...")
    return "Natija"

natija = cache or qimmat_operatsiya()
```

### 3.6 Taqqoslash operatorlarini zanjirlash (Chaining Comparison Operators)

**Nazariy qism:**
Python taqqoslash operatorlarini zanjir shaklida yozish imkonini beradi, bu kodni qisqartiradi va o'qishni osonlashtiradi.

**Amaliy misollar:**

```python
# 1. Oddiy zanjirlash
yosh = 25
if 18 <= yosh <= 35:
    print("Siz yoshlar dasturiga to'g'ri kelasiz")

# 2. Ko'p qiymatli tekshirish
x = 10
if 0 <= x <= 100:
    print("Son 0 dan 100 gacha oraliqda")

# 3. Satrlar bilan ishlash
harf = 'K'
if 'A' <= harf <= 'Z':
    print("Katta harf")

# 4. Mantiqiy operatorlar bilan
bal = 85
if 0 <= bal <= 100 and bal >= 70:
    print("Siz o'tdingiz")
```

### 3.7 For tsikllari (For Loops)

**Nazariy qism:**
For tsikli ketma-ketliklar bo'ylab iteratsiya qilish uchun ishlatiladi.

**Asosiy xususiyatlari:**

- range() funksiyasi
- enumerate() funksiyasi
- zip() funksiyasi
- break va continue operatorlari

**Amaliy misollar:**

```python
# 1. Oddiy for tsikli
for i in range(5):
    print(f"Hisob: {i}")

# 2. enumerate bilan ishlash
mevalar = ["olma", "banan", "uzum"]
for index, meva in enumerate(mevalar, 1):
    print(f"{index}. {meva}")

# 3. Ikki ro'yxat bilan ishlash
ismlar = ["Ali", "Vali", "Gani"]
yoshlar = [20, 25, 30]
for ism, yosh in zip(ismlar, yoshlar):
    print(f"{ism}ning yoshi {yosh}da")

# 4. break va continue
for i in range(10):
    if i == 3:
        continue  # 3 ni o'tkazib yuborish
    if i == 7:
        break    # 7 da to'xtatish
    print(i)
```

### 3.8 For..Else

**Nazariy qism:**
For..else konstruksiyasi tsikl to'liq bajarilganda (break ishlatilmaganda) else qismini bajarish imkonini beradi.

**Amaliy misollar:**

```python
# 1. Tub sonni tekshirish
def tub_son(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            print(f"{n} soni {i} ga bo'linadi")
            break
    else:
        print(f"{n} - tub son")
        return True
    return False

# 2. Ro'yxatda element qidirish
sonlar = [1, 3, 5, 7, 9]
qidirilayotgan = 4

for son in sonlar:
    if son == qidirilayotgan:
        print("Son topildi!")
        break
else:
    print("Son topilmadi")

# 3. Parol tekshirish
parollar = ['123456', 'admin', 'qwerty']
yangi_parol = input("Yangi parol kiriting: ")

for parol in parollar:
    if yangi_parol == parol:
        print("Bu parol band!")
        break
else:
    print("Parol qabul qilindi")
```

### 3.9 Ichki tsikllar (Nested Loops)

**Nazariy qism:**
Ichki tsikllar - bu bir tsikl ichida boshqa tsiklning joylashishi. Ular murakkab strukturalar va algoritmlar yaratishda qo'llaniladi.

**Amaliy misollar:**

```python
# 1. Ko'paytirish jadvali
for i in range(1, 6):
    for j in range(1, 6):
        print(f"{i} * {j} = {i*j}\\t", end="")
    print()  # yangi qator

# 2. Matrix bilan ishlash
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for i in range(len(matrix)):
    for j in range(len(matrix[i])):
        print(f"{matrix[i][j]}", end=" ")
    print()

# 3. Pattern chizish
n = 5
for i in range(n):
    for j in range(i + 1):
        print("*", end=" ")
    print()

# 4. Takrorlanuvchi elementlarni topish
list1 = [1, 2, 3, 4]
list2 = [3, 4, 5, 6]
takrorlanuvchilar = []

for x in list1:
    for y in list2:
        if x == y:
            takrorlanuvchilar.append(x)
```

### 3.10 Iterable lar (Iterables)

**Nazariy qism:**
Iterable - bu element bo'ylab aylanish mumkin bo'lgan ob'ekt. Python da ko'p turdagi iterablelar mavjud.

**Asosiy iterable turlari:**

- List (ro'yxat)
- Tuple (kortej)
- Set (to'plam)
- Dictionary (lug'at)
- String (satr)
- Range

**Amaliy misollar:**

```python
# 1. Turli iterablelar bilan ishlash
# List
sonlar = [1, 2, 3]
for son in sonlar:
    print(son)

# String
matn = "Python"
for harf in matn:
    print(harf.upper())

# Dictionary
talaba = {
    'ism': 'Ali',
    'yosh': 20,
    'kurs': 2
}

for kalit, qiymat in talaba.items():
    print(f"{kalit}: {qiymat}")

# 2. Iterator yaratish
class CountDown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.start <= 0:
            raise StopIteration
        self.start -= 1
        return self.start + 1

# Ishlatish
countdown = CountDown(5)
for i in countdown:
    print(i)
```

### 3.11 While tsikllari (While Loops)

**Nazariy qism:**
While tsikli shart bajarilguncha kodning ma'lum bir qismini takrorlaydi.

**Amaliy misollar:**

```python
# 1. Oddiy while
i = 1
while i <= 5:
    print(i)
    i += 1

# 2. Break bilan while
parol = "1234"
urinishlar = 3

while urinishlar > 0:
    kiritilgan = input("Parolni kiriting: ")
    if kiritilgan == parol:
        print("To'g'ri!")
        break
    urinishlar -= 1
    print(f"Noto'g'ri. {urinishlar} ta urinish qoldi.")

# 3. Tasodifiy son topish o'yini
import random
tasodifiy = random.randint(1, 100)
topildi = False

while not topildi:
    taxmin = int(input("Sonni toping (1-100): "))
    if taxmin == tasodifiy:
        print("Topdingiz!")
        topildi = True
    elif taxmin < tasodifiy:
        print("Kattaroq son kiriting")
    else:
        print("Kichikroq son kiriting")
```

### 3.12 Cheksiz tsikllar (Infinite Loops)

**Nazariy qism:**
Cheksiz tsikl - bu to'xtatuvchi shart bo'lmagan yoki shart hech qachon bajarilmaydigan tsikl.

**Amaliy misollar:**

```python
# 1. Server simulyatsiyasi
import time

def server_loop():
    while True:
        command = input("Buyruqni kiriting (exit to'xtash uchun): ")
        if command.lower() == 'exit':
            print("Server to'xtatilmoqda...")
            break
        print(f"Buyruq bajarilmoqda: {command}")
        time.sleep(1)

# 2. Ma'lumotlarni monitoring qilish
from datetime import datetime

def monitor():
    while True:
        current_time = datetime.now()
        print(f"Joriy vaqt: {current_time}")
        # Har 5 sekundda yangilanadi
        time.sleep(5)

# 3. Event loop
def event_loop():
    events = []
    while True:
        if events:
            event = events.pop(0)
            process_event(event)
        else:
            print("Eventlar kutilmoqda...")
            time.sleep(1)
```
