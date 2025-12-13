# Instrucțiuni condiționale și cicluri

**Instrucțiunile condiționale** permit programului să execute anumite blocuri de cod în funcție de îndeplinirea condițiilor. Ele reprezintă baza pentru controlul fluxului de execuție în Python.

---

### Operatorii principali ai condițiilor:

1. **`if`**: Execută un bloc de cod dacă condiția este adevărată.
2. **`elif`** (prescurtare de la *else if*): Verifică o altă condiție, dacă cea precedentă este falsă.
3. **`else`**: Execută un bloc de cod dacă toate condițiile de mai sus sunt false.

---

### Sintaxă

```python
if condiție:
    # bloc de cod care se va executa dacă condiția este adevărată
elif altă_condiție:
    # bloc de cod care se va executa dacă altă_condiție este adevărată
else:
    # bloc de cod care se va executa dacă nicio condiție nu este îndeplinită
```

---

### Exemple:

#### Bloc simplu `if`:

```python
x = 10
if x > 5:
    print("x este mai mare decât 5")
```

**Rezultat**:

```
x este mai mare decât 5
```

---

#### Utilizarea `if-elif-else`:

```python
x = 15
if x < 10:
    print("x este mai mic decât 10")
elif x == 15:
    print("x este egal cu 15")
else:
    print("x este mai mare decât 15")
```

**Rezultat**:

```
x este egal cu 15
```

---

#### Condiții imbricate:

```python
x = 20
if x > 10:
    if x < 30:
        print("x este mai mare decât 10, dar mai mic decât 30")
```

**Rezultat**:

```
x este mai mare decât 10, dar mai mic decât 30
```

---

### Expresii condiționale

Python suportă **operatorul ternar** — o formă compactă de scriere a unei condiții.

#### Exemplu:

```python
x = 5
result = "pozitiv" if x > 0 else "negativ"
print(result)
```

**Rezultat**:

```
pozitiv
```

---

### Cod compact folosind tupluri

În Python pot fi utilizate tupluri pentru a scrie cod compact, care înlocuiește operatorii condiționali. Această abordare se bazează pe indexarea tuplului în funcție de rezultatul expresiei logice.

#### Sintaxă:

```python
(if_test_is_false, if_test_is_true)[test]
```

Unde:

* `if_test_is_false` — valoarea care va fi aleasă dacă `test` este `False` (sau `0`).
* `if_test_is_true` — valoarea care va fi aleasă dacă `test` este `True` (sau `1`).
* `test` — expresia logică.

---

### Exemplu:

#### Exemplul 1:

```python
nice = True  # Variabilă care determină starea
caract = ("ugly", "nice")[nice]  # Tuplul alege valoarea după index
print("The cat is", caract)
```

**Rezultat**:

```
The cat is nice
```

#### Exemplul 2:

```python
nice = False  # Variabilă care determină starea
caract = ("ugly", "nice")[nice]  # Index 0, deoarece nice = False
print("The cat is", caract)
```

**Rezultat**:

```
The cat is ugly
```

---

### Explicație:

1. Valoarea logică `True` este interpretată ca `1`, iar `False` ca `0`.
2. Indexarea tuplului `(if_test_is_false, if_test_is_true)[test]` folosește acest fapt:

   * Dacă `test = True`, este ales elementul cu indexul `1` (al doilea).
   * Dacă `test = False`, este ales elementul cu indexul `0` (primul).

---

### Avantaje:

* Scriere compactă.
* Convenabil pentru cazuri cu două valori posibile.

### Limitări:

* Această abordare nu este recomandată pentru condiții complexe, deoarece reduce lizibilitatea codului.
* Asigurați-vă că `test` ia întotdeauna valoarea `True` sau `False`. În caz contrar, rezultatul poate fi imprevizibil.

---

#### Pentru o lizibilitate și flexibilitate mai bună este adesea preferabil să se utilizeze operatorul ternar:

```python
caract = "nice" if nice else "ugly"
print("The cat is", caract)
```

**Rezultat**:

```
The cat is nice
```

---

### Operatorii de comparație

Operatorii de comparație sunt utilizați pentru verificarea condițiilor:

| Operator | Descriere         | Exemplu  |
| -------- | ----------------- | -------- |
| `==`     | Egal              | `x == y` |
| `!=`     | Diferit           | `x != y` |
| `<`      | Mai mic           | `x < y`  |
| `>`      | Mai mare          | `x > y`  |
| `<=`     | Mai mic sau egal  | `x <= y` |
| `>=`     | Mai mare sau egal | `x >= y` |

---

### Operatorii logici

Pentru combinarea mai multor condiții se folosesc **operatorii logici**:

| Operator | Descriere                                                  | Exemplu            |
| -------- | ---------------------------------------------------------- | ------------------ |
| `and`    | Returnează `True` dacă ambele condiții sunt adevărate      | `x > 5 and y < 10` |
| `or`     | Returnează `True` dacă cel puțin o condiție este adevărată | `x > 5 or y < 10`  |
| `not`    | Inversează condiția                                        | `not (x > 5)`      |

#### Exemplu:

```python
x = 10
y = 5
if x > 5 and y < 10:
    print("Ambele condiții sunt adevărate")
```

**Rezultat**:

```
Ambele condiții sunt adevărate
```

---

### Lucrul cu `in` și `not in`

Acești operatori sunt utilizați pentru verificarea existenței unui element în colecții (șiruri, liste, tupluri, dicționare).

#### Exemplu:

```python
fruits = ["яблоко", "банан", "вишня"]
if "яблоко" in fruits:
    print("Mărul există în listă")
```

**Rezultat**:

```
Mărul există în listă
```

---

### Exemple cu introducerea datelor

```python
age = int(input("Introduceți vârsta dumneavoastră: "))

if age < 18:
    print("Sunteți minor.")
elif age >= 18 and age < 65:
    print("Sunteți adult.")
else:
    print("Sunteți pensionar.")
```

**Rezultat (în funcție de datele introduse)**:

```
Introduceți vârsta dumneavoastră: 25
Sunteți adult.
```

---

### Analogia Switch…Case în Python

În Python nu există un operator încorporat `switch…case`, însă există mai multe modalități de a obține un comportament similar, folosind `if…elif…else`, dicționare sau funcții. Să analizăm principalele abordări.

---

### 1. Utilizarea `if…elif…else`

Aceasta este cea mai evidentă metodă de a gestiona condiții diferite.

#### Exemplu:

```python
option = int(input("Input the option...[1..3]: "))
if option == 1:
    print("Print")
elif option == 2:
    print("Read")
elif option == 3:
    print("Exit")
else:
    print("Repeat input")
```

---

### 2. Utilizarea dicționarelor

Dicționarele permit asocierea cheilor cu valori sau funcții specifice. Acesta este un analog simplu și comod al `switch…case`.

#### Exemplu:

```python
choices = {
    1: "Print",
    2: "Read",
    3: "Exit"
}

key = int(input("Input the option...[1..3]: "))
result = choices.get(key, "Repeat input")  # Dacă cheia nu este găsită, se folosește valoarea implicită
print(result)
```

---

### 3. Utilizarea funcțiilor în interiorul unui dicționar

Dacă este necesar să se execute acțiuni diferite pentru fiecare opțiune, se pot stoca funcții într-un dicționar.

#### Exemplu:

```python
def print_action():
    return "You chose to Print"

def read_action():
    return "You chose to Read"

def exit_action():
    return "You chose to Exit"

# Dicționarul de acțiuni
actions = {
    1: print_action,
    2: read_action,
    3: exit_action
}

key = int(input("Input the option...[1..3]: "))
action = actions.get(key, lambda: "Repeat input")  # Funcție lambda pentru valoarea implicită
print(action())  # Apelăm funcția selectată
```

---

### 4. Utilizarea unei funcții cu returnare din dicționar

Se poate crea o funcție care va returna valoarea corespunzătoare dintr-un dicționar.

#### Exemplu:

```python
def switch_case(option):
    return {
        1: "Print",
        2: "Read",
        3: "Exit"
    }.get(option, "Repeat input")  # Valoare implicită

print(switch_case(2))  # Read
print(switch_case(7))  # Repeat input
```

---

### Metoda `get()` în dicționare

Metoda `get()` permite extragerea în siguranță a unei valori după cheie. Dacă cheia nu există, se returnează valoarea implicită (sau `None`, dacă valoarea implicită nu este specificată).

#### Sintaxă:

```python
Dict.get(key, default=None)
```

#### Exemplu:

```python
my_dict = {"a": 1, "b": 2, "c": 3}

print(my_dict.get("b"))         # 2
print(my_dict.get("d"))         # None
print(my_dict.get("d", "N/A"))  # N/A
```

---

### **Construcția `match…case` în Python**

Odată cu apariția Python 3.10 a fost adăugat operatorul `match`, care permite utilizarea potrivirii structurale cu șabloane (structural pattern matching). Acesta este un instrument puternic pentru procesarea datelor de diferite tipuri și forme, care simplifică codul și îl face mai lizibil.

---

### **Caracteristicile principale ale construcției `match…case`**

* **Capabilități extinse:** `match` este mai mult decât un `switch` standard din alte limbaje, deoarece suportă potrivirea structurilor complexe de date.
* **Șabloane:** Construcția suportă secvențe, dicționare, tipuri de date primitive (`int`, `float`, `str` etc.), precum și instanțe de clase.
* **Îmbunătățirea lizibilității:** Simplifică procesarea datelor, înlocuind construcțiile complexe `if…elif…else`.

---

### **Sintaxă**

```python
match subject:
    case pattern1:
        # Acțiuni, dacă pattern1 se potrivește
    case pattern2:
        # Acțiuni, dacă pattern2 se potrivește
    case _:
        # Caracter joker (wildcard) pentru celelalte cazuri
```

---

### **Cum funcționează `match…case`**

1. **Compararea:** Expresia `subject` este comparată cu șabloanele specificate în `case`.
2. **Prioritatea:** Compararea are loc de sus în jos. De îndată ce este găsită o potrivire, se execută blocul corespunzător.
3. **Caracterul joker `_`:** Este utilizat ca „caz implicit”, dacă nu este găsită nicio altă potrivire.
4. **Tipul de date:** Literalii sunt comparați după valoare, iar singletonii (`True`, `False`, `None`) — după identitate.

---

### **Exemple de utilizare**

#### Exemplu simplu

```python
def check_status(code):
    match code:
        case 200:
            return "OK"
        case 404:
            return "Not Found"
        case 500:
            return "Internal Server Error"
        case _:
            return "Unknown Status Code"

print(check_status(200))  # OK
print(check_status(404))  # Not Found
print(check_status(123))  # Unknown Status Code
```

#### Structuri de date complexe

```python
data = {"type": "circle", "radius": 5}

match data:
    case {"type": "circle", "radius": r}:
        print(f"Circle with radius {r}")
    case {"type": "square", "side": s}:
        print(f"Square with side {s}")
    case _:
        print("Unknown shape")
```

#### Potrivirea secvențelor

```python
items = [1, 2, 3]

match items:
    case [1, 2, 3]:
        print("Exact match!")
    case [1, *_]:
        print("Starts with 1")
    case _:
        print("No match")
```

---

### **Șabloane în Structural Pattern Matching**

Șabloanele din construcția `match…case` în Python permit definirea condițiilor de potrivire a valorilor, care pot fi atât simple, cât și complexe. Este important de menționat că șabloanele nu doar verifică potrivirea cu o valoare, ci pot și extrage date pentru utilizare ulterioară. Să analizăm principalele tipuri de șabloane.

---

### **1. Valori simple**

### Exemplu: Potrivire cu o valoare unică

```python
match 'a':
    case 'a':
        print("Matched 'a'")
```

Acest șablon compară pur și simplu șirul `'a'` cu valoarea `'a'`. În cazul unei potriviri, se execută codul din blocul `case`.

---

### **2. Potrivirea cu colecții**

### Exemplu: Potrivirea cu o colecție de valori

```python
match ['a', 'b']:
    case ['a', 'b']:
        print("Matched list ['a', 'b']")
```

Acest șablon compară o colecție (listă) cu un conținut exact specificat.

### Exemplu: Extragerea valorilor dintr-o colecție

```python
match ['a', 42]:
    case ['a', value1]:
        print(f"Matched 'a' and extracted value1: {value1}")
```

Aici are loc potrivirea cu o colecție formată din două elemente. Al doilea element este salvat în variabila `value1`.

### Exemplu: Utilizarea operatorului `*` pentru colectarea elementelor rămase

```python
match ['a', 42, 'b', 56]:
    case ['a', *values]:
        print(f"Matched 'a' and collected remaining values: {values}")
```

În acest exemplu, cu ajutorul lui `*values`, toate elementele rămase din colecție după primul sunt salvate în variabila `values`. Acest șablon este util pentru lucrul cu colecții de lungime variabilă. Este important de menționat că într-un șablon poate exista un singur element cu `*`, care colectează toate celelalte valori.

---

### **3. Utilizarea operatorilor logici**

### Exemplu: Utilizarea operatorului `|` (OR)

```python
match 'b':
    case 'a' | 'b' | 'c':
        print("Matched 'a', 'b' or 'c'")
```

Operatorul `|` permite crearea unui șablon care se potrivește cu oricare dintre mai multe valori. În acest caz, șablonul se potrivește cu una dintre valorile `'a'`, `'b'` sau `'c'`.

### Exemplu: Utilizarea `|` cu extragerea valorii

```python
match 'b':
    case ('a' | 'b' | 'c') as letter:
        print(f"Matched '{letter}' and extracted letter.")
```

Aici este utilizat tot operatorul `|`, dar valoarea potrivită este atribuită variabilei `letter`, permițând folosirea ei ulterior.

---

## **4. Utilizarea caracterului joker `_`**

### Exemplu: Potrivirea cu o colecție care începe cu un element specific

```python
match ['z', 1, 2, 3]:
    case ['z', _]:
        print("Matched collection starting with 'z'")
```

Caracterul joker `_` este utilizat pentru a desemna orice valoare care nu ne interesează. În acest exemplu, șablonul se potrivește cu orice colecție care începe cu `'z'`, iar celelalte elemente sunt ignorate.

---

### **5. Șabloane cu combinații**

### Exemplu: Potrivirea cu un tuplu și extragerea valorilor

```python
match ('a', 5, 'z'):
    case ('a', number, _):
        print(f"Matched 'a' and extracted number: {number}")
```

Aici, un tuplu cu trei elemente este verificat, iar doar valorile de interes sunt extrase, celelalte fiind ignorate cu ajutorul caracterului joker `_`.

---

### **Avantajele `match…case`**

* Crește lizibilitatea codului, simplificând procesarea datelor complexe.
* Oferă flexibilitate în lucrul cu secvențe, dicționare și obiecte.
* Permite potrivirea cu tipuri de date și extragerea valorilor.

### Sfaturi utile:

1. **Evitați condițiile redundante**: verificați doar ceea ce este necesar.
2. **Folosiți operatorii logici pentru a simplifica codul**.
3. **Testați cazurile limită**: verificați cum funcționează codul cu date de intrare diferite.

---

# Cicluri în Python

Ciclurile sunt unul dintre cele mai importante instrumente ale programării, deoarece permit
executarea repetată a anumitor blocuri de cod.
În Python există două tipuri principale de cicluri: **for** și **while** (ciclu controlat de numărare și ciclu controlat de condiție). În această lecție le vom analiza în detaliu sintaxa, particularitățile și exemplele de utilizare.

---

## **1. Ciclul `for`**

Ciclul `for` este utilizat pentru a parcurge elementele unei secvențe (de exemplu, listă, șir, tuplu) sau ale altor obiecte iterabile (dicționare, mulțimi). Acest ciclu execută un bloc de cod pentru fiecare element din secvență.

### **Sintaxa ciclului `for`**

```python
for element in secvență:
    # bloc de cod
```

### **Exemplu: Parcurgerea elementelor dintr-o listă**

```python
fruits = ["mere", "banane", "cireșe"]
for fruit in fruits:
    print(fruit)
```

Rezultat:

```
mere
banane
cireșe
```

Ciclul `for` parcurge pe rând toate elementele din listă și execută codul din bloc. Variabila `fruit` conține elementul curent al listei la fiecare iterație.

---

### **Ciclul `for` cu funcția `range`**

Funcția `range` generează o secvență de numere și este adesea utilizată pentru a specifica un interval de indici într-un ciclu.

#### **Sintaxă:**

```python
for i in range(start, stop, step):
    # bloc de cod
```

* `start`: valoarea de început (inclusiv, implicit 0).
* `stop`: valoarea de final (neinclusiv).
* `step`: pasul (implicit 1).

### **Exemplu: Afișarea numerelor de la 1 la 5**

```python
for i in range(1, 6):
    print(i)
```

Rezultat:

```
1
2
3
4
5
```

### **Exemplu: Utilizarea unui pas**

```python
for i in range(0, 10, 2):
    print(i)
```

Rezultat:

```
0
2
4
6
8
```

Aici ciclul parcurge numerele de la 0 la 9 cu pasul 2.

---

## **2. Ciclul `while`**

Ciclul `while` execută un bloc de cod atât timp cât condiția este adevărată. Acest tip de ciclu este folosit, de obicei, atunci când numărul de iterații nu este cunoscut dinainte și execuția continuă până la îndeplinirea unei condiții.

### **Sintaxa ciclului `while`**

```python
while condiție:
    # bloc de cod
```

### **Exemplu: Ciclu controlat de condiție**

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

Rezultat:

```
0
1
2
3
4
```

Ciclul continuă să se execute atâta timp cât variabila `i` este mai mică decât 5. După fiecare iterație, valoarea lui `i` este incrementată cu 1.

----

## **3. Controlul ciclurilor: `break`, `continue`, `else`**

### **3.1 Operatorul `break`**

Operatorul `break` este utilizat pentru a ieși imediat dintr-un ciclu, indiferent dacă condiția de continuare mai este sau nu îndeplinită.

### **Exemplu: Utilizarea `break` pentru ieșirea din ciclu**

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

Rezultat:

```
0
1
2
3
4
```

Ciclul se va opri atunci când variabila `i` devine egală cu 5.

---

### **3.2 Operatorul `continue`**

Operatorul `continue` sare peste iterația curentă și continuă execuția ciclului cu următorul pas.

### **Exemplu: Utilizarea `continue` pentru a sări peste numerele pare**

```python
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
```

Rezultat:

```
1
3
5
7
9
```

În acest exemplu, numerele pare sunt ignorate.

---

### **3.3 Operatorul `else`**

În Python, ciclurile pot avea un bloc `else`, care se execută dacă ciclul se încheie normal (fără a fi întrerupt de `break`).

### **Exemplu: Ciclu cu `else`**

```python
for i in range(3):
    print(i)
else:
    print("Ciclul s-a încheiat")
```

Rezultat:

```
0
1
2
Ciclul s-a încheiat
```

Dacă ciclul nu este întrerupt cu `break`, blocul `else` va fi executat.

---

## **4. Cicluri imbricate**

Ciclurile pot fi imbricate unul în altul. Ciclul exterior rulează de mai multe ori, iar pentru fiecare iterație a acestuia se execută ciclul interior.

### **Exemplu: Cicluri imbricate**

```python
for i in range(3):
    for j in range(2):
        print(f"i = {i}, j = {j}")
```

Rezultat:

```
i = 0, j = 0
i = 0, j = 1
i = 1, j = 0
i = 1, j = 1
i = 2, j = 0
i = 2, j = 1
```

Ciclul exterior se execută de trei ori, iar pentru fiecare iterație, ciclul interior se execută de două ori.

---

## **1. List Comprehension**

### **Ce este List Comprehension?**

**List Comprehension** este o modalitate concisă și expresivă de a crea liste în Python. În loc să folosim un ciclu `for` clasic pentru a adăuga elemente într-o listă, putem construi o listă nouă pe baza uneia existente, aplicând transformări și filtre într-o singură expresie.

### **Sintaxa List Comprehension**

```python
[expresie for element in obiect_iterabil if condiție]
```

* **expresie**: elementul care va fi adăugat în noua listă (poate include operații).
* **element**: variabila care parcurge elementele.
* **obiect_iterabil**: colecția parcursă (listă, șir, tuplu etc.).
* **condiție** (opțional): filtru pentru selectarea elementelor.

---

### **Exemple de List Comprehension**

#### 1. **Exemplu simplu**

```python
squares = [x**2 for x in range(5)]
print(squares)
```

Rezultat:

```
[0, 1, 4, 9, 16]
```

Am creat o listă cu pătratele numerelor de la 0 la 4.

---

#### 2. **Cu condiție**

```python
even_squares = [x**2 for x in range(10) if x % 2 == 0]
print(even_squares)
```

Rezultat:

```
[0, 4, 16, 36, 64]
```

Lista conține doar pătratele numerelor pare.

---

#### 3. **Transformarea șirurilor**

```python
words = ["apple", "banana", "cherry"]
uppercased = [word.upper() for word in words]
print(uppercased)
```

Rezultat:

```
['APPLE', 'BANANA', 'CHERRY']
```

---

### **Avantajele List Comprehension**

* **Lizibilitate**: cod mai scurt și mai clar.
* **Performanță**: de obicei mai rapid decât un ciclu `for` clasic.

---

## **2. Funcția `enumerate`**

### **Ce este `enumerate`?**

Funcția **`enumerate`** este utilizată pentru a obține simultan indexul și valoarea elementelor dintr-un obiect iterabil. Este foarte utilă atunci când aveți nevoie atât de element, cât și de poziția lui.

### **Sintaxa `enumerate`**

```python
enumerate(obiect_iterabil, start=0)
```

* **obiect_iterabil**: secvența parcursă.
* **start** (opțional): valoarea de început a indexului.

---

### **Exemplu de utilizare `enumerate`**

```python
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(f"Index: {index}, Fruit: {fruit}")
```

Rezultat:

```
Index: 0, Fruit: apple
Index: 1, Fruit: banana
Index: 2, Fruit: cherry
```

---

### **Utilizarea `enumerate` cu index de start**

```python
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits, start=1):
    print(f"Index: {index}, Fruit: {fruit}")
```

Rezultat:

```
Index: 1, Fruit: apple
Index: 2, Fruit: banana
Index: 3, Fruit: cherry
```

---

### **Avantajele funcției `enumerate`**

* **Comoditate**: nu mai este nevoie să gestionați manual indexul.
* **Claritate**: cod mai curat și mai ușor de înțeles.

---

## **3. Modulul `random`**

Modulul **`random`** oferă funcții pentru generarea numerelor aleatoare și pentru efectuarea de operații aleatorii. Este utilizat frecvent în simulări, jocuri și aplicații probabilistice.

### **Funcții principale din modulul `random`**

1. **`random.random()`** — număr real aleator între 0 și 1.

```python
import random
print(random.random())
```

---

2. **`random.randint(a, b)`** — număr întreg aleator între `a` și `b` (inclusiv).

```python
print(random.randint(1, 10))
```

---

3. **`random.choice(sequence)`** — alege un element aleator dintr-o secvență.

```python
fruits = ["apple", "banana", "cherry"]
print(random.choice(fruits))
```

---

4. **`random.shuffle(sequence)`** — amestecă elementele unei liste.

```python
cards = [1, 2, 3, 4, 5]
random.shuffle(cards)
print(cards)
```

---

5. **`random.sample(sequence, k)`** — selectează `k` elemente unice aleator.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(random.sample(numbers, 3))
```

---

6. **`random.uniform(a, b)`** — număr real aleator între `a` și `b`.

```python
print(random.uniform(1, 10))
```

---

### **Exemplu: Simularea aruncării unei monede**

```python
flip = random.choice(["Heads", "Tails"])
print(f"Rezultatul aruncării monedei este: {flip}")
```

---

### **Avantajele modulului `random`**

* **Flexibilitate**: multe funcții utile pentru lucrul cu aleatoriu.
* **Simplitate**: ușor de utilizat și integrat în aplicații.

---

## **Concluzie**

* Ciclul **`while`** este folosit atunci când nu se cunoaște dinainte numărul exact de iterații.
* Ciclul **`for`** este ideal atunci când știm câte elemente trebuie parcurse sau lucrăm cu o secvență.

Alegerea între `for` și `while` depinde de problema concretă: 
   - dacă există un număr clar de pași sau o colecție, **`for`** este mai potrivit;
   - dacă execuția depinde de o condiție, **`while`** este alegerea corectă.
