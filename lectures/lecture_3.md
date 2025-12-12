# Dicționare și tuple în Python

### Dicționare (dict)

**Dicționarul** în Python — este o colecție neordonată, modificabilă, care stochează date sub formă de perechi "cheie-valoare". Fiecare cheie din dicționar este unică, iar valoarea ei poate fi de orice tip. Dicționarul poate fi folosit pentru căutarea rapidă a valorilor după cheie.

#### Caracteristici principale:

* **Neordonate** (până la Python 3.7; începând cu această versiune, dicționarele păstrează ordinea inserării).
* **Modificabile** (poți adăuga, modifica sau șterge elemente).
* **Cheile sunt unice**: două chei identice într-un dicționar nu pot exista.

Dicționarele sunt optimizate pentru extragerea datelor. Trebuie să cunoaștem cheia pentru a accesa valoarea.
În Python, dicționarele sunt definite între acolade {}, fiecare element fiind o pereche în forma - `key:value`.

### **Cheile dicționarelor în Python**

În Python, cheile unui dicționar pot fi doar tipuri de date **imutable**. Aceasta se datorează faptului că cheile dicționarului trebuie să fie hash-uibile, iar tipurile modificabile, cum ar fi listele și mulțimile, nu pot fi folosite ca chei deoarece hash-ul lor se poate schimba.

**Ce poate fi folosit ca cheie:**

1. **Numere** (int, float).
2. **Șiruri de caractere** (str).
3. **Tuple** (tuple), dacă conțin doar elemente imutabile.
4. **frozenset** — versiunea imutabilă a mulțimii, care poate fi folosită ca cheie.
5. **Tipuri Boolean** (True, False).

**Exemplu de folosire a `frozenset` ca și cheie:**

```python
students_courses = {}
name_age = frozenset(['Anatoly', 32])
students_courses.update({name_age: ['Python', 'C++']})

print(students_courses)  # => {frozenset({32, 'Anatoly'}): ['Python', 'C++']}
```

**Ce nu poate fi folosit ca cheie:**

* **Liste** (list)
* **Mulțimi** (set)
* **Alte tipuri de date modificabile**

Astfel, pentru utilizarea unor structuri complexe de date ca și chei (de exemplu, perechi de valori), se poate folosi `frozenset`, deoarece este imutabil.

### Sintaxă:

```python
# Crearea unui dicționar
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Accesarea valorii după cheie
print(my_dict["name"])  # Alice

# Adăugarea unui element nou
my_dict["job"] = "Engineer"
print(my_dict)  # {'name': 'Alice', 'age': 25, 'city': 'New York', 'job': 'Engineer'}

# Ștergerea unui element
del my_dict["age"]
print(my_dict)  # {'name': 'Alice', 'city': 'New York', 'job': 'Engineer'}

# Obținerea tuturor cheilor sau valorilor
print(my_dict.keys())   # dict_keys(['name', 'city', 'job'])
print(my_dict.values()) # dict_values(['Alice', 'New York', 'Engineer'])
```

## Metode ale dicționarului:

### 1. **`get(key)`**

Metoda `get(key)` returnează valoarea asociată cheii specificate. Dacă cheia lipsește, returnează `None` (sau al doilea argument, dacă este specificat).

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25}

# Obținerea valorii după cheie
print(my_dict.get("name"))  # "Alice"
print(my_dict.get("gender"))  # None

# Se poate specifica o valoare implicită
print(my_dict.get("gender", "Unknown"))  # "Unknown"
```

### 2. **`items()`**

Metoda `items()` returnează o vizualizare a tuturor perechilor (cheie, valoare) din dicționar sub formă de iterator.

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Obținerea tuturor perechilor cheie-valoare
print(my_dict.items())  # dict_items([('name', 'Alice'), ('age', 25), ('city', 'New York')])

# Convertim în listă
print(list(my_dict.items()))  # [('name', 'Alice'), ('age', 25), ('city', 'New York')]
```

### 3. **`pop(key)`**

Metoda `pop(key)` șterge perechea "cheie-valoare" după cheie și returnează valoarea corespunzătoare. Dacă cheia lipsește, va fi ridicată excepția `KeyError`.

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Ștergem perechea cu cheia "age"
value = my_dict.pop("age")
print(value)  # 25
print(my_dict)  # {'name': 'Alice', 'city': 'New York'}

# Încercarea de a șterge o cheie inexistentă va cauza eroare
# my_dict.pop("gender")  # KeyError: 'gender'
```

### 4. **`update()`**

Metoda `update()` este folosită pentru a actualiza dicționarul cu noi perechi "cheie-valoare". Dacă cheia există deja, valoarea ei va fi actualizată. Dacă cheia lipsește, va fi adăugată o nouă pereche "cheie-valoare".

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25}

# Actualizarea dicționarului cu noi perechi cheie-valoare
my_dict.update({"age": 26, "city": "New York"})
print(my_dict)  # {'name': 'Alice', 'age': 26, 'city': 'New York'}

# Se poate actualiza dicționarul folosind un alt dicționar
other_dict = {"gender": "female", "country": "USA"}
my_dict.update(other_dict)
print(my_dict)  # {'name': 'Alice', 'age': 26, 'city': 'New York', 'gender': 'female', 'country': 'USA'}
```

### 5. **`keys()`**

Metoda returnează o vizualizare a tuturor cheilor din dicționar. Această vizualizare este un iterator și poate fi convertită într-o listă sau utilizată într-un ciclu.

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Obținerea tuturor cheilor
keys = my_dict.keys()
print(keys)  # dict_keys(['name', 'age', 'city'])

# Convertim în listă
print(list(keys))  # ['name', 'age', 'city']

# Utilizare într-un ciclu
for key in my_dict.keys():
    print(key)
```

### 6. **`popitem()`**

Metoda șterge și returnează o pereche (cheie, valoare) din dicționar. Perechea este returnată ca un tuple `(key, value)`. În Python 3.7+, elementul care va fi șters este ultima pereche adăugată, deoarece dicționarele au devenit ordonate începând cu această versiune.

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Ștergerea și returnarea ultimului element
key, value = my_dict.popitem()
print(key, value)  # de exemplu: 'city New York'

# Verificăm că elementul a fost șters
print(my_dict)  # {'name': 'Alice', 'age': 25}
```

### 7. **`values()`**

Metoda returnează toate valorile dicționarului sub formă de **obiect `dict_values`**, care este iterabil. Nu returnează o listă, dar poate fi convertit într-o listă folosind funcția `list()`.

Exemplu:

```python
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Obținerea tuturor valorilor din dicționar
values = my_dict.values()
print(values)  # dict_values(['Alice', 25, 'New York'])

# Conversia într-o listă
values_list = list(values)
print(values_list)  # ['Alice', 25, 'New York']
```

Metodele **`count()`** și **`index()`** sunt utilizate de obicei pentru liste, dar nu se aplică direct dicționarelor, deoarece un dicționar reprezintă un set de perechi "cheie-valoare". Totuși, le putem explica pentru lucrul cu liste:

### 8. **`count()`**

Metoda **`count()`** returnează numărul de apariții ale unui element într-o listă.

Exemplu:

```python
my_list = [1, 2, 3, 4, 2, 5, 2]

# Numărarea aparițiilor numărului 2
count = my_list.count(2)
print(count)  # Va afișa 3
```

### 9. **`index()`**

Metoda **`index()`** returnează indexul primei apariții a unui element în listă. Dacă elementul nu este găsit, apare eroarea **`ValueError`**.

Exemplu:

```python
my_list = [1, 2, 3, 4, 2, 5]

# Obținerea indexului primei apariții a numărului 2
index = my_list.index(2)
print(index)  # Va afișa 1

# Încercarea de a găsi un element care nu există va cauza eroare
# my_list.index(6)  # ValueError: 6 is not in list
```

### 10. **`fromkeys()`**

Metoda este utilizată pentru crearea unui dicționar nou cu chei specificate, toate având aceeași valoare implicită. Metoda returnează un dicționar nou, în care fiecărei chei i se atribuie valoarea trecută ca al doilea argument sau `None`, dacă nu este specificată nicio valoare.

### Sintaxă:

```python
dict.fromkeys(iterable, value=None)
```

* **`iterable`** — o secvență (de exemplu, listă, tuple, șir) care conține cheile.
* **`value`** — valoarea care va fi atribuită tuturor cheilor (implicit `None`).

Exemplu 1: Folosirea **`fromkeys()`** cu o valoare specificată:

```python
keys = ['a', 'b', 'c']
new_dict = dict.fromkeys(keys, 0)
print(new_dict)  # Va afișa {'a': 0, 'b': 0, 'c': 0}
```

Exemplu 2: Folosirea **`fromkeys()`** fără valoare:

```python
keys = ['a', 'b', 'c']
new_dict = dict.fromkeys(keys)
print(new_dict)  # Va afișa {'a': None, 'b': None, 'c': None}
```

Această metodă este utilă atunci când vrem să creăm un dicționar cu un set de chei, dar valorile vor fi identice sau dorim doar să inițializăm dicționarul cu o valoare implicită.

### 11. **`clear()`**

Metoda este utilizată pentru ștergerea tuturor elementelor din dicționar. După aplicarea ei, dicționarul devine gol.

### Sintaxă:

```python
dict.clear()
```

* **Această metodă nu primește argumente.**

Exemplu de utilizare **`clear()`**:

```python
my_dict = {'a': 1, 'b': 2, 'c': 3}
print("Înainte de curățare:", my_dict)  # Va afișa: {'a': 1, 'b': 2, 'c': 3}

my_dict.clear()
print("După curățare:", my_dict)  # Va afișa: {}
```

După apelarea metodei **`clear()`**, toate perechile "cheie-valoare" din dicționar vor fi șterse, iar dicționarul va deveni gol.
Această metodă este utilă atunci când trebuie să golim dicționarul de toate elementele, dar dicționarul în sine rămâne disponibil pentru utilizare ulterioară.

### 12. **`copy()`**

Metoda **`copy()`** este utilizată pentru a crea o copie superficială a dicționarului. Aceasta înseamnă că se creează un nou dicționar care conține aceleași chei și valori ca și cel original, dar modificările în noul dicționar nu vor afecta dicționarul original.

### Sintaxă:

```python
new_dict = dict.copy()
```

### Exemplu de utilizare **`copy()`**:

```python
original_dict = {'a': 1, 'b': 2, 'c': 3}
new_dict = original_dict.copy()

print("Dicționar original:", original_dict)  # Va afișa: {'a': 1, 'b': 2, 'c': 3}
print("Copie a dicționarului:", new_dict)   # Va afișa: {'a': 1, 'b': 2, 'c': 3}

# Modificăm copia
new_dict['a'] = 10
print("Copie modificată:", new_dict)         # Va afișa: {'a': 10, 'b': 2, 'c': 3}
print("Dicționar original după modificarea copiei:", original_dict)  # Va afișa: {'a': 1, 'b': 2, 'c': 3}
```

Este important de menționat că metoda **`copy()`** creează o copie superficială, adică, dacă valorile din dicționar sunt obiecte modificabile (de exemplu, liste), acestea vor fi partajate între dicționarul original și copie.

---

### 13. **`setdefault()`**

Metoda **`setdefault()`** este utilizată pentru a obține valoarea asociată unei chei, iar dacă cheia nu există în dicționar, metoda adaugă cheia cu valoarea specificată. Ea returnează valoarea asociată cheii dacă aceasta există sau adaugă cheia cu valoarea dată și returnează această valoare.

### Sintaxă:

```python
dict.setdefault(key, default_value)
```

* **`key`** — cheia al cărei valoare dorim să o obținem.
* **`default_value`** — valoarea care va fi setată dacă cheia lipsește. Dacă nu este specificată, valoarea implicită este `None`.

### Exemplu de utilizare **`setdefault()`**:

```python
my_dict = {'a': 1, 'b': 2, 'c': 3}

# Obținem valoarea pentru cheia 'b'
print(my_dict.setdefault('b', 100))  # Va afișa: 2 (valoarea pentru 'b')

# Cheia 'd' lipsește, o adăugăm cu valoarea 4
print(my_dict.setdefault('d', 4))    # Va afișa: 4

# Dicționarul după adăugarea noii chei
print(my_dict)  # Va afișa: {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Dacă cheia 'a' există deja, ea nu se va schimba
print(my_dict.setdefault('a', 10))   # Va afișa: 1 (valoarea pentru 'a')
```

Metoda **`setdefault()`** este utilă atunci când dorim să adăugăm în siguranță o cheie nouă în dicționar fără a suprascrie valoarea existentă.

**Particularități**:

* Această metodă este utilă pentru iterarea valorilor din dicționar.
* Valorile pot fi de orice tip, inclusiv alte colecții, funcții etc.

**Observații suplimentare**:

* Dacă dicționarul este gol, apelarea metodei **`popitem()`** va genera eroarea `KeyError`.
* În Python 3.6 și versiunile anterioare, dicționarele nu erau ordonate, iar metoda **`popitem()`** returna o pereche arbitrară.
* Metoda **`keys()`** returnează o vizualizare a cheilor, nu o listă efectivă. Aceasta înseamnă că nu copiază cheile în memorie și operează cu datele curente ale dicționarului.
* Vizualizarea suportă iterația și poate fi folosită într-un ciclu sau convertită în alte colecții (de exemplu, listă).

Aceste metode sunt esențiale pentru lucrul cu dicționarele, permițând căutarea, modificarea, ștergerea și adăugarea de elemente.

---

### Tuple (kortejuri)

**Tuple** — este o colecție ordonată de date care este **imutabilă**. Elementele unui tuple pot fi de orice tip, iar tuple-urile pot conține elemente repetitive. Ele sunt folosite adesea pentru a stoca date care nu trebuie modificate.

#### Caracteristici principale:

* **Ordonate** (păstrează ordinea elementelor).
* **Imutabile** (elementele nu pot fi modificate după creare).
* **Indexare**: elementele pot fi accesate prin index.

Tuple-urile sunt folosite pentru protejarea datelor împotriva modificării și, în general, rulează mai rapid decât listele, deoarece nu se pot modifica dinamic.

#### Sintaxă:

```python
# Crearea unui tuple
my_tuple = (1, 2, 3, 4, 5)

# Accesarea elementelor
print(my_tuple[0])  # 1

# Tuple-urile pot conține tipuri de date diferite
mixed_tuple = (1, "apple", 3.14, True)

# Tuple-urile suportă slicing
print(my_tuple[1:3])  # (2, 3)
```

## Metode principale pentru tuple:

### 1. **`count(value)`**

Metoda returnează numărul de apariții ale valorii **`value`** în tuple.

Exemplu:

```python
my_tuple = (1, 2, 3, 1, 4, 1)
print(my_tuple.count(1))  # Va afișa: 3
```

### 2. **`index(value, start=0, end=len(tuple))`**

Metoda **`index()`** returnează indexul primei apariții a valorii **`value`**. Se poate specifica și un interval de căutare prin parametrii **`start`** și **`end`**.

Exemplu:

```python
my_tuple = (1, 2, 3, 4, 5)
print(my_tuple.index(3))         # Va afișa: 2

# Cu parametrii start și end
print(my_tuple.index(4, 2, 5))   # Va afișa: 3
```
### 3. **`__contains__(value)`**

Metoda **`__contains__()`** verifică dacă o valoare **`value`** se află în tuple. Este folosită atunci când aplicăm operatorul **`in`**.

Exemplu:

```python
my_tuple = (1, 2, 3, 4, 5)
print(3 in my_tuple)  # Va afișa: True
print(6 in my_tuple)  # Va afișa: False
```

### 4. **`len()`**

Deși **`len()`** este o funcție încorporată, este folosită frecvent cu tuple pentru a obține numărul de elemente din tuple.

Exemplu:

```python
my_tuple = (1, 2, 3, 4, 5)
print(len(my_tuple))  # Va afișa: 5
```

### 5. **`max()` și `min()`**

Acestea nu sunt metode ale tuple-urilor, dar pot fi folosite cu tuple pentru a obține valoarea maximă sau minimă.

Exemplu:

```python
my_tuple = (1, 2, 3, 4, 5)
print(max(my_tuple))  # Va afișa: 5
print(min(my_tuple))  # Va afișa: 1
```

Tuple-urile nu suportă metode de adăugare, ștergere sau modificare a elementelor, deoarece sunt imutabile. Totuși, metodele de mai sus sunt utile pentru analiza conținutului unui tuple.

#### Avantajele tuple-urilor:

* **Performanță**: tuple-urile ocupă mai puțină memorie și rulează mai rapid decât listele.
* **Folosire ca chei în dicționare**: deoarece tuple-urile sunt imutabile, ele pot fi folosite ca chei în dicționare (spre deosebire de liste).

#### Operații cu tuple:

* **Concatenare**: se pot combina două tuple-uri.

```python
tuple1 = (1, 2)
tuple2 = (3, 4)
print(tuple1 + tuple2)  # (1, 2, 3, 4)
```

* **Înmulțire**: se poate repeta un tuple de mai multe ori.

```python
tuple1 = (1, 2)
print(tuple1 * 3)  # (1, 2, 1, 2, 1, 2)
```

**Comparație**:

* Dicționarele sunt convenabile pentru stocarea perechilor "cheie-valoare", atunci când este nevoie de acces rapid după cheie.
* Tuple-urile sunt mai potrivite pentru reprezentarea colecțiilor imutabile de date, când ordinea contează, dar elementele nu trebuie modificate.

---

## Constructori de colecții

În Python există funcții speciale numite **constructori de colecții**, care permit transformarea datelor în diferite tipuri de colecții. Aceste funcții sunt folosite frecvent pentru a crea colecții noi din alte tipuri de date sau pentru a converti datele în colecții.

### 1. **`list()`**

Funcția `list()` creează o listă dintr-un obiect iterabil (de exemplu, șir, set, tuple, range etc.). Permite transformarea altor colecții în listă.

Exemplu:

```python
# Transformarea unui șir într-o listă
string = "hello"
list_from_string = list(string)
print(list_from_string)  # ['h', 'e', 'l', 'l', 'o']

# Transformarea unui range într-o listă
range_obj = range(5)
list_from_range = list(range_obj)
print(list_from_range)  # [0, 1, 2, 3, 4]
```

### 2. **`tuple()`**

Funcția `tuple()` creează un tuple din orice obiect iterabil. Tuple-urile sunt similare listelor, dar sunt imutabile.

Exemplu:

```python
# Transformarea unei liste într-un tuple
my_list = [1, 2, 3, 4]
tuple_from_list = tuple(my_list)
print(tuple_from_list)  # (1, 2, 3, 4)

# Transformarea unui șir într-un tuple
string = "hello"
tuple_from_string = tuple(string)
print(tuple_from_string)  # ('h', 'e', 'l', 'l', 'o')
```

### 3. **`set()`**

Funcția `set()` creează un set dintr-un obiect iterabil. Seturile în Python sunt colecții neordonate care nu permit elemente duplicate.

Exemplu:

```python
# Transformarea unei liste într-un set
my_list = [1, 2, 2, 3, 4, 4]
set_from_list = set(my_list)
print(set_from_list)  # {1, 2, 3, 4}

# Transformarea unui șir într-un set
string = "hello"
set_from_string = set(string)
print(set_from_string)  # {'h', 'e', 'l', 'o'}
```

### 4. **`dict()`**

Funcția `dict()` creează un dicționar. De obicei primește un obiect iterabil de perechi cheie-valoare sau se pot folosi argumente sub formă de cuvinte cheie.

Exemplu:

```python
# Transformarea unei liste de tuple-uri într-un dicționar
my_list = [("apple", 1), ("banana", 2), ("cherry", 3)]
dict_from_list = dict(my_list)
print(dict_from_list)  # {'apple': 1, 'banana': 2, 'cherry': 3}

# Crearea unui dicționar folosind cuvinte cheie
dict_from_keywords = dict(apple=1, banana=2, cherry=3)
print(dict_from_keywords)  # {'apple': 1, 'banana': 2, 'cherry': 3}
```

### 5. **`frozenset()`**

Funcția `frozenset()` creează un set imutabil. Este util atunci când este nevoie de un set care să nu fie modificat după creare.

Exemplu:

```python
# Transformarea unei liste într-un frozenset
my_list = [1, 2, 2, 3, 4]
frozenset_from_list = frozenset(my_list)
print(frozenset_from_list)  # frozenset({1, 2, 3, 4})

# Transformarea unui șir într-un frozenset
string = "hello"
frozenset_from_string = frozenset(string)
print(frozenset_from_string)  # frozenset({'h', 'e', 'l', 'o'})
```

### De ce să folosim constructorii de colecții?

Constructorii de colecții sunt utili atunci când trebuie să:

* Transformăm datele dintr-un tip în altul (de exemplu, din șir în listă).
* Ne asigurăm că o colecție nu conține elemente duplicate (de exemplu, la crearea unui set).
* Creăm o colecție cu restricții, cum ar fi un set imutabil cu `frozenset()`.

Aceste funcții permit o manipulare flexibilă a datelor și transformarea lor în tipul de colecție potrivit pentru operațiile ulterioare.
