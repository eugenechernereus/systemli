## GitHub - автоматическая сборка Sphinx и публикация сайта через GitHub Pages

При каждом git push документация будет пересобираться автоматически.

#### Используется:

- Sphinx
- Docker
- GitHub Actions
- GitHub Pages

* * *
### 1. Создать репозиторий на GitHub

### 2. Подключить локальный проект

**В папке проекта:**

```bash
git init
git add .
git commit -m "initial sphinx docs"
```

-m - задает сообщение коммита

**Добавляем репозиторий:**

```bash
git remote add origin https://github.com/USERNAME/name-repository.git
```

**Отправляем:**

```
git branch -M main
git push -u origin main
```

-M - переименование главной ветки

### 3. Создать GitHub Actions
(Можно сделать на сайте: Settings - Pages)

**Создаём папку:**

`mkdir -p .github/workflows`

**Создаём файл:**

`nano .github/workflows/docs.yml`

```yaml
name: Build Sphinx Docs

on:
  push:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"

      - name: Install Sphinx
        run: |
          pip install sphinx sphinx-rtd-theme

      - name: Build docs
        run: |
          sphinx-build -b html source build/html

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: build/html

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages

    steps:
      - name: Deploy
        uses: actions/deploy-pages@v4
```

### 4. Включить GitHub Pages

В репозитории:

`Settings - Pages - Source - GitHub Actions - Static`

### 5. Сделать commit

```bash
git add .
git commit -m "add auto build docs"
git push
```

* * *
## SSH для GitHub

### 1. Проверка существующих ключей

```bash
ls -al ~/.ssh
```

- Ищем файлы id_rsa, id_ed25519 или похожие
- Если ключи есть → можно использовать их
- Если нет → создаём новый

### 2. Создание нового SSH-ключа

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### 3. Добавление ключа в SSH-агент

Запускаем агент:

```bash
eval "$(ssh-agent -s)"
```

Добавляем ключ:

```bash
ssh-add ~/.ssh/id_ed25519
```

### 4. Копируем публичный ключ

```bash
cat ~/.ssh/id_ed25519.pub
```

### 5. Добавляем ключ в GitHub

`GitHub → Settings → SSH and GPG keys → New SSH key`

### 6. Меняем URL репозитория на SSH

Проверка:
```bash
git remote -v
```

Меняем:
```bash
git remote set-url origin git@github.com:username/repo.git
```

Проверяем:
```bash
git remote -v
```

### 7. Проверка соединения

```bash
ssh -T git@github.com
```

Ожидаемо:
```text
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### 8. Теперь пушим без пароля

```bash
git push -u origin main
```

* * *
#### чтобы ключ автоматически добавлялся при каждой сессии, добавь в ~/.bashrc или ~/.profile:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

