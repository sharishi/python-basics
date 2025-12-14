### Module și Pachete în Python. Lucrul cu Shell

#### 1. **Module în Python**

Un modul este un fișier cu extensia `.py`, care conține definiții de funcții, clase și variabile, și poate include, de asemenea, cod executabil. Modulele sunt folosite pentru structurarea codului, creșterea lizibilității și reutilizarea acestuia.

##### Importarea unui modul:

* Un modul poate fi importat folosind comanda `import`.
* Elemente specifice dintr-un modul pot fi importate folosind comanda `from`.

**Exemple:**

```python
# Importarea întregului modul
import math
print(math.sqrt(16))  # Output: 4.0

# Importarea unei funcții specifice din modul
from math import pi
print(pi)  # Output: 3.141592653589793

# Importarea cu alias
import numpy as np
array = np.array([1, 2, 3])
print(array)  # Output: [1 2 3]
```

##### Module încorporate:

Python oferă numeroase module încorporate, de exemplu:

* `os`, `sys`, `math`, `datetime`, `random`.

##### Crearea propriului modul:

Fișier `my_module.py`:

```python
def greet(name):
    return f"Hello, {name}!"

PI = 3.14159
```

Utilizare:

```python
import my_module
print(my_module.greet("Alice"))  # Output: Hello, Alice!
print(my_module.PI)             # Output: 3.14159
```

---

### Lucrul cu atributul `__name__` în Python

1. **Ce este atributul `__name__`?**
   Atributul `__name__` este o variabilă predefinită în Python, care stochează un șir ce reprezintă numele modulului curent.

2. **Valoarea lui `__name__`:**

   * Când modulul este rulat direct, valoarea atributului `__name__` este `'__main__'`.
   * Când modulul este importat într-altul, valoarea `__name__` devine numele modulului respectiv.

---

### Exemplu:

```python
# example.py

print(__name__)
```

* **Dacă fișierul `example.py` este rulat direct:**

  ```
  __main__
  ```

* **Dacă fișierul `example.py` este importat ca modul într-un alt fișier:**

  ```python
  import example
  ```

  Va afișa:

  ```
  example
  ```

3. **Folosirea lui `__name__` pentru controlul execuției codului:**
   Se folosește frecvent construcția `if __name__ == '__main__':`, pentru ca codul să fie executat doar atunci când modulul este rulat direct și nu la importarea lui într-un alt modul.

### Exemplu cu `if __name__ == '__main__':`

```python
# example.py

def print_message():
    print("Hello from the function!")

if __name__ == '__main__':
    print("This code is running directly!")
    print_message()
```

* **La rularea directă a fișierului `example.py`** va afișa:

  ```
  This code is running directly!
  Hello from the function!
  ```

* **Dacă fișierul `example.py` este importat într-un alt modul:**

  ```python
  import example
  ```

  Codul din blocul `if __name__ == '__main__':` nu va fi executat.

### De ce este util?

* **Separarea codului pentru testare și utilizare:** Permite scrierea de teste și exemple demonstrative în interiorul modulului, care vor fi executate doar la rularea directă, dar nu la importul modulului în alte programe.
* **Reutilizarea codului:** Codul destinat reutilizării (de exemplu funcții sau clase) nu va fi executat la importarea modulului într-un alt fișier.

---
### 2. **Pachete în Python**

Un pachet este o colecție de module organizate într-un director. Directorul pachetului trebuie să conțină fișierul `__init__.py` (în Python 3.3 și mai sus acesta poate fi gol).

#### De ce sunt necesare pachetele în Python?

1. **Organizarea codului:**
   Pachetele permit gruparea modulelor pe funcționalitate, simplificând structura proiectului și făcând codul mai ușor de înțeles și de întreținut.

2. **Scalabilitate:**
   Pachetele facilitează extinderea proiectului, adăugând noi module fără confuzie în numele fișierelor.

3. **Reutilizarea codului:**
   Datorită pachetelor se pot crea componente modulare, ușor de conectat și reutilizat în diferite părți ale proiectului.

4. **Izolarea spațiului de nume:**
   Pachetele ajută la evitarea conflictelor de nume între module, deoarece fiecare modul se află în pachetul său, iar accesul se face prin numele său (de exemplu, `package.module`).

5. **Curățenia structurii proiectului:**
   Pachetele contribuie la o organizare mai clară și logică a fișierelor, ceea ce este deosebit de important în proiectele mari.

---

Pachetele facilitează întreținerea și dezvoltarea proiectului, precum și separarea convenabilă a diferitelor părți ale programului, păstrând flexibilitatea și lizibilitatea codului.

##### Structura unui pachet:

```
my_package/
    __init__.py
    module1.py
    module2.py
```

**Exemplu de utilizare:**

```python
# În fișierul module1.py
def func1():
    return "Function 1"

# În fișierul module2.py
def func2():
    return "Function 2"

# Importarea modulului din pachet
from my_package import module1
print(module1.func1())  # Output: Function 1
```

##### Inițializarea pachetului:

Fișierul `__init__.py` permite definirea elementelor care vor fi importate la utilizarea `from package import *`.

**Exemplu:**

```python
# În __init__.py
__all__ = ['module1', 'module2']
```

---

#### 3. **Lucrul cu Shell**

Shell în Python este un mediu interactiv de execuție, care permite scrierea și rularea codului linie cu linie.

##### Principalele Shell-uri:

1. **Python REPL (Read-Eval-Print Loop):**

   * Lansare: comanda `python` sau `python3` în terminal.
   * Folosit pentru testarea rapidă a codului.

2. **IPython:**

   * Shell îmbunătățit cu autocompletare și funcționalități interactive.
   * Instalare: `pip install ipython`.
   * Lansare: comanda `ipython`.

3. **Jupyter Notebook:**

   * Mediu interactiv pentru scrierea și rularea codului.
   * Instalare: `pip install notebook`.
   * Lansare: comanda `jupyter notebook`.

##### Rularea scripturilor Python prin Shell:

* Lansarea fișierului:

  ```bash
  python script.py
  ```
* Transmiterea argumentelor:

  ```bash
  python script.py arg1 arg2
  ```
* Preluarea argumentelor în script:

  ```python
  import sys
  print(sys.argv)  # Output: ['script.py', 'arg1', 'arg2']
  ```

---
#### 4. **Lucrul cu module externe**

Pentru instalarea și gestionarea modulelor externe se folosește `pip`.

**Exemplu de instalare:**

```bash
pip install requests
```

**Exemplu de utilizare a unui modul instalat:**

```python
import requests
response = requests.get("https://api.github.com")
print(response.status_code)  # Output: 200
```

---

### Mediu virtual (Virtual Environment) în Python

#### Ce este un mediu virtual?

Mediul virtual este un mediu izolat pentru proiectele Python, care permite instalarea dependențelor (biblioteci și pachete) separat pentru fiecare proiect. Aceasta ajută la evitarea conflictelor între diferite proiecte care rulează pe aceeași mașină.

---

#### Avantajele principale:

1. **Izolarea dependențelor:**

   * Fiecare proiect are propria versiune a bibliotecilor.
   * Python-ul sistemului rămâne neatins.

2. **Gestionarea versiunilor pachetelor:**

   * Este ușor să folosești versiuni diferite ale aceleiași biblioteci pentru proiecte diferite.

3. **Simplitate în configurare:**

   * Crearea și activarea mediilor virtuale se integrează ușor în fluxul de lucru.

---

#### Pași pentru crearea și utilizarea mediului virtual

1. **Verifică dacă Python este instalat:**

   * Verifică versiunea Python:

     ```bash
     python --version
     ```

2. **Crearea mediului virtual:**

   * Execută comanda:

     ```bash
     python -m venv myenv
     ```
   * Aici `myenv` este numele folderului unde va fi creat mediul virtual.

3. **Activarea mediului virtual:**

   * **Windows:**

     ```bash
     .\myenv\Scripts\activate
     ```
   * **macOS/Linux:**

     ```bash
     source myenv/bin/activate
     ```
   * După activare, vei vedea numele mediului în promptul terminalului:

     ```
     (myenv) PS C:\Users\username\project>
     ```

4. **Instalarea bibliotecilor:**

   * După activare, toate pachetele se instalează local pentru mediul curent:

     ```bash
     pip install requests
     ```

5. **Dezactivarea mediului virtual:**

   * Pentru a ieși din mediu, folosește:

     ```bash
     deactivate
     ```

6. **Ștergerea mediului virtual:**

   * Pur și simplu șterge folderul `myenv`:

     ```bash
     rm -rf myenv  # macOS/Linux
     rmdir /s myenv # Windows
     ```

---

#### Utilizarea fișierului `requirements.txt`

Pentru o gestionare mai ușoară a dependențelor se folosește fișierul `requirements.txt`.

1. **Crearea fișierului `requirements.txt`:**

   * Salvează lista bibliotecilor instalate:

     ```bash
     pip freeze > requirements.txt
     ```

2. **Instalarea dependențelor din fișier:**

   * Execută comanda:

     ```bash
     pip install -r requirements.txt
     ```

---

#### Exemplu de flux de lucru:

```bash
# Crearea mediului virtual
python -m venv venv

# Activarea
.\venv\Scripts\activate

# Instalarea bibliotecilor
pip install flask

# Salvarea dependențelor
pip freeze > requirements.txt

# Dezactivarea
deactivate
```

Acum știi cum să lucrezi cu mediile virtuale în Python!
