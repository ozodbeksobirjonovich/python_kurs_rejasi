- 1.1 Python nima?
    
    **Python** – bu yuqori darajadagi, talqin qiluvchi (interpreted), umumiy maqsadli dasturlash tili bo'lib, u dasturlash jarayonini soddalashtirishga qaratilgan.
    
    Pythonning asosiy xususiyatlari:
    
    - **O'qilishi oson**: Pythonning sintaksisi inson o'qishiga qulay bo'lib, dasturchilarga murakkab muammolarni oddiy va tushunarli tarzda yechishga imkon beradi.
    - **Keng kutubxonalar**: Python ko'plab standart kutubxonalar va uchinchi tomon paketlari (third party) ga ega.
    - **Platformadan mustaqil**: Python kodlari Windows, macOS, Linux va boshqa operatsion tizimlarda ishlashi mumkin.
    - **Ochiq manbaga ega**: Python bepul va ochiq manba dasturlash tili.
    - **Dynamic typing**: O'zgaruvchilar turini avtomatik aniqlash imkoniyati.
    - **Katta hamjamiyat**: Faol rivojlanuvchi va yordam beruvchi hamjamiyat.
    
    Qo'llanilish sohalari:
    
    - Veb dasturlash (Django, Flask)
    - Ma'lumotlar tahlili (Pandas, NumPy)
    - Sun'iy intellekt (TensorFlow, PyTorch)
    - Avtomatlashtirish
    - O'yinlar yaratish (Pygame)
    - Desktop ilovalar (PyQt, Tkinter)
    
    **Amaliy misollar:**
    
    ```python
    # 1. Oddiy matematik amallar
    print(2 + 2)  # 4
    print(10 / 3)  # 3.3333...
    print(2 ** 3)  # 8
    
    # 2. Matn bilan ishlash
    ism = "Python"
    print(f"Salom, {ism}!")  # Salom, Python!
    
    # 3. Ro'yxatlar bilan ishlash
    sonlar = [1, 2, 3, 4, 5]
    print(sum(sonlar))  # 15
    ```
    
- 1.2 Pythonni o'rnatish
    
    Pythonni o'rnatish jarayoni quyidagi bosqichlardan iborat:
    
    1. **Rasmiy web-saytdan yuklab olish**:
        - https://www.python.org/ saytiga kiring
        - "Downloads" bo'limini tanlang
        - Operatsion tizimingizga mos versiyani tanlang
    2. **O'rnatish jarayoni**:
        - Windows uchun:
            - "Add Python to PATH" variantini belgilang
            - "Install Now" tugmasini bosing
        - macOS uchun:
            - .pkg faylni yuklab oling va ishga tushiring
            - O'rnatish yo'riqnomasini bajaring
        - Linux uchun:
            
            ```bash
            sudo apt update
            sudo apt install python3
            ```
            
    3. **O'rnatishni tekshirish**:
    
    ```bash
    python --version
    # yoki
    python3 --version
    ```
    
    1. **Pip package manager ni tekshirish**:
    
    ```bash
    pip --version
    # yoki
    pip3 --version
    ```
    
    **Amaliy misollar:**
    
    ```python
    # Terminal yoki CMD da quyidagilarni bajaring:
    
    # 1. Python versiyasini tekshirish
    python --version
    
    # 2. Python interpreterini ishga tushirish
    python
    
    # 3. Pip orqali paket o'rnatish
    pip install requests
    
    # 4. O'rnatilgan paketlar ro'yxatini ko'rish
    pip list
    ```
    
- 1.3 Python interpreteri
    
    Python interpreteri - bu Python kodlarini qatorma-qator o'qiydigan va bajaradigan dastur.
    
    **Asosiy komponentlari:**
    
    - **Interpreter core** - asosiy bajaruvchi qism
    - **Memory manager** - xotira bilan ishlashni boshqaradi
    - **Compiler** - Python kodini bytecode ga o'giradi
    - **Standard Library** - asosiy kutubxonalar to'plami
    
    **Interpreter rejimlari:**
    
    1. **Interaktiv rejim**:
    
    ```python
    $ python
    >>> 2 + 2
    4
    >>> print("Salom")
    Salom
    >>> exit()  # chiqish uchun
    ```
    
    1. **Script rejim**:
    
    ```python
    # main.py
    print("Bu script rejim")
    x = 10
    y = 20
    print(f"Yig'indi: {x + y}")
    
    # Ishga tushirish:
    # python main.py
    ```
    
    1. **IDLE rejim**:
    - Python bilan birga keladigan oddiy IDE
    - Kod yozish va debug qilish imkoniyati
    - Syntax highlighting
    
    **Amaliy misollar:**
    
    ```python
    # 1. Interaktiv rejimda kalkulyator
    >>> 45 * 2
    90
    >>> 100 / 5
    20.0
    
    # 2. O'zgaruvchilar bilan ishlash
    >>> x = 10
    >>> y = 20
    >>> print(f"{x} + {y} = {x + y}")
    10 + 20 = 30
    
    # 3. Loop yaratish
    >>> for i in range(3):
    ...     print(f"Qator {i + 1}")
    Qator 1
    Qator 2
    Qator 3
    ```
    
- 1.4 Kod muharrirlari
    
    Zamonaviy Python dasturlash uchun kuchli IDE va kod muharrirlari mavjud.
    
    **Mashhur IDE lar:**
    
    1. **Visual Studio Code**:
        - Bepul va kengaytiriladigan
        - Python Extension
        - Debugging imkoniyati
        - Git integratsiyasi
    2. **PyCharm**:
        - Professional va Community versiyalari
        - Kuchli debugging
        - Database tools
        - Framework support
    3. **Sublime Text**:
        - Tez va yengil
        - Ko'p pluginlar
        - Split editing
    4. **Jupyter Notebook**:
        - Interaktiv dasturlash
        - Markdown support
        - Data visualization
    
    **Muhim IDE xususiyatlari:**
    
    - Syntax highlighting
    - Code completion
    - Error detection
    - Git integration
    - Debugging tools
    - Terminal integration
    
    **Amaliy misollar:**
    
    ```python
    # VS Code da yangi fayl yaratish va ishga tushirish
    # test.py
    def salomlash(ism):
        """Salomlashish funksiyasi"""
        return f"Salom, {ism}!"
    
    # Terminal integration
    # python test.py
    
    # Debugging
    def calculate_sum(n):
        total = 0
        for i in range(n):  # breakpoint qo'yish mumkin
            total += i
        return total
    
    # Git integration
    # git add .
    # git commit -m "Initial commit"
    ```
    
- 1.5 Birinchi Python dasturingiz
    
    Birinchi Python dasturini yaratish orqali asosiy tushunchalarni o'rganamiz.
    
    **Asosiy komponentlar:**
    
    1. Fayl yaratish (.py kengaytma)
    2. Kod yozish
    3. Saqlash
    4. Ishga tushirish
    5. Natijani tekshirish
    
    **Amaliy misollar:**
    
    ```python
    # 1. Hello World
    # hello.py
    print("Salom, Dunyo!")
    
    # 2. Foydalanuvchi kiritishi
    # input.py
    ism = input("Ismingizni kiriting: ")
    yosh = int(input("Yoshingizni kiriting: "))
    print(f"Salom {ism}, siz {yosh} yoshdasiz!")
    
    # 3. Kalkulyator
    # calc.py
    a = float(input("Birinchi sonni kiriting: "))
    b = float(input("Ikkinchi sonni kiriting: "))
    amal = input("Amalni kiriting (+,-,*,/): ")
    
    if amal == '+':
        natija = a + b
    elif amal == '-':
        natija = a - b
    elif amal == '*':
        natija = a * b
    elif amal == '/':
        natija = a / b if b != 0 else "0 ga bo'lib bo'lmaydi"
    else:
        natija = "Noto'g'ri amal"
    
    print(f"Natija: {natija}")
    ```
    
    **Dasturni ishga tushirish:**
    
    ```bash
    python hello.py
    python input.py
    python calc.py
    ```
    
- 1.6 Python kengaytmalari (Extensions)
    
    Python ekotizimini kengaytiruvchi va rivojlantiruvchi turli xil kengaytmalar mavjud.
    
    **Asosiy kengaytma turlari:**
    
    1. IDE kengaytmalari
    2. Linting tools
    3. Formatting tools
    4. Testing frameworks
    5. Documentation tools
    
    **Mashhur kengaytmalar:**
    
    - **VS Code uchun:**
        - Python
        - Pylance
        - Python Docstring Generator
        - Python Test Explorer
    - **PyCharm plugins:**
        - Python Security
        - Requirements
        - Python Enhancement Proposals
    
    **Amaliy misollar:**
    
    ```python
    # 1. Pylint bilan kod sifatini tekshirish
    # bad_code.py
    x=1
    y= 2
    if x==y:
        print('Equal')
    else:
        print('Not equal')
    
    # Pylint natijasi:
    # Missing docstring
    # Bad variable naming
    # Missing whitespace
    
    # 2. Black bilan formatlash
    # before_format.py
    def calculate(x,y):
        return{'sum':x+y,'diff':x-y,'product':x*y}
    
    # After Black:
    def calculate(x, y):
        return {
            "sum": x + y,
            "diff": x - y,
            "product": x * y,
        }
    
    # 3. Docstring generator
    def complex_function(a: int, b: str, c: list) -> dict:
        """
        This function does something with the input parameters.
    
        Args:
            a (int): First parameter
            b (str): Second parameter
            c (list): Third parameter
    
        Returns:
            dict: Result dictionary
        """
        pass
    ```
    
- 1.7 Python kodini tekshirish (Linting)
    
    Linting - bu kodni statik tahlil qilish va potentsial xatoliklarni topish jarayoni.
    
    **Asosiy linting vositalari:**
    
    1. **Pylint**:
        - Keng qamrovli tekshiruv
        - PEP 8 standartiga moslik
        - Xatoliklarni batafsil tushuntirish
    2. **Flake8**:
        - Tez ishlashi
        - Moslashuvchanlik
        - Plugin tizimi
    3. **PyCodeStyle**:
        - PEP 8 tekshiruvi
        - Toza sintaksis
    
    **Amaliy misollar:**
    
    ```python
    # 1. Yomon yozilgan kod
    # bad_code.py
    def function(x,y):
        z=x+y
        if(z>10):
            print("Katta")
        return z
    
    # Pylint natijasi:
    # C0103: Variable name "z" doesn't conform to snake_case naming style
    # C0326: No space allowed before bracket
    # C0304: Final newline missing
    
    # 2. Yaxshilangan kod
    def calculate_sum(x, y):
        """Calculate sum of two numbers."""
        result = x + y
        if result > 10:
            print("Katta")
        return result
    
    # 3. Flake8 bilan tekshirish
    # messy_code.py
    import os,sys
    def complex_function( x ):
        y=x*2
        return{'result':y}
    
    # Flake8 natijasi:
    # E231 missing whitespace after ','
    # E201 whitespace after '('
    # E225 missing whitespace around operator
    ```
    
- 1.8 Python kodini formatlash (Formatting)
    
    Kod formatlash - bu kodni o'qishga qulay va standartlarga mos shaklga keltirish.
    
    **Asosiy formatlash vositalari:**
    
    1. **Black**:
        - Avtomatik formatlash
        - Qat'iy qoidalar
        - Configuratsiyasiz
    2. **YAPF**:
        - Moslashuvchan
        - Ko'p stillar
    3. **Autopep8**:
        - PEP 8 ga moslashtirish
        - Minimal o'zgarishlar
    
    **Amaliy misollar:**
    
    ```python
    # 1. Formatlanmagan kod
    def bad_format(    x,y   ):
        return {'a':x,'b':y,'sum':x+y,'product':x*y}
    
    # Black bilan formatlangan
    def bad_format(x, y):
        return {
            "a": x,
            "b": y,
            "sum": x + y,
            "product": x * y,
        }
    
    # 2. YAPF misoli
    class   BadClass :
        def __init__ (self,name,age):
            self.name=name
            self.age=age
    
        def get_info(self):
            return f"{self.name} is {self.age} years old"
    
    # Formatlangan
    class BadClass:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def get_info(self):
            return f"{self.name} is {self.age} years old
    ```
    
- 1.9 Python kodini bajarish (Execution)
    
    Python kodini bajarish turli usullar va muhitlarda amalga oshirilishi mumkin.
    
    **Bajarish usullari:**
    
    1. Terminal/Command prompt
    2. IDE ichida
    3. Jupyter notebook
    4. Script fayl orqali
    5. Module sifatida
    
    **Amaliy misollar:**
    
    ```python
    # 1. Terminal orqali
    # hello.py
    print("Terminal orqali bajarildi")
    
    # Bajarish:
    # python hello.py
    
    # 2. Module sifatida
    # my_module.py
    def greet(name):
        return f"Salom, {name}!"
    
    if __name__ == "__main__":
        print(greet("Python"))
    
    # 3. Interactive rejimda
    # python
    >>> x = 10
    >>> y = 20
    >>> print(f"{x} + {y} = {x + y}")
    
    # 4. Shebang bilan (Linux/Unix)
    #!/usr/bin/env python3
    print("Shebang orqali bajarildi")
    ```
    
- 1.10 Python implementatsiyalari
    
    Python turli implementatsiyalari mavjud bo'lib, har biri o'z maqsad va afzalliklariga ega.
    
    **Asosiy implementatsiyalar:**
    
    1. **CPython**
        - Standart implementatsiya
        - C tili bilan yozilgan
        - Eng ko'p ishlatiladi
    2. **PyPy**
        - Tezroq ishlaydi
        - JIT compiler
        - CPython bilan mos
    3. **Jython**
        - Java Virtual Machine
        - Java kutubxonalari
    4. **IronPython**
        - .NET frameworki
        - Windows integratsiyasi
    
    **Amaliy misollar:**
    
    ```python
    # 1. CPython misollar
    # Standart Python kodi
    def factorial(n):
        if n <= 1:
            return 1
        return n * factorial(n - 1)
    
    # 2. PyPy tezlik testi
    def heavy_calculation():
        total = 0
        for i in range(1000000):
            total += i * i
        return total
    
    # 3. Jython Java integratsiyasi
    from java.util import ArrayList
    list = ArrayList()
    list.add("Salom")
    list.add("Dunyo")
    
    # 4. IronPython .NET
    import clr
    clr.AddReference("System.Windows.Forms")
    from System.Windows.Forms import MessageBox
    MessageBox.Show("Salom!")
    ```
    
- 1.11 Python kodi qanday ishlanadi?
    
    Python kodining bajarilish jarayoni bir necha bosqichlardan iborat.
    
    **Bajarilish bosqichlari:**
    
    1. Parsing (Tahlil)
    2. Compilation (Kompilyatsiya)
    3. Bytecode generation
    4. PVM execution
    
    **Asosiy tushunchalar:**
    
    - AST (Abstract Syntax Tree)
    - Bytecode
    - Python Virtual Machine
    - Memory management
    
    **Amaliy misollar:**
    
    ```python
    # 1. Bytecode ko'rish
    def example():
        x = 1
        y = 2
        return x + y
    
    import dis
    dis.dis(example)
    
    # 2. AST ko'rish
    import ast
    code = """
    def greet(name):
        return f"Hello, {name}!"
    """
    tree = ast.parse(code)
    print(ast.dump(tree))
    
    # 3. Memory tracking
    import sys
    x = [1, 2, 3]
    print(sys.getsizeof(x))
    
    # 4. Compilation
    import py_compile
    py_compile.compile("my_script.py")
    ```
    
- 1.12 O'rganish yo'llari (Learning Paths)
    
    Python o'rganish yo'llari har bir dasturchi uchun individual bo'lishi mumkin.
    
    **Asosiy yo'nalishlar:**
    
    1. Web Development
    2. Data Science
    3. Machine Learning
    4. Automation
    5. Game Development
    
    **Har bir bosqich uchun kerakli bilimlar:**
    
    1. **Boshlang'ich daraja**
        - Sintaksis
        - Ma'lumot turlari
        - Control flow
    2. **O'rta daraja**
        - OOP
        - File handling
        - Exceptions
    3. **Professional daraja**
        - Advanced Python
        - Frameworks
        - Testing
    
    **Amaliy misollar:**
    
    ```python
    # 1. Boshlang'ich daraja
    # Variables and types
    name = "Python"
    age = 30
    height = 1.75
    is_programming = True
    
    # 2. O'rta daraja
    # OOP
    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age
    
        def greet(self):
            return f"Hi, I'm {self.name}"
    
    # 3. Professional daraja
    # Decorators
    def timing_decorator(func):
        def wrapper(*args, **kwargs):
            import time
            start = time.time()
            result = func(*args, **kwargs)
            end = time.time()
            print(f"{func.__name__} took {end-start} seconds")
            return result
        return wrapper
    ```
