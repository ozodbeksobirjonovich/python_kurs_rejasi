### 11.1 Kirish (Introduction)

**Nazariy qism:**
Python paketlari dasturlashni osonlashtirish, kod takrorlanishini kamaytirish va turli funksionallikni qo'shish uchun ishlatiladi.

**Asosiy mashhur paketlar:**

1. requests - HTTP so'rovlar uchun
2. beautifulsoup4 - web scraping uchun
3. pandas - data analiz uchun
4. numpy - ilmiy hisob-kitoblar uchun
5. pillow - rasmlar bilan ishlash uchun

### 11.2 API nima? (What are APIs)

**Nazariy qism:**
API (Application Programming Interface) - dasturlar o'rtasida ma'lumot almashish uchun interface.

**Asosiy tushunchalar:**

- Endpoint - API manzili
- Request methodlari (GET, POST, PUT, DELETE)
- Response kodlari (200, 404, 500...)
- JSON formati

**Amaliy misollar:**

```python
import requests

# 1. Oddiy API so'rov
response = requests.get('<https://api.github.com>')
print(f"Status: {response.status_code}")
print(f"Content: {response.json()}")

# 2. Headers bilan ishlash
headers = {
    'User-Agent': 'Python/1.0',
    'Accept': 'application/json'
}
response = requests.get('<https://api.github.com/users>', headers=headers)

# 3. Parametrlar bilan so'rov
params = {
    'page': 1,
    'per_page': 10
}
response = requests.get('<https://api.github.com/users>', params=params)
```

### 11.3 OpenWeatherMap API

**Nazariy qism:**
OpenWeatherMap API ob-havo ma'lumotlarini olish uchun keng qo'llaniladigan API.

**Amaliy misollar:**

```python
import requests
from datetime import datetime

class WeatherAPI:
    def __init__(self, api_key):
        self.api_key = api_key
        self.base_url = "<http://api.openweathermap.org/data/2.5>"

    def get_current_weather(self, city):
        """Joriy ob-havo ma'lumotlarini olish"""
        endpoint = f"{self.base_url}/weather"
        params = {
            'q': city,
            'appid': self.api_key,
            'units': 'metric'  # Celsius
        }

        response = requests.get(endpoint, params=params)
        return response.json()

    def get_forecast(self, city):
        """5 kunlik prognoz olish"""
        endpoint = f"{self.base_url}/forecast"
        params = {
            'q': city,
            'appid': self.api_key,
            'units': 'metric'
        }

        response = requests.get(endpoint, params=params)
        return response.json()

# Ishlatish
weather = WeatherAPI('YOUR_API_KEY')
tashkent_weather = weather.get_current_weather('Tashkent')

print(f"""
Shahar: {tashkent_weather['name']}
Harorat: {tashkent_weather['main']['temp']}°C
Namlik: {tashkent_weather['main']['humidity']}%
Holat: {tashkent_weather['weather'][0]['description']}
""")
```

### 11.4 Ob-havo ma'lumotlarini olish (Weather Data)

**Nazariy qism:**
API orqali olingan ma'lumotlarni qayta ishlash va saqlash.

**Amaliy misollar:**

```python
import json
from datetime import datetime

class WeatherData:
    def __init__(self, api_key):
        self.api = WeatherAPI(api_key)

    def get_city_weather(self, city):
        """Shahar ob-havosini olish va formatlash"""
        try:
            data = self.api.get_current_weather(city)
            return {
                'city': data['name'],
                'temperature': round(data['main']['temp']),
                'humidity': data['main']['humidity'],
                'description': data['weather'][0]['description'],
                'timestamp': datetime.now().isoformat()
            }
        except requests.RequestException as e:
            return {'error': str(e)}

    def save_weather_data(self, city, filename='weather_history.json'):
        """Ob-havo ma'lumotlarini faylga saqlash"""
        data = self.get_city_weather(city)

        try:
            with open(filename, 'r') as f:
                history = json.load(f)
        except FileNotFoundError:
            history = []

        history.append(data)

        with open(filename, 'w') as f:
            json.dump(history, f, indent=4)

        return data

# Ishlatish
weather_data = WeatherData('YOUR_API_KEY')
result = weather_data.save_weather_data('Tashkent')
print(json.dumps(result, indent=2))
```

### 11.5 API kalitlarini yashirish

**Nazariy qism:**
API kalitlari va boshqa muhim ma'lumotlarni xavfsiz saqlash va boshqarish usullari.

**Amaliy misollar:**

```python
# 1. Environment variables bilan ishlash
import os
from pathlib import Path
from dotenv import load_dotenv

class Config:
    """Configuration manager"""
    def __init__(self):
        # .env faylini yuklaymiz
        env_path = Path('.') / '.env'
        load_dotenv(dotenv_path=env_path)

    def get_api_key(self, key_name):
        """API kalitini olish"""
        api_key = os.getenv(key_name)
        if not api_key:
            raise ValueError(f"{key_name} topilmadi")
        return api_key

# 2. JSON config fayldan foydalanish
class JSONConfig:
    def __init__(self, config_file='config.json'):
        self.config_file = config_file
        self.config = self._load_config()

    def _load_config(self):
        """Config faylni yuklash"""
        try:
            with open(self.config_file) as f:
                return json.load(f)
        except FileNotFoundError:
            return {}

    def get_api_key(self, service_name):
        """Service uchun API kalitini olish"""
        try:
            return self.config['api_keys'][service_name]
        except KeyError:
            raise ValueError(f"{service_name} uchun API kalit topilmadi")

# 3. Xavfsiz config manager
from cryptography.fernet import Fernet

class SecureConfig:
    def __init__(self, key_file='secret.key'):
        self.key_file = key_file
        self.key = self._load_or_generate_key()
        self.fernet = Fernet(self.key)

    def _load_or_generate_key(self):
        """Kalitni yuklash yoki yaratish"""
        try:
            with open(self.key_file, 'rb') as f:
                return f.read()
        except FileNotFoundError:
            key = Fernet.generate_key()
            with open(self.key_file, 'wb') as f:
                f.write(key)
            return key

    def encrypt_and_save(self, data, filename='secure_config.enc'):
        """Ma'lumotlarni shifrlash va saqlash"""
        encrypted = self.fernet.encrypt(json.dumps(data).encode())
        with open(filename, 'wb') as f:
            f.write(encrypted)

    def load_and_decrypt(self, filename='secure_config.enc'):
        """Shifrlangan ma'lumotlarni yuklash"""
        with open(filename, 'rb') as f:
            encrypted = f.read()
        return json.loads(self.fernet.decrypt(encrypted))
```

### 11.6 Ma'lumot saqlash va tahlil (Data Storage and Analysis)

**Nazariy qism:**
Olingan ma'lumotlarni saqlash, tahlil qilish va vizualizatsiya qilish.

**Amaliy misollar:**

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datetime import datetime, timedelta

class WeatherAnalyzer:
    def __init__(self, data_file='weather_history.json'):
        self.data_file = data_file
        self.df = self._load_data()

    def _load_data(self):
        """JSON fayldan ma'lumotlarni DataFrame ga yuklash"""
        with open(self.data_file) as f:
            data = json.load(f)
        return pd.DataFrame(data)

    def get_temperature_stats(self):
        """Harorat statistikasi"""
        return {
            'mean': self.df['temperature'].mean(),
            'min': self.df['temperature'].min(),
            'max': self.df['temperature'].max()
        }

    def plot_temperature_trend(self):
        """Harorat o'zgarishini chizish"""
        plt.figure(figsize=(12, 6))
        sns.lineplot(data=self.df, x='timestamp', y='temperature')
        plt.title('Harorat o'zgarishi')
        plt.xticks(rotation=45)
        plt.tight_layout()
        return plt

    def generate_report(self, output_file='weather_report.html'):
        """HTML hisobot yaratish"""
        stats = self.get_temperature_stats()

        report = f"""
        <html>
        <head>
            <title>Ob-havo hisoboti</title>
            <style>
                body {{ font-family: Arial; padding: 20px; }}
                .stats {{ margin: 20px 0; }}
            </style>
        </head>
        <body>
            <h1>Ob-havo hisoboti</h1>
            <div class="stats">
                <h2>Statistika</h2>
                <p>O'rtacha harorat: {stats['mean']:.1f}°C</p>
                <p>Minimal harorat: {stats['min']}°C</p>
                <p>Maksimal harorat: {stats['max']}°C</p>
            </div>
            <div class="graph">
                <h2>Grafik</h2>
                <img src="temperature_trend.png">
            </div>
        </body>
        </html>
        """

        # Grafikni saqlash
        self.plot_temperature_trend()
        plt.savefig('temperature_trend.png')

        # Hisobotni saqlash
        with open(output_file, 'w') as f:
            f.write(report)

# Ishlatish
analyzer = WeatherAnalyzer()
analyzer.generate_report()
```

### 11.7 Web Scraping

**Nazariy qism:**
Web sahifalardan ma'lumotlarni avtomatik yig'ish uchun BeautifulSoup va requests kutubxonalaridan foydalanish.

**Amaliy misollar:**

```python
import requests
from bs4 import BeautifulSoup
import csv
from datetime import datetime

class WeatherScraper:
    def __init__(self):
        self.headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36'
        }

    def scrape_weather_news(self, url):
        """Ob-havo yangiliklar sahifasidan ma'lumot yig'ish"""
        try:
            response = requests.get(url, headers=self.headers)
            response.raise_for_status()

            soup = BeautifulSoup(response.text, 'html.parser')
            articles = soup.find_all('article', class_='weather-news')

            news = []
            for article in articles:
                news.append({
                    'title': article.find('h2').text.strip(),
                    'date': article.find('time').get('datetime'),
                    'summary': article.find('p').text.strip(),
                    'link': article.find('a')['href']
                })

            return news

        except requests.RequestException as e:
            print(f"Xatolik yuz berdi: {e}")
            return []

    def save_to_csv(self, news, filename='weather_news.csv'):
        """Ma'lumotlarni CSV faylga saqlash"""
        if not news:
            return

        with open(filename, 'w', newline='', encoding='utf-8') as f:
            writer = csv.DictWriter(f, fieldnames=news[0].keys())
            writer.writeheader()
            writer.writerows(news)

class WeatherDataCollector:
    def __init__(self):
        self.scraper = WeatherScraper()
        self.api = WeatherAPI('YOUR_API_KEY')

    def collect_all_data(self, city, news_url):
        """Barcha ma'lumotlarni yig'ish"""
        # API dan ob-havo ma'lumotlari
        weather_data = self.api.get_current_weather(city)

        # Web sahifadan yangiliklar
        news_data = self.scraper.scrape_weather_news(news_url)

        return {
            'weather': weather_data,
            'news': news_data,
            'collected_at': datetime.now().isoformat()
        }
```

### 11.8 Selenium bilan brauzer avtomatizatsiyasi

**Nazariy qism:**
Selenium web-sahifalar bilan interaktiv ishlash, formalarni to'ldirish va dinamik kontentni olish imkonini beradi.

**Amaliy misollar:**

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

class WeatherSiteAutomation:
    def __init__(self):
        # Chrome brauzerini headless rejimda ishga tushirish
        options = webdriver.ChromeOptions()
        options.add_argument('--headless')
        self.driver = webdriver.Chrome(options=options)

    def __enter__(self):
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self.driver.quit()

    def search_weather(self, city):
        """Ob-havo ma'lumotlarini qidirish"""
        try:
            # Sahifani ochish
            self.driver.get("<https://example-weather-site.com>")

            # Qidiruv maydoni
            search = WebDriverWait(self.driver, 10).until(
                EC.presence_of_element_located((By.ID, "search"))
            )
            search.send_keys(city)
            search.submit()

            # Natijani kutish
            result = WebDriverWait(self.driver, 10).until(
                EC.presence_of_element_located((By.CLASS_NAME, "weather-info"))
            )

            return {
                'temperature': result.find_element(By.CLASS_NAME, 'temp').text,
                'conditions': result.find_element(By.CLASS_NAME, 'conditions').text
            }

        except Exception as e:
            print(f"Xatolik: {e}")
            return None

    def take_screenshot(self, filename):
        """Sahifa screenshotini olish"""
        self.driver.save_screenshot(filename)

# Screenshot bilan ma'lumot yig'ish
def collect_weather_data(city):
    with WeatherSiteAutomation() as automation:
        data = automation.search_weather(city)
        if data:
            automation.take_screenshot(f"{city}_weather.png")
        return data
```

### 11.9 PDF bilan ishlash

**Nazariy qism:**
PyPDF2 va reportlab kutubxonalari PDF fayllarini yaratish, o'qish va tahrirlash imkonini beradi.

**Amaliy misollar:**

```python
from reportlab.lib import colors
from reportlab.lib.pagesizes import letter
from reportlab.platypus import SimpleDocTemplate, Table, TableStyle, Paragraph
from reportlab.lib.styles import getSampleStyleSheet
import PyPDF2

class WeatherReportGenerator:
    def __init__(self):
        self.styles = getSampleStyleSheet()

    def create_weather_report(self, data, filename="weather_report.pdf"):
        """PDF hisobot yaratish"""
        doc = SimpleDocTemplate(filename, pagesize=letter)
        elements = []

        # Sarlavha
        title = Paragraph(
            f"Ob-havo hisoboti - {data['city']}",
            self.styles['Heading1']
        )
        elements.append(title)

        # Ma'lumotlar jadvali
        table_data = [
            ['Parametr', 'Qiymat'],
            ['Harorat', f"{data['temperature']}°C"],
            ['Namlik', f"{data['humidity']}%"],
            ['Holat', data['description']]
        ]

        table = Table(table_data, colWidths=[200, 200])
        table.setStyle(TableStyle([
            ('BACKGROUND', (0, 0), (-1, 0), colors.grey),
            ('TEXTCOLOR', (0, 0), (-1, 0), colors.whitesmoke),
            ('ALIGN', (0, 0), (-1, -1), 'CENTER'),
            ('GRID', (0, 0), (-1, -1), 1, colors.black),
            ('FONTNAME', (0, 0), (-1, 0), 'Helvetica-Bold'),
            ('FONTSIZE', (0, 0), (-1, 0), 14),
            ('TOPPADDING', (0, 0), (-1, -1), 12),
            ('BOTTOMPADDING', (0, 0), (-1, -1), 12),
        ]))
        elements.append(table)

        # PDF yaratish
        doc.build(elements)

    def merge_reports(self, input_files, output_file):
        """Bir nechta PDF fayllarni birlashtirish"""
        merger = PyPDF2.PdfMerger()

        for file in input_files:
            merger.append(file)

        merger.write(output_file)
        merger.close()

    def extract_text(self, pdf_file):
        """PDF dan matnni ajratib olish"""
        with open(pdf_file, 'rb') as file:
            reader = PyPDF2.PdfReader(file)
            text = ""
            for page in reader.pages:
                text += page.extract_text()
        return text

# Ishlatish
generator = WeatherReportGenerator()

# Bitta shahar uchun hisobot
data = {
    'city': 'Tashkent',
    'temperature': 25,
    'humidity': 45,
    'description': 'Quyoshli'
}
generator.create_weather_report(data, "tashkent_weather.pdf")

# Bir nechta hisobotlarni birlashtirish
files = ['tashkent_weather.pdf', 'samarkand_weather.pdf']
generator.merge_reports(files, 'combined_report.pdf')
```

### 11.10 Excel bilan ishlash

**Nazariy qism:**
openpyxl kutubxonasi Excel fayllari bilan ishlash, ma'lumotlarni o'qish va yozish imkonini beradi.

**Amaliy misollar:**

```python
from openpyxl import Workbook, load_workbook
from openpyxl.styles import Font, PatternFill, Alignment
from openpyxl.utils import get_column_letter

class WeatherExcelReport:
    def __init__(self):
        self.wb = Workbook()
        self.ws = self.wb.active
        self.ws.title = "Ob-havo ma'lumotlari"
        self._setup_styles()

    def _setup_styles(self):
        """Excel jadval stillarini sozlash"""
        self.header_font = Font(bold=True, size=12, color="FFFFFF")
        self.header_fill = PatternFill("solid", fgColor="4F81BD")
        self.cell_alignment = Alignment(horizontal='center')

    def apply_header_style(self, cell):
        """Header stilini qo'llash"""
        cell.font = self.header_font
        cell.fill = self.header_fill
        cell.alignment = self.cell_alignment

    def create_report(self, weather_data, filename="weather_data.xlsx"):
        """Excel hisobot yaratish"""
        # Headers
        headers = ['Sana', 'Shahar', 'Harorat', 'Namlik', 'Holat']
        for col, header in enumerate(headers, 1):
            cell = self.ws.cell(row=1, column=col, value=header)
            self.apply_header_style(cell)

        # Data
        for row, data in enumerate(weather_data, 2):
            self.ws.cell(row=row, column=1, value=data['date'])
            self.ws.cell(row=row, column=2, value=data['city'])
            self.ws.cell(row=row, column=3, value=data['temperature'])
            self.ws.cell(row=row, column=4, value=data['humidity'])
            self.ws.cell(row=row, column=5, value=data['description'])

        # Adjust column widths
        for col in range(1, 6):
            self.ws.column_dimensions[get_column_letter(col)].width = 15

        # Add formulas
        last_row = len(weather_data) + 1
        self.ws.cell(row=last_row+1, column=3, value=f"=AVERAGE(C2:C{last_row})")

        self.wb.save(filename)

    @staticmethod
    def read_report(filename):
        """Excel fayldan ma'lumotlarni o'qish"""
        wb = load_workbook(filename)
        ws = wb.active

        data = []
        for row in ws.iter_rows(min_row=2, values_only=True):
            if not any(row):  # Empty row check
                break
            data.append({
                'date': row[0],
                'city': row[1],
                'temperature': row[2],
                'humidity': row[3],
                'description': row[4]
            })

        return data

# Ishlatish
report = WeatherExcelReport()

# Test data
weather_data = [
    {
        'date': '2024-01-01',
        'city': 'Tashkent',
        'temperature': 25,
        'humidity': 45,
        'description': 'Quyoshli'
    },
    {
        'date': '2024-01-01',
        'city': 'Samarkand',
        'temperature': 23,
        'humidity': 50,
        'description': 'Bulutli'
    }
]

# Hisobot yaratish
report.create_report(weather_data)

# Hisobotni o'qish
data = WeatherExcelReport.read_report("weather_data.xlsx")
print(data)
```

### 11.11 Command Query Separation Principle

**Nazariy qism:**
Command Query Separation (CQS) - metodlarni command (holatni o'zgartiruvchi) va query (ma'lumot qaytaruvchi) larga ajratish prinsipi.

**Amaliy misollar:**

```python
from dataclasses import dataclass
from datetime import datetime
from typing import List, Optional

@dataclass
class WeatherRecord:
    city: str
    temperature: float
    humidity: int
    recorded_at: datetime

class WeatherDatabase:
    """CQS prinsipi asosida yaratilgan ob-havo ma'lumotlar bazasi"""

    def __init__(self):
        self._records: List[WeatherRecord] = []

    # Command metodlari (holatni o'zgartiradi)
    def add_record(self, record: WeatherRecord) -> None:
        """Yangi yozuv qo'shish (command)"""
        self._records.append(record)

    def clear_records(self) -> None:
        """Barcha yozuvlarni o'chirish (command)"""
        self._records.clear()

    def remove_city_records(self, city: str) -> None:
        """Shahar yozuvlarini o'chirish (command)"""
        self._records = [r for r in self._records if r.city != city]

    # Query metodlari (faqat ma'lumot qaytaradi)
    def get_record_count(self) -> int:
        """Yozuvlar sonini qaytarish (query)"""
        return len(self._records)

    def get_city_records(self, city: str) -> List[WeatherRecord]:
        """Shahar yozuvlarini qaytarish (query)"""
        return [r for r in self._records if r.city == city]

    def get_latest_record(self, city: str) -> Optional[WeatherRecord]:
        """Eng so'nggi yozuvni qaytarish (query)"""
        city_records = self.get_city_records(city)
        return max(city_records, key=lambda r: r.recorded_at) if city_records else None

class WeatherService:
    """CQS prinsipi asosida yaratilgan ob-havo xizmati"""

    def __init__(self, api_key: str):
        self.api = WeatherAPI(api_key)
        self.db = WeatherDatabase()

    # Command metodlari
    def update_weather_data(self, city: str) -> None:
        """Ob-havo ma'lumotlarini yangilash (command)"""
        weather = self.api.get_current_weather(city)
        record = WeatherRecord(
            city=city,
            temperature=weather['main']['temp'],
            humidity=weather['main']['humidity'],
            recorded_at=datetime.now()
        )
        self.db.add_record(record)

    def clear_old_records(self, days: int) -> None:
        """Eski yozuvlarni o'chirish (command)"""
        cutoff = datetime.now() - timedelta(days=days)
        self._records = [r for r in self._records if r.recorded_at >= cutoff]

    # Query metodlari
    def get_average_temperature(self, city: str) -> float:
        """O'rtacha haroratni hisoblash (query)"""
        records = self.db.get_city_records(city)
        if not records:
            return 0.0
        return sum(r.temperature for r in records) / len(records)

    def get_temperature_range(self, city: str) -> tuple[float, float]:
        """Harorat oralig'ini qaytarish (query)"""
        records = self.db.get_city_records(city)
        if not records:
            return (0.0, 0.0)
        temps = [r.temperature for r in records]
        return (min(temps), max(temps))

# Ishlatish
service = WeatherService('YOUR_API_KEY')

# Commands (holatni o'zgartirish)
service.update_weather_data('Tashkent')
service.update_weather_data('Samarkand')

# Queries (ma'lumot olish)
avg_temp = service.get_average_temperature('Tashkent')
temp_range = service.get_temperature_range('Tashkent')
```

### 11.12 NumPy

**Nazariy qism:**
NumPy - Python'da raqamli hisob-kitoblar uchun asosiy kutubxona. U ko'p o'lchamli massivlar va matematik funksiyalar bilan ishlash imkonini beradi.

**Amaliy misollar:**

```python
import numpy as np

class WeatherDataAnalysis:
    """NumPy yordamida ob-havo ma'lumotlarini tahlil qilish"""

    def __init__(self, data: np.ndarray):
        """
        Data format:
        [temperature, humidity, pressure]
        """
        self.data = data

    def get_basic_stats(self):
        """Asosiy statistikani hisoblash"""
        return {
            'mean': np.mean(self.data, axis=0),
            'std': np.std(self.data, axis=0),
            'min': np.min(self.data, axis=0),
            'max': np.max(self.data, axis=0)
        }

    def calculate_correlations(self):
        """Korrelyatsiyani hisoblash"""
        return np.corrcoef(self.data.T)

    def find_anomalies(self, threshold=2):
        """Anomaliyalarni topish"""
        mean = np.mean(self.data, axis=0)
        std = np.std(self.data, axis=0)
        z_scores = np.abs((self.data - mean) / std)
        return np.where(z_scores > threshold)

    def smooth_data(self, window_size=3):
        """Ma'lumotlarni tekislash"""
        return np.array([
            np.convolve(self.data[:, i], np.ones(window_size)/window_size, mode='valid')
            for i in range(self.data.shape[1])
        ]).T

    def forecast_simple(self, steps=1):
        """Oddiy prognoz"""
        return np.mean(self.data[-3:], axis=0) + np.std(self.data[-3:], axis=0) * \\
               np.random.normal(0, 0.1, size=(steps, self.data.shape[1]))

# Ishlatish
# Test data: [temp, humidity, pressure]
data = np.array([
    [25, 60, 1013],
    [26, 58, 1012],
    [24, 65, 1014],
    [27, 55, 1011],
    [23, 70, 1015]
])

analysis = WeatherDataAnalysis(data)

# Asosiy statistika
stats = analysis.get_basic_stats()
print("O'rtacha:", stats['mean'])
print("Standart chetlanish:", stats['std'])

# Korrelyatsiya
corr = analysis.calculate_correlations()
print("\\nKorrelyatsiya matritsa:")
print(corr)

# Anomaliyalar
anomalies = analysis.find_anomalies()
print("\\nAnomaliyalar:", anomalies)

# Prognoz
forecast = analysis.forecast_simple(3)
print("\\nKeyingi 3 kun uchun prognoz:")
print(forecast)
```
