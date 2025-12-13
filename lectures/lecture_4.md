### **Funcții în Python**

Funcțiile — sunt un concept important în programare, care permit organizarea codului, creșterea lizibilității acestuia, reducerea duplicării și fac programul mai flexibil. Să analizăm principalele caracteristici și avantaje ale utilizării funcțiilor în Python:

### Caracteristicile de bază ale funcțiilor:

1. **Bloc de cod care execută o sarcină**:
   Funcția reprezintă un bloc de cod care execută o anumită sarcină. Acest cod este rulat doar atunci când funcția este apelată.

2. **Împărțirea programului în părți**:
   Funcțiile ajută la împărțirea unui program mare în părți mai mici și mai ușor de înțeles. Fiecare bloc execută o sarcină separată, ceea ce face programul mai ușor de înțeles și de întreținut.

3. **Evitarea repetițiilor**:
   Utilizarea funcțiilor permite evitarea repetării aceluiași cod. În loc să scrii aceleași operații de mai multe ori, poți pur și simplu să apelezi funcția la momentul necesar.

4. **Transmiterea datelor**:
   În funcții pot fi transmise date pe care aceasta le va utiliza. Aceste date se numesc **parametri** sau **argumente**. Astfel, funcția poate lucra cu diferite valori de intrare.

5. **Returnarea valorilor**:
   Funcția poate returna o valoare sau rezultatul muncii sale folosind operatorul `return`. Acest lucru permite funcției să calculeze ceva și să transmită rezultatul înapoi în program.

### Avantajele utilizării funcțiilor:

* **Lizibilitate și organizare**: Funcțiile permit împărțirea codului în părți logice, ceea ce îmbunătățește structura programului.
* **Utilizare multiplă**: Funcțiile permit utilizarea aceluiași cod în diferite părți ale programului, ceea ce reduce duplicarea.
* **Controlabilitate**: Proiectele mari sunt mai ușor de întreținut și actualizat dacă sunt structurate cu ajutorul funcțiilor.

### **1. Crearea funcțiilor**

Crearea funcțiilor:

* În Python, funcțiile sunt create folosind cuvântul cheie `def`, urmat de numele funcției, lista de parametri (dacă există), două puncte și corpul funcției.\

Returnarea valorii:

* Folosiți cuvântul cheie return pentru a returna o valoare din funcție. Dacă în funcție nu există operatorul return, aceasta își va încheia oricum execuția, dar va returna valoarea None în mod implicit.
  **Sintaxă:**

```python
def function_name(parameters):
    # Corpul funcției
    # Operațiile care trebuie executate
    return value  # (opțional)
```

Exemplu de funcție care primește doi parametri și returnează suma lor:

```python
def add_numbers(a, b):
    return a + b

result = add_numbers(5, 3)
print(result)  # Va afișa: 8
```

### Cuvântul rezervat `pass` în Python

* `pass` este utilizat pentru a defini o declarație nulă (NULL).
* Spre deosebire de comentarii, care sunt ignorate de interpret, `pass` nu este ignorat.
* Instrucțiunea `pass` poate fi utilizată ca o construcție de rezervă atunci când programatorul nu știe ce cod trebuie să scrie pentru o funcție sau o clasă.
* De asemenea, `pass` este utilizat pentru a „lăsa” o funcție sau un bloc de cod gol, fără a provoca erori.

**Exemplu**:

```python
def nullFunction():
    pass

nullFunction()  # funcția nu face nimic
```

### **2. Argumentele și parametrii funcției**

* **Parametrii** — sunt variabilele care sunt definite în declarația funcției. Ei reprezintă datele pe care funcția le poate utiliza în corpul său.
* **Argumentele** — sunt valorile efective care sunt transmise funcției atunci când aceasta este apelată.

Funcțiile pot avea diferite tipuri de parametri:

#### **2.1. Argumente poziționale**

Acestea sunt cele mai simple argumente, care sunt transmise funcției într-o anumită ordine.

Exemplu:

```python
def greet(name, age):
    print(f"Hello, {name}. You are {age} years old.")

greet("Alice", 25)  # Argumente poziționale
```

#### **2.2. Argumente denumite**

La utilizarea argumentelor denumite, ordinea în care acestea sunt transmise nu contează. În schimb, se poate indica explicit numele parametrului.

Exemplu:

```python
def greet(name, age):
    print(f"Hello, {name}. You are {age} years old.")

greet(age=25, name="Alice")  # Argumente denumite
```

#### **2.3. Argumente cu valori implicite**

Funcțiile pot avea valori implicite pentru unii parametri. Dacă argumentul nu este transmis la apelul funcției, va fi utilizată valoarea implicită.

Exemplu:

```python
def greet(name, age=18):
    print(f"Hello, {name}. You are {age} years old.")

greet("Alice")  # Se utilizează valoarea implicită pentru age
```

#### **2.4. Număr variabil de argumente**

Folosind `*args`, se poate transmite un număr variabil de argumente poziționale. Acest lucru permite funcției să accepte orice număr de argumente.
Astfel, funcția va primi un tuplu de argumente și va putea accesa corespunzător elementele

Exemplu:

```python
def add_numbers(*args):
    return sum(args)

print(add_numbers(1, 2, 3))  # 6
print(add_numbers(4, 5, 6, 7, 8))  # 30
```

Folosind `**kwargs`, se poate transmite un număr variabil de argumente denumite.\
Astfel, funcția va primi un dicționar de argumente și va putea accesa corespunzător elementele:\
Exemplu:

```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25)  # Va afișa: name: Alice, age: 25
```

### **3. Returnarea valorilor**

Funcțiile pot returna un rezultat cu ajutorul operatorului `return`. Returnarea unei valori încheie execuția funcției și transmite rezultatul în locul apelului.

Exemplu:

```python
def square(x):
    return x ** 2

result = square(4)
print(result)  # 16
```

Dacă funcția nu returnează în mod explicit nicio valoare, Python returnează automat `None`.

Exemplu:

```python
def greet(name):
    print(f"Hello, {name}")

result = greet("Alice")
print(result)  # None
```

### **4. Funcții lambda**

Funcțiile lambda — sunt funcții anonime mici, care sunt definite cu ajutorul cuvântului cheie `lambda`. Ele sunt de obicei utilizate pentru operații unice, cum ar fi sortarea sau filtrarea.

Sintaxă:

```python
lambda arguments: expression
```

Exemplu:

```python
square = lambda x: x ** 2
print(square(5))  # 25
```

* O funcție lambda poate primi orice număr de argumente, dar poate conține doar o singură expresie. Această expresie este evaluată, iar rezultatul este returnat automat.
* Funcțiile lambda nu necesită specificarea explicită a comenzii `return`, deoarece rezultatul expresiei este returnat implicit.
* Expresiile lambda sunt utilizate frecvent în programarea funcțională.

**Exemplu**:

```python
# Funcție lambda în interiorul funcției map
numbers = [1, 2, 3, 4]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16]
```

Funcțiile lambda sunt utile atunci când este necesar să se definească rapid o funcție mică, de exemplu, pentru utilizare în `map()`, `filter()` sau `sorted()`.

#### Exemplu de utilizare a funcției `sorted()` cu o expresie lambda ca parametru

Funcția `sorted()` este utilizată pentru sortarea obiectelor iterabile. Ea returnează o listă sortată, fără a modifica obiectul original. În același timp, se poate specifica ordinea de sortare (crescătoare sau descrescătoare), precum și aplicarea unei logici proprii de sortare prin intermediul parametrului `key`.

**Sintaxă**:

```python
sorted(iterable, key=key, reverse=reverse)
```

* **iterable** — parametru obligatoriu, obiectul care trebuie sortat.
* **key** — parametru opțional, funcția care determină ordinea de sortare.
* **reverse** — parametru opțional, dacă este setat la `True`, sortarea va avea loc în ordine inversă.

### Exemplu:

```python
names = ['Alice', 'Jhon', 'Annie', 'David', 'Eve', 'Jhonny', 'Mary']

# Sortare după lungimea șirurilor
sorted_names = sorted(names, key=lambda x: len(x))
print(sorted_names)
```

**Rezultat**:

```
['Eve', 'Mary', 'Annie', 'Jhon', 'Alice', 'David', 'Jhonny']
```

Aici este utilizată funcția lambda `lambda x: len(x)`, care permite sortarea listei de șiruri după lungimea fiecărui element.

### **5. Funcții imbricate**

În Python, funcțiile pot fi imbricate, adică o funcție poate fi definită în interiorul altei funcții. Funcțiile imbricate pot utiliza variabile din funcția externă, ceea ce permite crearea de închideri (closures).

Exemplu:

```python
def outer_function(x):
    def inner_function(y):
        return y * 2
    return inner_function(x)

result = outer_function(5)
print(result)  # 10
```

### 6. Spații de nume

**Spațiul de nume** — este o colecție utilizată de nume. În Python se poate reprezenta
spațiul de nume ca o mapare a fiecărui nume definit către obiectele
corespunzătoare.

* Diferite spații de nume pot coexista într-un anumit moment de timp, dar
  ele sunt complet izolate.
* Spațiul de nume care conține toate numele încorporate este creat la pornirea
  interpretului Python și există până când încheiem execuția.
   Acesta este motivul pentru care funcțiile încorporate, cum ar fi `id()` (permite obținerea adresei din
  memoria RAM a unui anumit obiect), `print()` etc. sunt întotdeauna disponibile pentru noi din orice
  parte a programului. Fiecare modul creează propriul său spațiu de nume global.
* Aceste spații de nume diferite sunt izolate. Prin urmare, același nume, care
  poate exista în module diferite, nu intră în conflict.
* Modulele pot conține diferite funcții și clase. La apelarea unei funcții, se creează
  un spațiu de nume local, în care sunt definite toate numele utilizate în corpul
  funcției. În mod similar, lucrurile stau la fel și pentru o clasă.
*

### **7. Domeniul de vizibilitate (Scope)**

**Domeniul de acțiune (sau de vizibilitate)** — este partea programului din care
se poate accesa direct un spațiu de nume fără niciun
prefix (adică variabila este recunoscută).

În Python există mai multe niveluri ale domeniului de vizibilitate:

* **Domeniul de vizibilitate local** — variabilele definite în interiorul unei funcții.
* **Domeniul de vizibilitate al funcției** — variabilele definite în funcție, dar accesibile și pentru funcțiile imbricate.
* **Domeniul de vizibilitate global** — variabilele definite în afara tuturor funcțiilor, accesibile oriunde în program.
* **Domeniul de vizibilitate al funcțiilor încorporate** — funcțiile standard Python, cum ar fi `print()`.\
  Atunci când o referință este făcută în interiorul unei funcții, numele este căutat mai întâi
  în spațiul de nume local, apoi în spațiul de nume global și, în final,
  în spațiul de nume încorporat.

Exemplu:

```python
x = 10  # Variabilă globală

def my_function():
    x = 5  # Variabilă locală
    print(x)

my_function()  # Va afișa: 5
print(x)  # Va afișa: 10
```

Pentru a face o variabilă vizibilă și accesibilă la **nivel global**, se utilizează cuvântul cheie `global`.

#### Particularități:

1. **Variabilă locală**:

   * Este accesibilă doar în interiorul funcției.
   * Este distrusă după finalizarea execuției funcției.
2. **Cuvântul cheie `global`**:

   * Face variabila globală, chiar dacă este creată în interiorul funcției.
   * Permite modificarea unei variabile globale în interiorul funcției.

#### Exemplu:

```python
def my_phone():
    global phone  # Facem variabila globală
    phone = "78997788"
    return phone

phone = "69777777"  # Variabilă globală
print("Global phone number is", phone)  # Va afișa: 69777777
print("My phone number is --> " + my_phone())  # Va afișa: 78997788
print("Updated global phone number is", phone)  # Va afișa: 78997788
```

**Rezultat**:

```
Global phone number is 69777777
My phone number is --> 78997788
Updated global phone number is 78997788
```

#### Exemplu de modificare a unei variabile globale:

```python
x = 10  # Variabilă globală

def update_global():
    global x
    x += 5  # Modificăm valoarea variabilei globale
    print("Inside function:", x)

update_global()  # Va afișa: Inside function: 15
print("Outside function:", x)  # Va afișa: Outside function: 15
```

#### Când se utilizează `global`:

* Atunci când este necesară modificarea unei variabile globale în interiorul unei funcții.
* Dacă variabila trebuie să fie accesibilă atât în interiorul funcției, cât și în afara ei.

#### Important:

* Utilizarea lui `global` trebuie minimizată pentru a păstra lizibilitatea și predictibilitatea codului. În schimb, este mai bine să se transmită variabilele ca parametri ai funcției și să se returneze valorile acestora.
* Durata de viață a unei variabile este perioada în care
  variabila se află în memorie. Durata de viață a variabilelor din interiorul funcției este egală cu durata
  execuției acesteia.
* Ele sunt distruse imediat ce ne întoarcem din
  funcție (cu excepția cazului când este utilizat
  cuvântul cheie `global`). Prin urmare, funcția nu
  reține valoarea
  apelurilor anterioare.

---

### **8. Recursivitatea**

Recursivitatea — este situația în care o funcție se apelează pe ea însăși. Recursivitatea este adesea utilizată pentru rezolvarea problemelor care pot fi împărțite în subprobleme de același tip, de exemplu, în căutarea și sortarea datelor.

Exemplu de calcul al factorialului:

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n-1)

print(factorial(5))  # 120
```

### **9. Docstring-uri (docstrings)**

Docstring-urile — sunt șiruri de caractere care sunt plasate imediat după declararea unei funcții, pentru a descrie comportamentul acesteia. Ele ajută la îmbunătățirea lizibilității și mentenabilității codului.

Exemplu:

```python
def greet(name):
    """
    Funcție pentru salutarea utilizatorului după nume.
    
    :param name: Numele utilizatorului
    :return: Șir cu salutul
    """
    return f"Hello, {name}!"

print(greet.__doc__)  # Va afișa descrierea funcției
```

### 10. Module în Python

* **Modulul** — este un fișier care conține definiții de variabile și instrucțiuni Python.
* Modulele ajută la organizarea codului, făcând programele mai ușor de citit și de întreținut.
* Numele modulului corespunde numelui fișierului Python și are extensia `.py`.

#### Importarea modulelor

Pentru a utiliza conținutul unui modul, acesta trebuie **importat** folosind cuvântul cheie `import`.

#### Exemplu:

```python
import math
print(math.pi)  # 3.141592653589793
```

După import, toate funcțiile și variabilele modulului sunt disponibile folosind sintaxa `nume_modul.nume_atribut`.

### Importarea atributelor individuale

Se pot importa doar elemente specifice ale unui modul folosind `from ... import`.

#### Exemplu:

```python
from math import pi
print(pi)  # 3.141592653589793
```

---

### Separarea codului în module

În proiectele mari este util să se separe codul în module pentru comoditate și lizibilitate.

#### Exemplu:

Creăm două fișiere:

1. **`module_example5.py`** — conține funcții și date.
2. **`example5.py`** — apelează modulul și îl utilizează.

---

#### Conținutul fișierului `module_example5.py`:

```python
# Definirea dicționarului angajatului
employee = {
    "name": "John",
    "surname": "Smith",
    "age": 18,
    "phone_number": "+37368778899",
    "email": "john@gmail.com"
}

# Funcție pentru alcătuirea listei de preferințe
def choice(food):
    result = ""
    for x in food:
        result += "\n" + x
    return result
```

---

#### Conținutul fișierului `example5.py`:

```python
# Importăm modulul
import module_example5

# Utilizăm datele și funcțiile din modul
fruits = ["яблоки", "бананы", "черешня"]
print(
    "Angajatul {} preferă următoarele fructe:".format(
        module_example5.employee["name"]
    ) + module_example5.choice(fruits)
)
```

---

#### Rezultatul executării `example5.py`:

```
Angajatul John preferă următoarele fructe:
яблоки
бананы
черешня
```

Acest lucru ajută la structurarea proiectului: funcțiile, datele și logica de business sunt separate.

### Redenumirea modulelor folosind `as`

* Redenumirea unui modul la import permite simplificarea utilizării acestuia.
* Sintaxă:

  ```python
  import nume_modul as alias
  ```
* Este utilizată pentru a scurta sau a face mai convenabil numele modulului.

#### Exemplu:

```python
# Importul modulului cu alias
import module_example5 as m5

# Exemplu de utilizare
fruits = ["яблоки", "бананы", "черешня"]
print("Angajatul {} preferă următoarele fructe: ".format(m5.employee["name"]) + m5.choice(fruits))
```

În acest exemplu:

* Modulul `module_example5` este redenumit în `m5` pentru scurtare.
* Este ușor să accesăm conținutul modulului prin alias, de exemplu: `m5.employee["name"]`.
  Această metodă permite utilizarea atributelor importate direct, fără a indica numele complet al modulului.

### **Concluzie**

Funcțiile — sunt unul dintre cele mai puternice instrumente din Python. Ele permit structurarea codului, reutilizarea blocurilor de cod, lucrul cu argumente și returnarea valorilor. Utilizarea funcțiilor contribuie la îmbunătățirea lizibilității și mentenabilității programelor, în special în proiecte mari.
