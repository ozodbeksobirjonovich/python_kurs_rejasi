### 9.1 Python standart kutubxonasi haqida

**Nazariy qism:**
Python standart kutubxonasi - bu Python bilan birga keladigan va keng qamrovli vazifalarni bajaruvchi modullar to'plami.

**Asosiy kategoriyalar:**

1. Built-in Functions va Types
2. Text Processing Services
3. Data Types
4. Numeric and Mathematical Modules
5. File and Directory Access
6. Data Persistence
7. Generic Operating System Services

**Amaliy misollar:**

```python
# 1. Built-in funksiyalar
numbers = [1, -2, 3, -4, 5]
print(abs(-5))         # 5
print(sum(numbers))    # 3
print(max(numbers))    # 5
print(min(numbers))    # -4

# 2. Math moduli
import math

print(math.pi)         # 3.141592653589793
print(math.sqrt(16))   # 4.0
print(math.floor(3.7)) # 3
print(math.ceil(3.2))  # 4

# 3. Statistics moduli
import statistics

data = [2, 2, 3, 4, 4, 4, 5]
print(statistics.mean(data))   # O'rtacha: 3.428...
print(statistics.median(data)) # Mediana: 4
print(statistics.mode(data))   # Moda: 4

# 4. Collections moduli
from collections import Counter, defaultdict, namedtuple

# Counter ishlatish
text = "hello world"
counts = Counter(text)
print(counts)  # Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})

# defaultdict ishlatish
d = defaultdict(list)
d['a'].append(1)  # KeyError bo'lmaydi
print(d)  # defaultdict(<class 'list'>, {'a': [1]})

# namedtuple ishlatish
Point = namedtuple('Point', ['x', 'y'])
p = Point(11, 22)
print(p.x, p.y)  # 11 22
```

### 9.2 Fayl yo'llari bilan ishlash (Paths)

**Nazariy qism:**
Python da fayl yo'llari bilan ishlash uchun ikki asosiy modul mavjud:

1. os.path - an'anaviy modul
2. pathlib - zamonaviy, obyektga yo'naltirilgan yondashuv

**Amaliy misollar:**

```python
# 1. os.path bilan ishlash
import os.path

# Yo'l yaratish
path = os.path.join('folder', 'subfolder', 'file.txt')
print(path)  # folder/subfolder/file.txt

# Yo'l komponentlarini olish
print(os.path.dirname(path))   # folder/subfolder
print(os.path.basename(path))  # file.txt
print(os.path.splitext(path))  # ('folder/subfolder/file', '.txt')

# 2. pathlib bilan ishlash
from pathlib import Path

# Yo'l yaratish
path = Path('folder') / 'subfolder' / 'file.txt'
print(path)  # folder/subfolder/file.txt

# Yo'l komponetlari
print(path.parent)     # folder/subfolder
print(path.name)       # file.txt
print(path.suffix)     # .txt
print(path.stem)       # file

# 3. Yo'llar bilan ishlash
file_path = Path('example/data.txt')

# Absolyut yo'l
print(file_path.absolute())

# Yo'l mavjudligini tekshirish
print(file_path.exists())

# Yo'l turi
print(file_path.is_file())
print(file_path.is_dir())
```

### 9.3 Kataloglar bilan ishlash (Directories)

**Nazariy qism:**
Python da kataloglar bilan ishlash uchun os va pathlib modullari ishlatiladi. Ular kataloglarni yaratish, o'chirish va ular ustida turli amallarni bajarish imkonini beradi.

**Amaliy misollar:**

```python
import os
from pathlib import Path

# 1. os moduli bilan
# Katalog yaratish
os.makedirs('data/subfolder', exist_ok=True)

# Katalogdagi fayllarni ko'rish
for item in os.listdir('data'):
    print(item)

# Katalogni o'chirish
os.rmdir('empty_folder')  # Bo'sh katalog uchun
import shutil
shutil.rmtree('data')     # Rekursiv o'chirish

# 2. pathlib bilan
# Katalog yaratish
folder = Path('new_folder')
folder.mkdir(parents=True, exist_ok=True)

# Katalogdagi fayllarni ko'rish
for item in folder.iterdir():
    if item.is_file():
        print(f"File: {item.name}")
    elif item.is_dir():
        print(f"Directory: {item.name}")

# Fayllarni filter qilish
python_files = list(folder.glob('*.py'))
all_files = list(folder.rglob('*'))  # Rekursiv qidirish

# 3. Katalog operatsiyalari
work_dir = Path('project')
work_dir.mkdir()

# Ichki kataloglar
(work_dir / 'src').mkdir()
(work_dir / 'tests').mkdir()

# Fayllar yaratish
(work_dir / 'README.md').touch()
(work_dir / 'src' / 'main.py').touch()
```

### 9.4 Fayllar bilan ishlash (Files)

**Nazariy qism:**
Python da fayllar bilan ishlash uchun built-in open() funksiyasi va with kontekst menejeri ishlatiladi.

**Amaliy misollar:**

```python
# 1. Fayl yaratish va yozish
with open('data.txt', 'w', encoding='utf-8') as file:
    file.write('Hello\\n')
    file.write('World\\n')

# 2. Fayl o'qish
# Butun faylni o'qish
with open('data.txt', 'r', encoding='utf-8') as file:
    content = file.read()
    print(content)

# Qatorma-qator o'qish
with open('data.txt', 'r', encoding='utf-8') as file:
    for line in file:
        print(line.strip())

# 3. Binary fayllar bilan ishlash
with open('image.jpg', 'rb') as file:
    binary_data = file.read()

# 4. Fayl pozitsiyasi bilan ishlash
with open('data.txt', 'r') as file:
    file.seek(5)    # 5-pozitsiyaga o'tish
    print(file.tell())  # Joriy pozitsiya
    data = file.read(10)  # 10 bayt o'qish

# 5. Xavfsiz fayl operatsiyalari
def safe_write(filename, content):
    """Xavfsiz fayl yozish"""
    temp_file = filename + '.tmp'
    try:
        with open(temp_file, 'w') as file:
            file.write(content)
        os.replace(temp_file, filename)
    except Exception as e:
        if os.path.exists(temp_file):
            os.remove(temp_file)
        raise e
```

### 9.5 Zip fayllar bilan ishlash

**Nazariy qism:**
zipfile moduli ZIP arxivlari bilan ishlash uchun to'liq funksionallikni taqdim etadi.

**Amaliy misollar:**

```python
import zipfile
from pathlib import Path

# 1. ZIP arxiv yaratish
def create_zip(zip_name, files):
    with zipfile.ZipFile(zip_name, 'w', zipfile.ZIP_DEFLATED) as zipf:
        for file in files:
            zipf.write(file)

# 2. ZIP arxivdan o'qish
def read_zip(zip_name):
    with zipfile.ZipFile(zip_name, 'r') as zipf:
        # Arxiv tarkibini ko'rish
        print(zipf.namelist())

        # Ma'lum bir faylni o'qish
        with zipf.open('example.txt') as f:
            content = f.read().decode('utf-8')
            print(content)

# 3. ZIP arxivga papka qo'shish
def zip_directory(zip_name, directory):
    with zipfile.ZipFile(zip_name, 'w') as zipf:
        for file_path in Path(directory).rglob('*'):
            if file_path.is_file():
                arcname = file_path.relative_to(directory)
                zipf.write(file_path, arcname)

# 4. ZIP arxivni parolga olish
def create_encrypted_zip(zip_name, files, password):
    with zipfile.ZipFile(zip_name, 'w', zipfile.ZIP_DEFLATED) as zipf:
        for file in files:
            zipf.write(file, pwd=password.encode())

# Ishlatish
files_to_zip = ['file1.txt', 'file2.txt']
create_zip('archive.zip', files_to_zip)
zip_directory('project.zip', 'project_folder')
```

### 9.6 CSV fayllar bilan ishlash

**Nazariy qism:**
csv moduli CSV (Comma-Separated Values) formatidagi fayllar bilan ishlash uchun qulay interfeys taqdim etadi.

**Amaliy misollar:**

```python
import csv
from collections import namedtuple

# 1. CSV faylga yozish
def write_csv_file():
    data = [
        ['Ism', 'Yosh', 'Shahar'],
        ['Ali', 25, 'Toshkent'],
        ['Vali', 30, 'Samarqand']
    ]

    with open('users.csv', 'w', newline='') as file:
        writer = csv.writer(file)
        writer.writerows(data)

# 2. CSV faylni o'qish
def read_csv_file():
    with open('users.csv', 'r') as file:
        reader = csv.reader(file)
        headers = next(reader)  # Sarlavhalarni o'qish

        for row in reader:
            print(f"{row[0]} - {row[1]} yosh, {row[2]}dan")

# 3. DictReader va DictWriter ishlatish
def work_with_dict_csv():
    # Yozish
    users = [
        {'name': 'Ali', 'age': 25, 'city': 'Toshkent'},
        {'name': 'Vali', 'age': 30, 'city': 'Samarqand'}
    ]

    with open('users_dict.csv', 'w', newline='') as file:
        fieldnames = ['name', 'age', 'city']
        writer = csv.DictWriter(file, fieldnames=fieldnames)

        writer.writeheader()
        writer.writerows(users)

    # O'qish
    with open('users_dict.csv', 'r') as file:
        reader = csv.DictReader(file)
        for row in reader:
            print(f"{row['name']} - {row['age']} yosh")

# 4. namedtuple bilan ishlash
def use_namedtuple_csv():
    User = namedtuple('User', ['name', 'age', 'city'])
    users = []

    with open('users.csv', 'r') as file:
        reader = csv.reader(file)
        next(reader)  # Sarlavhalarni o'tkazib yuborish

        for row in reader:
            user = User(row[0], int(row[1]), row[2])
            users.append(user)

    return users

# 5. CSV faylni filtrlash
def filter_csv(min_age):
    with open('users.csv', 'r') as file:
        reader = csv.DictReader(file)
        filtered = [row for row in reader if int(row['age']) >= min_age]

    return filtered
```

### 9.7 JSON fayllar bilan ishlash

**Nazariy qism:**
json moduli JSON (JavaScript Object Notation) formatidagi ma'lumotlar bilan ishlash uchun metodlarni taqdim etadi.

**Amaliy misollar:**

```python
import json
from pathlib import Path

# 1. JSON ga yozish
def write_json_data():
    data = {
        'name': 'Ali',
        'age': 25,
        'cities': ['Toshkent', 'Samarqand'],
        'married': False,
        'children': None
    }

    with open('data.json', 'w', encoding='utf-8') as f:
        json.dump(data, f, indent=4, ensure_ascii=False)

# 2. JSON dan o'qish
def read_json_data():
    with open('data.json', 'r', encoding='utf-8') as f:
        data = json.load(f)
        return data

# 3. Custom objects bilan ishlash
class User:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def to_json(self):
        return {
            'name': self.name,
            'age': self.age
        }

def user_to_json(obj):
    if isinstance(obj, User):
        return obj.to_json()
    raise TypeError(f'Object {obj} is not JSON serializable')

# 4. JSON validation
def validate_json_schema(data, required_fields):
    return all(field in data for field in required_fields)

# 5. JSON fayllarni birlashtirish
def merge_json_files(file_list):
    result = []
    for file_path in file_list:
        with open(file_path, 'r') as f:
            data = json.load(f)
            result.extend(data if isinstance(data, list) else [data])
    return result
```

### 9.8 SQLite ma'lumotlar bazasi bilan ishlash

**Nazariy qism:**
sqlite3 moduli SQLite ma'lumotlar bazasi bilan ishlash uchun interfeys taqdim etadi. SQLite - yengil, faylga asoslangan ma'lumotlar bazasi.

**Amaliy misollar:**

```python
import sqlite3
from contextlib import contextmanager

# 1. Ma'lumotlar bazasi menejeri
@contextmanager
def database_connection(db_name):
    conn = sqlite3.connect(db_name)
    try:
        yield conn
    finally:
        conn.close()

# 2. Jadval yaratish va ma'lumot qo'shish
def create_users_table():
    with database_connection('users.db') as conn:
        cursor = conn.cursor()

        # Jadval yaratish
        cursor.execute('''
            CREATE TABLE IF NOT EXISTS users (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                name TEXT NOT NULL,
                age INTEGER,
                email TEXT UNIQUE
            )
        ''')

        # Ma'lumot qo'shish
        users = [
            ('Ali', 25, 'ali@example.com'),
            ('Vali', 30, 'vali@example.com')
        ]
        cursor.executemany(
            'INSERT INTO users (name, age, email) VALUES (?, ?, ?)',
            users
        )
        conn.commit()

# 3. Ma'lumotlarni o'qish
def get_users(min_age=0):
    with database_connection('users.db') as conn:
        cursor = conn.cursor()
        cursor.execute('SELECT * FROM users WHERE age >= ?', (min_age,))
        return cursor.fetchall()

# 4. Ma'lumotlarni yangilash
def update_user_email(user_id, new_email):
    with database_connection('users.db') as conn:
        cursor = conn.cursor()
        cursor.execute(
            'UPDATE users SET email = ? WHERE id = ?',
            (new_email, user_id)
        )
        conn.commit()

# 5. Xavfsiz tranzaksiyalar
def transfer_money(from_id, to_id, amount):
    with database_connection('bank.db') as conn:
        try:
            cursor = conn.cursor()

            # Balansni tekshirish
            cursor.execute('SELECT balance FROM accounts WHERE id = ?', (from_id,))
            balance = cursor.fetchone()[0]

            if balance < amount:
                raise ValueError("Insufficient funds")

            # Pul o'tkazish
            cursor.execute('''
                UPDATE accounts
                SET balance = balance - ?
                WHERE id = ?''', (amount, from_id))

            cursor.execute('''
                UPDATE accounts
                SET balance = balance + ?
                WHERE id = ?''', (amount, to_id))

            conn.commit()
        except:
            conn.rollback()
            raise
```

### 9.9 Vaqt belgilari bilan ishlash (Timestamps)

**Nazariy qism:**
time moduli vaqt bilan ishlash uchun past darajadagi funksiyalarni taqdim etadi. Asosan Unix timestamp va vaqt o'lchash uchun ishlatiladi.

**Amaliy misollar:**

```python
import time

# 1. Vaqtni o'lchash
def measure_time(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Bajarilish vaqti: {end_time - start_time:.4f} sekund")
        return result
    return wrapper

@measure_time
def complex_operation():
    time.sleep(2)  # 2 sekund kutish
    return "Tugadi"

# 2. Time formatting
def time_examples():
    current = time.time()  # Unix timestamp

    # Local time
    local_time = time.localtime(current)
    formatted = time.strftime("%Y-%m-%d %H:%M:%S", local_time)
    print(f"Lokal vaqt: {formatted}")

    # UTC time
    utc_time = time.gmtime(current)
    utc_formatted = time.strftime("%Y-%m-%d %H:%M:%S", utc_time)
    print(f"UTC vaqt: {utc_formatted}")

# 3. Performance o'lchash
def performance_timer():
    start = time.perf_counter()  # Aniq o'lchash uchun
    # Operatsiyalar
    end = time.perf_counter()
    return end - start

# 4. Rate limiting
class RateLimiter:
    def __init__(self, calls_limit, time_period):
        self.calls_limit = calls_limit
        self.time_period = time_period
        self.calls = []

    def can_make_call(self):
        current_time = time.time()
        # Eski qo'ng'iroqlarni o'chirish
        self.calls = [call for call in self.calls
                     if current_time - call < self.time_period]

        if len(self.calls) < self.calls_limit:
            self.calls.append(current_time)
            return True
        return False
```

### 9.10 Sana va vaqt bilan ishlash (DateTimes)

**Nazariy qism:**
datetime moduli sana va vaqt bilan ishlash uchun yuqori darajadagi funksionallikni taqdim etadi.

**Amaliy misollar:**

```python
from datetime import datetime, date, time, timedelta
import pytz  # Time zones uchun

# 1. Datetime yaratish va formatlash
def datetime_examples():
    # Joriy vaqt
    now = datetime.now()
    print(f"Hozir: {now}")

    # Ma'lum bir vaqt
    specific = datetime(2024, 1, 1, 12, 0)
    print(f"Yangi yil: {specific}")

    # Formatting
    formatted = now.strftime("%Y-%m-%d %H:%M:%S")
    print(f"Formatlangan: {formatted}")

    # Parsing
    date_str = "2024-01-01 12:00:00"
    parsed = datetime.strptime(date_str, "%Y-%m-%d %H:%M:%S")
    print(f"Parse qilingan: {parsed}")

# 2. Timezone bilan ishlash
def timezone_examples():
    # Timezone yaratish
    tz_tashkent = pytz.timezone('Asia/Tashkent')
    tz_nyc = pytz.timezone('America/New_York')

    # Lokal vaqtni timezone bilan
    local_time = datetime.now(tz_tashkent)
    print(f"Toshkent vaqti: {local_time}")

    # Vaqtni boshqa timezonega o'tkazish
    nyc_time = local_time.astimezone(tz_nyc)
    print(f"Nyu-York vaqti: {nyc_time}")

# 3. Vaqt oralig'i bilan ishlash
def date_calculations():
    today = date.today()

    # 30 kun qo'shish
    future = today + timedelta(days=30)
    print(f"30 kundan keyin: {future}")

    # Ikki sana orasidagi farq
    date1 = date(2024, 1, 1)
    date2 = date(2024, 12, 31)
    difference = date2 - date1
    print(f"Kunlar farqi: {difference.days}")

# 4. Vaqt solishtirish
def is_working_hours(dt=None):
    if dt is None:
        dt = datetime.now()

    # Ish vaqti 9:00 dan 18:00 gacha
    return (
        dt.weekday() < 5 and  # Du-Ju
        time(9, 0) <= dt.time() <= time(18, 0)
    )
```

### 9.11 Vaqt farqlari bilan ishlash (Time Deltas)

**Nazariy qism:**
timedelta klassi vaqt oralig'i (farqi) bilan ishlash uchun qulay interfeys taqdim etadi.

**Amaliy misollar:**

```python
from datetime import datetime, timedelta

# 1. Timedelta yaratish va qo'llash
def timedelta_examples():
    now = datetime.now()

    # Vaqt qo'shish
    tomorrow = now + timedelta(days=1)
    next_week = now + timedelta(weeks=1)
    next_hour = now + timedelta(hours=1)

    # Vaqt ayirish
    yesterday = now - timedelta(days=1)
    last_week = now - timedelta(weeks=1)

    # Timedelta properties
    delta = timedelta(days=1, hours=12)
    print(f"Jami soatlar: {delta.total_seconds() / 3600}")

# 2. Vaqt oralig'ini hisoblash
def calculate_age(birthdate):
    today = date.today()
    age = today.year - birthdate.year

    # Tug'ilgan kun bu yil o'tdimi tekshirish
    if today < date(today.year, birthdate.month, birthdate.day):
        age -= 1

    return age

# 3. Vaqt intervallari bilan ishlash
class TimeInterval:
    def __init__(self, start, end):
        self.start = start
        self.end = end

    def duration(self):
        return self.end - self.start

    def overlaps(self, other):
        return (self.start < other.end and
                other.start < self.end)

    def merge(self, other):
        if not self.overlaps(other):
            raise ValueError("Intervals don't overlap")

        return TimeInterval(
            min(self.start, other.start),
            max(self.end, other.end)
        )

# 4. Deadline checker
class DeadlineChecker:
    def __init__(self, deadline):
        self.deadline = deadline

    def time_remaining(self):
        now = datetime.now()
        if now > self.deadline:
            return timedelta(0)
        return self.deadline - now

    def is_overdue(self):
        return datetime.now() > self.deadline

    def status(self):
        remaining = self.time_remaining()
        if remaining == timedelta(0):
            return "Muddati o'tgan"

        days = remaining.days
        hours = remaining.seconds // 3600

        if days > 0:
            return f"{days} kun qoldi"
        return f"{hours} soat qoldi"

```

### 9.12 Tasodifiy qiymatlarni yaratish (Random)

**Nazariy qism:**
random moduli tasodifiy sonlar va elementlarni generatsiya qilish uchun ishlatiladi. Kriptografik xavfsizlik uchun secrets moduli tavsiya etiladi.

**Amaliy misollar:**

```python
import random
import secrets
import string

# 1. Tasodifiy sonlar
def random_number_examples():
    # Butun sonlar
    print(random.randint(1, 10))      # 1 dan 10 gacha
    print(random.randrange(0, 101, 2)) # Juft sonlar 0-100

    # O'nlik sonlar
    print(random.random())      # 0.0 dan 1.0 gacha
    print(random.uniform(1, 10)) # 1.0 dan 10.0 gacha

# 2. Tasodifiy tanlash
def random_choice_examples():
    items = ['olma', 'banan', 'apelsin', 'uzum']

    # Bitta element
    print(random.choice(items))

    # Bir nechta element
    print(random.choices(items, k=2))  # Takrorlanishi mumkin
    print(random.sample(items, k=2))   # Takrorlanmaydi

    # Ro'yxatni aralashtirish
    random.shuffle(items)

# 3. Xavfsiz tasodifiy qiymatlar
def generate_secure_token(length=32):
    """Xavfsiz token yaratish"""
    return secrets.token_hex(length)

def generate_password(length=12):
    """Xavfsiz parol yaratish"""
    characters = string.ascii_letters + string.digits + string.punctuation
    return ''.join(secrets.choice(characters) for _ in range(length))

# 4. Vazn bilan tanlash
def weighted_choice_examples():
    items = ['A', 'B', 'C']
    weights = [10, 5, 1]  # A ko'proq tanlanadi

    results = random.choices(
        items,
        weights=weights,
        k=1000
    )
    print(f"A tanlandi: {results.count('A')} marta")

# 5. Random sinf yaratish
class RandomSequence:
    def __init__(self, start, end, count):
        self.numbers = []
        while len(self.numbers) < count:
            num = random.randint(start, end)
            if num not in self.numbers:
                self.numbers.append(num)

    def get_numbers(self):
        return self.numbers
```

### 9.13 Brauzerni ochish (webbrowser)

**Nazariy qism:**
webbrowser moduli tizimning standart brauzerini boshqarish imkonini beradi.

**Amaliy misollar:**

```python
import webbrowser
from urllib.parse import urlencode

# 1. URL ochish
def open_url_examples():
    # Oddiy URL ochish
    webbrowser.open('<https://www.google.com>')

    # Yangi oynada ochish
    webbrowser.open_new('<https://www.python.org>')

    # Yangi tabda ochish
    webbrowser.open_new_tab('<https://docs.python.org>')

# 2. Qidiruv URL yaratish
def search_web(query, engine='google'):
    base_urls = {
        'google': '<https://www.google.com/search?'>,
        'bing': '<https://www.bing.com/search?'>,
        'duckduckgo': '<https://duckduckgo.com/?'>
    }

    params = {'q': query}
    url = base_urls.get(engine, base_urls['google']) + urlencode(params)
    webbrowser.open(url)

# 3. Brauzer tanlov
def set_browser_examples():
    # Ma'lum brauzerda ochish
    chrome = webbrowser.get('chrome')
    chrome.open('<https://www.python.org>')

    firefox = webbrowser.get('firefox')
    firefox.open('<https://www.python.org>')

# 4. URL validatsiya
def validate_and_open_url(url):
    """URL ni tekshirib ochish"""
    from urllib.parse import urlparse

    try:
        result = urlparse(url)
        if all([result.scheme, result.netloc]):
            webbrowser.open(url)
            return True
        return False
    except Exception as e:
        print(f"Noto'g'ri URL: {e}")
        return False
```

### 9.14 Elektron pochta yuborish (SMTP)

**Nazariy qism:**
smtplib moduli SMTP protokoli orqali elektron pochta yuborish imkonini beradi.

**Amaliy misollar:**

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.application import MIMEApplication
import os

# 1. Oddiy xat yuborish
def send_simple_email(to_email, subject, body, smtp_config):
    msg = MIMEText(body)
    msg['Subject'] = subject
    msg['From'] = smtp_config['from_email']
    msg['To'] = to_email

    with smtplib.SMTP(smtp_config['server'], smtp_config['port']) as server:
        server.starttls()
        server.login(smtp_config['username'], smtp_config['password'])
        server.send_message(msg)

# 2. HTML formatdagi xat
def send_html_email(to_email, subject, html_content, smtp_config):
    msg = MIMEMultipart('alternative')
    msg['Subject'] = subject
    msg['From'] = smtp_config['from_email']
    msg['To'] = to_email

    html_part = MIMEText(html_content, 'html')
    msg.attach(html_part)

    with smtplib.SMTP(smtp_config['server'], smtp_config['port']) as server:
        server.starttls()
        server.login(smtp_config['username'], smtp_config['password'])
        server.send_message(msg)

# 3. Fayl bilan xat yuborish
def send_email_with_attachment(to_email, subject, body, file_path, smtp_config):
    msg = MIMEMultipart()
    msg['Subject'] = subject
    msg['From'] = smtp_config['from_email']
    msg['To'] = to_email

    # Matn qo'shish
    msg.attach(MIMEText(body))

    # Fayl qo'shish
    with open(file_path, 'rb') as f:
        attachment = MIMEApplication(f.read())
        attachment.add_header(
            'Content-Disposition',
            'attachment',
            filename=os.path.basename(file_path)
        )
        msg.attach(attachment)

    with smtplib.SMTP(smtp_config['server'], smtp_config['port']) as server:
        server.starttls()
        server.login(smtp_config['username'], smtp_config['password'])
        server.send_message(msg)
```

### 9.15 Shablonlar (Templates)

**Nazariy qism:**
string.Template va jinja2 modullari matn shablonlari bilan ishlash uchun ishlatiladi.

**Amaliy misollar:**

```python
from string import Template
from jinja2 import Template as Jinja2Template

# 1. String Template
def string_template_examples():
    # Oddiy shablon
    template = Template("Salom, $name!")
    result = template.substitute(name="John")
    print(result)

    # Dictionary bilan
    template = Template("$name $age yoshda")
    data = {'name': 'John', 'age': 30}
    print(template.substitute(data))

# 2. Jinja2 Template
def jinja2_template_examples():
    # Oddiy shablon
    template = Jinja2Template("""
    Salom, {{ name }}!
    {% if age >= 18 %}
    Siz voyaga yetgansiz.
    {% else %}
    Siz hali voyaga yetmagansiz.
    {% endif %}
    """)

    result = template.render(name="John", age=20)
    print(result)

# 3. HTML shablon
def html_template():
    template = Jinja2Template("""
    <!DOCTYPE html>
    <html>
    <head>
        <title>{{ title }}</title>
    </head>
    <body>
        <h1>{{ heading }}</h1>
        <ul>
        {% for item in items %}
            <li>{{ item }}</li>
        {% endfor %}
        </ul>
    </body>
    </html>
    """)

    data = {
        'title': 'My Page',
        'heading': 'Items List',
        'items': ['Item 1', 'Item 2', 'Item 3']
    }

    return template.render(**data)
```

### 9.16 Buyruq-qator argumentlari (argparse)

**Nazariy qism:**
argparse moduli buyruq qatori argumentlarini qayta ishlash uchun kuchli va moslashuvchan vositani taqdim etadi.

**Amaliy misollar:**

```python
import argparse

# 1. Oddiy argument parser
def basic_argument_parser():
    parser = argparse.ArgumentParser(
        description='Fayl konvertatsiya dasturi'
    )

    # Majburiy argument
    parser.add_argument(
        'input_file',
        help='Kirish fayli'
    )

    # Ixtiyoriy argument
    parser.add_argument(
        '-o', '--output',
        help='Chiqish fayli'
    )

    # Flag argument
    parser.add_argument(
        '-v', '--verbose',
        action='store_true',
        help='Batafsil ma\\'lumot ko\\'rsatish'
    )

    return parser.parse_args()

# 2. Murakkab argument parser
def advanced_argument_parser():
    parser = argparse.ArgumentParser(
        description='Ma\\'lumotlar bazasi boshqaruv dasturi'
    )

    # Sub-commands
    subparsers = parser.add_subparsers(
        dest='command',
        help='Mavjud buyruqlar'
    )

    # Create command
    create_parser = subparsers.add_parser(
        'create',
        help='Yangi yozuv yaratish'
    )
    create_parser.add_argument(
        'name',
        help='Yozuv nomi'
    )

    # List command
    list_parser = subparsers.add_parser(
        'list',
        help='Yozuvlarni ko\\'rsatish'
    )
    list_parser.add_argument(
        '--sort',
        choices=['name', 'date'],
        help='Saralash turi'
    )

    return parser.parse_args()

# 3. Custom action
class ValidateFileAction(argparse.Action):
    def __call__(self, parser, namespace, values, option_string=None):
        if not values.endswith('.txt'):
            parser.error('Fayl .txt formatida bo\\'lishi kerak')
        setattr(namespace, self.dest, values)

def file_argument_parser():
    parser = argparse.ArgumentParser()
    parser.add_argument(
        'file',
        action=ValidateFileAction,
        help='TXT fayl'
    )
    return parser.parse_args()

# Ishlatish
if __name__ == '__main__':
    args = advanced_argument_parser()

    if args.command == 'create':
        print(f"Creating: {args.name}")
    elif args.command == 'list':
        print(f"Listing (sort: {args.sort})")
```

### 9.17 Tashqi dasturlarni bajarish (subprocess)

**Nazariy qism:**
subprocess moduli tashqi dasturlarni boshqarish, ular bilan muloqot qilish va natijalarini olish imkonini beradi.

**Amaliy misollar:**

```python
import subprocess
import os
import sys

# 1. Oddiy buyruq bajarish
def run_simple_command():
    # Shell=False xavfsizroq
    result = subprocess.run(
        ['ls', '-l'],
        capture_output=True,
        text=True
    )
    print(result.stdout)

# 2. Pipe bilan ishlash
def pipe_commands():
    # grep orqali qidirish
    ps = subprocess.Popen(
        ['ps', 'aux'],
        stdout=subprocess.PIPE,
        text=True
    )

    grep = subprocess.Popen(
        ['grep', 'python'],
        stdin=ps.stdout,
        stdout=subprocess.PIPE,
        text=True
    )

    ps.stdout.close()
    output = grep.communicate()[0]
    print(output)

# 3. Interactive jarayon
def interactive_process():
    process = subprocess.Popen(
        ['python', '-i'],
        stdin=subprocess.PIPE,
        stdout=subprocess.PIPE,
        stderr=subprocess.PIPE,
        text=True
    )

    # Python interpretatoriga buyruq yuborish
    stdout, stderr = process.communicate('print("Hello!")\\n')
    print(stdout)

# 4. Xavfsiz jarayon boshqaruvi
class ProcessManager:
    def __init__(self, command):
        self.command = command
        self.process = None

    def start(self):
        try:
            self.process = subprocess.Popen(
                self.command,
                stdout=subprocess.PIPE,
                stderr=subprocess.PIPE
            )
        except subprocess.SubprocessError as e:
            print(f"Jarayon boshlanmadi: {e}")
            return False
        return True

    def stop(self):
        if self.process:
            self.process.terminate()
            try:
                self.process.wait(timeout=5)
            except subprocess.TimeoutExpired:
                self.process.kill()
            self.process = None
```

### 9.18 Python Standart kutubxonasi - yaxshi amaliyotlar

**Nazariy qism:**
Standart kutubxonadan samarali foydalanish uchun quyidagi tamoyillarga amal qilish kerak:

1. Xavfsizlik
2. Xatoliklarni to'g'ri boshqarish
3. Resurslardan optimal foydalanish
4. Ko'd qayta ishlatilishi

**Amaliy misollar:**

```python
# 1. Context manager bilan ishlash
def safe_file_operations():
    """Xavfsiz fayl operatsiyalari"""
    from contextlib import contextmanager

    @contextmanager
    def atomic_write(filepath):
        temp_path = filepath + '.tmp'
        try:
            with open(temp_path, 'w') as f:
                yield f
            os.replace(temp_path, filepath)
        except Exception:
            if os.path.exists(temp_path):
                os.remove(temp_path)
            raise

# 2. Logging tizimi
def setup_logging():
    """Logging tizimini sozlash"""
    import logging

    logging.basicConfig(
        level=logging.INFO,
        format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
        handlers=[
            logging.FileHandler('app.log'),
            logging.StreamHandler()
        ]
    )

    logger = logging.getLogger(__name__)
    return logger

# 3. Cache decorator
def cache_decorator(func):
    """Natijalarni keshlaydigan decorator"""
    from functools import wraps
    cache = {}

    @wraps(func)
    def wrapper(*args, **kwargs):
        key = str(args) + str(kwargs)
        if key not in cache:
            cache[key] = func(*args, **kwargs)
        return cache[key]

    return wrapper

# 4. ConfigParser
def config_management():
    """Konfiguratsiya fayli bilan ishlash"""
    from configparser import ConfigParser

    config = ConfigParser()

    # Default konfiguratsiya
    config['DEFAULT'] = {
        'host': 'localhost',
        'port': '8080',
        'debug': 'true'
    }

    # Faylga saqlash
    with open('config.ini', 'w') as f:
        config.write(f)

    # Fayldan o'qish
    config.read('config.ini')
    return dict(config['DEFAULT'])

# 5. Error handling utilities
class AppError(Exception):
    """Custom xatolik klassi"""
    pass

def safe_operation(func):
    """Xatoliklarni boshqaruvchi decorator"""
    @wraps(func)
    def wrapper(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except Exception as e:
            logger = logging.getLogger(__name__)
            logger.error(f"Error in {func.__name__}: {str(e)}")
            raise AppError(f"Operation failed: {str(e)}")
    return wrapper
```

Bu Python standart kutubxonasi bo'limini yakunlaydi. Asosiy mavzular:

1. Built-in funksiyalar va modullar
2. Fayllar bilan ishlash
3. Ma'lumotlar bazasi
4. Vaqt bilan ishlash
5. Xavfsizlik va konfiguratsiya
