## Диаграммы Mermaid
* * *
### Для совместимости всех платформ рекомендуется HTML код

```html
<div class="mermaid">
graph TD
  User --> WebApp
  WebApp --> PaymentSystem
  WebApp --> EmailService
</div>
```

<div class="mermaid">
graph TD
  User --> WebApp
  WebApp --> PaymentSystem
  WebApp --> EmailService
</div>

* * *
### Для правильного отображения диаграмм в Sphinx название пишется в {}:
**{mermaid}**

* * *
#### В .md файле:

```mermaid
graph TD

A[User] --> B[API]
B --> C[Database]
B --> D[Cache]
```

```{mermaid}
graph TD

A[User] --> B[API]
B --> C[Database]
B --> D[Cache]
```

* * *
#### Пример диаграммы архитектуры

```mermaid
graph LR

User --> Nginx
Nginx --> Backend
Backend --> Redis
Backend --> Postgres
```

```{mermaid}
graph LR

User --> Nginx
Nginx --> Backend
Backend --> Redis
Backend --> Postgres
```

Подходит для:

- архитектуры системы
- микросервисов
- CI/CD
- сетей
- потоков данных

* * *
#### Sequence диаграммы

```mermaid
sequenceDiagram

User->>API: Request
API->>DB: Query
DB-->>API: Result
API-->>User: Response
```

```{mermaid}
sequenceDiagram

User->>API: Request
API->>DB: Query
DB-->>API: Result
API-->>User: Response
```

* * *
#### Flowchart

```mermaid
flowchart TD

Start --> Login
Login --> Dashboard
Dashboard --> Settings
Settings --> Logout
```

```{mermaid}
flowchart TD

Start --> Login
Login --> Dashboard
Dashboard --> Settings
Settings --> Logout
```

* * *
#### Mermaid поддерживает:

- Flowcharts
- Sequence diagrams
- Class diagrams
- State diagrams
- Git graphs
- ER diagrams
- Gantt charts

#### Архитектура

```mermaid
graph TD
Frontend --> API
API --> Database
API --> Queue
Queue --> Worker
```

```{mermaid}
graph TD
Frontend --> API
API --> Database
API --> Queue
Queue --> Worker
```

* * *
**Такая документация:**

✅ выглядит как **docs Kubernetes / GitLab**
✅ диаграммы обновляются вместе с кодом
✅ хранится в Git
✅ можно редактировать как обычный текст

#### Что показывают архитектурные диаграммы

- компоненты системы
- сервисы
- базы данных
- очереди
- API
- пользователей
- взаимодействие между ними

* * *
### Более сложный пример (микросервисы)

```mermaid
graph LR

User --> Nginx
Nginx --> Gateway

Gateway --> AuthService
Gateway --> OrderService
Gateway --> PaymentService

AuthService --> Redis
OrderService --> Postgres
PaymentService --> Stripe
```

```{mermaid}
graph LR

User --> Nginx
Nginx --> Gateway

Gateway --> AuthService
Gateway --> OrderService
Gateway --> PaymentService

AuthService --> Redis
OrderService --> Postgres
PaymentService --> Stripe
```

Это уже показывает:

- gateway
- микросервисы
- базы
- внешние сервисы

* * *

## C4 Model (профессиональный стандарт)

Модель C4 разбивает архитектуру на уровни:

| Уровень | Что показывает |
| --- | --- |
| Context | систему целиком |
| Container | сервисы |
| Component | модули |
| Code | классы |

### 1. Context diagram

```mermaid
graph TD

User --> WebApp
WebApp --> PaymentSystem
WebApp --> EmailService
```

```{mermaid}
graph TD

User --> WebApp
WebApp --> PaymentSystem
WebApp --> EmailService
```

Показывает **внешние системы**.

### 2. Container diagram

```mermaid
graph TD

User --> ReactApp
ReactApp --> API
API --> Postgres
API --> Redis
```

```{mermaid}
graph TD

User --> ReactApp
ReactApp --> API
API --> Postgres
API --> Redis
```

Показывает **основные сервисы**.

### 3. Component diagram

```mermaid
graph TD

API --> AuthModule
API --> OrderModule
API --> PaymentModule
OrderModule --> DB
```

```{mermaid}
graph TD

API --> AuthModule
API --> OrderModule
API --> PaymentModule
OrderModule --> DB
```

Показывает **внутреннюю структуру сервиса**.

#### Где такие диаграммы используют
Практически во всех крупных проектах:

- Kubernetes
- GitLab
- FastAPI
- Apache Kafka

#### Пример DevOps архитектуры

```mermaid
graph TD

Developer --> GitHub
GitHub --> CI
CI --> DockerRegistry
DockerRegistry --> Kubernetes
Kubernetes --> Users
```

```{mermaid}
graph TD

Developer --> GitHub
GitHub --> CI
CI --> DockerRegistry
DockerRegistry --> Kubernetes
Kubernetes --> Users
```

Это показывает **pipeline доставки приложения**.

#### Почему это полезно
Архитектурные диаграммы:

✅ быстро объясняют систему
✅ помогают новым разработчикам
✅ показывают зависимости
✅ документируют инфраструктуру

* * *
## Полезные значки
🚀 Быстрый старт
📦 Установка
⚙️ Конфигурация
🐳 Docker запуск
<br>
ℹ️ NOTE
⚠️ WARNING
💡 TIP
❗ Important
🔥 Danger
<br>
🐳 Docker
🐍 Python
☸️ Kubernetes
🗄️ PostgreSQL
⚡ Redis
<br>
✅ поддерживается
❌ не поддерживается
⚠️ экспериментально
🚧 в разработке

### Примеры использования

ℹ️ Note (заметка)

Используют для:

- дополнительной информации
- уточнений
- комментариев

⚠️ Warning (предупреждение)

Используется когда:

- можно сломать систему
- есть риск потери данных
- есть ограничения

💡 Tip (совет)

Подходит для:

- полезных лайфхаков
- ускорения работы

❗ Important

Используется **для критически важной информации**.

🔥 Danger

Используют для:

- опасных операций
- destructive commands

