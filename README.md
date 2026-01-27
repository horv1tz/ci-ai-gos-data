# Структура курса в Markdown формате

Этот репозиторий содержит контент интерактивного курса в markdown-формате с YAML-метаданными.

## Структура папок

```
ci-ai-gos-data/
├── index.md                    # Файл для индексации (метаданные курса)
├── README.md                   # Эта инструкция
├── assets/
│   ├── citronchik.png          # Изображение маскота
│   └── images/                 # SVG-иллюстрации
│       ├── rocket.svg
│       ├── brain.svg
│       ├── memo.svg
│       ├── magic.svg
│       ├── puzzle.svg
│       ├── shield.svg
│       ├── detective.svg
│       └── trophy.svg
├── step-0-intro/               # Введение
├── step-1-theory/              # Теория: LLM
├── step-2-theory/              # Теория: РКЗФ
├── step-3-task/                # Практика: РКЗФ
├── step-4-theory/              # Теория: Few-Shot
├── step-5-task/                # Практика: Few-Shot
├── step-6-theory/              # Теория: CoT
├── step-7-task/                # Практика: CoT
├── step-8-theory/              # Теория: Безопасность
├── step-9-task/                # Практика: Обезличивание
├── step-10-test/               # Финальный тест
└── step-11-result/             # Результат
```

## Типы шагов

### 1. Введение (`intro`)

Вводный экран курса.

**Файлы:**
```
step-N-intro/
├── meta.yaml       # Метаданные
└── content.md      # Контент
```

**meta.yaml:**
```yaml
id: start                    # Уникальный идентификатор
type: intro                  # Тип шага
title: "Название"            # Заголовок
time_estimate_min: 5         # Время в минутах
illustration: rocket         # ID иллюстрации (без расширения)
mascot_quip: "Реплика"       # Фраза маскота
next_step: step-1-theory     # Следующий шаг
```

### 2. Теория (`theory`)

Экран с теоретическим материалом.

**Файлы:**
```
step-N-theory/
├── meta.yaml       # Метаданные
└── content.md      # Контент в markdown
```

**meta.yaml:**
```yaml
id: theory_llm
type: theory
title: "Модуль 1. Как думает машина?"
time_estimate_min: 5
illustration: brain
mascot_quip: "Фраза маскота"
next_step: step-2-theory
```

### 3. Практика (`task`)

Экран с практическим заданием, которое проверяется ИИ.

**Файлы:**
```
step-N-task/
├── meta.yaml       # Метаданные + критерии
└── content.md      # Описание задания
```

**meta.yaml:**
```yaml
id: task_rcjf
type: task
title: "Практика: РКЗФ"
time_estimate_min: 5
illustration: magic
mascot_quip: "Фраза маскота"
task_prompt: "Краткий текст для поля ввода"
evaluation_criteria: "Скрытые критерии для LLM-проверки ответа"
next_step: step-4-theory
```

**Важно:** Поле `evaluation_criteria` содержит инструкции для ИИ-валидатора и не показывается пользователю.

### 4. Тест (`test`)

Экран с тестовыми вопросами.

**Файлы:**
```
step-N-test/
├── meta.yaml       # Метаданные
├── content.md      # Вводный текст
└── questions.yaml  # Вопросы теста
```

**meta.yaml:**
```yaml
id: quiz
type: test
title: "Финальный тест"
time_estimate_min: 5
illustration: trophy
mascot_quip: "Фраза маскота"
next_step: step-11-result
```

**questions.yaml:**
```yaml
questions:
  - id: 1
    question: "Текст вопроса"
    options:
      - "Вариант A"
      - "Вариант B"
      - "Вариант C"
    correct_index: 1          # Индекс правильного ответа (0-based)

  - id: 2
    question: "Второй вопрос"
    options:
      - "Да"
      - "Нет"
    correct_index: 0
```

### 5. Результат (`result`)

Финальный экран с итогами.

**Файлы:**
```
step-N-result/
├── meta.yaml       # Метаданные
└── content.md      # Итоговый контент
```

**meta.yaml:**
```yaml
id: result
type: result
title: "Курс завершен!"
time_estimate_min: 0
illustration: trophy
mascot_quip: "Фраза маскота"
next_step: null              # Последний шаг
```

## Иллюстрации

Доступные SVG-иллюстрации хранятся в `assets/images/`:

| ID | Файл | Описание |
|----|------|----------|
| `rocket` | rocket.svg | Ракета — для введения |
| `brain` | brain.svg | Мозг — для теории о LLM |
| `memo` | memo.svg | Документ — для теории о промптинге |
| `magic` | magic.svg | Волшебная палочка — для практики |
| `puzzle` | puzzle.svg | Пазл — для Few-Shot |
| `detective` | detective.svg | Лупа — для Chain of Thought |
| `shield` | shield.svg | Щит — для безопасности |
| `trophy` | trophy.svg | Кубок — для теста и результата |

## Добавление нового шага

1. Создайте папку с именем `step-N-<type>/` (например, `step-12-theory/`)
2. Создайте `meta.yaml` с метаданными
3. Создайте `content.md` с контентом
4. Для теста добавьте `questions.yaml`
5. Обновите `next_step` в предыдущем шаге
6. Добавьте шаг в список `steps` в `index.md`

## Маскот

Маскот курса — **ЦИтрончик** (`assets/citronchik.png`).

Настройки маскота задаются в `index.md`:

```yaml
mascot:
  name: "ЦИтрончик"
  image: "assets/citronchik.png"
  phrases:
    - "Фраза 1"
    - "Фраза 2"
```

Каждый шаг может содержать свою реплику маскота в поле `mascot_quip`.

## Формат контента

Контент пишется в стандартном Markdown:

- Заголовки: `#`, `##`, `###`
- Жирный: `**текст**`
- Курсив: `*текст*`
- Списки: `-` или `1.`
- Цитаты: `>`
- Код: ` ``` `
- Таблицы: `| col1 | col2 |`
- Выделение: `==текст==` (для подсветки)

## Пример добавления нового модуля теории

```bash
# 1. Создаём папку
mkdir step-12-theory

# 2. Создаём meta.yaml
cat > step-12-theory/meta.yaml << 'EOF'
id: theory_new
type: theory
title: "Новый модуль"
time_estimate_min: 5
illustration: brain
mascot_quip: "Новая реплика маскота"
next_step: step-13-task
EOF

# 3. Создаём content.md
cat > step-12-theory/content.md << 'EOF'
## Заголовок

Текст теории...
EOF
```


