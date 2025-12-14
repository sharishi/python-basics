# Programare Orientată pe Obiecte (OOP) în Python

Python este un limbaj de programare multiparadigmă, ceea ce înseamnă că suportă mai multe stiluri de programare.
Unul dintre abordările populare pentru rezolvarea problemelor de programare este crearea de obiecte sau utilizarea programării orientate pe obiecte (OOP).

---

**Programarea Orientată pe Obiecte (OOP)** este o paradigmă de programare care organizează codul în jurul obiectelor, nu al acțiunilor. În OOP, obiectele combină datele și funcțiile care lucrează cu aceste date într-o entitate unică. Aceasta permite crearea de programe mai flexibile, scalabile și ușor de întreținut.

În Python, programarea orientată pe obiecte se bazează pe utilizarea **claselor** și **obiectelor**.

---

### 1. **Clase și obiecte**

#### Clasa

O clasă este un fel de șablon sau plan pentru crearea obiectelor. Ea descrie ce atribute (proprietăți) și metode (funcții) vor avea obiectele create pe baza ei. Clasa nu este un obiect în sine, ci servește ca instrucțiune pentru crearea obiectelor.

Când creezi un obiect dintr-o clasă, acesta moștenește toate atributele și metodele definite în clasă. Atributele stochează date, iar metodele efectuează operații pe aceste date.

**Definirea unei clase**:

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name  # atribut
        self.breed = breed  # atribut
    
    def bark(self):  # metodă
        print(f"{self.name} spune Ham!")
```

#### Despre constructori

* `__init__`: Constructorul (sau inițializatorul) este apelat la crearea unui nou obiect. Inițializează atributele obiectului.

  * `__init__()` este o funcție încorporată a clasei.
  * Este apelat automat o singură dată pentru fiecare obiect creat și nu poate fi apelat manual ulterior.
* `self`: Referința la instanța curentă a obiectului. Toate atributele și metodele clasei se accesează prin `self`.

#### Obiect

Obiectul este o instanță concretă a unei clase. Fiecare obiect creat pe baza clasei moștenește atributele și metodele, dar poate avea valori unice pentru atributele sale.

**Crearea obiectelor**:

```python
dog1 = Dog("Buddy", "Golden Retriever")
dog2 = Dog("Max", "Beagle")

dog1.bark()  # Buddy spune Ham!
dog2.bark()  # Max spune Ham!
```

---

### 2. **Atribute și metode**

* **Atribute**: Variabile definite în interiorul clasei, folosite pentru a stoca date specifice fiecărui obiect. Ele permit obiectului să conțină informații despre proprietățile sale.
  Exemplu: Pentru obiectul clasei "Mașină", atributele pot fi marca ("Toyota"), culoarea ("roșu"), anul fabricației (2020) și viteza (150 km/h).

* **Metode**: Funcții definite în interiorul clasei, care efectuează acțiuni legate de obiect. Ele pot modifica datele obiectului, efectua calcule sau returna informații despre starea obiectului.
  Exemplu: Pentru clasa "Mașină", metoda `porneste_motor()` poate porni motorul, `franeaza()` reduce viteza, iar `descriere()` returnează un șir cu informații despre marcă, culoare și anul fabricației.

**Exemplu cu atribute și metode**:

```python
class Car:
    def __init__(self, brand, model, year):
        self.brand = brand
        self.model = model
        self.year = year
    
    def display_info(self):
        print(f"{self.year} {self.brand} {self.model}")
```

**Crearea obiectului și apelul metodei**:

```python
car = Car("Toyota", "Camry", 2020)
car.display_info()  # 2020 Toyota Camry
```

---

# Totul în Python este obiect

Aceasta înseamnă că orice entitate cu care lucrezi — numere, șiruri, liste, funcții sau module — este un obiect.
Fiecare obiect are valori (stare) și metode (acțiuni), deoarece toate obiectele sunt create pe baza claselor.
Clasa poate fi considerată un șablon care definește ce date (atribute) și comportament (metode) va avea obiectul creat.

Exemple:

* Clasa `int` definește obiecte care reprezintă numere întregi.
* Clasa `list` definește structura listelor și metodele pentru manipularea lor, cum ar fi adăugarea sau ștergerea elementelor.

Clasele sunt baza OOP, permițând organizarea codului și crearea unor structuri de date complexe care includ atât date, cât și funcții pentru procesarea lor.

---

### 3. Proprietăți și atribute în Python

1. **Proprietăți ale obiectului**
   Ele descriu comportamentul și starea obiectului și pot fi implementate folosind atributele instanței sau ale clasei.

2. **Atributul instanței (atribut dinamic)**
   Este o variabilă care aparține unui obiect concret. Este definită pentru un singur obiect și poate fi folosită doar în contextul acestuia. Se creează în constructorul `__init__(self, ...)` și poate avea valori diferite pentru fiecare instanță.

3. **Atributul clasei (atribut static)**
   Este o variabilă care aparține clasei însăși, nu obiectelor individuale. Toate obiectele clasei pot folosi același atribut. Se definește în afara constructorului și poate fi accesat fără a crea un obiect.

---

### Exemple de atribute de instanță și de clasă

1. **Atribut de instanță**

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand  # atribut instanță
        self.model = model  # atribut instanță

car1 = Car("Tesla", "Model S")
car2 = Car("BMW", "X5")

print(car1.brand)  # Tesla
print(car2.brand)  # BMW
```

2. **Atribut de clasă**

```python
class Car:
    wheels = 4  # atribut de clasă comun tuturor instanțelor

    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

car1 = Car("Tesla", "Model S")
car2 = Car("BMW", "X5")

print(car1.wheels)  # 4
print(car2.wheels)  # 4
print(Car.wheels)   # 4
```

În exemplul de mai sus, `wheels` este atributul clasei, comun tuturor obiectelor și accesibil atât prin instanțe, cât și prin clasă.

### 4. Gestionarea accesului în limbajele orientate pe obiecte

În limbajele clasice orientate pe obiecte, precum C++ și Java, accesul la membrii unei clase este controlat prin cuvintele cheie `public`, `private` și `protected`. Aceste cuvinte cheie ajută la implementarea principiului **încapsulării**, care limitează accesul la date și metode, permițând gestionarea modului în care acestea sunt utilizate.
În Python, nu există un mecanism încorporat pentru restricționarea strictă a accesului la variabilele sau metodele unei clase. În schimb, se folosește convenția prefixării numelui variabilei sau metodei cu unul sau două underscore-uri pentru a emula comportamentul specificatorilor de acces „protected” și „private”. Implicit, toți membrii unei clase sunt publici și pot fi accesați din exterior.

---

#### 1. **Private (Membri privați ai clasei)**

Membrii privați ai clasei (variabile și metode) nu sunt de regulă accesibili din exteriorul clasei. Aceștia pot fi utilizați doar în interiorul clasei, ascunzând detaliile de implementare și prevenind folosirea incorectă a datelor din codul extern. Membrii privați sunt de obicei încapsulați pentru a asigura interacțiuni sigure cu obiectul.

**Exemplu:**

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.__balance = balance  # Variabilă privată

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
        else:
            print("Suma trebuie să fie pozitivă")

    def get_balance(self):
        return self.__balance

account = BankAccount("Alice")
account.deposit(100)
print(account.get_balance())  # Va afișa: 100

# Eroare: Nu se poate accesa variabila privată
# print(account.__balance)  # Atributul 'BankAccount' este privat
```

Aici, variabila `__balance` este privată și nu poate fi accesată din exterior. Accesul se face prin metodele `deposit` și `get_balance`.

---

#### 2. **Public (Membri publici ai clasei)**

Membrii publici ai clasei (de regulă metodele) sunt accesibili din exterior. Pentru a apela o metodă publică, este suficient să creezi o instanță a clasei. Membrii publici constituie interfața principală pentru interacțiunea cu obiectul.

**Exemplu:**

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def start_engine(self):
        print(f"{self.brand} {self.model} motorul a fost pornit.")

car = Car("Tesla", "Model 3")
car.start_engine()  # Va afișa: Tesla Model 3 motorul a fost pornit.
```

În acest exemplu, metoda `start_engine` este publică și poate fi apelată din exterior, creând un obiect al clasei `Car`.

---

#### 3. **Protected (Membri protejați ai clasei)**

Membrii protejați ai clasei sunt accesibili în interiorul clasei și în clasele derivate (subclase). Accesul protejat limitează folosirea datelor din exterior, dar permite moștenitorilor să lucreze cu ele, sprijinind principiul **moștenirii**.

**Exemplu:**

```python
class Animal:
    def __init__(self, name):
        self.name = name
        self._health = 100  # Atribut protejat

    def get_health(self):
        return self._health

class Dog(Animal):
    def __init__(self, name):
        super().__init__(name)

    def bark(self):
        print(f"{self.name} spune: Ham!")

    def decrease_health(self, damage):
        self._health -= damage

dog = Dog("Rex")
dog.bark()  # Va afișa: Rex spune: Ham!
dog.decrease_health(10)
print(dog.get_health())  # Va afișa: 90

# Eroare: Nu se poate accesa atributul protejat din exterior
# print(dog._health)  # Atributul '_health' este protejat
```

Aici, atributul `_health` este protejat. Este accesibil în clasa `Animal` și în subclasa `Dog`, dar nu poate fi modificat direct din exterior.

---

### Destructorii și ștergerea atributelor și obiectelor în Python

În Python, destructorii și mecanismele de ștergere a obiectelor sunt gestionate de colectorul de gunoi (garbage collector), care elimină automat obiectele când nu mai există referințe către ele. Totuși, Python permite și ștergerea explicită a atributelor și obiectelor folosind metode și operatori speciali.

#### 4. **Destructorii în Python**

Destructorul este o metodă apelată automat la distrugerea obiectului. În Python, se numește `__del__`. Este apelat când obiectul nu mai este accesibil (nu mai există referințe către el).

**Exemplu:**

```python
class MyClass:
    def __init__(self, name):
        self.name = name
        print(f"Obiectul {self.name} a fost creat")

    def __del__(self):
        print(f"Obiectul {self.name} a fost distrus")

obj = MyClass("Obiect Test")
del obj  # Apel explicit al destructorului
```

Ieșire:

```
Obiectul Obiect Test a fost creat
Obiectul Obiect Test a fost distrus
```

Destructorul este folosit pentru eliberarea resurselor, cum ar fi închiderea fișierelor sau a conexiunilor de rețea.
**Notă**: Destructorul nu este întotdeauna apelat imediat ce obiectul iese din domeniul de vizibilitate, colectorul de gunoi poate elibera memoria cu întârziere.

---

#### 5. **Ștergerea atributelor**

Atributele unui obiect pot fi șterse cu funcția `del`. Aceasta permite ștergerea atât a atributelor, cât și a obiectului însuși.

**Exemplu:**

```python
class MyClass:
    def __init__(self, name):
        self.name = name

obj = MyClass("Obiect Test")
print(obj.name)  # Va afișa: Obiect Test
del obj.name     # Ștergerea atributului
# Eroare: Atributul 'name' nu mai există
# print(obj.name)  # AttributeError: 'MyClass' object has no attribute 'name'
```

Aici, atributul `name` este șters cu operatorul `del`, iar accesul ulterior la acesta va genera o eroare.
### 3. **Ștergerea obiectelor**

Pentru a șterge complet un obiect (adică toate referințele către acesta), se folosește operatorul `del`. Acesta nu distruge obiectul imediat, ci doar reduce contorul de referințe al obiectului. Când contorul de referințe ajunge la zero, obiectul este distrus de colectorul de gunoi (garbage collector).

**Exemplu:**

```python
class MyClass:
    def __init__(self):
        print("Obiect creat")

obj1 = MyClass()
obj2 = obj1  # Se creează o a doua referință către obiect

del obj1  # Ștergerea primei referințe
# Obiectul încă există pentru că există referința obj2

del obj2  # Ștergerea celei de-a doua referințe
# Acum obiectul este distrus
```

În acest exemplu, obiectul va fi șters numai după ce ambele referințe (`obj1` și `obj2`) au fost eliminate.

---

### 4. **Ștergerea automată: Garbage Collector**

Python folosește un colector de gunoi pentru gestionarea automată a memoriei. Acesta urmărește obiectele și elimină automat pe cele care nu mai sunt folosite (când nu mai există referințe către ele). Sistemul de colectare folosește **contorul de referințe** și **algoritmul pentru detectarea ciclurilor**, pentru a elibera memoria la timp.

**Exemplu:**

```python
import gc

class MyClass:
    def __init__(self):
        print("Obiect creat")

obj = MyClass()
del obj  # Ștergerea explicită a obiectului
gc.collect()  # Apel manual al colectorului de gunoi
```

Deși obiectul este șters cu `del`, uneori este nevoie să apelăm colectorul de gunoi manual prin `gc.collect()` pentru a ne asigura că obiectele neutilizate sunt distruse.

---

### Rezumat:

* **Destructorul `__del__`** este apelat când obiectul este distrus de colectorul de gunoi.
* **Ștergerea atributelor** se face cu operatorul `del`.
* **Ștergerea obiectelor** se realizează cu `del`, dar obiectul va fi distrus numai când nu mai există referințe către el.
* **Garbage collector-ul** gestionează automat memoria, însă uneori se poate apela manual prin modulul `gc`.

---

## **Decoratori în Python**

**Decoratori** în Python sunt funcții care permit modificarea sau extinderea comportamentului altor funcții sau metode. Ei funcționează ca un învelitor (wrapper) în jurul unei funcții sau metode și pot adăuga logică suplimentară fără a modifica funcția originală. Decoratorii sunt utilizați pentru reutilizarea codului, îmbunătățirea lizibilității și respectarea principiilor de încapsulare și abstractizare.

---

### 1. **Ce este un decorator?**

Un decorator este o funcție care primește o altă funcție ca argument și returnează o funcție nouă, de obicei cu comportament extins sau modificat.

**Exemplu simplu:**

```python
def my_decorator(func):
    def wrapper():
        print("Înainte de apelul funcției.")
        func()  # apelul funcției originale
        print("După apelul funcției.")
    return wrapper

@my_decorator
def say_hello():
    print("Salut!")

say_hello()
```

**Ieșire:**

```
Înainte de apelul funcției.
Salut!
După apelul funcției.
```

Aici:

* `my_decorator` adaugă comportament înainte și după funcția `say_hello`.
* `@my_decorator` este un „syntactic sugar” care echivalează cu `say_hello = my_decorator(say_hello)`.

---

### 2. **Decoratori cu argumente**

Dacă funcția decorată primește argumente, decoratorul trebuie să le gestioneze. Se poate folosi `*args` și `**kwargs` pentru a transmite orice argumente.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Înainte de apelul funcției cu argumente.")
        result = func(*args, **kwargs)
        print("După apelul funcției.")
        return result
    return wrapper

@my_decorator
def greet(name):
    print(f"Salut, {name}!")

greet("Alice")
```

**Ieșire:**

```
Înainte de apelul funcției cu argumente.
Salut, Alice!
După apelul funcției.
```

---

### 3. **Decoratori cu valoare returnată**

Decoratorii pot modifica și valoarea returnată a funcției.

```python
def multiply_decorator(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result * 2
    return wrapper

@multiply_decorator
def add(a, b):
    return a + b

print(add(2, 3))  # 10
```

Aici, `multiply_decorator` înmulțește rezultatul funcției `add` cu 2.

---

### 4. **Folosirea `functools.wraps`**

Pentru a păstra numele și documentația funcției originale, se folosește `functools.wraps`.

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Înainte de funcție.")
        result = func(*args, **kwargs)
        print("După funcție.")
        return result
    return wrapper

@my_decorator
def say_hello():
    """Funcție care salută."""
    print("Salut!")

print(say_hello.__name__)  # say_hello
print(say_hello.__doc__)   # Funcție care salută.
```

Fără `@wraps`, funcția decorată își poate pierde numele și docstring-ul. `@wraps(func)` păstrează aceste metadate.

---

### Concluzii:

* Decoratorii permit extinderea sau modificarea comportamentului funcțiilor și metodelor fără a schimba codul original.
* Decoratori precum `@property` permit controlul accesului la atributele claselor.
* Pentru păstrarea metadatelor originale, folosiți `functools.wraps`.

---
### Principiile OOP
---

### Abstracția în programarea orientată pe obiecte

**Abstracția** este procesul de creare a unui model simplificat al unui obiect, care permite concentrarera doar pe cele mai importante caracteristici, ignorând detalii mai puțin relevante sau irelevante în anumit context. În programare, abstracția ajută la simplificarea sistemelor complexe, ascunzând complexitatea internă a obiectelor și lăsând doar informațiile necesare pentru a lucra cu ele.

#### Exemplu de abstracție în viața reală:

Când vorbim despre un **laptop**, nu ne gândim la toate detaliile precum materialul carcasei (plastic, metal), componentele interne (ecran LCD, circuite integrate etc.) sau mecanismele de funcționare. Percepem laptopul ca un obiect unic cu funcții principale, precum procesarea datelor și conectarea la internet. Important pentru noi este ce poate face laptopul, nu cum funcționează intern. Acesta este un exemplu de abstracție — ignorăm detaliile secundare și ne concentrăm pe esențial.

#### De ce este nevoie de abstracție în programare?

Abstracția permite:

* **Reducerea complexității**: izolând detaliile de implementare, putem concentra atenția asupra aspectelor cheie ale obiectului sau sistemului.
* **Simplificarea dezvoltării**: dezvoltatorii pot lucra cu obiecte sau funcții fără a se preocupa de modul în care sunt implementate intern.
* **Îmbunătățirea lizibilității codului**: ascunderea logicii complexe și expunerea doar a interfeței fac codul mai ușor de înțeles și utilizat.

#### Exemplu de abstracție în OOP:

Să presupunem că avem o clasă care reprezintă un vehicul. Prin abstracție putem ascunde detalii precum mecanismul motorului sau suspensia, oferind doar funcții principale precum deplasare, oprire și accelerare.

```python
class Vehicle:
    def start_engine(self):
        print("Motor pornit")
        
    def stop_engine(self):
        print("Motor oprit")
        
class Car(Vehicle):
    def open_trunk(self):
        print("Portbagaj deschis")
        
class Bicycle(Vehicle):
    def ring_bell(self):
        print("Clopoțel sună")

# Utilizarea abstracției
car = Car()
car.start_engine()  # Pornire motor
car.open_trunk()    # Deschidere portbagaj

bike = Bicycle()
bike.start_engine()  # Pornire motor
bike.ring_bell()     # Sunet clopoțel
```

Aici, **Vehicle** reprezintă o abstracție pentru toate vehiculele, ascunzând detalii de implementare. Putem lucra cu obiectele **Car** și **Bicycle** cunoscând doar acțiunile principale (de exemplu, pornirea motorului sau clopoțelul bicicletei), fără a ști cum sunt implementate intern.

---

### 1. **Încapsularea**

### Principiul încapsulării datelor

Încapsularea este principiul OOP prin care datele interne ale unui obiect sunt ascunse față de exterior și pot fi modificate doar prin metode publice. Aceasta previne modificările necontrolate ale stării obiectului și controlează accesul la date.

* **Membrii privați** ai clasei ascund implementarea și protejează datele.
* **Membrii publici** oferă interfață pentru interacțiunea cu obiectul.
* **Membrii protejați** sunt disponibili pentru clasele derivate, susținând principiul **moștenirii**.

Această abordare crește siguranța, simplifică mentenanța și organizează mai bine codul.

#### Exemplu de încapsulare:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Atribut privat

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def get_balance(self):
        return self.__balance
```

**Crearea obiectului și accesul la atribute private:**

```python
account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 1500
```

Accesul direct la atributul privat nu este permis:

```python
# print(account.__balance)  # Eroare, nu se poate accesa atributul privat
```

---

### **Getter și Setter în Python**

**Getter** și **Setter** sunt metode folosite pentru a obține (getter) și seta (setter) valorile atributelor obiectului. Ele fac parte din principiul încapsulării și permit acces controlat la date, ascunzând detaliile implementării.

În Python, în loc de metode explicite, se pot folosi proprietăți cu decoratori `@property`, dar se pot folosi și metode tradiționale.

#### 1. **Getter**

Metoda getter oferă acces la valoarea unui atribut al obiectului. Este de obicei publică și permite accesarea atributelor protejate.

**Exemplu:**

```python
class Person:
    def __init__(self, name, age):
        self._name = name  # Atribut protejat
        self._age = age    # Atribut protejat

    # Getter pentru nume
    def get_name(self):
        return self._name

    # Getter pentru vârstă
    def get_age(self):
        return self._age


# Utilizare getter
person = Person("Alice", 30)
print(person.get_name())  # Alice
print(person.get_age())   # 30
```

Metodele `get_name` și `get_age` oferă acces la atributele protejate `_name` și `_age`.

---

#### 2. **Setter**

Metoda setter permite setarea valorii unui atribut, controlând modul în care se modifică datele obiectului.

**Exemplu:**

```python
class Person:
    def __init__(self, name, age):
        self._name = name  # Atribut protejat
        self._age = age    # Atribut protejat

    # Setter pentru nume
    def set_name(self, name):
        if len(name) > 0:
            self._name = name
        else:
            print("Numele nu poate fi gol")

    # Setter pentru vârstă
    def set_age(self, age):
        if age > 0:
            self._age = age
        else:
            print("Vârsta trebuie să fie un număr pozitiv")


# Utilizare setter
person = Person("Alice", 30)
person.set_name("Bob")
person.set_age(25)

print(person.get_name())  # Bob
print(person.get_age())   # 25
```

În acest exemplu, metodele `set_name` și `set_age` verifică valorile înainte de a le seta, asigurând validarea datelor.

#### 3. **Folosirea decoratorilor pentru proprietăți (Property)**

În Python se pot folosi decoratorii `@property` pentru a crea getter-e și `@<attribute>.setter` pentru a crea setter-e. Aceasta permite accesarea atributelor ca și cum ar fi variabile obișnuite, dar cu aplicarea logicii prin metode.

**Exemplu de utilizare a proprietăților (property):**

```python
class Person:
    def __init__(self, name, age):
        self._name = name
        self._age = age

    # Getter pentru nume
    @property
    def name(self):
        return self._name

    # Setter pentru nume
    @name.setter
    def name(self, value):
        if len(value) > 0:
            self._name = value
        else:
            print("Numele nu poate fi gol")

    # Getter pentru vârstă
    @property
    def age(self):
        return self._age

    # Setter pentru vârstă
    @age.setter
    def age(self, value):
        if value > 0:
            self._age = value
        else:
            print("Vârsta trebuie să fie un număr pozitiv")
```

**Utilizarea proprietăților:**

```python
person = Person("Alice", 30)
print(person.name)  # Alice
person.name = "Bob"  # Setarea unui nume nou
print(person.name)  # Bob

person.age = 25  # Setarea unei vârste noi
print(person.age)  # 25
```

În acest exemplu:

* `@property` transformă metoda într-un getter, care permite obținerea valorii atributului `name` sau `age` fără a apela metoda ca funcție.
* `@name.setter` și `@age.setter` permit setarea valorilor atributelor, dar cu verificarea suplimentară că valorile respectă anumite condiții.

#### Avantajele utilizării `property`:

* Sintaxă convenabilă și permite lucrul cu atributele ca și cu variabile obișnuite, dar cu logică suplimentară.
* Crește încapsularea, deoarece permite controlul accesului și modificării atributelor obiectului fără a dezvălui detaliile interne ale implementării.

###№ Concluzii:

* **Getter** oferă acces la atributul obiectului.
* **Setter** permite setarea valorilor atributelor cu logică suplimentară.
* În Python se pot folosi decoratorii `@property` și `@<attribute>.setter` pentru a simplifica lucrul cu getter-e și setter-e, păstrând încapsularea și verificarea datelor.

---

### Decoratori `@classmethod` și `@staticmethod` în Python

Decoratorii `@classmethod` și `@staticmethod` sunt folosiți pentru definirea metodelor dintr-o clasă, care au anumite caracteristici în ceea ce privește accesul la obiect și clasă. Aceste metode ajută la lucrul flexibil cu atributele clasei și ale instanței, precum și oferă modalități de organizare a codului atunci când metoda nu depinde de instanța clasei.

#### 1. **`@classmethod`**

O metodă, notată cu `@classmethod`, primește primul argument ca fiind clasa însăși (de obicei denumită `cls`) în loc de instanță (care este transmisă în metodele obișnuite ca `self`).

* **Scop principal:** Metodele marcate ca `@classmethod` pot fi apelate atât pentru instanța clasei, cât și pentru clasa în sine. Ele pot modifica atributele clasei, dar nu au acces la atributele instanțelor specifice.

**Exemplu:**

```python
class MyClass:
    count = 0  # Atribut al clasei

    def __init__(self, name):
        self.name = name
        MyClass.count += 1  # Creștem contorul la fiecare instanță creată

    @classmethod
    def get_count(cls):
        return cls.count  # Returnăm numărul de instanțe ale clasei

# Creăm mai multe obiecte
obj1 = MyClass("Alice")
obj2 = MyClass("Bob")

print(MyClass.get_count())  # Utilizarea clasei pentru a apela metoda class
print(obj1.get_count())     # Utilizarea instanței pentru a apela metoda class
```

**Ieșire:**

```
2
2
```

Aici metoda `get_count` este o metodă a clasei, deoarece primește `cls` ca argument și poate modifica atributele clasei (de exemplu, `count`).

#### 2. **`@staticmethod`**

O metodă, notată cu `@staticmethod`, nu are acces la atributele instanței (`self`) sau ale clasei (`cls`). Ea pur și simplu efectuează o sarcină care nu depinde de starea obiectului sau a clasei. Astfel de metode sunt adesea folosite pentru funcții utilitare care aparțin logic clasei, dar nu depind de starea acesteia.

* **Scop principal:** Metodele statice, de obicei, nu folosesc parametrii `self` sau `cls` și pot fi apelate atât pentru instanța clasei, cât și pentru clasa însăși.

**Exemplu:**

```python
class MyClass:
    @staticmethod
    def greet(name):
        print(f"Salut, {name}!")

# Poate fi apelată atât pentru instanță, cât și pentru clasă
MyClass.greet("Alice")
obj = MyClass("Bob")
obj.greet("Charlie")
```

**Ieșire:**

```
Salut, Alice!
Salut, Charlie!
```

Aici metoda `greet` este statică, deoarece nu folosește nici instanța (`self`), nici clasa (`cls`) și efectuează o sarcină simplă (afișarea unui mesaj de salut).

#### 3. **Comparație între `@classmethod` și `@staticmethod`:**

* **`@classmethod`:**

  * Lucrează cu clasa și atributele acesteia.
  * Primul argument — `cls`, reprezentând clasa.
  * Poate fi apelată prin instanță sau direct prin clasă.

* **`@staticmethod`:**

  * Nu lucrează cu clasa sau instanța și nu are argumente `self` sau `cls`.
  * Este utilizată pentru funcții logic legate de clasă, dar care nu folosesc starea acesteia.
  * Poate fi apelată prin instanță sau direct prin clasă.

#### Concluzii:

* `@classmethod` permite metodei să lucreze cu clasa și atributele acesteia, spre deosebire de metodele obișnuite, care lucrează cu instanța.
* `@staticmethod` oferă o modalitate de a crea metode care nu depind de starea nici a instanței, nici a clasei.

### 2. **Moștenire**

Moștenirea este un mecanism al programării orientate pe obiecte, care permite crearea unei noi clase pe baza uneia deja existente, folosind caracteristicile acesteia (metode și atribute) fără a fi nevoie să modificăm clasa inițială.
Aceasta ajută la evitarea duplicării codului și permite reutilizarea funcționalității.

* **Clasa derivată (clasă copil)** — este clasa care moștenește atributele și metodele altei clase (părinte).
* **Clasa de bază (clasă părinte)** — este clasa care furnizează proprietăți și metode pentru a fi utilizate în clasele copil.

**Exemplu de moștenire**:

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        print(f"{self.name} face un sunet")

class Dog(Animal):
    def speak(self):
        print(f"{self.name} spune Ham!")
        
class Cat(Animal):
    def speak(self):
        print(f"{self.name} spune Miau!")
```

**Utilizarea moștenirii**:

```python
dog = Dog("Rex")
cat = Cat("Whiskers")

dog.speak()  # Rex spune Ham!
cat.speak()  # Whiskers spune Miau!
```

Aici, clasele `Dog` și `Cat` moștenesc metoda `speak` de la clasa părinte `Animal`, dar o suprascriu pentru a executa acțiuni specifice.

### **Moștenire multiplă**

Python suportă moștenirea multiplă, ceea ce permite unei clase să moștenească proprietăți și metode de la mai multe clase. Totuși, acest lucru poate cauza conflicte între atribute sau metode, care se rezolvă prin metode de rezolvare a ordinii, cum ar fi **Method Resolution Order (MRO)**.

#### Exemplu de moștenire multiplă:

```python
class Animal:
    def speak(self):
        print("Animalul vorbește")

class Bird:
    def fly(self):
        print("Pasărea zboară")

class Bat(Animal, Bird):
    pass

bat = Bat()
bat.speak()  # Animalul vorbește
bat.fly()    # Pasărea zboară
```

Aici clasa `Bat` moștenește metodele ambelor clase `Animal` și `Bird`.

#### 1. **Folosirea lui `super()` în moștenire:**

În Python există funcția încorporată `super()`, care returnează un obiect proxy, permițând referirea la clasa părinte. Este utilizată pentru a apela metodele clasei părinte, ceea ce este important la suprascrierea metodelor în clasa copil.

##### **Sintaxă:**

```python
class ParentClass:
    def __init__(self):
        print("Inițializarea clasei părinte")

    def greet(self):
        print("Salut din clasa părinte!")

class SubClass(ParentClass):
    def __init__(self):
        super().__init__()  # Apelarea constructorului clasei părinte
        print("Inițializarea clasei copil")

    def greet(self):
        super().greet()  # Apelarea metodei clasei părinte
        print("Salut din clasa copil!")

# Creăm obiectul clasei copil
obj = SubClass()
obj.greet()
```

##### **Rezultat:**

```
Inițializarea clasei părinte
Inițializarea clasei copil
Salut din clasa părinte!
Salut din clasa copil!
```

În acest exemplu:

* `SubClass` moștenește de la `ParentClass`.
* În metoda `__init__()` a clasei copil `SubClass` se apelează constructorul clasei părinte folosind `super()`, pentru a nu repeta logica de inițializare.
* În metoda `greet()` a clasei copil se apelează versiunea părinte a metodei prin `super()`.

#### 3. **De ce folosim `super()`?**

* **Simplificarea apelurilor:** Folosirea lui `super()` permite evitarea legării stricte la numele clasei părinte, utilă la moștenirea multiplă.
* **Suport pentru moștenirea multiplă:** `super()` funcționează corect la moștenirea multiplă, asigurând ordinea corectă a apelurilor metodelor conform MRO.

### 4. **Moștenire multiplă și `super()`**

Python suportă moștenirea multiplă, iar `super()` ajută la organizarea corectă a apelurilor metodelor din mai multe clase de bază.

![img.png](../images/lecture_8/img_1.png)

**Exemplu cu moștenire multiplă:**

```python
class A:
    def __init__(self):
        print("Inițializarea A")

class B(A):
    def __init__(self):
        super().__init__()
        print("Inițializarea B")

class C(A):
    def __init__(self):
        super().__init__()
        print("Inițializarea C")

class D(B, C):
    def __init__(self):
        super().__init__()
        print("Inițializarea D")

# Creăm obiectul clasei D
d = D()
```

**Rezultat:**

```
Inițializarea C
Inițializarea B
Inițializarea A
Inițializarea D
```

Se observă că Python apelează mai întâi inițializarea clasei `C`, apoi `B`, apoi `A`, conform algoritmului de rezolvare a ordinii (MRO).

#### Concluzii:

* **Moștenirea** permite crearea de clase noi pe baza celor existente, reutilizând codul.
* `super()` este folosit pentru apelarea metodelor clasei părinte și asigură funcționarea corectă la moștenirea multiplă.

### 5. **Polimorfism**

Polimorfismul permite utilizarea acelorași metode (interfață comună) pentru obiecte din clase diferite, ceea ce crește flexibilitatea programelor. Metodele pot avea același nume, dar comportamentul lor depinde de tipul obiectului pentru care sunt apelate.

Presupunem că trebuie să colorăm o figură. Există mai multe tipuri de figură (dreptunghi, pătrat, cerc). Totuși, am putea folosi aceeași metodă pentru a colora oricare dintre aceste forme.

#### Exemplu de polimorfism:

```python
class Bird:
    def speak(self):
        print("Tweet")

class Dog:
    def speak(self):
        print("Ham")

animals = [Bird(), Dog()]
for animal in animals:
    animal.speak()  # Va afișa "Tweet" și "Ham"
```

Aici, ambele clase, `Bird` și `Dog`, au metoda `speak`, dar cu implementări diferite. Acesta este un exemplu de polimorfism — aceeași metodă poate avea implementări diferite pentru clase diferite.

### 6. **Clase abstracte**

Știm deja ce este abstracția; în Python, abstracția este adesea realizată folosind clase abstracte.

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print("Ham!")

class Cat(Animal):
    def speak(self):
        print("Miau!")

# dog = Animal()  # Eroare, nu se poate crea un obiect dintr-o clasă abstractă
```

Aici, clasa `Animal` este abstractă și nu poate fi instanțiată. Pentru a crea obiecte, trebuie să creăm clase derivate care să implementeze metodele abstracte.

### 8. **Constructori și destructori**

* **Constructor** — este metoda apelată la crearea unui obiect. În Python, este metoda `__init__`.
* **Destructor** — este metoda apelată la ștergerea unui obiect. În Python, este metoda `__del__`.

**Exemplu cu constructor și destructor:**

```python
class MyClass:
    def __init__(self):
        print("Obiect creat")
    
    def __del__(self):
        print("Obiect distrus")

obj = MyClass()  # Va afișa "Obiect creat"
del obj  # Va afișa "Obiect distrus"
```

### Toate clasele din Python moștenesc de la `object`

Din versiunea Python 3, toate clasele sunt **de tip nou**, deoarece moștenesc implicit de la clasa de bază comună `object`. Acest lucru le integrează într-o ierarhie unificată, ceea ce simplifică lucrul cu clasele și metodele lor.

#### Ce înseamnă acest lucru:

1. **Moștenire implicită:**

   * Dacă creați o clasă fără a specifica explicit clasa de bază, Python o moștenește automat de la `object`.

   **Exemplu:**

   ```python
   class MyClass:
       pass
   ```

   Această clasă este echivalentă cu:

   ```python
   class MyClass(object):
       pass
   ```

2. **Metode din clasa `object` (Metode magice):**
   Clasele moștenesc automat metodele clasei de bază `object`, cum ar fi:

   * `__str__()` — pentru obținerea reprezentării sub formă de șir.
   * `__repr__()` — pentru obținerea reprezentării "oficiale" a obiectului.
   * `__eq__()` — pentru compararea obiectelor.
   * `__hash__()` — pentru obținerea valorii hash a obiectului.
   * `__init__()` — constructor de bază.
   * `__del__()` — destructor de bază.
   * Și altele.

#### Exemple de metode magice:

1. **`__init__(self, ...)`**
   Constructorul clasei, apelat la crearea unei noi instanțe, inițializează atributele obiectului.

   **Exemplu:**

   ```python
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age
       
   person1 = Person("Alice", 30)  # __init__ apelat la creare
   ```

2. **`__str__(self)`**
   Apelat când se folosește `str()` sau `print()` pe obiect; returnează reprezentarea în șir a obiectului.

   **Exemplu:**

   ```python
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age

       def __str__(self):
           return f"{self.name}, {self.age} ani"

   person1 = Person("Alice", 30)
   print(person1)  # Va afișa: Alice, 30 ani
   ```

3. **`__repr__(self)`**
   Apelat când se folosește `repr()` sau când obiectul este afișat în consolă; returnează o reprezentare utilă pentru depanare.

   **Exemplu:**

   ```python
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age

       def __repr__(self):
           return f"Person('{self.name}', {self.age})"

   person1 = Person("Alice", 30)
   print(repr(person1))  # Va afișa: Person('Alice', 30)
   ```

4. **`__add__(self, other)`**
   Permite suprascrierea operației de adunare (`+`) între obiecte.

   **Exemplu:**

   ```python
   class Point:
       def __init__(self, x, y):
           self.x = x
           self.y = y

       def __add__(self, other):
           return Point(self.x + other.x, self.y + other.y)

   point1 = Point(1, 2)
   point2 = Point(3, 4)
   result = point1 + point2  # Apelează __add__
   print(result.x, result.y)  # Va afișa: 4 6
   ```

5. **`__eq__(self, other)`**
   Permite suprascrierea comparației de egalitate (`==`) între obiecte.

   **Exemplu:**

   ```python
   class Person:
       def __init__(self, name, age):
           self.name = name
           self.age = age

       def __eq__(self, other):
           return self.name == other.name and self.age == other.age

   person1 = Person("Alice", 30)
   person2 = Person("Alice", 30)
   print(person1 == person2)  # Va afișa: True
   ```

### Funcția ca obiect în Python

În Python, funcțiile sunt obiecte de primă clasă, ceea ce înseamnă că pot fi:

* Atribuite variabilelor.
* Transmise altor funcții ca argumente.
* Returnate din alte funcții.
* Stocate în structuri de date, cum ar fi liste sau dicționare.
#### Caracteristicile principale ale funcțiilor ca obiecte:

1. **Funcția poate fi atribuită unei variabile:**

```python
def greet(name):
    return f"Hello, {name}!"

say_hello = greet  # Atribuim funcția unei variabile
print(say_hello("Alice"))  # Afișare: Hello, Alice!
```

2. **Funcția poate fi transmisă ca argument altei funcții:**
   Aceasta permite crearea de construcții flexibile, cum ar fi funcțiile de ordin înalt.

**Exemplu:**

```python
def apply_function(func, value):
    return func(value)

def square(x):
    return x ** 2

print(apply_function(square, 5))  # Afișare: 25
```

3. **Funcția poate fi returnată dintr-o altă funcție:**

```python
def multiplier(factor):
    def multiply_by(value):
        return value * factor
    return multiply_by

double = multiplier(2)
print(double(10))  # Afișare: 20
print(multiplier(2)(10))
```

4. **Funcțiile pot fi folosite în structuri de date:**

```python
def add(x, y):
    return x + y

def subtract(x, y):
    return x - y

operations = {
    "add": add,
    "subtract": subtract
}

print(operations["add"](10, 5))       # Afișare: 15
print(operations["subtract"](10, 5)) # Afișare: 5
```

#### Funcția are metoda `__call__()`

Funcția în Python este un obiect care are metoda specială `__call__()`. Aceasta permite apelarea obiectelor-funcție ca și cum ar fi funcții obișnuite.

**Exemplu:**

```python
def example_function(x):
    return x * 2

print(example_function.__call__(10))  # Echivalent cu example_function(10), afișare: 20
```

#### Clase cu metoda `__call__`

Obiectele claselor cu metoda `__call__` pot fi, de asemenea, apelate ca funcții.

**Exemplu:**

```python
class Adder:
    def __init__(self, value):
        self.value = value

    def __call__(self, other):
        return self.value + other

add_five = Adder(5)
print(add_five(10))  # Afișare: 15
```

---

## Definirea claselor în module și importarea lor

#### 1. **Ce este un modul în Python?**

Un modul este un fișier cu extensia `.py` care conține definiții de funcții, clase, variabile sau cod executabil. Permite organizarea codului în blocuri logice și reutilizarea lui.

#### 2. **Crearea unei clase într-un modul**

O clasă poate fi definită într-un modul separat pentru a fi importată și utilizată în alte părți ale programului.

**Exemplu:**

Creăm modulul `shapes.py` cu clasa `Rectangle`:

```python
# shapes.py
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)
```

#### 3. **Importarea modulului**

Pentru a folosi clasa din modul, se folosește `import` sau `from ... import`.

##### 3.1. **Importarea întregului modul**

```python
import shapes

rect = shapes.Rectangle(10, 5)
print(f"Arie: {rect.area()}")        # Afișare: Arie: 50
print(f"Perimetru: {rect.perimeter()}")  # Afișare: Perimetru: 30
```

##### 3.2. **Importarea unei clase specifice**

```python
from shapes import Rectangle

rect = Rectangle(8, 4)
print(f"Arie: {rect.area()}")        # Afișare: Arie: 32
print(f"Perimetru: {rect.perimeter()}")  # Afișare: Perimetru: 24
```

##### 3.3. **Import cu alias**

```python
from shapes import Rectangle as Rect

rect = Rect(6, 3)
print(f"Arie: {rect.area()}")        # Afișare: Arie: 18
print(f"Perimetru: {rect.perimeter()}")  # Afișare: Perimetru: 18
```

##### 3.4. **Importarea întregului conținut al modulului (nu recomandat)**

```python
from shapes import *

rect = Rectangle(7, 2)
print(f"Arie: {rect.area()}")        # Afișare: Arie: 14
print(f"Perimetru: {rect.perimeter()}")  # Afișare: Perimetru: 18
```

> **Notă:** `from module import *` nu este recomandat, deoarece poate provoca conflicte de nume.

#### 4. **Organizarea modulelor**

În proiecte mari, modulele pot fi grupate în pachete. Un pachet este un director care conține module și fișierul `__init__.py` (poate fi gol).

**Exemplu de structură:**

```
project/
│
├── shapes/
│   ├── __init__.py
│   ├── rectangle.py
│   ├── circle.py
│
├── main.py
```

**Conținut `rectangle.py`:**

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height
```

**Conținut `circle.py`:**

```python
import math

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * (self.radius ** 2)
```

**Importarea modulelor în `main.py`:**

```python
from shapes.rectangle import Rectangle
from shapes.circle import Circle

rect = Rectangle(10, 5)
print(f"Aria dreptunghiului: {rect.area()}")  # Afișare: Aria dreptunghiului: 50

circle = Circle(7)
print(f"Aria cercului: {circle.area()}")     # Afișare: Aria cercului: 153.93804002589985
```

#### 5. **Lucrul cu căile modulelor**

Dacă modulul nu se află în directorul curent, se poate folosi:

* Variabila de mediu `PYTHONPATH`.
* Adăugarea căii manual:

```python
import sys
sys.path.append('/path/to/directory')
from shapes import Rectangle
```

### 9. **Concluzie**

Programarea orientată pe obiecte în Python oferă instrumente puternice pentru crearea unui cod clar și ușor de întreținut. Conceputurile OOP, precum clasele, obiectele, încapsularea, moștenirea, polimorfismul și abstracția, permit rezolvarea eficientă a problemelor și crearea de programe flexibile și extensibile. Python, cu suportul său pentru aceste principii, este un limbaj excelent pentru implementarea OOP.
