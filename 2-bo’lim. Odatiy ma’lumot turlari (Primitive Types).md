### 2.1 O'zgaruvchilar (Variables)

**Nazariy qism:**
O'zgaruvchilar - bu kompyuter xotirasida ma'lumotlarni saqlash uchun ishlatiladigan konteynerlar. Python dinamik tipli til bo'lgani uchun, o'zgaruvchilar turini oldindan e'lon qilish shart emas.

**Asosiy xususiyatlari:**

- Dinamik tiplash
- Avtomatik xotira boshqaruvi
- Case-sensitive (katta-kichik harflarni farqlash)
- Kalit so'zlardan foydalanib bo'lmaydi

**Amaliy misollar:**

```python
# 1. Oddiy o'zgaruvchilar
ism = "Abror"
yosh = 25
vazn = 70.5
faol = True

# 2. Bir nechta o'zgaruvchilarga qiymat berish
x, y, z = 1, 2, 3

# 3. O'zgaruvchi turini tekshirish
print(type(ism))    # <class 'str'>
print(type(yosh))   # <class 'int'>
print(type(vazn))   # <class 'float'>
print(type(faol))   # <class 'bool'>

# 4. O'zgaruvchilar bilan amallar
a = 10
b = 20
natija = a + b
print(f"{a} + {b} = {natija}")  # 10 + 20 = 30
```

### 2.2 O'zgaruvchi nomlari (Variable Names)

**Nazariy qism:**
O'zgaruvchi nomlari dastur kodining o'qilishi va tushunarli bo'lishida muhim rol o'ynaydi.

**Asosiy qoidalar:**

1. Faqat harflar, raqamlar va pastki chiziq (_)
2. Raqam bilan boshlanmaydi
3. Kalit so'zlar (if, for, while...) ishlatilmaydi
4. Case-sensitive (katta-kichik harf farqlanadi)

**Amaliy misollar:**

```python
# 1. To'g'ri nomlash
user_name = "John"
age_of_user = 25
totalSum = 100
MAX_VALUE = 1000  # konstantalar uchun

# 2. Noto'g'ri nomlash
# 1user = "John"      # Raqam bilan boshlanishi mumkin emas
# my-name = "John"    # Chiziqcha ishlatish mumkin emas
# class = "Math"      # Kalit so'z ishlatish mumkin emas

# 3. Nom uzunligi va mazmunliligi
x = 1000  # yaxshi emas
student_total_score = 1000  # yaxshi

# 4. Snake case vs Camel case
first_name = "John"  # Snake case (tavsiya etiladi)
firstName = "John"   # Camel case
```

### 2.3 Satrlar (Strings)

**Nazariy qism:**
Satrlar - bu matnli ma'lumotlarni saqlash uchun ishlatiladigan ma'lumot turi. Python da satrlar o'zgarmas (immutable) hisoblanadi.

**Asosiy xususiyatlari:**

- Bir qatorli va ko'p qatorli
- Indekslanishi mumkin
- Kesib olish (slicing) imkoniyati
- Concatenation (+) operatori
- Takrorlash (*) operatori

**Amaliy misollar:**

```python
# 1. Satr yaratish usullari
s1 = 'Birinchi satr'
s2 = "Ikkinchi satr"
s3 = '''Ko'p
qatorli
satr'''

# 2. Indekslash va kesish
matn = "Python"
print(matn[0])     # P
print(matn[-1])    # n
print(matn[0:2])   # Py
print(matn[2:])    # thon
print(matn[::-1])  # nohtyP

# 3. Satrlarni birlashtirish
ism = "John"
familiya = "Doe"
to_liq_ism = ism + " " + familiya
print(to_liq_ism)  # John Doe

# 4. Satrni takrorlash
belgi = "-"
chiziq = belgi * 10
print(chiziq)  # ----------
```

### 2.4 Qochish ketma-ketliklari (Escape Sequences)

**Nazariy qism:**
Qochish ketma-ketliklari - bu maxsus belgilarni satrlarda ifodalash uchun ishlatiladigan maxsus belgilar kombinatsiyasi.

**Asosiy qochish ketma-ketliklari:**

- \n - yangi qator
- \t - tabulyatsiya
- \\ - teskari chiziq
- \' - bir tirnoq
- \" - qo'sh tirnoq
- \r - carriage return
- \b - backspace

**Amaliy misollar:**

```python
# 1. Yangi qator va tabulyatsiya
print("Birinchi qator\nIkkinchi qator")
print("Ism:\tJohn\nYosh:\t25")

# 2. Tirnoqlardan foydalanish
print('I\'m a programmer')
print("\"Python\" - zo'r dasturlash tili")

# 3. Maxsus belgilar
print("C:\\Users\\Documents")
print("Narx: 1000\rYangi")  # Yangi000

# 4. Raw string
print(r"C:\\Users\\Documents")  # Qochish ketma-ketliklarini e'tiborsiz qoldiradi

# 5. Ko'p qatorli formatli matn
query = """
SELECT *
    FROM users
    WHERE age > 18
    ORDER BY name;
"""
```

### 2.5 Formatlangan satrlar (Formatted Strings)

**Nazariy qism:**
Formatlangan satrlar (f-strings) - Python 3.6+ dan boshlab kiritilgan, satrlarni formatlashning eng qulay va o'qilishi oson usuli.

**Formatlash usullari:**

1. f-string (f"{var}")
2. .format() metodi
3. % operatori
4. Template strings

**Amaliy misollar:**

```python
# 1. f-string
ism = "John"
yosh = 25
print(f"Salom, mening ismim {ism} va men {yosh} yoshdaman")

# 2. Sonlarni formatlash
son = 3.14159
print(f"Pi soni: {son:.2f}")  # 3.14
narx = 1234567
print(f"Narx: {narx:,}")  # 1,234,567

# 3. .format() metodi
print("Salom, {}, sizning yoshingiz {}".format(ism, yosh))
print("Koordinatalar: {x}, {y}".format(x=10, y=20))

# 4. % operatori
print("Salom, %s, sizning yoshingiz %d" % (ism, yosh))

# 5. Template strings
from string import Template
shablon = Template("Salom, $ism!")
print(shablon.substitute(ism="John"))

```

### 2.6 Satrlarga oid metodlar (String Methods)

**Nazariy qism:**
Python satrlari uchun ko'plab foydali metodlar mavjud. Bu metodlar satrlar bilan ishlashni osonlashtiradi.

**Asosiy metodlar kategoriyalari:**

1. Konvertatsiya metodlari (upper, lower, title)
2. Qidiruv metodlari (find, index, count)
3. Tekshirish metodlari (startswith, endswith, isdigit)
4. O'zgartirish metodlari (replace, strip, split)

**Amaliy misollar:**

```python
# 1. Konvertatsiya metodlari
text = "python programming"
print(text.upper())      # PYTHON PROGRAMMING
print(text.title())      # Python Programming
print(text.capitalize()) # Python programming

# 2. Qidiruv metodlari
text = "Python is amazing, Python is great"
print(text.count("Python"))    # 2
print(text.find("amazing"))    # 10
print(text.index("is"))       # 7

# 3. Tekshirish metodlari
son = "12345"
matn = "Python"
print(son.isdigit())     # True
print(matn.isalpha())    # True
print(matn.startswith("Py")) # True

# 4. O'zgartirish metodlari
text = "   python   "
print(text.strip())           # "python"
print(text.replace("py", "MY")) # "   MYthon   "
print("1,2,3".split(","))     # ['1', '2', '3']
```

### 2.7 Raqamlar (Numbers)

**Nazariy qism:**
Python da 3 xil asosiy raqamli ma'lumot turlari mavjud:

1. int - butun sonlar
2. float - o'nlik sonlar
3. complex - kompleks sonlar

**Raqamlar bilan ishlash:**

- Asosiy matematik operatorlar
- Maxsus operatorlar (//, %, **)
- math moduli funksiyalari

**Amaliy misollar:**

```python
import math

# 1. Asosiy arifmetik amallar
a, b = 15, 4
print(f"Qo'shish: {a + b}")      # 19
print(f"Ayirish: {a - b}")       # 11
print(f"Ko'paytirish: {a * b}")  # 60
print(f"Bo'lish: {a / b}")       # 3.75
print(f"Butun bo'lish: {a // b}")# 3
print(f"Qoldiq: {a % b}")        # 3
print(f"Daraja: {a ** 2}")       # 225

# 2. Math moduli funksiyalari
x = 16
y = -3.14
print(f"Ildiz: {math.sqrt(x)}")        # 4.0
print(f"Absolut: {abs(y)}")            # 3.14
print(f"Yaxlitlash: {round(y, 1)}")    # -3.1
print(f"Pi soni: {math.pi}")           # 3.141592653589793

# 3. Complex sonlar
z1 = 2 + 3j
z2 = 1 - 2j
print(f"Kompleks sonlar yig'indisi: {z1 + z2}")
```

### 2.8 Raqamlar bilan ishlash (Working with Numbers)

**Nazariy qism:**
Raqamlar bilan ishlashda turli xil operatsiyalar va konversiyalardan foydalaniladi.

**Asosiy operatsiyalar:**

- Arifmetik amallar
- Taqqoslash operatorlari
- Tayinlash operatorlari
- Maxsus funksiyalar

**Amaliy misollar:**

```python
from decimal import Decimal
import math

# 1. Aniq hisob-kitoblar
print(0.1 + 0.2)                 # 0.30000000000000004
print(Decimal('0.1') + Decimal('0.2'))  # 0.3

# 2. Sonlarni yaxlitlash
x = 3.7
print(round(x))      # 4
print(math.floor(x)) # 3
print(math.ceil(x))  # 4

# 3. Random sonlar
import random
print(random.randint(1, 10))      # 1 dan 10 gacha
print(random.random())            # 0 dan 1 gacha
print(random.choice([1,2,3,4,5])) # Ro'yxatdan tasodifiy

# 4. Sonlar ustida amallar
x = 5
x += 3   # x = x + 3
x *= 2   # x = x * 2
print(x)  # 16
```

### 2.9 Turni o'zgartirish (Type Conversion)

**Nazariy qism:**
Python da turni o'zgartirish ikki xil bo'ladi:

1. Implicit (avtomatik) konversiya
2. Explicit (aniq) konversiya

**Asosiy konversiya funksiyalari:**

- int() - butun songa
- float() - o'nlik songa
- str() - satrga
- bool() - mantiqiy turga
- list(), tuple(), set() - to'plamlarga

**Amaliy misollar:**

```python
# 1. Asosiy konversiyalar
x = int("100")       # Satrdan butun songa
y = float("3.14")    # Satrdan o'nlik songa
z = str(123)         # Sondan satrga
b = bool(1)          # Sondan mantiqiy turga

# 2. Xavfli konversiyalar
try:
    x = int("abc")  # ValueError
except ValueError as e:
    print(f"Xato: {e}")

# 3. Mantiqiy konversiyalar
print(bool(""))      # False
print(bool("0"))     # True
print(bool([]))      # False
print(bool([0]))     # True

# 4. Ko'p bosqichli konversiyalar
x = 3.14
y = str(int(x))
print(y)  # "3"
```
