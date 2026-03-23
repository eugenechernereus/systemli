## Как включить автогенерацию API

### 1. Добавить расширения и путь к коду в `conf.py`:

```python
extensions = [
    "myst_parser",
    "sphinx.ext.autodoc",
    "sphinx.ext.napoleon"
]
```

```python
import os
import sys
sys.path.insert(0, os.path.abspath(".."))
```

### 2. Создать страницу API:

Например:

```text
source/api.rst
```

```rst
API Reference
=============

.. automodule:: myproject.math
   :members:
   :undoc-members:
   :show-inheritance:
```

### 3. Автоматическая генерация всех модулей:

```bash
sphinx-apidoc -o source/api ../myproject
```

- source/api - папка с документацией
- myproject - код

* * *
#### Что генерируется автоматически

- модули
- классы
- функции
- методы
- атрибуты
- исключения
<br>
#### Система используется в огромных проектах:

- FastAPI
- NumPy
- Kubernetes
- TensorFlow
<br>
#### Плюсы:

- документация всегда актуальна
- не нужно писать её отдельно
- легко поддерживать
- отлично работает с CI/CD