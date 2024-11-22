### 10.1 PyPI va pip asoslari

**Nazariy qism:**
Python Package Index (PyPI) - Python dasturchilar hamjamiyati tomonidan yaratilgan paketlar va kutubxonalarning markaziy repozitoriyasi.

**Asosiy tushunchalar:**

1. PyPI - package repository
2. pip - package installer
3. Package dependencies
4. Package versioning

**Amaliy misollar:**

```python
# 1. pip orqali paket o'rnatish
# Terminal:
# pip install requests

import requests

# HTTP so'rov yuborish
response = requests.get('<https://api.github.com>')
print(response.json())

# 2. Package versiyasini tekshirish
import requests
print(requests.__version__)

# 3. Requirements file yaratish
"""
# requirements.txt
requests==2.28.1
pandas>=1.3.0
numpy
"""

# Terminal:
# pip install -r requirements.txt

# 4. Paket ma'lumotlarini olish
# Terminal:
# pip show requests
```

### 10.2 Virtual muhitlar

**Nazariy qism:**
Virtual muhit - izolyatsiyalangan Python muhiti bo'lib, har bir loyiha uchun alohida paketlar va ularning versiyalarini saqlash imkonini beradi.

**Amaliy misollar:**

```bash
# 1. Virtual muhit yaratish
python -m venv myenv

# 2. Faollashtirish
# Windows:
myenv\\Scripts\\activate
# Unix:
source myenv/bin/activate

# 3. Virtual muhit bilan ishlash
pip install requests
pip freeze > requirements.txt

# 4. Virtual muhit uchun skript
def setup_virtualenv():
    import subprocess
    import os

    # Virtual muhit yaratish
    subprocess.run(["python", "-m", "venv", "myenv"])

    # Faollashtirish scripti yaratish
    if os.name == 'nt':  # Windows
        with open("activate.bat", "w") as f:
            f.write("call myenv\\\\Scripts\\\\activate")
    else:  # Unix
        with open("activate.sh", "w") as f:
            f.write("source myenv/bin/activate")

# 5. Requirements bilan ishlash
def install_requirements():
    import subprocess

    # Requirements faylini yaratish
    requirements = [
        "requests==2.28.1",
        "pandas>=1.3.0",
        "numpy"
    ]

    with open("requirements.txt", "w") as f:
        f.write("\\n".join(requirements))

    # Paketlarni o'rnatish
    subprocess.run(["pip", "install", "-r", "requirements.txt"])
```

### 10.3 Pipenv bilan ishlash

**Nazariy qism:**
Pipenv - virtual muhit va paket boshqaruvini birlashtirgan zamonaviy vosita. U Pipfile va Pipfile.lock fayllaridan foydalanadi.

**Amaliy misollar:**

```python
# Terminal commands:
# pip install pipenv
# pipenv install requests

# Pipfile example
"""
[[source]]
url = "<https://pypi.org/simple>"
verify_ssl = true
name = "pypi"

[packages]
requests = "*"
pandas = ">=1.3.0"

[dev-packages]
pytest = "*"
black = "*"

[requires]
python_version = "3.8"
"""

# Python script for pipenv management
import os
import subprocess

class PipenvManager:
    def __init__(self, project_dir):
        self.project_dir = project_dir

    def install_package(self, package_name, dev=False):
        """Paket o'rnatish"""
        cmd = ["pipenv", "install"]
        if dev:
            cmd.append("--dev")
        cmd.append(package_name)
        subprocess.run(cmd, cwd=self.project_dir)

    def run_script(self, script):
        """Pipenv muhitida script bajarish"""
        subprocess.run(["pipenv", "run", script],
                      cwd=self.project_dir)

    def lock_dependencies(self):
        """Dependencies ni lock qilish"""
        subprocess.run(["pipenv", "lock"],
                      cwd=self.project_dir)

# Ishlatish
manager = PipenvManager("./my_project")
manager.install_package("requests")
manager.install_package("pytest", dev=True)
```

### 10.4 O'z paketingizni yaratish

**Nazariy qism:**
Python paketini yaratish uchun kerakli strukturani tuzish va [setup.py](http://setup.py/) faylini to'g'ri konfiguratsiya qilish kerak.

**Amaliy misollar:**

```python
# Project structure
"""
my_package/
    my_package/
        __init__.py
        core.py
    tests/
        test_core.py
    setup.py
    README.md
    LICENSE
"""

# setup.py
from setuptools import setup, find_packages

setup(
    name="my_package",
    version="0.1.0",
    packages=find_packages(),
    install_requires=[
        "requests>=2.25.0",
        "pandas>=1.3.0",
    ],
    author="Your Name",
    author_email="your.email@example.com",
    description="A short description",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    url="<https://github.com/username/my_package>",
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    python_requires=">=3.6",
)

# core.py
class MyPackage:
    """Main package class"""
    def __init__(self, name):
        self.name = name

    def greet(self):
        return f"Hello from {self.name}!"

# __init__.py
from .core import MyPackage
__version__ = "0.1.0"

# test_core.py
def test_greeting():
    from my_package.core import MyPackage
    pkg = MyPackage("Test")
    assert pkg.greet() == "Hello from Test!"
```

### 10.5 Virtual muhitlar VSCode'da

**Nazariy qism:**
VSCode Python extension virtual muhitlar bilan ishlashni osonlashtiradi va loyiha uchun kerakli muhitni avtomatik aniqlaydi.

**Amaliy misollar:**

```python
# 1. VSCode settings.json
{
    "python.defaultInterpreterPath": "${workspaceFolder}/venv/bin/python",
    "python.terminal.activateEnvironment": true,
    "python.linting.enabled": true,
    "python.formatting.provider": "black"
}

# 2. Launch configuration (.vscode/launch.json)
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "env": {
                "PYTHONPATH": "${workspaceFolder}"
            }
        }
    ]
}

# 3. Tasks configuration (.vscode/tasks.json)
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Install Requirements",
            "type": "shell",
            "command": "${command:python.interpreterPath} -m pip install -r requirements.txt",
            "problemMatcher": []
        },
        {
            "label": "Run Tests",
            "type": "shell",
            "command": "${command:python.interpreterPath} -m pytest",
            "group": {
                "kind": "test",
                "isDefault": true
            }
        }
    ]
}

# 4. Workspace manager
class VSCodeWorkspace:
    def __init__(self, workspace_path):
        self.workspace_path = workspace_path

    def setup_virtual_env(self):
        """Virtual muhit yaratish va sozlash"""
        import venv
        import os

        venv_path = os.path.join(self.workspace_path, "venv")
        venv.create(venv_path, with_pip=True)

        # VSCode settings yaratish
        settings_dir = os.path.join(self.workspace_path, ".vscode")
        os.makedirs(settings_dir, exist_ok=True)

        settings = {
            "python.defaultInterpreterPath": "${workspaceFolder}/venv/bin/python",
            "python.formatting.provider": "black"
        }

        with open(os.path.join(settings_dir, "settings.json"), "w") as f:
            import json
            json.dump(settings, f, indent=4)
```

### 10.6 Pipfile bilan ishlash

**Nazariy qism:**
Pipfile - paketlar va ularning versiyalarini, shuningdek development va production muhitlari uchun kerakli paketlarni alohida saqlash imkonini beradi.

**Amaliy misollar:**

```python
# 1. Pipfile yaratish va boshqarish
class PipfileManager:
    def __init__(self, project_path):
        self.project_path = project_path
        self.pipfile_path = os.path.join(project_path, "Pipfile")

    def create_pipfile(self):
        """Asosiy Pipfile yaratish"""
        content = """
[[source]]
url = "<https://pypi.org/simple>"
verify_ssl = true
name = "pypi"

[packages]

[dev-packages]

[requires]
python_version = "3.8"
        """
        with open(self.pipfile_path, "w") as f:
            f.write(content.strip())

    def add_package(self, package_name, version=None, dev=False):
        """Paket qo'shish"""
        import toml

        with open(self.pipfile_path, "r") as f:
            pipfile = toml.load(f)

        section = "dev-packages" if dev else "packages"
        if version:
            pipfile[section][package_name] = version
        else:
            pipfile[section][package_name] = "*"

        with open(self.pipfile_path, "w") as f:
            toml.dump(pipfile, f)

# 2. Pipfile dan requirements.txt yaratish
def generate_requirements():
    import subprocess
    subprocess.run(["pipenv", "lock", "-r"], stdout=open("requirements.txt", "w"))

# 3. Development va production muhitlarini boshqarish
class EnvironmentManager:
    def install_dev_dependencies(self):
        """Development paketlarini o'rnatish"""
        subprocess.run(["pipenv", "install", "--dev"])

    def install_prod_dependencies(self):
        """Production paketlarini o'rnatish"""
        subprocess.run(["pipenv", "install", "--deploy"])

    def export_requirements(self, dev=False):
        """Requirements faylini yaratish"""
        cmd = ["pipenv", "lock", "-r"]
        if dev:
            cmd.append("--dev")
        subprocess.run(cmd)
```

### 10.7 Bog'liqliklarni boshqarish

**Nazariy qism:**
Bog'liqliklarni to'g'ri boshqarish loyiha barqarorligini ta'minlashda muhim rol o'ynaydi. Buning uchun versiyalarni to'g'ri belgilash va dependency resolution muhim.

**Amaliy misollar:**

```python
# 1. Dependency manager
class DependencyManager:
    def __init__(self):
        self.dependencies = {}
        self.dev_dependencies = {}

    def add_dependency(self, package, version=None, dev=False):
        target = self.dev_dependencies if dev else self.dependencies
        target[package] = version or "*"

    def generate_requirements(self, dev=False):
        """Requirements faylini yaratish"""
        deps = {**self.dependencies}
        if dev:
            deps.update(self.dev_dependencies)

        lines = [f"{pkg}{ver if ver != '*' else ''}"
                for pkg, ver in deps.items()]
        return "\\n".join(lines)

    def check_conflicts(self):
        """Version konfliktlarini tekshirish"""
        import pkg_resources

        try:
            pkg_resources.working_set.resolve(
                [pkg_resources.Requirement.parse(
                    f"{pkg}{ver if ver != '*' else ''}"
                ) for pkg, ver in self.dependencies.items()]
            )
            return True
        except pkg_resources.VersionConflict as e:
            return f"Conflict detected: {str(e)}"

# 2. Version checker
class VersionChecker:
    @staticmethod
    def parse_version(version_str):
        """Semantic versioning parser"""
        import re
        match = re.match(r'^(\\d+)\\.(\\d+)\\.(\\d+)', version_str)
        if match:
            return tuple(map(int, match.groups()))
        raise ValueError("Invalid version format")

    @staticmethod
    def compare_versions(v1, v2):
        """Version comparison"""
        v1_parts = VersionChecker.parse_version(v1)
        v2_parts = VersionChecker.parse_version(v2)
        return (v1_parts > v2_parts) - (v1_parts < v2_parts)

# 3. Package updater
class PackageUpdater:
    def __init__(self):
        self.requirements = {}

    def load_requirements(self, filename="requirements.txt"):
        """Requirements faylini o'qish"""
        import re
        with open(filename) as f:
            for line in f:
                if line.strip() and not line.startswith('#'):
                    pkg, ver = re.match(
                        r'([^=<>]+)(?:[=<>]=?(.+))?',
                        line.strip()
                    ).groups()
                    self.requirements[pkg.strip()] = ver.strip() if ver else None

    def check_updates(self):
        """Yangilanishlarni tekshirish"""
        import pkg_resources
        updates = {}

        for pkg, ver in self.requirements.items():
            try:
                installed = pkg_resources.get_distribution(pkg)
                if ver and installed.version != ver:
                    updates[pkg] = {
                        'current': installed.version,
                        'required': ver
                    }
            except pkg_resources.DistributionNotFound:
                updates[pkg] = {'current': None, 'required': ver}

        return updates
```

### 10.8 Paketlarni nashr etish

**Nazariy qism:**
PyPI ga paket nashr etish uchun kerakli fayllarni tayyorlash va twine orqali yuklash kerak.

**Amaliy misollar:**

```python
# 1. Package builder
class PackageBuilder:
    def __init__(self, package_dir):
        self.package_dir = package_dir

    def create_package_structure(self):
        """Paket strukturasini yaratish"""
        import os

        # Asosiy kataloglar
        directories = [
            'src',
            'tests',
            'docs'
        ]

        for directory in directories:
            os.makedirs(os.path.join(self.package_dir, directory), exist_ok=True)

        # Asosiy fayllar
        self._create_setup_py()
        self._create_readme()
        self._create_manifest()

    def _create_setup_py(self):
        """setup.py yaratish"""
        setup_content = '''
from setuptools import setup, find_packages

setup(
    name="my-package",
    version="0.1.0",
    packages=find_packages(where="src"),
    package_dir={"": "src"},
    install_requires=[
        "requests>=2.25.0",
    ],
    author="Your Name",
    author_email="your.email@example.com",
    description="Package description",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
    ],
)
'''
        with open(os.path.join(self.package_dir, 'setup.py'), 'w') as f:
            f.write(setup_content.strip())

    def build_package(self):
        """Paketni build qilish"""
        import subprocess
        subprocess.run(['python', 'setup.py', 'sdist', 'bdist_wheel'])

# 2. Package publisher
class PackagePublisher:
    def __init__(self, package_dir):
        self.package_dir = package_dir

    def publish_to_pypi(self, repository='pypi'):
        """PyPI ga nashr etish"""
        import subprocess

        # Build
        subprocess.run(['python', 'setup.py', 'sdist', 'bdist_wheel'])

        # Upload using twine
        cmd = ['twine', 'upload']
        if repository == 'testpypi':
            cmd.extend(['--repository-url', '<https://test.pypi.org/legacy/>'])
        cmd.append('dist/*')

        subprocess.run(cmd)

# 3. Test PyPI uploader
def upload_to_test_pypi():
    """Test PyPI ga yuklash"""
    import os
    from pathlib import Path

    # .pypirc fayli yaratish
    pypirc_content = '''
[distutils]
index-servers =
    testpypi

[testpypi]
repository = <https://test.pypi.org/legacy/>
username = __token__
password = your-test-pypi-token
'''

    pypirc_path = Path.home() / '.pypirc'
    with open(pypirc_path, 'w') as f:
        f.write(pypirc_content.strip())

    # Upload using twine
    os.system('twine upload --repository testpypi dist/*')
```

### 10.9 Docstrings va dokumentatsiya

**Nazariy qism:**
Docstrings - Python kodini dokumentatsiyalashning asosiy usuli. Ular funksiyalar, klasslar va modullar uchun qo'llaniladi.

**Amaliy misollar:**

```python
# 1. Function documentation
def calculate_average(numbers: list) -> float:
    """Calculate the average of a list of numbers.

    Args:
        numbers (list): A list of numbers (int or float)

    Returns:
        float: The average of the numbers

    Raises:
        ValueError: If the list is empty
        TypeError: If any element is not a number

    Examples:
        >>> calculate_average([1, 2, 3])
        2.0
    """
    if not numbers:
        raise ValueError("List cannot be empty")

    if not all(isinstance(x, (int, float)) for x in numbers):
        raise TypeError("All elements must be numbers")

    return sum(numbers) / len(numbers)

# 2. Class documentation
class DataProcessor:
    """A class for processing data.

    This class provides methods for loading, processing, and saving data.
    It supports various data formats and processing operations.

    Attributes:
        data (pd.DataFrame): The loaded data
        processed (bool): Whether the data has been processed

    Example:
        >>> processor = DataProcessor()
        >>> processor.load_data("data.csv")
        >>> processor.process()
        >>> processor.save("output.csv")
    """

    def __init__(self):
        """Initialize the DataProcessor."""
        self.data = None
        self.processed = False

    def load_data(self, filename: str) -> None:
        """Load data from a file.

        Args:
            filename (str): The path to the data file
        """
        pass

# 3. Module documentation
"""
Data Processing Module
=====================

This module provides utilities for data processing and analysis.
It includes classes and functions for:

- Data loading and saving
- Basic data processing
- Statistical analysis

Usage:
    >>> from data_processing import DataProcessor
    >>> processor = DataProcessor()
"""

# 4. Automated documentation generator
def generate_docs():
    """Generate documentation using Sphinx"""
    import subprocess

    # Create Sphinx project
    subprocess.run(['sphinx-quickstart', 'docs'])

    # Update conf.py
    conf_content = '''
import os
import sys
sys.path.insert(0, os.path.abspath('..'))

extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.napoleon',
    'sphinx.ext.viewcode'
]
'''

    with open('docs/conf.py', 'a') as f:
        f.write(conf_content)

    # Generate documentation
    subprocess.run(['sphinx-apidoc', '-o', 'docs', '.'])
    subprocess.run(['sphinx-build', 'docs', 'docs/_build'])
```

### 10.10 Pydoc va help() sistemasi

**Nazariy qism:**
Pydoc va help() funksiyalari Python kodining interaktiv dokumentatsiyasini ko'rish imkonini beradi.

**Amaliy misollar:**

```python
# 1. Interactive help system
class HelpSystem:
    """Example class for demonstrating help system."""

    def get_help(self, object_name=None):
        """Get help for a specific object or general help.

        Args:
            object_name (str, optional): Name of the object
        """
        if object_name:
            help(object_name)
        else:
            help()

    def show_doc(self, object_name):
        """Show documentation for an object using pydoc."""
        import pydoc
        print(pydoc.render_doc(object_name))

# 2. Custom help formatter
class CustomDocFormatter:
    """Format documentation in a custom style."""

    @staticmethod
    def format_docstring(obj):
        """Format an object's docstring.

        Args:
            obj: Any Python object with a docstring

        Returns:
            str: Formatted documentation
        """
        import inspect

        doc = inspect.getdoc(obj)
        if not doc:
            return "No documentation available"

        # Format sections
        sections = doc.split('\\n\\n')
        formatted = []

        for section in sections:
            if ':' in section:
                # This is probably a section with arguments or returns
                title, content = section.split(':', 1)
                formatted.append(f"{title.strip().upper()}:")
                formatted.append(content.strip())
            else:
                formatted.append(section.strip())

        return '\\n\\n'.join(formatted)

# 3. Documentation browser
class DocBrowser:
    """Browse and search documentation."""

    def __init__(self):
        self.history = []

    def view(self, obj):
        """View documentation for an object."""
        import pydoc

        doc = pydoc.render_doc(obj)
        self.history.append(obj)
        return doc

    def search(self, term):
        """Search in documentation."""
        import pydoc

        return pydoc.apropos(term)

    def serve_docs(self, port=8000):
        """Start documentation server."""
        import pydoc

        pydoc.serve(port=port)

# Usage example
if __name__ == "__main__":
    # Interactive help
    help_sys = HelpSystem()
    help_sys.get_help('str')

    # Custom formatting
    formatter = CustomDocFormatter()
    print(formatter.format_docstring(DocBrowser))

    # Documentation browser
    browser = DocBrowser()
    browser.serve_docs()
```

### 10.11 Matematik amallarni bajaruvchi paket yaratish

**Nazariy qism:**
Professional paket yaratish jarayonida quyidagi komponentlar bo'lishi kerak:

1. Modul strukturasi
2. To'liq dokumentatsiya
3. Unit testlar
4. CI/CD integratsiya

**Amaliy misollar:**

```python
# 1. mathlib/core.py
"""Core mathematical operations module."""
from typing import Union

Number = Union[int, float]

class MathOperations:
    """Class for basic mathematical operations."""

    @staticmethod
    def add(a: Number, b: Number) -> Number:
        """Add two numbers.

        Args:
            a: First number
            b: Second number

        Returns:
            Sum of two numbers
        """
        return a + b

    @staticmethod
    def subtract(a: Number, b: Number) -> Number:
        """Subtract second number from first."""
        return a - b

    @staticmethod
    def multiply(a: Number, b: Number) -> Number:
        """Multiply two numbers."""
        return a * b

    @staticmethod
    def divide(a: Number, b: Number) -> float:
        """Divide first number by second."""
        if b == 0:
            raise ValueError("Cannot divide by zero")
        return a / b

# 2. mathlib/advanced.py
import math
from typing import List

class AdvancedMath:
    """Advanced mathematical operations."""

    @staticmethod
    def square_root(n: Number) -> float:
        """Calculate square root."""
        if n < 0:
            raise ValueError("Cannot calculate square root of negative number")
        return math.sqrt(n)

    @staticmethod
    def power(base: Number, exp: Number) -> Number:
        """Calculate power of number."""
        return math.pow(base, exp)

    @staticmethod
    def mean(numbers: List[Number]) -> float:
        """Calculate arithmetic mean."""
        if not numbers:
            raise ValueError("List cannot be empty")
        return sum(numbers) / len(numbers)

# 3. tests/test_mathlib.py
import pytest
from mathlib.core import MathOperations
from mathlib.advanced import AdvancedMath

def test_basic_operations():
    math = MathOperations()

    assert math.add(2, 3) == 5
    assert math.subtract(5, 3) == 2
    assert math.multiply(2, 4) == 8
    assert math.divide(6, 2) == 3.0

    with pytest.raises(ValueError):
        math.divide(5, 0)

def test_advanced_operations():
    adv = AdvancedMath()

    assert adv.square_root(16) == 4.0
    assert adv.power(2, 3) == 8.0
    assert adv.mean([1, 2, 3, 4, 5]) == 3.0

    with pytest.raises(ValueError):
        adv.square_root(-1)

# 4. setup.py
from setuptools import setup, find_packages

setup(
    name="mathlib",
    version="0.1.0",
    packages=find_packages(),
    install_requires=[],
    extras_require={
        'dev': [
            'pytest>=6.0',
            'pytest-cov>=2.0',
            'black>=21.0'
        ]
    },
    author="Your Name",
    author_email="your.email@example.com",
    description="A comprehensive math library",
    long_description=open("README.md").read(),
    long_description_content_type="text/markdown",
    url="<https://github.com/yourusername/mathlib>",
    classifiers=[
        "Development Status :: 3 - Alpha",
        "Intended Audience :: Developers",
        "License :: OSI Approved :: MIT License",
        "Programming Language :: Python :: 3",
        "Programming Language :: Python :: 3.7",
        "Programming Language :: Python :: 3.8",
        "Programming Language :: Python :: 3.9",
    ],
    python_requires=">=3.7",
)
```

### 10.12 github-actions.yml

**Nazariy qism:**
GitHub Actions orqali CI/CD ni sozlash va avtomatik testlash, build va deploy qilish.

**Amaliy misollar:**

```yaml
# .github/workflows/python-package.yml
name: Python Package

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.7, 3.8, 3.9]

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install .[dev]

    - name: Run tests
      run: |
        pytest --cov=mathlib tests/

    - name: Upload coverage
      uses: codecov/codecov-action@v2

  publish:
    needs: test
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && startsWith(github.ref, 'refs/tags')

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'

    - name: Build package
      run: |
        pip install build
        python -m build

    - name: Publish to PyPI
      uses: pypa/gh-action-pypi-publish@v1.4.2
      with:
        user: __token__
        password: ${{ secrets.PYPI_API_TOKEN }}
```

### 10.13 Standart kutubxonadan foydalanish bo'yicha yaxshi amaliyotlar

**Amaliy misollar:**

```python
# 1. Logging configuration
import logging

def setup_logging():
    """Configure logging for the package."""
    logging.basicConfig(
        level=logging.INFO,
        format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
        handlers=[
            logging.FileHandler('mathlib.log'),
            logging.StreamHandler()
        ]
    )

# 2. Exception handling
class MathError(Exception):
    """Base exception for mathlib."""
    pass

class DivisionError(MathError):
    """Error raised for division problems."""
    pass

def safe_divide(a: Number, b: Number) -> float:
    """Safe division with proper error handling."""
    try:
        if b == 0:
            raise DivisionError("Division by zero")
        return a / b
    except TypeError as e:
        raise MathError(f"Invalid number type: {e}")
    except Exception as e:
        raise MathError(f"Unexpected error: {e}")

# 3. Configuration management
from typing import Dict, Any
import json

class Config:
    """Configuration management class."""

    def __init__(self, config_file: str = 'config.json'):
        self.config_file = config_file
        self.settings: Dict[str, Any] = {}
        self.load()

    def load(self) -> None:
        """Load configuration from file."""
        try:
            with open(self.config_file) as f:
                self.settings = json.load(f)
        except FileNotFoundError:
            self.settings = {}

    def save(self) -> None:
        """Save configuration to file."""
        with open(self.config_file, 'w') as f:
            json.dump(self.settings, f, indent=4)
```

Bu Python Package Index (PyPI) bo'limini yakunlaydi. Asosiy mavzular:

1. Paketlarni o'rnatish va boshqarish
2. Virtual muhitlar
3. Paket yaratish va nashr etish
4. Dokumentatsiya va testing
5. CI/CD integratsiya
