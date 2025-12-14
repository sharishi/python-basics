# **Gestionarea excepțiilor și interacțiunea cu fișierele de date în Python**

---

## **Gestionarea excepțiilor**

Gestionarea excepțiilor este un aspect esențial al dezvoltării software, care ajută la controlul erorilor din program și previne terminarea neașteptată a acestuia. În Python, acest lucru se realizează cu ajutorul construcției `try-except`, precum și prin elemente suplimentare precum `finally`, `else` și `raise`, care oferă o gestionare mai flexibilă și mai robustă a erorilor.

---

### **1. Ce sunt excepțiile?**

O **excepție** este un eveniment care apare atunci când survine o eroare în program, de exemplu: împărțirea la zero, introducerea unor date invalide sau lipsa unui fișier necesar. Atunci când apare o excepție, execuția normală a programului este întreruptă, iar Python caută un mecanism de tratare a erorii.

---

### **2. Construcția de bază: `try-except`**

Pentru gestionarea excepțiilor în Python se utilizează construcția `try-except`:

```python
try:
    # Cod care poate genera o excepție
    x = 1 / 0  # Împărțirea la zero va genera o excepție
except ZeroDivisionError:
    # Cod executat în cazul apariției excepției
    print("Eroare: împărțire la zero!")
```

* **`try`**: blocul de cod în care poate apărea o excepție.
* **`except`**: blocul care interceptează și tratează excepția.

---

### **3. Tratarea mai multor tipuri de excepții**

Este posibil să specificăm mai multe tipuri de excepții care pot fi tratate:

```python
try:
    x = int(input("Introduceți un număr: "))
    y = 10 / x
except ZeroDivisionError:
    print("Eroare: împărțire la zero.")
except ValueError:
    print("Eroare: valoare introdusă invalidă (nu este un număr).")
```

Python verifică excepțiile în ordinea în care sunt definite.

---

### **4. Utilizarea blocului `else`**

Blocul `else` se execută doar dacă în blocul `try` nu a apărut nicio eroare:

```python
try:
    x = int(input("Introduceți un număr: "))
    y = 10 / x
except ZeroDivisionError:
    print("Eroare: împărțire la zero.")
except ValueError:
    print("Eroare: valoare introdusă invalidă.")
else:
    print(f"Rezultatul împărțirii: {y}")
```

Blocul `else` este util pentru codul care trebuie rulat exclusiv în cazul unei execuții reușite.

---

### **5. Utilizarea blocului `finally`**

Blocul `finally` se execută **întotdeauna**, indiferent dacă a apărut sau nu o excepție. Este frecvent utilizat pentru eliberarea resurselor (închiderea fișierelor, conexiunilor la baze de date etc.).

```python
try:
    file = open("data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("Eroare: fișierul nu a fost găsit.")
else:
    print("Fișierul a fost deschis cu succes.")
finally:
    file.close()
    print("Fișierul a fost închis.")
```

---

### **6. Ridicarea excepțiilor cu `raise`**

În anumite situații este necesar să generăm manual o excepție folosind `raise`:

```python
def check_age(age):
    if age < 0:
        raise ValueError("Vârsta nu poate fi negativă!")
    print(f"Vârsta: {age}")

try:
    check_age(-5)
except ValueError as e:
    print(f"Eroare: {e}")
```

Instrucțiunea `raise` poate fi utilizată atât pentru excepții standard, cât și pentru excepții personalizate.

---

### **7. Excepții personalizate (custom exceptions)**

Pentru a crea excepții proprii, se definește o clasă care moștenește din `Exception`:

```python
class NegativeAgeError(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

def check_age(age):
    if age < 0:
        raise NegativeAgeError("Vârsta nu poate fi negativă!")
    print(f"Vârsta: {age}")

try:
    check_age(-5)
except NegativeAgeError as e:
    print(f"Eroare: {e}")
```

Excepțiile personalizate oferă un control mai precis asupra tipurilor de erori din aplicație.

---

### **8. De ce este importantă gestionarea excepțiilor?**

* Previne terminarea bruscă a programului.
* Oferă mesaje clare utilizatorului despre problemele apărute.
* Îmbunătățește lizibilitatea și structura codului.
* Permite controlul logicii aplicației în situații neprevăzute.

---

### **9. Rezumat**

* **`try-except`** – interceptează și tratează erorile.
* **`else`** – se execută dacă nu apare nicio excepție.
* **`finally`** – se execută întotdeauna, ideal pentru curățarea resurselor.
* **`raise`** – ridică manual o excepție.
* **Excepțiile personalizate** – permit gestionarea specifică a erorilor.

Gestionarea excepțiilor în Python este un instrument puternic pentru dezvoltarea unor aplicații sigure, stabile și ușor de întreținut, în special în proiecte complexe unde pot apărea numeroase situații de eroare.


### **Prelegere: Interacțiunea cu fișierele de date în Python**

Lucrul cu fișierele este una dintre sarcinile fundamentale în programare, iar Python oferă instrumente convenabile pentru citirea, scrierea și manipularea fișierelor. În această secțiune vom analiza principalele modalități de interacțiune cu fișierele în Python.

---

Un fișier este un loc denumit de pe disc, destinat stocării datelor. Acesta este utilizat pentru păstrarea pe termen lung a informațiilor în memorie nevolatilă, de exemplu pe hard disk.

Memoria operativă (RAM) este volatilă, adică își pierde datele la oprirea calculatorului. De aceea, pentru a păstra informațiile care trebuie utilizate și după repornire, apelăm la fișiere.

Pentru a facilita accesul și organizarea fișierelor, acestea sunt grupate în foldere (directoare).

---

Fișierele dintr-un catalog (folder) pot fi vizualizate cu ajutorul diferitelor instrumente și metode. În Python, pentru acest lucru sunt utilizate module precum `os` și `glob`, precum și comenzile integrate ale sistemului de operare.

1. **Utilizarea modulului `os`**:

   Modulul `os` oferă funcții pentru lucrul cu sistemul de operare, inclusiv gestionarea fișierelor și directoarelor. Pentru a vizualiza fișierele din directorul curent se utilizează funcția `os.listdir()`:

   ```python
   import os

   files = os.listdir()  # Lista fișierelor din directorul curent
   print(files)
   ```

   De asemenea, se poate specifica o cale către un director concret:

   ```python
   files = os.listdir('/path/to/directory')
   print(files)
   ```

2. **Utilizarea modulului `glob`**:

   Modulul `glob` permite găsirea tuturor căilor care corespund unui anumit șablon. Acest lucru este util dacă este necesar să găsim toate fișierele cu o anumită extensie sau care corespund unui model specific:

   ```python
   import glob

   files = glob.glob('*.txt')  # Toate fișierele cu extensia .txt din directorul curent
   print(files)
   ```

3. **Vizualizarea fișierelor cu ajutorul comenzilor sistemului de operare**:

   În linia de comandă sau terminal pot fi utilizate comenzi pentru afișarea conținutului directoarelor:

   * În Windows: `dir`
   * În Linux/macOS: `ls`

---

### **Crearea unui subdirector nou**

Pentru crearea unui subdirector nou în Python se utilizează funcția `os.mkdir()` sau `os.makedirs()`.

* **`os.mkdir()`** creează un singur subdirector:

  ```python
  import os

  os.mkdir('new_directory')  # Crearea unui subdirector nou
  ```

* **`os.makedirs()`** permite crearea mai multor niveluri de subdirectoare, dacă acestea nu există:

  ```python
  import os

  os.makedirs('parent_directory/child_directory')  # Crearea unei structuri de foldere imbricate
  ```

Dacă subdirectorul există deja, va apărea o eroare, dacă nu se utilizează tratarea erorilor sau parametrul `exist_ok=True` în funcția `makedirs`:

```python
os.makedirs('new_directory', exist_ok=True)  # Dacă directorul există, nu va apărea eroare
```

---

### **Căutarea anumitor fișiere într-un director**

Pentru a căuta fișiere concrete într-un director se poate utiliza modulul `os` pentru parcurgerea fișierelor cu ajutorul `os.listdir()` sau `os.walk()`.

1. **Utilizarea `os.listdir()`**:
   Funcția `os.listdir()` returnează o listă cu toate fișierele și directoarele dintr-un director specificat. Apoi se poate aplica filtrarea pentru a găsi fișierele dorite.

   ```python
   import os

   files = os.listdir('/path/to/directory')
   for file in files:
       if file.endswith('.txt'):  # Exemplu de căutare a tuturor fișierelor text
           print(file)
   ```

2. **Utilizarea `os.walk()`**:
   Funcția `os.walk()` parcurge recursiv toate subdirectoarele și returnează calea către fiecare fișier. Este utilă pentru căutarea fișierelor în structuri de directoare complexe.

   ```python
   import os

   for dirpath, dirnames, filenames in os.walk('/path/to/directory'):
       for filename in filenames:
           if filename.endswith('.txt'):
               print(os.path.join(dirpath, filename))
   ```

---

### **Căutarea fișierelor pe baza șabloanelor**

Pentru a căuta fișiere care corespund unui anumit șablon (de exemplu, toate fișierele cu extensia `.txt` sau care conțin o anumită parte în nume), se poate utiliza modulul `glob`. Acest modul suportă șabloane cu caractere joker (de exemplu, `*` și `?`).

1. **Căutarea fișierelor cu șabloane folosind `glob`**:

   ```python
   import glob

   files = glob.glob('/path/to/directory/*.txt')  # Toate fișierele .txt din director
   for file in files:
       print(file)
   ```

   * `*` — corespunde oricărui număr de caractere (inclusiv zero).
   * `?` — corespunde unui singur caracter.

2. **Căutare recursivă cu `glob`**:
   Pentru a căuta fișiere în subdirectoare utilizând șabloane se poate folosi modul recursiv cu `**`:

   ```python
   files = glob.glob('/path/to/directory/**/*.txt', recursive=True)  # Căutare în subdirectoare
   for file in files:
       print(file)
   ```

Acest lucru permite căutarea flexibilă a fișierelor într-un director pe baza șabloanelor, fiind foarte util pentru lucrul cu structuri mari de directoare.

---

În Python există mai multe funcții pentru crearea, citirea, actualizarea și ștergerea fișierelor.

Pentru a citi date dintr-un fișier sau a scrie în acesta, este necesar mai întâi să deschidem fișierul. După finalizarea lucrului cu fișierul, acesta trebuie închis pentru a elibera resursele asociate.

Astfel, operațiile cu fișierele în Python se desfășoară în următoarea ordine:

* Deschiderea fișierului.
* Citirea sau scrierea (efectuarea operațiilor asupra conținutului fișierului).
* Închiderea fișierului.

---

### **1. Deschiderea fișierelor**

Pentru lucrul cu fișierele în Python se utilizează funcția încorporată `open()`. Aceasta deschide fișierul și returnează un obiect fișier, care este utilizat pentru citirea, scrierea sau modificarea datelor.

```python
file = open('example.txt', 'r')  # Deschiderea fișierului pentru citire (read)
```

Modurile de deschidere a fișierului:

* `'r'`: citire (read). Fișierul trebuie să existe.
* `'w'`: scriere (write). Creează un fișier nou sau golește fișierul existent.
* `'a'`: adăugare (append). Datele sunt adăugate la sfârșitul fișierului.
* `'b'`: mod binar (binary). De exemplu, pentru lucrul cu imagini.
* `'x'`: crearea unui fișier nou. Eroare dacă fișierul există deja.
* `'t'`: mod text (text, implicit).

Exemplu:

```python
file = open('example.txt', 'w')  # Deschiderea fișierului pentru scriere
file.write("Hello, world!")  # Scrierea unui șir de caractere în fișier
file.close()  # Închiderea fișierului
```

Important: fișierul trebuie întotdeauna închis după terminarea lucrului cu acesta, pentru a evita scurgerile de resurse.

---
#### 2. **Citirea datelor din fișiere**

După ce fișierul este deschis în modul de citire, pot fi utilizate mai multe metode pentru extragerea datelor:

* **`read()`** — citește întregul conținut al fișierului ca un șir de caractere:

  ```python
  file = open('example.txt', 'r')
  content = file.read()
  print(content)
  file.close()
  ```

* **`readline()`** — citește o singură linie:

  ```python
  file = open('example.txt', 'r')
  line = file.readline()  # Citește o singură linie
  print(line)
  file.close()
  ```

* **`readlines()`** — citește toate liniile și le returnează sub formă de listă:

  ```python
  file = open('example.txt', 'r')
  lines = file.readlines()  # Citește toate liniile
  print(lines)
  file.close()
  ```

---

#### 3. **Scrierea datelor în fișiere**

Pentru scrierea datelor într-un fișier se utilizează metoda `write()` sau `writelines()`:

* **`write()`** — scrie un șir de caractere:

  ```python
  file = open('example.txt', 'w')
  file.write("Hello, world!")  # Scrierea unei singure linii
  file.close()
  ```

* **`writelines()`** — scrie o listă de șiruri de caractere:

  ```python
  file = open('example.txt', 'w')
  lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
  file.writelines(lines)  # Scrierea mai multor linii
  file.close()
  ```

---

#### 4. **Utilizarea managerului de context (`with`)**

Deschiderea și închiderea manuală a fișierelor poate fi o sursă de erori, dacă fișierul nu este închis la timp. Pentru a evita această problemă, se poate utiliza construcția `with`, care închide automat fișierul după finalizarea lucrului cu acesta:

```python
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
```

Această abordare garantează că fișierul va fi închis, chiar dacă în timpul lucrului apare o eroare.

---

În Python se poate lucra cu diferite tipuri de fișiere, fiecare având propriile sale particularități. Toate aceste fișiere pot fi împărțite în mai multe categorii, în funcție de conținutul și formatul lor:

### 1. **Fișiere text**

Fișierele text conțin date sub formă de text obișnuit. Fiecare linie dintr-un astfel de fișier este o secvență de caractere, iar fișierele pot fi deschise și citite ca text obișnuit.

* **Extensie**: `.txt`, `.csv`, `.json`, `.log`, `.xml` și altele.
* **Exemplu**: date text, fișiere CSV, JSON și XML.

În Python, pentru lucrul cu fișiere text se pot utiliza funcțiile standard:

```python
with open('file.txt', 'r') as file:
    content = file.read()
    print(content)
```

#### Exemplu de lucru cu CSV:

```python
import csv

with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

#### Exemplu de lucru cu JSON:

```python
import json

with open('data.json', 'r') as file:
    data = json.load(file)
    print(data)
```

---

### 2. **Fișiere binare**

Fișierele binare conțin date într-un format non-text, de exemplu imagini, video sau audio. Aceste fișiere pot conține orice date binare, care nu trebuie interpretate ca text.

* **Extensie**: `.jpg`, `.png`, `.gif`, `.mp4`, `.mp3`, `.bin`, `.exe` și altele.
* **Exemplu**: imagini, video, audio, arhive.

Pentru lucrul cu fișiere binare în Python se utilizează modul `'rb'` (citire) și `'wb'` (scriere):

```python
with open('image.jpg', 'rb') as file:
    binary_data = file.read()

with open('output.jpg', 'wb') as file:
    file.write(binary_data)
```

---

### 3. **Fișiere CSV (Comma-Separated Values)**

Fișierele CSV reprezintă fișiere text, în care datele sunt separate prin virgule (sau alți separatori, cum ar fi punct și virgulă). CSV este utilizat frecvent pentru stocarea tabelelor, a datelor în rânduri și coloane.

* **Extensie**: `.csv`
* **Exemplu**: tabele de date.

Lucrul cu fișiere CSV în Python se realizează frecvent cu ajutorul modulului `csv`:

```python
import csv

# Citirea CSV
with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)

# Scrierea în CSV
with open('output.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Name', 'Age'])
    writer.writerow(['Alice', 30])
```

---
### 4. **JSON (JavaScript Object Notation)**

JSON — este un format text utilizat pentru stocarea datelor sub formă de obiecte. Este folosit pe scară largă în programarea web și pentru interacțiunea cu API-uri. JSON reprezintă date textuale în format cheie-valoare.

* **Extensie**: `.json`
* **Exemplu**: schimbul de date între server și client.

Pentru lucrul cu JSON în Python se folosește modulul `json`:

```python
import json

# Citirea JSON
with open('data.json', 'r') as file:
    data = json.load(file)
    print(data)

# Scrierea în JSON
data = {"name": "Alice", "age": 30}
with open('output.json', 'w') as file:
    json.dump(data, file)
```

---

### 5. **XML (Extensible Markup Language)**

XML este folosit pentru reprezentarea datelor într-o structură ierarhică. Reprezintă un format text cu etichete, similar cu HTML. Este folosit frecvent pentru stocarea datelor structurate și schimbul de informații între aplicații.

* **Extensie**: `.xml`
* **Exemplu**: schimbul de date între sisteme, fișiere de configurare.

Pentru lucrul cu XML în Python se pot folosi biblioteci standard, cum ar fi `xml.etree.ElementTree`:

```python
import xml.etree.ElementTree as ET

# Citirea XML
tree = ET.parse('data.xml')
root = tree.getroot()

# Afișarea elementelor
for child in root:
    print(child.tag, child.attrib)

# Scrierea în XML
data = ET.Element("root")
child = ET.SubElement(data, "child", name="Alice")
tree = ET.ElementTree(data)
tree.write("output.xml")
```

---

### 6. **Fișiere log**

Fișierele log sunt fișiere text, folosite frecvent pentru stocarea înregistrărilor despre evenimente într-o aplicație sau sistem. Fișierele log pot conține informații despre timp, tipul evenimentului și alți parametri.

* **Extensie**: `.log`
* **Exemplu**: jurnale de sistem, jurnale de aplicație.

De obicei, pentru lucrul cu fișierele log se folosește citirea și scrierea obișnuită, ca la fișiere text:

```python
with open('app.log', 'r') as file:
    for line in file:
        print(line.strip())
```

---

### 7. **Fișiere SQLite (baze de date)**

SQLite este o bază de date ușoară, care stochează datele într-un singur fișier. Este utilizată pentru stocarea datelor în aplicații mici.

* **Extensie**: `.sqlite`, `.db`
* **Exemplu**: baze de date locale.

Pentru lucrul cu SQLite în Python se folosește modulul `sqlite3`:

```python
import sqlite3

# Conectarea la baza de date
conn = sqlite3.connect('database.db')
cursor = conn.cursor()

# Executarea unei interogări SQL
cursor.execute('SELECT * FROM users')
rows = cursor.fetchall()
for row in rows:
    print(row)

# Închiderea conexiunii
conn.close()
```

---

### 8. **Arhive (de exemplu, ZIP)**

Arhivele sunt folosite pentru stocarea mai multor fișiere într-un singur fișier, cu posibilitate de compresie. Sunt utilizate frecvent pentru împachetarea și transferul datelor.

* **Extensie**: `.zip`, `.tar`, `.gz`
* **Exemplu**: fișiere comprimate.

Pentru lucrul cu arhivele în Python se poate folosi modulul `zipfile` pentru formatul ZIP:

```python
import zipfile

# Crearea unei arhive
with zipfile.ZipFile('archive.zip', 'w') as zipf:
    zipf.write('file.txt')

# Extracția din arhivă
with zipfile.ZipFile('archive.zip', 'r') as zipf:
    zipf.extractall('extracted_folder')
```

---

#### 9. **Gestionarea erorilor la lucrul cu fișierele**

La lucrul cu fișierele pot apărea erori, cum ar fi lipsa fișierului sau probleme de permisiuni. Pentru a gestiona astfel de erori, se poate folosi construcția `try-except`:

```python
try:
    with open('nonexistent_file.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print("Eroare: fișierul nu a fost găsit!")
except IOError:
    print("Eroare de intrare-ieșire!")
```

---

### Concluzie

Python oferă un spectru larg de posibilități pentru lucrul cu diferite tipuri de fișiere: text, binar, CSV, JSON, XML, loguri, SQLite și arhive. Alegerea tipului potrivit de fișier depinde de sarcinile care trebuie rezolvate și de formatul datelor cu care se lucrează.
