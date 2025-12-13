# Lecția 1: Introducere în Python

### 1. De ce Python?

#### Python – limbaj de programare cross-platform

Python este un limbaj de programare cross-platform, ceea ce înseamnă că funcționează pe diferite platforme, cum ar fi **Windows**, **macOS**, **Linux**, și poate fi portat chiar și pe mașini virtuale **Java** și **.NET**.

#### Suport pentru mai multe paradigme

Python suportă mai multe stiluri de programare:

* **Programare procedurală**
* **Programare orientată pe obiecte**
* **Programare funcțională**

#### Caracteristici principale ale limbajului

* **Simplitatea sintaxei**: Python folosește o sintaxă lizibilă și intuitivă, ceea ce îl face ideal pentru începători.
* **Aplicabilitate largă**: Python este folosit în știința datelor, dezvoltarea web, machine learning, automatizare și alte domenii.
* **Suport și comunitate mare**: o bibliotecă extinsă de module și o comunitate activă.

#### Domenii principale de aplicare a Python

* **Dezvoltare web**: se poate folosi pentru crearea aplicațiilor web server-side, conectarea la baze de date și manipularea fișierelor.
* **Dezvoltare software**: potrivit pentru prototipare rapidă și dezvoltarea de software gata de producție.
* **Matematică și știință**: excelent pentru procesarea datelor mari și realizarea calculelor matematice complexe.
* **Scripturi de sistem**: folosit pentru scrierea de scripturi care automatizează procese în sistemele de operare.

![Python for everything](../images/lecture_1/img_2.png)

#### Exemple de proiecte mari realizate în Python

Python a fost utilizat în proiecte precum:

* **Wikipedia**
* **Google** (unde a lucrat Guido van Rossum, creatorul Python)
* **Yahoo!**, **CERN**, **NASA**
* Servicii populare precum **PayPal**, **Instagram**, **Spotify**

---

### 3. Limbaje de programare interpretate: ce înseamnă?

Când spunem că Python este un limbaj interpretat, înseamnă că codul Python nu este compilat în prealabil în cod mașină, așa cum se întâmplă în limbaje precum C sau C++, ci este interpretat direct în timpul execuției. Să vedem cum funcționează:

1. **Cod sursă**: Scrieți programul Python într-un fișier text cu extensia `.py`.
2. **Pornirea interpretului**: La rularea programului, interpretul Python citește și execută codul sursă linie cu linie.
3. **Bytecode intermediar**: În timpul execuției, codul Python este mai întâi transformat în bytecode – o reprezentare intermediară compactă care poate fi executată de mașina virtuală Python (PVM).
4. **Execuție**: Mașina virtuală Python (PVM) execută bytecode-ul, interacționând cu sistemul de operare și resursele calculatorului.

#### Cum diferă de limbajele compilate?

În limbajele compilate, precum C sau C++, codul sursă este mai întâi compilat într-un fișier executabil, care apoi este rulat. În schimb, limbajele interpretate nu necesită acest pas intermediar: programul rulează imediat, pe măsură ce interpretul citește codul.

#### Avantajele limbajelor interpretate:

* **Simplitate la depanare**: Erorile sunt mai ușor de identificat, deoarece codul rulează linie cu linie și se poate vedea imediat unde apare problema.
* **Flexibilitate**: Modificările pot fi implementate fără recompilare, ceea ce face dezvoltarea mai flexibilă.
* **Portabilitate**: Codul Python poate fi rulat pe diferite sisteme de operare fără recompilare.

#### Dezavantaje ale limbajelor interpretate:

* **Performanță**: Deoarece codul este interpretat linie cu linie în timp real, limbajele interpretate sunt adesea mai lente decât cele compilate.

Astfel, limbajele interpretate oferă flexibilitate și confort în dezvoltare, dar pot avea limitări de viteză, lucru important de luat în considerare atunci când alegeți un limbaj pentru anumite sarcini.

---

### 4. Instalare și configurare

1. **Descărcarea Python**

   * Deschideți site-ul oficial Python: [https://www.python.org/](https://www.python.org/).
   * În pagina principală, accesați secțiunea "Downloads" și selectați "Download Python X.X.X" (unde X.X.X este ultima versiune stabilă, de exemplu 3.10.5).
   * Alegeți versiunea pentru sistemul dvs. de operare (Windows, macOS sau Linux):

     * **Windows**: Selectați installer-ul pentru Windows (`Windows Installer`) și descărcați fișierul.
     * **macOS**: Descărcați fișierul `.pkg`.
     * **Linux**: Python este, de obicei, preinstalat. Dacă nu, folosiți comanda `sudo apt install python3` pentru Ubuntu sau `sudo dnf install python3` pentru Fedora.

2. **Instalarea Python pe Windows**

   * Deschideți fișierul descărcat (.exe).
   * În **prima fereastră a instalatorului**, bifați "Add Python to PATH". Este foarte important: adăugarea în PATH permite rularea Python din linia de comandă.
   * Apăsați "Install Now" și așteptați finalizarea instalării.

3. **Instalarea Python pe macOS**

   * Rulați fișierul descărcat (.pkg) și urmați pașii asistentului de instalare.
   * De obicei, Python se adaugă automat în PATH pe macOS.

4. **Verificarea instalării Python**
   După instalare, deschideți linia de comandă:

   * **Windows**: deschideți "Command Prompt" sau "PowerShell".
   * **macOS / Linux**: deschideți "Terminal".

   Introduceți comanda:

   ```bash
   python --version
   ```

   sau, dacă nu funcționează:

   ```bash
   python3 --version
   ```

   Ar trebui să vedeți versiunea Python, de exemplu `Python 3.10.5`. Aceasta confirmă că Python este instalat și gata de utilizare.
---

5. **Instalarea unui IDE sau editor de cod**
   Pentru confortul lucrului cu Python, alegeți și instalați un editor potrivit:

* **VS Code**: Editor ușor, gratuit, cu suport pentru plugin-uri Python. Descărcați-l de la [https://code.visualstudio.com/](https://code.visualstudio.com/).
* **PyCharm**: IDE complet pentru Python, cu funcții de autocompletare, depanare și interfață intuitivă. Există ediția gratuită Community Edition: [https://www.jetbrains.com/pycharm/download/](https://www.jetbrains.com/pycharm/download/).

#### [Alternativă](https://jupyter.org)

6. **Verificarea funcționării Python prin IDE**

* Deschideți IDE-ul și creați un fișier Python nou (de exemplu, `hello.py`).
* Scrieți un cod simplu pentru a verifica funcționarea:

```python
print("Hello, World!")
```

* Rulați scriptul (de obicei cu tasta `F5` sau cu butonul de run), și verificați dacă în terminal apare textul `Hello, World!`.

Acum Python este instalat și puteți începe să învățați și să scrieți cod!

**Rularea codului**:

* În terminal: folosiți comanda `python` sau `python3` în funcție de versiune.
* Prin IDE (de exemplu, PyCharm, VS Code, Jupyter Notebook).

---

### 5. Introducere în stilurile de scriere a identificatorilor

Stilurile de scriere a identificatorilor sunt convenții care ajută la creșterea lizibilității și structurării codului. Cele mai populare sunt **CamelCase** și **snake_case**. Ele se folosesc pentru numirea variabilelor, funcțiilor și claselor și ajută la diferențierea ușoară a părților codului după rolul lor.

![Python for everything](../images/lecture_1/img_1.png)

---

### 6. Indentarea în Python

Python folosește **indentarea** pentru a defini structura codului. Spre deosebire de alte limbaje, unde blocurile de cod sunt încadrate în acolade `{}`, în Python blocurile sunt definite prin nivelul de indentare, ceea ce face codul mai lizibil.

#### Reguli principale:

* **Dimensiunea indentării**: indentarea standard este de **4 spații**, dar este important să fiți consecvent. Utilizarea tab-urilor (`\t`) poate cauza erori.
* **Structurarea blocurilor**: toate liniile dintr-un bloc trebuie să aibă același nivel de indentare. Încălcarea acestui lucru va genera eroarea `IndentationError`.
* **Cicluri, condiții, funcții**: toate instrucțiunile din corpul funcțiilor, buclelor și condițiilor trebuie să fie cu un nivel de indentare mai mult decât linia care le definește.

**Exemplu:**

```python
def my_function():
    if True:
        print("În interiorul condiției")  # 4 spații înaintea acestei linii
    for i in range(3):
        print(i)  # tot 4 spații
```

Respectarea indentării îmbunătățește lizibilitatea codului și este o parte esențială a stilului Python.

---

### 7. Comentariile în Python

Comentariile în Python sunt folosite pentru a explica codul, a-i crește lizibilitatea sau a dezactiva temporar anumite linii. Ele nu sunt executate de interpret și ajută dezvoltatorii să înțeleagă mai bine logica programului.

#### Comentarii pe o singură linie

Se foloseste simbolul `#`. Tot ce este după acesta pe linie va fi ignorat de interpret.

```python
# Acesta este un comentariu pe o linie
print("Hello, World!")  # Comentariu după cod
```

#### Comentarii pe mai multe linii

Python nu are un sintax special pentru comentarii multi-linie, dar se folosesc mai multe linii cu `#`:

```python
# Prima linie de comentariu
# A doua linie de comentariu
# A treia linie de comentariu
```

De asemenea, șirurile multi-linie în ghilimele (`''' ... '''` sau `""" ... """`) pot fi folosite pentru comentarii multi-linie, de obicei ca **docstring** – șiruri de documentație.

```python
"""
Acesta este un comentariu multi-linie,
care poate fi folosit ca docstring.
"""
def my_function():
    """Acest docstring descrie funcția."""
    pass
```

#### Principii de bază pentru comentarii:

* **Fiți concis și clar**: comentariile trebuie să explice esența codului, nu să-l repete.
* **Explicați logica complexă**: folosiți comentarii acolo unde codul poate fi greu de înțeles.
* **Nu exagerați**: nu comentați acțiuni evidente, pentru a menține codul curat.

Comentariile fac codul mai ușor de înțeles și ajută alți dezvoltatori să înțeleagă rapid logica.

---

### 8. Variabile

* Variabilele sunt **containere** pentru stocarea valorilor.
* Spre deosebire de alte limbaje, în Python nu există cuvânt cheie pentru declararea unei variabile.
* Pentru a crea o variabilă, pur și simplu atribuiți o valoare:

```python
# Variabile de tip "string" se definesc cu ghilimele
nmbr1, name = 77.5, "Amber"
print(nmbr1)  # 77.5
print(name)   # "Amber"

# Sau putem atribui aceeași valoare mai multor variabile într-o linie
nmbr1 = nmbr2 = 77.5
print(nmbr1)  # 77.5
print(nmbr2)  # 77.5
```

* Variabilele nu trebuie să fie de un tip fix – ele pot schimba tipul după ce au fost inițializate.
* Interpretul determină tipul variabilei în momentul atribuirii.
* Operatorul de atribuire este simbolul egal (`=`).
* **Numele variabilelor sunt case-sensitive** (`age` și `Age` sunt variabile diferite) și **nu trebuie să înceapă cu cifre** (trebuie să înceapă cu literă sau underscore `_`), dar pot conține cifre în interior.

---

### 9. Tipurile de bază de date în Python

Python este un limbaj cu **tipizare dinamică**, unde tipul unei variabile este determinat automat în momentul atribuirii valorii. Python dispune atât de tipuri de bază, cât și de structuri de date mai complexe, care permit lucrul eficient cu diferite seturi de date.

![img.png](../images/lecture_1/img_3.png)

## Partea 1

1. **None**

   * **Descriere**: Instanță a tipului de obiect `NoneType`, care reprezintă o variabilă specială fără valoare efectivă.
   * **Exemplu**:

```python
x = None
print(type(x))  # <class 'NoneType'>
```

Se poate folosi funcția `type()` pentru a afla clasa unei variabile sau valori, și `isinstance()` pentru a verifica dacă un obiect aparține unei anumite clase.

2. **bool**

   * **Descriere**: Valori booleene, care pot fi `True` sau `False`.
   * **Exemplu**:

```python
is_active = True
is_completed = False
print(type(is_active))  # <class 'bool'>
```

3. **int**

   * **Descriere**: Tip de date pentru numere întregi, pozitive sau negative.
   * Numerele întregi pot avea orice lungime, limitate doar de memoria disponibilă a dispozitivului.
   * **Exemplu**:

```python
age = 25
temperature = -5
print(type(age))  # <class 'int'>
```

4. **float**

   * **Descriere**: Tip de date pentru numere cu virgulă mobilă, care pot avea parte zecimală.
   * Numerele reale au precizie până la 15 zecimale.
   * **Exemplu**:

```python
pi = 3.14159
price = 99.99
print(type(pi))  # <class 'float'>
```

5. **complex**

   * **Descriere**: Tip de date pentru numere complexe, cu parte reală și imaginară.
   * **Exemplu**:

```python
complex_num = 3 + 4j
print(isinstance(complex_num, complex))  # True
```

6. **str**

   * **Descriere**: Tip de date pentru stocarea informației textuale, șiruri de caractere.
   * **Exemplu**:

```python
name = "Alice"
greeting = 'Hello, world!'
print(type(name))  # <class 'str'>
```
---

### 10. Constructori pentru conversia tipurilor în Python

În Python, pentru conversia explicită (sau schimbarea) tipurilor de date se folosesc constructori speciali. Aceștia permit transformarea tipului unei variabile sau obiect, de exemplu din șir în număr sau invers.

Principalii constructori sunt:

1. **`int()`** — convertește datele în număr întreg:

```python
a = "10"
b = int(a)  # Convertim șirul în număr întreg
print(b)  # 10
```

2. **`float()`** — convertește datele în număr real:

```python
a = "10.5"
b = float(a)  # Convertim șirul în număr real
print(b)  # 10.5
```

3. **`str()`** — convertește datele în șir:

```python
a = 100
b = str(a)  # Convertim numărul întreg în șir
print(b)  # "100"
```

4. **`complex()`** — convertește în număr complex:

```python
a = 1, 2
b = complex(*a)  # Convertim în număr complex
print(b)  # (1+2j)
```

Schimbarea tipurilor de date este necesară pentru a lucra corect cu diferite operații, care cer tipuri compatibile. În Python, ca și în alte limbaje, diversele tipuri (int, string, list etc.) au reguli specifice, iar unele operații nu pot fi aplicate între tipuri diferite.

**Exemplu de eroare:**

```python
nmbr1 = 22
nmbr2 = "33"
print(nmbr1 + nmbr2)  # TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

Aici se încearcă adunarea unui `int` (`nmbr1 = 22`) cu un `str` (`nmbr2 = "33"`), ceea ce nu este permis.

**Exemplu corect cu conversia tipului:**

```python
nmbr1 = 22
nmbr2 = int("33")
print(nmbr1 + nmbr2)  # 55
```

Funcția `int()` transformă șirul `"33"` în număr întreg, astfel ambii operanzi sunt compatibili și adunarea funcționează.

---

### De ce este important să schimbăm tipurile de date?

1. **Operații matematice**: Adunarea, scăderea, multiplicarea necesită tipuri numerice. Încercarea de a aduna un șir cu un număr generează eroare.
2. **Operații pe șiruri**: Dacă dorim să combinăm valori ca șiruri, numerele trebuie transformate în șiruri.
3. **Procesarea datelor**: La preluarea datelor din surse externe (fișiere text, input utilizator), tipurile pot fi șiruri și trebuie convertite pentru prelucrare corectă.
4. **Flexibilitatea codului**: Folosind `int()`, `float()`, `str()` și altele putem manipula datele conform cerințelor și scrie cod mai flexibil și universal.

**Exemplu de concatenare a șirurilor:**

```python
nmbr1 = 22
nmbr2 = "33"
print(str(nmbr1) + nmbr2)  # "2233"
```

Funcția `str()` transformă `nmbr1` în șir, iar acum ambele valori pot fi combinate.

**Notă:**

* Conversia poate genera erori dacă datele nu sunt compatibile cu tipul țintă (de exemplu, încercarea de a converti un șir ne-numeric în `int`).
* Este important să verificăm sau să gestionăm erorile la conversia tipurilor în Python.

---

### 11. Operatori

Iată o prezentare a diferitelor tipuri de operatori în Python, folosiți pentru efectuarea diferitelor operații:

#### 1. **Operatori aritmetici**

Operatorii aritmetici efectuează operații matematice standard:

* **`+`**: Adunare
* **`-`**: Scădere
* **`*`**: Înmulțire
* **`/`**: Împărțire (rezultatul este un număr real)
* **`//`**: Împărțire întreagă (rezultatul este un număr întreg)
* **`%`**: Restul împărțirii
* **`**`**: Ridicare la putere

**Exemplu:**

```python
a = 10
b = 3
print(a + b)  # 13
print(a // b)  # 3
print(a ** b)  # 1000
```

#### 2. **Operatori de atribuire**

Operatorii de atribuire sunt folosiți pentru a atribui valori variabilelor:

* **`=`**: Atribuire
* **`+=`**: Adunare și atribuire (`a += b` este echivalent cu `a = a + b`)
* **`-=`**: Scădere și atribuire
* **`*=`**: Înmulțire și atribuire
* **`/=`**: Împărțire și atribuire
* **`//=`**: Împărțire întreagă și atribuire
* **`%=`**: Rest și atribuire
* **`**=`**: Ridicare la putere și atribuire

**Exemplu:**

```python
a = 10
a += 5  # a = a + 5
print(a)  # 15
```

#### 3. **Operatori de comparație**

Operatorii de comparație sunt folosiți pentru a compara valori:

* **`==`**: Egalitate
* **`!=`**: Diferit
* **`>`**: Mai mare
* **`<`**: Mai mic
* **`>=`**: Mai mare sau egal
* **`<=`**: Mai mic sau egal

**Exemplu:**

```python
a = 10
b = 5
print(a == b)  # False
print(a > b)   # True
```

#### 4. **Operatori de identitate**

Operatorii de identitate verifică dacă două obiecte se referă la același obiect în memorie:

* **`is`**: Verifică identitatea
* **`is not`**: Verifică lipsa identității

**Exemplu:**

```python
a = [1, 2, 3]
b = a
print(a is b)  # True
```

#### 5. **Operatori de apartenență (membership)**

Operatorii de apartenență verifică dacă un obiect face parte dintr-o colecție:

* **`in`**: Verifică dacă elementul este în colecție
* **`not in`**: Verifică dacă elementul nu este în colecție

**Exemplu:**

```python
a = [1, 2, 3]
print(2 in a)  # True
print(4 not in a)  # True
```

#### 6. **Operatori pentru lucrul cu șiruri de caractere**

În Python, șirurile permit anumite operații:

* **`+`**: Concatenare
* **`*`**: Repetarea șirului

**Exemplu:**

```python
a = "Hello"
b = " World"
print(a + b)  # "Hello World"
print(a * 3)  # "HelloHelloHello"
```

#### 7. **Operatori pe biți (bitwise)**

Operatorii pe biți operează la nivel de biți pentru numere întregi:

* **`&`**: AND pe biți
* **`|`**: OR pe biți
* **`^`**: XOR pe biți
* **`~`**: NOT pe biți
* **`<<`**: Shift la stânga
* **`>>`**: Shift la dreapta

**Exemplu:**

```python
a = 5  # 101 în binar
b = 3  # 011 în binar
print(a & b)  # 1 (101 & 011 = 001)
print(a | b)  # 7 (101 | 011 = 111)
```

Acești operatori permit efectuarea eficientă a diferitelor operații și manipularea datelor la nivel de biți.

#### 8. **Operatori logici în Python**

Operatorii logici sunt folosiți pentru evaluarea expresiilor logice:

**1. Operatorul AND**

* **Descriere**: Returnează `True` dacă ambele expresii sunt adevărate; altfel returnează `False`.
* **Exemplu:**

```python
a = 5
b = 10
c = 15
print(a < b and b < c)  # True
print(a < b and b > c)  # False
```

**2. Operatorul OR**

* **Descriere**: Returnează `True` dacă cel puțin una dintre expresii este adevărată; altfel returnează `False`.
* **Exemplu:**

```python
age = 17
print(age < 18 or age > 60)  # True
print(age < 16 or age > 60)  # False
```

**3. Operatorul NOT**

* **Descriere**: Inversează expresia logică.
* **Exemplu:**

```python
is_admin = True
print(not is_admin)  # False
```

