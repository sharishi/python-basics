 # Șiruri, liste și mulțimi în Python

---

### 1. Ce este indexarea?

**Indexarea** este modul de acces la elementele individuale ale unei secvențe (cum ar fi șiruri, liste sau tuple) prin poziția lor, numită **index**.

* **Indexii în Python încep de la 0** pentru primul element.
* **Indexii negativi** permit accesul la elemente de la sfârșitul secvenței.
* Indexarea permite extragerea, modificarea (pentru tipurile mutabile) sau utilizarea elementelor în diverse operații.

**Formula generală pentru indexare:**

```python
{nume_secventa}[index]
```

Indexarea este disponibilă pentru:

* **Șiruri (strings)**: secvențe de caractere.
* **Liste (lists)**: secvențe de elemente de orice tip.
* **Tuple**: secvențe imutabile de elemente.

#### **Indexarea șirurilor**

Șirurile în Python sunt secvențe de caractere, iar fiecărui caracter îi corespunde un index. Indexarea permite accesul la caracterele unui șir.

```python
s = "Python"

# Indexi pozitivi
print(s[0])  # 'P' — primul caracter
print(s[3])  # 'h' — al patrulea caracter

# Indexi negativi
print(s[-1])  # 'n' — ultimul caracter
print(s[-3])  # 'h' — al treilea caracter de la sfârșit
```

Dacă încercăm să accesăm un index în afara șirului, Python va genera o eroare:

```python
print(s[10])  # IndexError: string index out of range
```

---

#### **Indexarea listelor**

Listele suportă, de asemenea, indexarea, permițând accesul la elemente prin poziția lor.

* Funcționează similar cu șirurile.
* Elementele pot fi de orice tip, inclusiv alte liste.

**Exemplu:**

```python
lst = [10, 20, 30, 40, 50]

# Indexi pozitivi
print(lst[0])  # 10 — primul element
print(lst[3])  # 40 — al patrulea element

# Indexi negativi
print(lst[-1])  # 50 — ultimul element
print(lst[-3])  # 30 — al treilea element de la sfârșit
```

Pentru liste imbricate, indexarea poate fi multiplă:

```python
nested_lst = [1, [2, 3, 4], 5]
print(nested_lst[1])      # [2, 3, 4] — al doilea element (listă imbricată)
print(nested_lst[1][2])   # 4 — al treilea element din lista imbricată
```

Ca și în cazul șirurilor, încercarea de a accesa un index inexistent va genera o eroare:

```python
print(lst[10])  # IndexError: list index out of range
```
---

### 2. Mutabilitate și imutabilitate în Python

**Mutabilitatea (mutability)** și **imutabilitatea (immutability)** sunt proprietăți ale obiectelor care definesc dacă conținutul lor poate fi modificat după creare.

#### **Obiecte mutabile (mutable)**

Obiectele mutabile pot fi modificate după creare. Modificarea conținutului nu schimbă referința obiectului.

Exemple:

* **Liste (`list`)**
* **Mulțimi (`set`)**
* **Dicționare (`dict`)**

**Exemplu:**

```python
lst = [1, 2, 3]
lst[0] = 10  # Modificăm primul element
print(lst)  # [10, 2, 3]

# Adăugarea unui element nou
lst.append(4)
print(lst)  # [10, 2, 3, 4]
```
---
#### **Obiecte imutabile (immutable)**

Obiectele imutabile nu pot fi modificate după creare. Orice modificare creează un obiect nou în memorie.

Exemple:

* **Numere (`int`, `float`, `complex`)**
* **Șiruri (`str`)**
* **Tuple (`tuple`)**
* **Mulțimi înghețate (`frozenset`)**

**Exemplu:**

```python
s = "hello"
# s[0] = "H"  # Eroare! Nu se poate modifica un caracter din șir

# Modificarea șirului creează un șir nou
s = s.upper()
print(s)  # "HELLO"
```

---

#### **Diferența între obiectele mutabile și imutabile**

| Proprietate               | Obiecte mutabile                    | Obiecte imutabile                  |
| ------------------------- | ----------------------------------- | ---------------------------------- |
| Posibilitatea modificării | Poate fi modificat conținutul       | Nu poate fi modificat conținutul   |
| Utilizarea memoriei       | Modificările apar în același obiect | Se creează un obiect nou           |
| Exemple                   | `list`, `dict`, `set`               | `int`, `str`, `tuple`, `frozenset` |

---

#### **De ce este important?**

* **Obiectele imutabile** oferă stabilitate datelor și sunt utile în aplicații multithreaded.
* **Obiectele mutabile** sunt convenabile pentru lucrul cu seturi mari de date unde este necesară modificarea conținutului.

Înțelegerea mutabilității ajută la evitarea erorilor legate de modificări neintenționate ale datelor în Python.

---

### 3. **Slice-uri (slicing)**

Slice-urile permit extragerea de subșiruri sau subliste dintr-un șir, listă sau alt obiect indexabil.

**Sintaxă:**

```python
sequence[start:end:step]
```

* `start`: indexul de început al slice-ului (inclusiv).
* `end`: indexul de sfârșit al slice-ului (exclusiv).
* `step`: pasul cu care se iau elementele.

**Exemple:**

```python
s = "Hello, World!"
print(s[0:5])  # "Hello" — de la indexul 0 la 4
print(s[7:])   # "World!" — de la indexul 7 până la sfârșit
print(s[:5])   # "Hello" — de la început până la indexul 4
print(s[::2])  # "Hlo ol!" — fiecare al doilea caracter
```

Se pot folosi și indexi negativi:

```python
print(s[-6:-1])  # "World" — de la sfârșit, de la indexul -6 la -2
```

---

### 4. Șiruri (`str`)

Șirurile în Python sunt secvențe **imutabile** de caractere. Sunt folosite frecvent pentru procesarea datelor textuale.

#### Proprietăți principale ale șirurilor:

* Imutabile (nu poți modifica caracterele direct).
* Suportă indexare și slicing.
* Pot conține orice caractere, inclusiv spații și simboluri speciale.

#### Crearea șirurilor:

```python
s1 = "Salut, lume!"          # ghilimele duble
s2 = 'Python — un limbaj puternic'  # ghilimele simple
s3 = """Șir multi-linie
exemplu"""                 # ghilimele triple
```

#### Metode utile pentru șiruri:

* **Modificarea literelor:**

```python
s = "Python"
print(s.upper())  # "PYTHON"
print(s.lower())  # "python"
```

* **Eliminarea spațiilor sau caracterelor:**

```python
s = "  Hello, world!  "
print(s.strip())  # "Hello, world!"
```

* **Verificări:**

```python
s = "123"
print(s.isdigit())  # True
print(s.isalpha())  # False
```

* **Împărțire și concatenare:**

```python
s = "one,two,three"
print(s.split(","))                  # ['one', 'two', 'three']
print("-".join(['one', 'two', 'three']))  # "one-two-three"
```

* **Căutare și înlocuire:**

```python
s = "Python programming"
print(s.find("prog"))          # 7
print(s.replace("Python", "C++"))  # "C++ programming"
```

* **Numărarea aparițiilor unui substring:**

```python
string = "brown fox jumps over a lazy dog"
count = string.count("o")
print(count)  # 4
```

* **Lungimea șirului:**

```python
s = "Hello, World!"
print(len(s))  # 13
```

* **Ștergerea elementelor:**
  `del` nu se aplică direct pe șiruri, dar putem folosi slicing:

```python
s = "Hello, World!"
s = s[:5] + s[7:]  # elimină caracterele de la indexul 5 la 6
print(s)  # "Hello World!"
```

* **Funcția `print()`** pentru afișare:

```python
print(1, 2, 3, 4)               # 1 2 3 4
print(1, 2, 3, 4, sep=' - ')    # 1 - 2 - 3 - 4
print(1, 2, 3, 4, sep=' - ', end='!')  # 1 - 2 - 3 - 4!
```

* **Funcția `input()`** pentru citirea datelor de la utilizator:

```python
name = input('Enter your name: ')
print("Your name is", name)

nmbr = input('Enter a number: ')
print(int(nmbr) + 5)  # conversie la număr
```

* **Repetarea șirurilor:**

```python
s = "Hello"
print(s * 3)   # "HelloHelloHello"
print(s * -2)  # ""
print(s * 0)   # ""
```

* **Verificarea prezenței unui substring:**

```python
s = "Python programming"
if "Python" in s:
    print("Substring găsit!")
```

---

### Formatarea șirurilor în Python

#### 1. **F-strings (Python 3.6+)**

Permite inserarea variabilelor sau expresiilor direct în șir:

```python
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old")
# My name is Alice and I am 25 years old

x = 5
print(f"The value of x squared is {x**2}")
# The value of x squared is 25
```
---

#### **2. Operatorul %**

Metoda, asemănătoare cu cea din C, este folosită mai rar, dar încă poate fi întâlnită în proiecte vechi:

```python
name = "Alice"
age = 25
print("My name is %s and I am %d years old" % (name, age))
```

Rezultat:

```
My name is Alice and I am 25 years old
```

#### **3. Metoda `format()`**

Metoda `format()` permite înlocuirea placeholder-elor dintr-un șir cu valorile furnizate:

```python
name = "Alexei"
age = 30
print("Mă numesc {}. Am {} ani.".format(name, age))
```

Rezultat:

```
Mă numesc Alexei. Am 30 ani.
```

De asemenea, se pot folosi indici și argumente numite:

```python
print("Am {1} ani. Mă numesc {0}.".format(name, age))
print("Mă numesc {name}. Am {age} ani.".format(name='Alexei', age=30))
```

F-strings sunt preferate, deoarece sunt mai ușor de citit și mai convenabile.

---

#### Slice-uri:

```python
s = "Python"
print(s[0])  # "P"
print(s[-1])  # "n"
print(s[1:4])  # "yth"
```

---

## Ce sunt colecțiile în Python?

Colecțiile sunt containere folosite pentru stocarea unui set de date. În Python, colecțiile sunt structuri de date care permit stocarea mai multor elemente, facilitând lucrul cu grupuri de date. Colecțiile pot fi **mutable** (modificabile) sau **immutable** (nemodificabile), iar fiecare tip de colecție are propriile caracteristici.

În Python există patru tipuri de colecții principale:

1. **Listă (list)** — colecție ordonată și modificabilă. Poate conține elemente duplicate.

   Exemplu:

   ```python
   lst = [1, 2, 3, 2, 4]
   ```

2. **Mulțime (set)** — colecție neordonată, cu elemente unice. Elemente sunt nemodificabile, dar se pot adăuga și șterge. Nu conține duplicate.

   Exemplu:

   ```python
   st = {1, 2, 3, 4}
   ```

3. **Tuplu (tuple)** — colecție ordonată și nemodificabilă. Permite duplicarea elementelor.

   Exemplu:

   ```python
   tpl = (1, 2, 3, 2, 4)
   ```

4. **Dicționar (dict)** — colecție ordonată (din Python 3.7+) și modificabilă, care stochează perechi "cheie-valoare". Cheile nu se pot repeta.

   Exemplu:

   ```python
   d = {"name": "Alice", "age": 25}
   ```

# Să ne oprim mai detaliat asupra fiecărei colecții :)

---

### 1. **Liste (`list`)**

Listele în Python reprezintă secvențe **modificabile** de obiecte.

#### Proprietăți principale:

* Pot conține obiecte de tipuri diferite.
* Lungime dinamică.
* Suportă listă imbricată (nested lists).

#### Crearea listelor:

```python
lst1 = [1, 2, 3, 4]
lst2 = ["a", "b", "c"]
lst3 = [1, "Python", [2, 3, 4]]  # Listă imbricată
lst4 = list() # listă goală
```

#### Operații principale:

* **Adăugarea elementelor:**

```python
lst = [1, 2, 3]
lst.append(4)  # Adaugă la sfârșit: [1, 2, 3, 4]
lst.insert(1, 10)  # Adaugă la poziția specificată: [1, 10, 2, 3, 4]
```

* **Ștergerea elementelor:**

```python
lst = [1, 2, 3, 4]
lst.pop()      # Șterge ultimul element: [1, 2, 3]
lst.remove(2)  # Șterge prima apariție: [1, 3]
my_list.clear() # Șterge toate elementele: []
```

* **Concatenare și repetare:**

```python
lst1 = [1, 2]
lst2 = [3, 4]
print(lst1 + lst2)  # [1, 2, 3, 4]
print(lst1 * 2)     # [1, 2, 1, 2]
```

* **Sortare:**

```python
lst = [3, 1, 4, 2]
lst.sort()           # [1, 2, 3, 4]
lst.reverse()        # [4, 3, 2, 1]
lst.sort(reverse=True) # [4, 3, 2, 1]
```

* **Returnează o copie a listei:**

```python
my_list = [1, 2, 3]
new_list = my_list.copy()
print(new_list)  # [1, 2, 3]
```

* **Numărul de apariții ale unui element în listă:**

```python
my_list = [1, 2, 2, 3, 2]
count = my_list.count(2)
print(count)  # 3
```

* **Returnează indexul primului element egal cu item într-un interval specificat:**

```python
my_list = [1, 2, 2, 3, 2]
index = my_list.index(2, 2, 5)
print(index)  # 2
```

* **Adăugarea elementelor unui alt obiect iterabil la sfârșitul listei:**

```python
my_list = [1, 2, 3]
my_list.extend([4, 5])
print(my_list)  # [1, 2, 3, 4, 5]
```

* **Aplicarea unei funcții asupra fiecărui element:**
  `map()` aplică o funcție asupra fiecărui element dintr-un obiect iterabil și returnează un iterator:

```python
my_list = [1, 2, 3, 4, 5]
result = map(lambda x: x ** 2, my_list)
print(list(result))  # [1, 4, 9, 16, 25]

# Conversia unui șir de string-uri în numere
my_str_list = ['1', '2', '3']
result = map(int, my_str_list)
print(list(result))  # [1, 2, 3]
```

Funcția `map()` aplică funcția specificată (în exemplu `lambda x: x ** 2`) fiecărui element din `my_list`, creând un nou obiect iterabil cu rezultatele.

#### Slice-uri în liste:

```python
lst = [0, 1, 2, 3, 4]
print(lst[:3])   # [0, 1, 2]
print(lst[1::2]) # [1, 3]
```
---

### 3. **Mulțimi (`set`)**

Mulțimile în Python reprezintă colecții de elemente unice, care nu au o ordine fixă.

#### Proprietăți principale ale mulțimilor:

* Elementele sunt unice.
* Tipurile de date **immutable** (stringuri, numere, tuple) pot fi elemente ale mulțimii.
* Sunt suportate operații matematice: reuniune, intersecție, diferență.

#### Crearea mulțimilor:

```python
set1 = {1, 2, 3, 4}
set2 = set([1, 2, 2, 3])  # {1, 2, 3}
set3 = set()  # Mulțime goală
```

În Python, valorile `True` și `1` (la fel `False` și `0`) sunt considerate echivalente în mulțimi, deoarece mulțimile nu pot conține elemente duplicate. Dacă adaugi astfel de valori, interpretatorul le consideră identice și păstrează doar unul.

Exemplu:

```python
my_set = {0, "tulip", "rose", "iris", True, 1, 77, False, True}
print(my_set, len(my_set))
```

Rezultat:

```
{0, 'rose', 'iris', True, 'tulip', 77} 6
```

* În `my_set`, au fost incluse atât `True` cât și `1`, dar interpretatorul a păstrat doar unul.
* De asemenea, `False` și `0` sunt considerate echivalente, și în mulțime a rămas doar `0`.
* Duplicatele `True` și `1` au fost eliminate.

Astfel, mulțimile nu permit duplicate, iar dacă două elemente sunt echivalente (ex. `True` și `1`), se păstrează doar unul.

Un avantaj principal al utilizării mulțimilor față de liste este verificarea rapidă dacă un element **aparține** mulțimii.

---

#### Operații principale:

* **Adăugarea și ștergerea elementelor:**

```python
s = {1, 2, 3}
s.add(4)       # {1, 2, 3, 4}
s.discard(2)   # Elimină elementul dacă există, altfel nu face nimic: {1, 3, 4}
s.remove(3)    # Elimină elementul dacă există, altfel generează KeyError: {1, 4}
# s.remove(5)  # KeyError
s.clear()      # {}
```

* **Ștergerea unui element aleator:**
  Metoda **`pop()`** elimină un element aleator și îl returnează. Este utilă dacă vrei să elimini un element fără să te intereseze care este sau dacă vrei doar să-l preiei și să lucrezi cu el. Dacă mulțimea este goală, se generează `KeyError`.

Exemplu:

```python
my_set = {1, 2, 3, 4, 5}
removed_item = my_set.pop()
print(f"Element eliminat: {removed_item}")
print(f"Mulțimea după eliminare: {my_set}")
```

**Notă:** Deoarece mulțimile nu sunt ordonate, rezultatul lui `pop()` poate fi diferit de fiecare dată.

---

* **Reuniune și intersecție:**

```python
s1 = {1, 2, 3}
s2 = {3, 4, 5}
print(s1 | s2)           # {1, 2, 3, 4, 5} (reuniune)
c = s1.union(s2)         # {1, 2, 3, 4, 5} (reuniune)
print(s1 & s2)           # {3} (intersecție)
intersection_set = s1.intersection(s2)  # {3} (intersecție)
```

* **Diferență și diferență simetrică:**

```python
print(s1 - s2)           # {1, 2} (diferență)
diff_s1_s2 = s1.difference(s2)  # {1, 2}
print(s1 ^ s2)           # {1, 2, 4, 5} (diferență simetrică)
```

* **Returnează o copie a mulțimii:**

```python
fruits = {"apple", "banana", "cherry"}
new_fruits = fruits.copy()
print(new_fruits)  # {'banana', 'cherry', 'apple'}
```

* **Verifică dacă două mulțimi nu au elemente comune:**

```python
set1 = {1, 2, 3}
set2 = {4, 5, 6}
disjoint_sets = set1.isdisjoint(set2)
print(disjoint_sets)  # True
```

* **Verifică dacă o mulțime este subset a alteia:**

```python
set1 = {1, 2, 3, 4, 5}
set2 = {1, 2, 3}
result = set2.issubset(set1)
print(result)  # True
```

#### Verificări:

```python
s = {1, 2, 3}
print(2 in s)  # True
print(5 in s)  # False
```

---

**FROZENSET** — tip de date incorporat în Python, reprezentând o mulțime **nemodificabilă**. Spre deosebire de `set`, elementele din `frozenset` nu pot fi schimbate după creare. Suportă toate metodele mulțimii, cu excepția celor care modifică obiectul (`add()`, `remove()`, etc.).

### Caracteristici:

* Nemodificabil după creare.
* Suportă operații cu mulțimi: reuniune, intersecție, diferență etc.
* Poate fi folosit ca **cheie în dicționare**, spre deosebire de mulțimile obișnuite.

### Exemplu:

```python
# Creare frozenset
frozen_set = frozenset([1, 2, 3, 4, 5])
print(frozen_set)  # frozenset({1, 2, 3, 4, 5})

# Încercarea de a modifica frozenset va genera eroare
# frozen_set.add(6)  # Eroare: 'frozenset' object has no attribute 'add'

# Folosirea frozenset ca cheie în dicționar
my_dict = {frozen_set: "Acesta este un frozenset"}
print(my_dict)
```

### Metode principale **frozenset**:

* **union()**: reuniune
* **intersection()**: intersecție
* **difference()**: diferență
* **issubset()**: verifică dacă este subset
* **issuperset()**: verifică dacă este superset

### Exemplu de utilizare a metodelor:

```python
fs1 = frozenset([1, 2, 3])
fs2 = frozenset([3, 4, 5])

print(fs1.union(fs2))        # frozenset({1, 2, 3, 4, 5})
print(fs1.intersection(fs2)) # frozenset({3})
print(fs1.difference(fs2))   # frozenset({1, 2})
```

---

**frozenset** este util atunci când ai nevoie de colecții imuabile de elemente, de exemplu, pentru a fi folosite ca **chei în dicționare** sau pentru a transmite date în siguranță în aplicații multitasking.

### Funcții utile

Să vedem câteva funcții care ne ajută să lucrăm cu listele și mulțimile:

1. **`len()`** — returnează numărul de elemente dintr-o secvență (listă, mulțime etc.):

```python
my_list = [1, 2, 3, 4, 5]
print(len(my_list))  # 5

my_set = {1, 1, 2, 2}
print(len(my_set))  # 2
```

2. **`max()`** — returnează valoarea maximă dintr-o secvență:

```python
my_list = [5, 2, 8, 1, 9]
print(max(my_list))  # 9

my_set = {5, 2, 8, 1, 9}
print(max(my_set))  # 9
```

3. **`min()`** — returnează valoarea minimă dintr-o secvență:

```python
my_list = [5, 2, 8, 1, 9]
print(min(my_list))  # 1

my_set = {5, 2, 8, 1, 9}
print(min(my_set))  # 1
```

4. **`sorted()`** — sortează o secvență și returnează o listă nouă, sortată. Poți folosi parametrul `reverse=True` pentru sortare descrescătoare:

```python
my_list = [5, 2, 8, 1, 9]
sorted_list = sorted(my_list)
print(sorted_list)  # [1, 2, 5, 8, 9]

sorted_list_descending = sorted(my_list, reverse=True)
print(sorted_list_descending)  # [9, 8, 5, 2, 1]
```

Dacă sortezi o mulțime, rezultatul va fi o **listă**:

```python
my_set = {1, 1, 2, 2}
print(sorted(my_set))  # [1, 2]
```

5. **`sum()`** — returnează suma tuturor elementelor din secvență. Funcționează cu numere:

```python
my_list = [1, 2, 3, 4, 5]
print(sum(my_list))  # 15

my_set = {1, 2, 3, 4, 5}
print(sum(my_set))  # 15
```

---

### Concluzie: Compararea stringurilor, listelor și mulțimilor

| Proprietate           | Stringuri (`str`) | Liste (`list`)    | Mulțimi (`set`) |
| --------------------- | ----------------- | ----------------- | --------------- |
| Mutabilitate          | Nu                | Da                | Da              |
| Unicitate             | Nu                | Nu                | Da              |
| Indexare              | Da                | Da                | Nu              |
| Suport pentru slicing | Da                | Da                | Nu              |
| Utilizare             | Date textuale     | Orice tip de date | Date unice      |

Aceste structuri de date acoperă o gamă largă de sarcini, oferind instrumente pentru lucrul cu texte, secvențe și colecții de elemente unice.
