# Lecție: Lucrul cu SQLite în Python

## Introducere

Bună ziua! Astăzi vom analiza lucrul practic cu baze de date în Python. Scopul nostru este să învățăm să creăm baze de date, tabele și să efectuăm operațiuni de bază asupra datelor folosind funcționalitățile încorporate ale Python.

---

## 1. De ce sunt necesare bazele de date?

Imaginați-vă că dezvoltați o aplicație pentru evidența studenților. Puteți stoca datele în fișiere obișnuite, de exemplu text sau JSON. Însă apar probleme importante:

**Problema 1: Performanța**
Dacă aveți 50.000 de înregistrări și trebuie să găsiți un student după numărul matricol — va trebui să parcurgeți întregul fișier linie cu linie. Este lent.

**Problema 2: Structura datelor**
Într-un fișier text nu există o separare clară pe câmpuri. Este ușor să apară erori în format, iar datele devin greu de citit.

**Problema 3: Integritatea datelor**
Dacă două procese încearcă să modifice fișierul simultan, unul poate suprascrie modificările celuilalt. Datele se pot corupe.

**Problema 4: Lipsa unui limbaj de interogare**
Pentru a găsi „toți studenții peste 20 de ani”, trebuie să scrieți cod manual, să parcurgeți liniile și să verificați condițiile.

Bazele de date rezolvă toate aceste probleme oferind:

* căutare rapidă prin indici
* structură strictă (tabele cu tipuri de date)
* mecanisme de blocare pentru acces multi-utilizator
* limbaj de interogare (SQL) pentru filtrare și selecție

---

## 2. Ce este SQLite?

SQLite este o bază de date ușoară care:

* se stochează **într-un singur fișier** pe disc
* **nu necesită instalarea** unui server separat
* este **încorporată** în Python implicit
* este folosită în aplicații mobile, browsere, jocuri

Spre deosebire de SGBD-uri mari (PostgreSQL, MySQL), SQLite nu funcționează ca server separat. Este o bibliotecă care citește și scrie date direct în fișier.

**Când să folosești SQLite:**

* aplicații locale
* prototipuri
* baze încorporate în programe
* volume mici de date (până la câțiva gigabyți)

**Când NU să folosești SQLite:**

* aplicații web cu încărcare mare și mii de utilizatori simultan
* sisteme distribuite

---

## 3. Conectarea la baza de date în Python

### 3.1. Importarea modulului

Python conține un modul încorporat pentru SQLite:

```python
import sqlite3
```

Nu este necesară nicio instalare suplimentară.

### 3.2. Crearea conexiunii

Pentru a lucra cu baza, trebuie să creăm o **conexiune (connection)**:

```python
import sqlite3

# Creăm conexiunea cu baza de date
# Dacă fișierul nu există, SQLite îl va crea automat
conn = sqlite3.connect("university.db")

print("Conexiune realizată")
```

**Ce se întâmplă?**

* Dacă fișierul `university.db` nu există, va fi creat
* Dacă există, Python îl va deschide
* Variabila `conn` conține obiectul conexiunii

### 3.3. Crearea cursorului

Toate interogările SQL se execută prin obiectul **cursor**:

```python
cursor = conn.cursor()
```

**Cursorul** este instrumentul pentru executarea comenzilor SQL și obținerea rezultatelor.

Analogie: conexiunea este „linia telefonică”, iar cursorul este „microfonul” prin care vorbești cu baza.

---

## 4. Crearea tabelului

### 4.1. Ce este un tabel?

Tabelul este o structură de date formată din:

* **rânduri (rows)** — fiecare rând reprezintă un obiect
* **coloane (columns)** — fiecare coloană are nume și tip de date

Exemplu de tabel studenți:

```
| id | name       | age | email                |
|----|------------|-----|----------------------|
| 1  | Ivan       | 20  | ivan@university.edu  |
| 2  | Maria      | 22  | maria@university.edu |
| 3  | Peter      | 19  | peter@university.edu |
```

### 4.2. Tipuri de date în SQLite

SQLite suportă 5 tipuri principale:

* **INTEGER** — numere întregi (1, 42, -100)
* **REAL** — numere cu virgulă mobilă (3.14, -0.5)
* **TEXT** — șiruri de text ("Ivan", "Salut")
* **BLOB** — date binare (imagini, fișiere)
* **NULL** — lipsa valorii

### 4.3. Crearea tabelului: cod

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Creăm tabelul students
cursor.execute("""
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        age INTEGER,
        email TEXT UNIQUE
    )
""")

# Salvăm modificările
conn.commit()

print("Tabelul students a fost creat")
```

**Analiză comandă:**

* `CREATE TABLE IF NOT EXISTS students` — creează tabelul `students` dacă nu există
* `id INTEGER PRIMARY KEY AUTOINCREMENT` — coloană `id`, număr întreg, identificator unic, autoincremental
* `name TEXT NOT NULL` — coloană `name`, text, obligatoriu
* `age INTEGER` — coloană `age`, număr întreg, opțional
* `email TEXT UNIQUE` — coloană `email`, text, trebuie să fie unic

**Important:** `conn.commit()` — confirmă modificările în baza de date. Fără această comandă, tabelul nu va fi creat!

---

## 5. Adăugarea datelor în tabel

### 5.1. Comanda INSERT

Pentru inserarea datelor se folosește comanda `INSERT`:

```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...)
```
### 5.2. Inserarea unei singure înregistrări

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Inserăm un singur student
cursor.execute("""
    INSERT INTO students (name, age, email)
    VALUES (?, ?, ?)
""", ("Ivan Ivanov", 20, "ivan@university.edu"))

conn.commit()

print("Student adăugat")
```

**Aspect important: semnele `?`**

Simbolurile `?` din interogare sunt **placeholder-e**. Valorile se transmit separat sub formă de tuplu.

**De ce nu trebuie să faci așa:**

```python
# GREȘIT! NU FACEȚI ASTA!
name = "Ivan"
cursor.execute(f"INSERT INTO students (name) VALUES ('{name}')")
```

Aceasta este periculos! Deschide vulnerabilitatea **SQL Injection** — un atacator poate introduce caractere speciale și executa comenzi arbitrare în baza ta.

**Mod corect:**

```python
# CORECT
cursor.execute("INSERT INTO students (name, age, email) VALUES (?, ?, ?)",
               ("Ivan", 20, "ivan@university.edu"))
```

SQLite se ocupă automat de escaparea caracterelor periculoase.

---

### 5.3. Inserarea mai multor înregistrări

Pentru a adăuga mai multe înregistrări simultan, folosește metoda `executemany`:

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Lista de studenți
students = [
    ("Maria Petrova", 22, "maria@university.edu"),
    ("Peter Sidorov", 19, "peter@university.edu"),
    ("Anna Smirnova", 21, "anna@university.edu"),
    ("Dmitry Kozlov", 23, "dmitry@university.edu")
]

# Inserăm toți studenții cu o singură comandă
cursor.executemany("""
    INSERT INTO students (name, age, email)
    VALUES (?, ?, ?)
""", students)

conn.commit()

print(f"Studenți adăugați: {len(students)}")
```

Metoda `executemany` execută interogarea pentru fiecare element din listă. Este mult mai rapid decât apelarea `execute` într-un ciclu.

---

## 6. Selectarea datelor din tabel

### 6.1. Comanda SELECT

Comanda `SELECT` se folosește pentru **citirea datelor** din tabel:

```sql
SELECT column1, column2 FROM table_name
```

Pentru toate coloanele, folosește `*`:

```sql
SELECT * FROM table_name
```

### 6.2. Obținerea tuturor înregistrărilor

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Executăm interogarea
cursor.execute("SELECT * FROM students")

# Obținem toate rândurile
rows = cursor.fetchall()

# Afișăm rezultatul
for row in rows:
    print(row)
```

**Rezultat:**

```
(1, 'Ivan Ivanov', 20, 'ivan@university.edu')
(2, 'Maria Petrova', 22, 'maria@university.edu')
(3, 'Peter Sidorov', 19, 'peter@university.edu')
...
```

Fiecare rând este un **tuple**.

### 6.3. Selectarea unor coloane specifice

```python
cursor.execute("SELECT name, age FROM students")
rows = cursor.fetchall()

for row in rows:
    print(f"Nume: {row[0]}, Vârstă: {row[1]}")
```

**Rezultat:**

```
Nume: Ivan Ivanov, Vârstă: 20
Nume: Maria Petrova, Vârstă: 22
Nume: Peter Sidorov, Vârstă: 19
```

### 6.4. Metode de obținere a datelor

SQLite oferă trei metode:

**1. `fetchall()` — obține toate rândurile**

```python
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()  # Listă cu toate rândurile
```

**2. `fetchone()` — obține un singur rând**

```python
cursor.execute("SELECT * FROM students")
row = cursor.fetchone()  # Primul rând
print(row)
```

**3. `fetchmany(size)` — obține mai multe rânduri**

```python
cursor.execute("SELECT * FROM students")
rows = cursor.fetchmany(3)  # Primele 3 rânduri
```

---

## 7. Filtrarea datelor: WHERE

### 7.1. Ce este WHERE?

Deseori nu vrem toate înregistrările, ci doar cele care satisfac o condiție. Se folosește `WHERE`:

```sql
SELECT * FROM table_name WHERE condition
```

### 7.2. Exemple de filtrare

**Exemplu 1: Studenți peste 20 de ani**

```python
cursor.execute("SELECT name, age FROM students WHERE age > ?", (20,))
rows = cursor.fetchall()

for row in rows:
    print(row)
```

**Observație:** valoarea se transmite ca tuplu `(20,)`. Chiar dacă este un singur element, trebuie să existe virgula!

**Exemplu 2: Student cu email specific**

```python
cursor.execute("SELECT * FROM students WHERE email = ?", ("ivan@university.edu",))
row = cursor.fetchone()

if row:
    print(f"Student găsit: {row[1]}")
else:
    print("Student negăsit")
```

**Exemplu 3: Căutare după parte din șir (LIKE)**

```python
# Găsește toți studenții care au "Peter" în nume
cursor.execute("SELECT name FROM students WHERE name LIKE ?", ("%Peter%",))
rows = cursor.fetchall()

for row in rows:
    print(row[0])
```

Simbolul `%` înseamnă „orice secvență de caractere”.

---

## 8. Actualizarea și ștergerea datelor

### 8.1. Actualizarea înregistrărilor: UPDATE

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

# Schimbăm vârsta studentului cu id = 1
cursor.execute("""
    UPDATE students
    SET age = ?
    WHERE id = ?
""", (21, 1))

conn.commit()

print("Datele au fost actualizate")
```

**Atenție:** dacă nu folosești `WHERE`, se vor modifica **toate înregistrările**!

### 8.2. Ștergerea înregistrărilor: DELETE

```python
# Șterge studentul cu id = 3
cursor.execute("DELETE FROM students WHERE id = ?", (3,))
conn.commit()

print("Student șters")
```

**Atenție:** fără `WHERE`, se vor șterge **toate înregistrările**!
## 9. Tranzacții și siguranța datelor

### 9.1. Ce este o tranzacție?

**Tranzacția** este o secvență de operații care se execută **atomic**:

* fie se execută **toate operațiile**
* fie **niciuna** nu se execută

Exemplu: transferul de bani între conturi.

```
1. Retrage 1000₽ din contul A
2. Adaugă 1000₽ în contul B
```

Dacă apare o eroare între operații, banii „se pierd”. Tranzacția garantează că fie ambele operații se execută, fie niciuna.

---

### 9.2. Comenzi pentru tranzacții

* **`commit()`** — salvează modificările în baza de date
* **`rollback()`** — anulează toate modificările de la ultimul `commit()`

```python
import sqlite3

conn = sqlite3.connect("university.db")
cursor = conn.cursor()

try:
    # Executăm operațiile
    cursor.execute("INSERT INTO students (name, age) VALUES (?, ?)", ("Test", 25))
    cursor.execute("UPDATE students SET age = ? WHERE id = ?", (30, 1))
    
    # Dacă totul merge bine — salvăm
    conn.commit()
    print("Modificările au fost salvate")
    
except Exception as e:
    # Dacă apare eroare — revenim
    conn.rollback()
    print(f"Eroare: {e}")
    print("Modificările au fost anulate")
```

---

### 9.3. Utilizarea managerului de context

Python permite folosirea `with` pentru gestionarea automată a tranzacțiilor:

```python
import sqlite3

try:
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        
        cursor.execute("INSERT INTO students (name, age) VALUES (?, ?)", 
                      ("Commit automat", 26))
        
        # commit() este apelat automat la ieșirea din blocul with
        
except Exception as e:
    # rollback() este apelat automat în caz de eroare
    print(f"Eroare: {e}")
```

**Avantaje:**

* nu mai trebuie apelat manual `commit()` și `rollback()`
* cod mai curat și mai sigur
* conexiunea se închide automat

---

## 10. Exemplu complet: aplicație pentru evidența studenților

Vom crea o aplicație care:

* creează baza și tabelul
* adaugă studenți
* afișează lista
* caută studenți după vârstă

```python
import sqlite3

def create_database():
    """Crearea bazei de date și tabelului"""
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
        print("Baza de date este gata")

def add_student(name, age, email):
    """Adăugarea unui student nou"""
    try:
        with sqlite3.connect("university.db") as conn:
            cursor = conn.cursor()
            cursor.execute(
                "INSERT INTO students (name, age, email) VALUES (?, ?, ?)",
                (name, age, email)
            )
            print(f"Student {name} adăugat")
    except sqlite3.IntegrityError:
        print(f"Eroare: email {email} există deja")

def show_all_students():
    """Afișează toți studenții"""
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute("SELECT id, name, age, email FROM students")
        rows = cursor.fetchall()
        
        print("\n=== Lista studenților ===")
        for row in rows:
            print(f"ID: {row[0]}, Nume: {row[1]}, Vârstă: {row[2]}, Email: {row[3]}")

def find_students_by_age(min_age):
    """Găsește studenții mai mari de o anumită vârstă"""
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute(
            "SELECT name, age FROM students WHERE age >= ?",
            (min_age,)
        )
        rows = cursor.fetchall()
        
        print(f"\n=== Studenți peste {min_age} ani ===")
        for row in rows:
            print(f"Nume: {row[0]}, Vârstă: {row[1]}")

if __name__ == "__main__":
    # 1. Creăm baza
    create_database()
    
    # 2. Adăugăm studenți
    add_student("Ivan Ivanov", 20, "ivan@university.edu")
    add_student("Maria Petrova", 22, "maria@university.edu")
    add_student("Peter Sidorov", 19, "peter@university.edu")
    add_student("Anna Smirnova", 21, "anna@university.edu")
    
    # 3. Afișăm toți studenții
    show_all_students()
    
    # 4. Căutăm studenți peste 20 de ani
    find_students_by_age(20)
```

**Rezultat așteptat:**

```
Baza de date este gata
Student Ivan Ivanov adăugat
Student Maria Petrova adăugat
Student Peter Sidorov adăugat
Student Anna Smirnova adăugat

=== Lista studenților ===
ID: 1, Nume: Ivan Ivanov, Vârstă: 20, Email: ivan@university.edu
ID: 2, Nume: Maria Petrova, Vârstă: 22, Email: maria@university.edu
ID: 3, Nume: Peter Sidorov, Vârstă: 19, Email: peter@university.edu
ID: 4, Nume: Anna Smirnova, Vârstă: 21, Email: anna@university.edu

=== Studenți peste 20 ani ===
Nume: Ivan Ivanov, Vârstă: 20
Nume: Maria Petrova, Vârstă: 22
Nume: Anna Smirnova, Vârstă: 21
```

---

## 11. Recomandări și bune practici

### 11.1. Folosiți întotdeauna placeholder-e

```python
# RĂU - vulnerabil la SQL Injection
name = "Ivan"
cursor.execute(f"SELECT * FROM students WHERE name = '{name}'")

# BINE - sigur
cursor.execute("SELECT * FROM students WHERE name = ?", (name,))
```

### 11.2. Folosiți managerul de context `with`

```python
# BINE
with sqlite3.connect("university.db") as conn:
    cursor = conn.cursor()
    # codul vostru
    # commit() este apelat automat
```

### 11.3. Tratați erorile

```python
try:
    with sqlite3.connect("university.db") as conn:
        cursor = conn.cursor()
        cursor.execute("INSERT INTO students ...")
except sqlite3.IntegrityError as e:
    print(f"Eroare de integritate: {e}")
except sqlite3.Error as e:
    print(f"Eroare bază de date: {e}")
```

### 11.4. Închideți conexiunile

Dacă nu folosiți `with`, închideți conexiunea manual:

```python
conn = sqlite3.connect("university.db")
try:
    # lucru cu baza de date
    pass
finally:
    conn.close()
```

---

## Concluzie

Astăzi am învățat elementele de bază pentru lucrul cu SQLite în Python:

1. **Am creat conexiunea** la baza de date
2. **Am creat tabelul** cu coloane și tipuri de date
3. **Am adăugat date** folosind `INSERT`
4. **Am citit date** folosind `SELECT`
5. **Am filtrat date** folosind `WHERE`
6. **Am actualizat și șters** înregistrări
7. **Am lucrat cu tranzacții** pentru integritatea datelor

Aceste cunoștințe sunt fundamentul pentru lucrul cu orice bază de date. Principiile rămân aceleași, se schimbă doar sintaxa și funcționalitățile specifice fiecărui SGBD.
