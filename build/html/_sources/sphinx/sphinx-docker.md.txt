## Установка Sphinx на Linux Mint через Docker

* * *
### 1. Создаем папку проекта

```bash
mkdir sphinx-docs
cd sphinx-docs
```

* * *
### 2. Dockerfile для Sphinx

Создаём файл:

```bash
nano Dockerfile
```

Содержимое:

```text
FROM python:3.12-slim

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /docs
```

* * *
### 3. Mинимальный requirements.txt:

```text
sphinx
sphinx-rtd-theme
myst-parser
sphinx-autobuild
sphinx-copybutton
sphinx-design
sphinxcontrib-mermaid
```

#### после установки можно обновить список:

```bash
pip freeze > requirements.txt
```

* * *
### 4. docker-compose.yml

```bash
nano docker-compose.yml
```

```yaml
services:
  sphinx:
    build: .
    volumes:
      - .:/docs
    ports:
      - "8000:8000"
    command: sphinx-autobuild source build/html --host 0.0.0.0 --port 8000
    working_dir: /docs
```

* * *
### 5. настройка файла conf.py

```python
extensions = [
    "myst_parser",
    "sphinx.ext.mathjax",
    "sphinx_copybutton",
    "sphinx_design",
    "sphinxcontrib.mermaid",
]

templates_path = ['_templates']
exclude_patterns = []

html_theme = "sphinx_rtd_theme"

source_suffix = {
    ".rst": "restructuredtext",
    ".md": "markdown",
}

html_static_path = ['_static']
```

* * *
### 6. Инициализация проекта Sphinx

Запускаем контейнер:

```bash
docker compose run --rm sphinx sphinx-quickstart
```

Рекомендуемые ответы:

```text
Separate source and build directories: y
Project name: MyDocs
Author name: Your Name
Project version: 1.0
```

После этого появится структура:

```text
sphinx-docs/
 ├── build
 ├── source
 │   ├── conf.py
 │   ├── index.rst
 │   └── _static
 ├── Dockerfile
 └── docker-compose.yml
```

* * *
### 7. Запуск контейнера и автосборка:

```bash
docker compose up
```

После этого документация будет доступна в браузере:

```text
http://localhost:8000
```

### Итог
- изолированный Sphinx
- нет Python зависимостей в системе
- воспроизводимая сборка через Docker

* * *
### Полезные команды

#### пересоздать контейнер:

```bash
docker compose up -d --force-recreate
```

- --force-recreate → пересоздаёт контейнер с новыми настройками

- Образ используется старый (не пересобирается)

#### пересобрать образ:

```bash
docker compose build
docker compose up -d
```