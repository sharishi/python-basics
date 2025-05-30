# Обработка исключений и взаимодействие с файлами данных в Python



## Обработка исключений 
это важный аспект разработки, который помогает управлять ошибками в программе, избегая ее неожиданного завершения. В Python для этого используется конструкция `try-except`, а также дополнительные элементы, такие как `finally`, `else` и `raise`, для более гибкой и надежной обработки ошибок.

---

#### 1. **Что такое исключения?**

Исключение — это событие, которое возникает при ошибке в программе, например, деление на ноль, неправильный ввод данных или отсутствие нужного файла. Когда возникает исключение, выполнение программы прерывается, и Python ищет обработчик ошибок, чтобы решить проблему.

---

#### 2. **Основная конструкция: try-except**

Для обработки исключений в Python используется конструкция `try-except`:

```python
try:
    # Код, который может вызвать исключение
    x = 1 / 0  # Деление на ноль вызовет исключение
except ZeroDivisionError:
    # Код, который выполняется при возникновении исключения
    print("Ошибка: Деление на ноль!")
```

- **try**: блок кода, в котором может возникнуть исключение.
- **except**: блок, который перехватывает и обрабатывает исключения.

---

#### 3. **Обработка нескольких типов исключений**

Можно указать несколько типов исключений для обработки:

```python
try:
    x = int(input("Введите число: "))
    y = 10 / x
except ZeroDivisionError:
    print("Ошибка: Деление на ноль.")
except ValueError:
    print("Ошибка: Введено не число.")
```

Если возникает несколько ошибок, Python будет проверять их по порядку.

---

#### 4. **Использование блока `else`**

Блок `else` выполняется, если в блоке `try` не было ошибок:

```python
try:
    x = int(input("Введите число: "))
    y = 10 / x
except ZeroDivisionError:
    print("Ошибка: Деление на ноль.")
except ValueError:
    print("Ошибка: Введено не число.")
else:
    print(f"Результат деления: {y}")
```

Блок `else` полезен для выполнения кода, который должен выполняться только в случае успеха.

---

#### 5. **Использование блока `finally`**

Блок `finally` выполняется всегда, независимо от того, было ли исключение или нет. Это полезно для выполнения операций очистки или закрытия ресурсов (например, файлов или соединений с базой данных).

```python
try:
    file = open("data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("Ошибка: файл не найден.")
else:
    print("Файл успешно открыт.")
finally:
    file.close()
    print("Файл закрыт.")
```

---

#### 6. **Поднятие исключений с помощью `raise`**

Если в программе возникает ситуация, в которой нужно явно поднять исключение, можно использовать конструкцию `raise`:

```python
def check_age(age):
    if age < 0:
        raise ValueError("Возраст не может быть отрицательным!")
    print(f"Возраст: {age}")

try:
    check_age(-5)
except ValueError as e:
    print(f"Ошибка: {e}")
```

`raise` позволяет не только поднять стандартные исключения, но и создавать собственные исключения, наследуя их от класса `Exception`.

---

#### 7. **Исключения и пользовательские ошибки**

Для создания пользовательских исключений нужно определить свой класс, который будет наследовать от `Exception`:

```python
class NegativeAgeError(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

def check_age(age):
    if age < 0:
        raise NegativeAgeError("Возраст не может быть отрицательным!")
    print(f"Возраст: {age}")

try:
    check_age(-5)
except NegativeAgeError as e:
    print(f"Ошибка: {e}")
```

---

#### 8. **Зачем использовать обработку исключений?**

- Обработка исключений позволяет избежать аварийного завершения программы.
- Помогает информировать пользователя о проблемах и предоставляет возможность для их исправления.
- Обеспечивает чистоту кода и улучшает его читаемость.
- Позволяет контролировать выполнение программы в случае ошибок.

---

#### 9. **Резюме**

- **try-except**: используется для перехвата и обработки ошибок.
- **else**: выполняется, если исключений не было.
- **finally**: выполняется всегда, используется для очистки ресурсов.
- **raise**: позволяет поднять исключение вручную.
- Пользовательские исключения помогают более точно управлять ошибками.

Обработка исключений в Python — это мощный инструмент для написания надежных и безопасных программ, особенно в сложных проектах с большим количеством возможных ошибок.

---

---

---

### Лекция: Взаимодействие с файлами данных в Python

Работа с файлами — одна из основополагающих задач в программировании, и Python предоставляет удобные инструменты для чтения, записи и манипуляции файлами. В этом разделе рассмотрим основные способы взаимодействия с файлами в Python.

---

Файл — это именованное место на диске, предназначенное для хранения данных. Он используется для долговременного сохранения информации в энергонезависимой памяти, например, на жестком диске.

Оперативная память (RAM) является энергозависимой, то есть теряет данные при выключении компьютера. Поэтому для сохранения информации, которую необходимо использовать и после перезагрузки, мы обращаемся к файлам.

Для удобства доступа и организации файлов они группируются в папки (директории).

---

Файлы в каталоге (папке) можно просматривать с помощью различных инструментов и методов. В Python для этого используются модули, такие как `os` и `glob`, а также встроенные команды операционной системы.

1. **Использование модуля `os`**:

   Модуль `os` предоставляет функции для работы с операционной системой, включая управление файлами и каталогами. Для просмотра файлов в текущем каталоге используется функция `os.listdir()`:

   ```python
   import os

   files = os.listdir()  # Список файлов в текущем каталоге
   print(files)
   ```

   Также можно указать путь к конкретному каталогу:

   ```python
   files = os.listdir('/path/to/directory')
   print(files)
   ```

2. **Использование модуля `glob`**:

   Модуль `glob` позволяет находить все пути, соответствующие определенному шаблону. Это полезно, если нужно найти все файлы с определенным расширением или соответствующие регулярному выражению:

   ```python
   import glob

   files = glob.glob('*.txt')  # Все файлы с расширением .txt в текущем каталоге
   print(files)
   ```

3. **Просмотр файлов с помощью команд операционной системы**:

   В командной строке или терминале можно использовать команды для просмотра содержимого каталогов:
   - В Windows: `dir`
   - В Linux/macOS: `ls`

---

### Создание нового подкаталога

Для создания нового подкаталога в Python используется функция `os.mkdir()` или `os.makedirs()`. 

- **`os.mkdir()`** создаёт один подкаталог:
  ```python
  import os

  os.mkdir('new_directory')  # Создание нового подкаталога
  ```

- **`os.makedirs()`** позволяет создавать несколько уровней подкаталогов, если они не существуют:
  ```python
  import os

  os.makedirs('parent_directory/child_directory')  # Создание вложенной структуры папок
  ```

Если подкаталог уже существует, то возникнет ошибка, если не использовать обработку ошибок или параметр `exist_ok=True` в функции `makedirs`:
```python
os.makedirs('new_directory', exist_ok=True)  # Если каталог существует, ошибки не будет
```

---

### Поиск определённых файлов в каталоге

Для поиска конкретных файлов в каталоге можно использовать модуль `os` для перебора файлов с помощью `os.listdir()` или `os.walk()`.

1. **Использование `os.listdir()`**:
   Функция `os.listdir()` возвращает список всех файлов и каталогов в указанном каталоге. Затем можно применить фильтрацию для поиска конкретных файлов.

   ```python
   import os

   files = os.listdir('/path/to/directory')
   for file in files:
       if file.endswith('.txt'):  # Пример поиска всех текстовых файлов
           print(file)
   ```

2. **Использование `os.walk()`**:
   Функция `os.walk()` рекурсивно проходит по всем подкаталогам и возвращает путь к каждому файлу. Это полезно для поиска файлов в каталогах с вложенными папками.

   ```python
   import os

   for dirpath, dirnames, filenames in os.walk('/path/to/directory'):
       for filename in filenames:
           if filename.endswith('.txt'):
               print(os.path.join(dirpath, filename))
   ```

---

### Поиск файлов на основе шаблонов

Для поиска файлов, соответствующих определённому шаблону (например, все файлы с расширением `.txt` или с определённой частью имени), можно использовать модуль `glob`. Этот модуль поддерживает использование шаблонов с символами подстановки (например, `*` и `?`).

1. **Поиск файлов с шаблонами с помощью `glob`**:

   ```python
   import glob

   files = glob.glob('/path/to/directory/*.txt')  # Все .txt файлы в каталоге
   for file in files:
       print(file)
   ```

   - `*` — соответствует любому количеству символов (включая ноль).
   - `?` — соответствует любому одному символу.

2. **Рекурсивный поиск с `glob`**:
   Для поиска файлов в подкаталогах с использованием шаблонов можно использовать рекурсивный режим с `**`:

   ```python
   files = glob.glob('/path/to/directory/**/*.txt', recursive=True)  # Поиск в подкаталогах
   for file in files:
       print(file)
   ```

Это позволяет гибко искать файлы в каталоге на основе шаблонов, что полезно для работы с большими структурами каталогов.

---

В Python существует несколько функций для создания, чтения, обновления и удаления файлов.

Для того чтобы прочитать данные из файла или записать в него, сначала необходимо открыть файл. По завершении работы с файлом его нужно закрыть, чтобы освободить ресурсы, связанные с файлом.

Таким образом, операции с файлами в Python выполняются в следующем порядке:

- Открытие файла.
- Чтение или запись (выполнение операций с содержимым файла).
- Закрытие файла.


---

#### 1. **Открытие файлов**

Для работы с файлами в Python используется встроенная функция `open()`. Она открывает файл и возвращает объект файла, который используется для чтения, записи или модификации данных.

```python
file = open('example.txt', 'r')  # Открытие файла для чтения (read)
```

Режимы открытия файла:
- `'r'`: чтение (read). Файл должен существовать.
- `'w'`: запись (write). Создает новый файл или очищает существующий.
- `'a'`: добавление (append). Данные добавляются в конец файла.
- `'b'`: бинарный режим (binary). Например, для работы с изображениями.
- `'x'`: создание нового файла. Ошибка, если файл уже существует.
- `'t'`: текстовый режим (text, по умолчанию).

Пример:
```python
file = open('example.txt', 'w')  # Открытие файла для записи
file.write("Hello, world!")  # Запись строки в файл
file.close()  # Закрытие файла
```

Важно: всегда закрывать файл после завершения работы с ним, чтобы избежать утечек ресурсов.

---

#### 2. **Чтение данных из файлов**

После того как файл открыт в режиме чтения, можно использовать несколько методов для извлечения данных:

- **`read()`** — считывает все содержимое файла как строку:
  ```python
  file = open('example.txt', 'r')
  content = file.read()
  print(content)
  file.close()
  ```

- **`readline()`** — считывает одну строку:
  ```python
  file = open('example.txt', 'r')
  line = file.readline()  # Читает одну строку
  print(line)
  file.close()
  ```

- **`readlines()`** — считывает все строки и возвращает их в виде списка:
  ```python
  file = open('example.txt', 'r')
  lines = file.readlines()  # Читает все строки
  print(lines)
  file.close()
  ```

---

#### 3. **Запись данных в файлы**

Для записи данных в файл используется метод `write()` или `writelines()`:

- **`write()`** — записывает строку:
  ```python
  file = open('example.txt', 'w')
  file.write("Hello, world!")  # Запись одной строки
  file.close()
  ```

- **`writelines()`** — записывает список строк:
  ```python
  file = open('example.txt', 'w')
  lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
  file.writelines(lines)  # Запись нескольких строк
  file.close()
  ```

---

#### 4. **Использование менеджера контекста (`with`)**

Открытие и закрытие файлов вручную может быть источником ошибок, если не закрыть файл вовремя. Чтобы избежать этой проблемы, можно использовать конструкцию `with`, которая автоматически закрывает файл после завершения работы с ним:

```python
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
```

Этот подход гарантирует, что файл будет закрыт, даже если в процессе работы возникнет ошибка.


---

В Python можно работать с различными типами файлов, каждый из которых имеет свои особенности. Все эти файлы можно разделить на несколько категорий в зависимости от их содержания и формата:

### 1. **Текстовые файлы**

Текстовые файлы содержат данные в виде обычного текста. Каждая строка в таком файле является последовательностью символов, и файлы можно открыть и прочитать как обычный текст.

- **Расширение**: `.txt`, `.csv`, `.json`, `.log`, `.xml` и другие.
- **Пример**: текстовые данные, CSV, JSON и XML файлы.

В Python для работы с текстовыми файлами можно использовать стандартные функции:
```python
with open('file.txt', 'r') as file:
    content = file.read()
    print(content)
```

#### Пример работы с CSV:
```python
import csv

with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

#### Пример работы с JSON:
```python
import json

with open('data.json', 'r') as file:
    data = json.load(file)
    print(data)
```

---

### 2. **Бинарные файлы**

Бинарные файлы содержат данные в не текстовом формате, например, изображения, видео или аудио. Эти файлы могут содержать любые двоичные данные, которые не следует интерпретировать как текст.

- **Расширение**: `.jpg`, `.png`, `.gif`, `.mp4`, `.mp3`, `.bin`, `.exe`, и другие.
- **Пример**: изображения, видео, аудио, архивы.

Для работы с бинарными файлами в Python используют режим `'rb'` (чтение) и `'wb'` (запись):

```python
with open('image.jpg', 'rb') as file:
    binary_data = file.read()

with open('output.jpg', 'wb') as file:
    file.write(binary_data)
```

---

### 3. **Файлы CSV (Comma-Separated Values)**

Файлы CSV представляют собой текстовые файлы, в которых данные разделены запятыми (или другими разделителями, такими как точка с запятой). CSV часто используется для хранения таблиц, данных в строках и столбцах.

- **Расширение**: `.csv`
- **Пример**: таблицы данных.

Работа с CSV-файлами в Python часто выполняется с помощью модуля `csv`:
```python
import csv

# Чтение CSV
with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Запись в CSV
with open('output.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Name', 'Age'])
    writer.writerow(['Alice', 30])
```

---

### 4. **JSON (JavaScript Object Notation)**

JSON — это текстовый формат, используемый для хранения данных в виде объектов. Он широко используется в веб-программировании и взаимодействии с API. JSON представляет собой текстовые данные в формате ключ-значение.

- **Расширение**: `.json`
- **Пример**: обмен данными между сервером и клиентом.

Для работы с JSON в Python используется модуль `json`:
```python
import json

# Чтение JSON
with open('data.json', 'r') as file:
    data = json.load(file)
    print(data)

# Запись в JSON
data = {"name": "Alice", "age": 30}
with open('output.json', 'w') as file:
    json.dump(data, file)
```

---

### 5. **XML (Extensible Markup Language)**

XML используется для представления данных в иерархической структуре. Он представляет собой текстовый формат с тегами, похожими на HTML. Часто используется для хранения структурированных данных и обмена данными между приложениями.

- **Расширение**: `.xml`
- **Пример**: обмен данными между системами, конфигурационные файлы.

Для работы с XML в Python можно использовать стандартные библиотеки, такие как `xml.etree.ElementTree`:
```python
import xml.etree.ElementTree as ET

# Чтение XML
tree = ET.parse('data.xml')
root = tree.getroot()

# Выводим элементы
for child in root:
    print(child.tag, child.attrib)

# Запись в XML
data = ET.Element("root")
child = ET.SubElement(data, "child", name="Alice")
tree = ET.ElementTree(data)
tree.write("output.xml")
```

---

### 6. **Лог-файлы**

Лог-файлы — это текстовые файлы, которые часто используются для хранения записей о событиях в приложении или системе. Лог-файлы могут содержать данные о времени, типе события и других параметрах.

- **Расширение**: `.log`
- **Пример**: системные журналы, журналы приложений.

Обычно для работы с лог-файлами используют обычное чтение и запись, как с текстовыми файлами:
```python
with open('app.log', 'r') as file:
    for line in file:
        print(line.strip())
```

---

### 7. **Файлы SQLite (базы данных)**

SQLite — это легковесная база данных, которая хранит данные в одном файле. Она используется для хранения данных в небольших приложениях.

- **Расширение**: `.sqlite`, `.db`
- **Пример**: локальные базы данных.

Для работы с SQLite в Python используется модуль `sqlite3`:
```python
import sqlite3

# Подключение к базе данных
conn = sqlite3.connect('database.db')
cursor = conn.cursor()

# Выполнение SQL-запроса
cursor.execute('SELECT * FROM users')
rows = cursor.fetchall()
for row in rows:
    print(row)

# Закрытие соединения
conn.close()
```

---

### 8. **Архивы (например, ZIP)**

Архивы используются для хранения нескольких файлов в одном файле с возможностью сжатия. Часто применяются для упаковки и передачи данных.

- **Расширение**: `.zip`, `.tar`, `.gz`
- **Пример**: сжатые файлы.

Для работы с архивами в Python можно использовать модуль `zipfile` для формата ZIP:
```python
import zipfile

# Создание архива
with zipfile.ZipFile('archive.zip', 'w') as zipf:
    zipf.write('file.txt')

# Извлечение из архива
with zipfile.ZipFile('archive.zip', 'r') as zipf:
    zipf.extractall('extracted_folder')
```

---

#### 9. **Обработка ошибок при работе с файлами**

При работе с файлами могут возникать ошибки, такие как отсутствие файла или проблемы с правами доступа. Чтобы обработать такие ошибки, можно использовать конструкцию `try-except`:

```python
try:
    with open('nonexistent_file.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print("Ошибка: файл не найден!")
except IOError:
    print("Ошибка ввода-вывода!")
```

---

### Заключение

Python предоставляет широкий спектр возможностей для работы с различными типами файлов: текстовыми, бинарными, CSV, JSON, XML, логами, SQLite и архивами. Выбор подходящего типа файла зависит от задач, которые необходимо решить, а также от формата данных, с которыми предстоит работать.
