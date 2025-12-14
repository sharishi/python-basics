# Лекция: Работа с SQLite в Python

## Введение

Добрый день! Сегодня мы рассмотрим практическую работу с базами данных в Python. Наша цель — научиться создавать базы данных, таблицы и выполнять основные операции с данными используя встроенные возможности Python.


## 1. Зачем нужны базы данных?

Представьте, что вы разрабатываете приложение для учёта студентов. Вы можете хранить данные в обычных файлах, например в текстовых или JSON. Но при этом возникают серьёзные проблемы:

**Проблема 1: Производительность**  
Если у вас 50 000 записей студентов, и вам нужно найти конкретного студента по номеру зачётки — придётся читать весь файл построчно. Это медленно.

**Проблема 2: Структура данных**  
В текстовом файле нет чёткого разделения на поля. Легко допустить ошибку в формате, и данные станут нечитаемыми.

**Проблема 3: Целостность данных**  
Если два процесса одновременно попытаются изменить файл, один из них может перезаписать изменения другого. Данные повредятся.

**Проблема 4: Отсутствие языка запросов**  
Чтобы найти "всех студентов старше 20 лет", нужно писать код вручную, перебирать строки, проверять условия.

Базы данных решают все эти проблемы. Они предоставляют:
- быстрый поиск через индексы
- строгую структуру (таблицы с типами данных)
- механизмы блокировок для многопользовательского доступа
- язык запросов (SQL) для выборки и фильтрации



## 2. Что такое SQLite?

SQLite — это легковесная база данных, которая:
- хранится в **одном файле** на диске
- **не требует установки** отдельного сервера
- **встроена** в Python по умолчанию
- используется в мобильных приложениях, браузерах, играх

В отличие от больших СУБД (PostgreSQL, MySQL), SQLite не работает как отдельный сервер. Это библиотека, которая читает и пишет данные напрямую в файл.

**Когда использовать SQLite:**
- локальные приложения
- прототипирование
- встроенные базы в программах
- небольшие объёмы данных (до нескольких гигабайт)

**Когда НЕ использовать SQLite:**
- высоконагруженные веб-приложения с тысячами одновременных пользователей
- распределённые системы

## 3. Подключение к базе данных в Python

### 3.1. Импорт модуля

Python содержит встроенный модуль для работы с SQLite:

```python
import sqlite3
```

Никакой дополнительной установки не требуется.

### 3.2. Создание соединения

Чтобы начать работу с базой, нужно создать **соединение (connection)**:

```python
import sqlite3

# Создаём соединение с базой данных
# Если файла не существует, SQLite создаст его автоматически
conn = sqlite3.connect("university.db")

print("Соединение установлено")
```

**Что происходит?**
- Если файл `university.db` не существует, он будет создан
- Если файл существует, Python откроет его
- Переменная `conn` содержит объект соединения

### 3.3. Создание курсора

Все SQL-запросы выполняются через объект **курсор (cursor)**:

```python
cursor = conn.cursor()
```

**Курсор** — это инструмент для выполнения команд SQL и получения результатов.

Аналогия: соединение — это "телефонная линия", а курсор — это "микрофон", через который вы говорите с базой.


## 4. Создание таблицы

### 4.1. Что такое таблица?

Таблица — это структура данных, состоящая из:
- **строк** (записи, rows) — каждая строка представляет один объект
- **столбцов** (поля, columns) — каждый столбец имеет название и тип данных

Пример таблицы студентов:

```
| id | name       | age | email                |
|----|------------|-----|----------------------|
| 1  | Иван       | 20  | ivan@university.edu  |
| 2  | Мария      | 22  | maria@university.edu |
| 3  | Пётр       | 19  | petr@university.edu  |
```

### 4.2. Типы данных в SQLite

SQLite поддерживает 5 типов данных:

- **INTEGER** — целые числа (1, 42, -100)
- **REAL** — числа с плавающей точкой (3.14, -0.5)
- **TEXT** — текстовые строки ("Иван", "Привет")
- **BLOB** — бинарные данные (изображения, файлы)
- **NULL** — отсутствие значения

### 4.3. Создание таблицы: код

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Создаём таблицу students
cursor.execute("""
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        age INTEGER,
        email TEXT UNIQUE
    )
""")

# Сохраняем изменения
conn.commit()

print("Таблица students создана")
```

**Разбор команды:**

- `CREATE TABLE IF NOT EXISTS students` — создать таблицу с именем `students`, если она ещё не существует
- `id INTEGER PRIMARY KEY AUTOINCREMENT` — столбец `id`, целое число, уникальный идентификатор, автоматически увеличивается
- `name TEXT NOT NULL` — столбец `name`, текст, обязательное поле (нельзя оставить пустым)
- `age INTEGER` — столбец `age`, целое число, необязательное поле
- `email TEXT UNIQUE` — столбец `email`, текст, должен быть уникальным (два студента не могут иметь одинаковый email)

**Важно:** `conn.commit()` — эта команда **фиксирует изменения** в базе. Без неё таблица не будет создана!

## 5. Добавление данных в таблицу

### 5.1. Команда INSERT

Для вставки данных используется команда `INSERT`:

```
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...)
```

### 5.2. Вставка одной записи

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Вставляем одного студента
cursor.execute("""
    INSERT INTO students (name, age, email)
    VALUES (?, ?, ?)
""", ("Иван Иванов", 20, "ivan@university.edu"))

conn.commit()

print("Студент добавлен")
```

**Важный момент: знаки вопроса `?`**

Обратите внимание на символы `?` в запросе. Это **плейсхолдеры (заполнители)**. Значения передаются отдельно в виде кортежа.

**Почему нельзя писать так:**

```python
# НЕПРАВИЛЬНО! НЕ ДЕЛАЙТЕ ТАК!
name = "Иван"
cursor.execute(f"INSERT INTO students (name) VALUES ('{name}')")
```

Это опасно! Такой код открывает уязвимость **SQL Injection** — злоумышленник может передать специальные символы и выполнить произвольные команды в вашей базе.

**Правильный способ:**

```python
# ПРАВИЛЬНО
cursor.execute("INSERT INTO students (name, age, email) VALUES (?, ?, ?)",
               ("Иван", 20, "ivan@university.edu"))
```

SQLite автоматически экранирует опасные символы.

### 5.3. Вставка нескольких записей

Если нужно добавить сразу много записей, используйте метод `executemany`:

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Список студентов
students = [
    ("Мария Петрова", 22, "maria@university.edu"),
    ("Пётр Сидоров", 19, "petr@university.edu"),
    ("Анна Смирнова", 21, "anna@university.edu"),
    ("Дмитрий Козлов", 23, "dmitry@university.edu")
]

# Вставляем всех студентов одной командой
cursor.executemany("""
    INSERT INTO students (name, age, email)
    VALUES (?, ?, ?)
""", students)

conn.commit()

print(f"Добавлено студентов: {len(students)}")
```

Метод `executemany` выполняет запрос для каждого элемента списка. Это гораздо быстрее, чем вызывать `execute` в цикле.


## 6. Выборка данных из таблицы

### 6.1. Команда SELECT

Команда `SELECT` используется для **чтения данных** из таблицы:

```
SELECT column1, column2 FROM table_name
```

Чтобы выбрать все столбцы, используйте `*`:

```
SELECT * FROM table_name
```

### 6.2. Получение всех записей

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Выполняем запрос
cursor.execute("SELECT * FROM students")

# Получаем все строки
rows = cursor.fetchall()

# Выводим результат
for row in rows:
    print(row)
```

**Результат:**

```
(1, 'Иван Иванов', 20, 'ivan@university.edu')
(2, 'Мария Петрова', 22, 'maria@university.edu')
(3, 'Пётр Сидоров', 19, 'petr@university.edu')
...
```

Каждая строка представлена как **кортеж (tuple)**.

### 6.3. Выборка конкретных столбцов

Если нужны не все столбцы, укажите их имена:

```python
cursor.execute("SELECT name, age FROM students")
rows = cursor.fetchall()

for row in rows:
    print(f"Имя: {row[0]}, Возраст: {row[1]}")
```

**Результат:**

```
Имя: Иван Иванов, Возраст: 20
Имя: Мария Петрова, Возраст: 22
Имя: Пётр Сидоров, Возраст: 19
```

### 6.4. Методы получения данных

SQLite предоставляет три метода для получения результатов:

**1. `fetchall()` — получить все строки сразу**

```python
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()  # Список всех строк
```

**2. `fetchone()` — получить одну строку**

```python
cursor.execute("SELECT * FROM students")
row = cursor.fetchone()  # Только первая строка
print(row)
```

**3. `fetchmany(size)` — получить несколько строк**

```python
cursor.execute("SELECT * FROM students")
rows = cursor.fetchmany(3)  # Первые 3 строки
```

## 7. Фильтрация данных: WHERE

### 7.1. Что такое WHERE?

Часто нужно выбрать не все записи, а только те, которые удовлетворяют условию. Для этого используется `WHERE`:

```
SELECT * FROM table_name WHERE condition
```

### 7.2. Примеры фильтрации

**Пример 1: Студенты старше 20 лет**

```python
cursor.execute("SELECT name, age FROM students WHERE age > ?", (20,))
rows = cursor.fetchall()

for row in rows:
    print(row)
```

**Обратите внимание:** значение передаётся как кортеж `(20,)`. Даже если значение одно, нужна запятая!

**Пример 2: Студент с конкретным email**

```python
cursor.execute("SELECT * FROM students WHERE email = ?", ("ivan@university.edu",))
row = cursor.fetchone()

if row:
    print(f"Найден студент: {row[1]}")
else:
    print("Студент не найден")
```

**Пример 3: Поиск по части строки (LIKE)**

```python
# Найти всех студентов, у которых в имени есть "Пётр"
cursor.execute("SELECT name FROM students WHERE name LIKE ?", ("%Пётр%",))
rows = cursor.fetchall()

for row in rows:
    print(row[0])
```

Символ `%` означает "любая последовательность символов".

## 8. Обновление и удаление данных

### 8.1. Обновление записей: UPDATE

Если нужно изменить данные в существующих записях, используйте `UPDATE`:

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Изменить возраст студента с id = 1
cursor.execute("""
    UPDATE students
    SET age = ?
    WHERE id = ?
""", (21, 1))

conn.commit()

print("Данные обновлены")
```

**Внимание:** если не указать `WHERE`, изменятся **все записи** в таблице!

### 8.2. Удаление записей: DELETE

Для удаления используется команда `DELETE`:

```python
# Удалить студента с id = 3
cursor.execute("DELETE FROM students WHERE id = ?", (3,))
conn.commit()

print("Студент удалён")
```

**Внимание:** если не указать `WHERE`, удалятся **все записи**!


## 9. Транзакции и безопасность данных

### 9.1. Что такое транзакция?

**Транзакция** — это последовательность операций, которая выполняется **атомарно**:
- либо выполняются **все операции**
- либо **ни одна** не выполняется

Пример: перевод денег между счетами.

```
1. Снять 1000₽ со счёта А
2. Добавить 1000₽ на счёт Б
```

Если между операциями произойдёт сбой, деньги "потеряются". Транзакция гарантирует, что либо обе операции выполнятся, либо ни одна.

### 9.2. Команды для работы с транзакциями

- **`commit()`** — сохранить изменения в базе
- **`rollback()`** — отменить все изменения с момента последнего `commit()`

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

try:
    # Выполняем операции
    cursor.execute("INSERT INTO students (name, age) VALUES (?, ?)", ("Тест", 25))
    cursor.execute("UPDATE students SET age = ? WHERE id = ?", (30, 1))
    
    # Если всё прошло успешно — сохраняем
    conn.commit()
    print("Изменения сохранены")
    
except Exception as e:
    # Если произошла ошибка — откатываем
    conn.rollback()
    print(f"Ошибка: {e}")
    print("Изменения отменены")
```

### 9.3. Использование контекстного менеджера

Python позволяет использовать `with` для автоматического управления транзакциями:

```python
import sqlite3

try:
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        
        cursor.execute("INSERT INTO students (name, age) VALUES (?, ?)", 
                      ("Автоматический коммит", 26))
        
        # commit() вызывается автоматически при выходе из блока with
        
except Exception as e:
    # rollback() вызывается автоматически при ошибке
    print(f"Ошибка: {e}")
```

**Преимущества:**
- не нужно вручную вызывать `commit()` и `rollback()`
- код более чистый и безопасный
- соединение автоматически закрывается

## 10. Полный пример: приложение для учёта студентов

Давайте создадим законченное приложение, которое:
- создаёт базу и таблицу
- добавляет студентов
- показывает список
- ищет студентов по возрасту

```python
import sqlite3

def create_database():
    """Создание базы данных и таблицы"""
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute("""
            CREATE TABLE IF NOT EXISTS students (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                name TEXT NOT NULL,
                age INTEGER,
                email TEXT UNIQUE
            )
        """)
        print("База данных готова")

def add_student(name, age, email):
    """Добавление нового студента"""
    try:
        with sqlite3.connect("university.db") as conn:
            cursor = conn.cursor()
            cursor.execute(
                "INSERT INTO students (name, age, email) VALUES (?, ?, ?)",
                (name, age, email)
            )
            print(f"Студент {name} добавлен")
    except sqlite3.IntegrityError:
        print(f"Ошибка: email {email} уже существует")

def show_all_students():
    """Показать всех студентов"""
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute("SELECT id, name, age, email FROM students")
        rows = cursor.fetchall()
        
        print("\n=== Список студентов ===")
        for row in rows:
            print(f"ID: {row[0]}, Имя: {row[1]}, Возраст: {row[2]}, Email: {row[3]}")

def find_students_by_age(min_age):
    """Найти студентов старше указанного возраста"""
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute(
            "SELECT name, age FROM students WHERE age >= ?",
            (min_age,)
        )
        rows = cursor.fetchall()
        
        print(f"\n=== Студенты старше {min_age} лет ===")
        for row in rows:
            print(f"Имя: {row[0]}, Возраст: {row[1]}")

if __name__ == "__main__":
    # 1. Создаём базу
    create_database()
    
    # 2. Добавляем студентов
    add_student("Иван Иванов", 20, "ivan@university.edu")
    add_student("Мария Петрова", 22, "maria@university.edu")
    add_student("Пётр Сидоров", 19, "petr@university.edu")
    add_student("Анна Смирнова", 21, "anna@university.edu")
    
    # 3. Показываем всех студентов
    show_all_students()
    
    # 4. Ищем студентов старше 20 лет
    find_students_by_age(20)
```

**Результат выполнения:**

```
База данных готова
Студент Иван Иванов добавлен
Студент Мария Петрова добавлен
Студент Пётр Сидоров добавлен
Студент Анна Смирнова добавлен

=== Список студентов ===
ID: 1, Имя: Иван Иванов, Возраст: 20, Email: ivan@university.edu
ID: 2, Имя: Мария Петрова, Возраст: 22, Email: maria@university.edu
ID: 3, Имя: Пётр Сидоров, Возраст: 19, Email: petr@university.edu
ID: 4, Имя: Анна Смирнова, Возраст: 21, Email: anna@university.edu

=== Студенты старше 20 лет ===
Имя: Иван Иванов, Возраст: 20
Имя: Мария Петрова, Возраст: 22
Имя: Анна Смирнова, Возраст: 21
```

## 11. Рекомендации и лучшие практики

### 11.1. Всегда используйте плейсхолдеры

```python
# ПЛОХО - уязвимо к SQL Injection
name = "Иван"
cursor.execute(f"SELECT * FROM students WHERE name = '{name}'")

# ХОРОШО - безопасно
cursor.execute("SELECT * FROM students WHERE name = ?", (name,))
```

### 11.2. Используйте контекстный менеджер `with`

```python
# ХОРОШО
with sqlite3.connect("university.db") as conn:
    cursor = conn.cursor()
    # ваш код
    # commit() вызовется автоматически
```

### 11.3. Обрабатывайте ошибки

```python
try:
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute("INSERT INTO students ...")
except sqlite3.IntegrityError as e:
    print(f"Ошибка целостности данных: {e}")
except sqlite3.Error as e:
    print(f"Ошибка базы данных: {e}")
```

### 11.4. Закрывайте соединения

Если не используете `with`, обязательно закрывайте соединение:

```python
conn = sqlite3.connect("university.db")
try:
    # работа с базой
    pass
finally:
    conn.close()
```


## Заключение

Сегодня мы изучили основы работы с SQLite в Python:

1. **Создали соединение** с базой данных
2. **Создали таблицу** с нужными столбцами и типами данных
3. **Добавили данные** с помощью `INSERT`
4. **Прочитали данные** с помощью `SELECT`
5. **Отфильтровали данные** с помощью `WHERE`
6. **Обновили и удалили** записи
7. **Научились работать с транзакциями** для обеспечения целостности данных

Эти знания — фундамент для работы с любыми базами данных. Принципы остаются теми же, меняется только синтаксис и возможности конкретной СУБД.
