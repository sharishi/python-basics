# Lecție: **Expresii regulate în Python**

Expresiile regulate (sau **regex**) sunt un instrument puternic pentru lucrul cu textul. Ele permit căutarea, înlocuirea, verificarea sau extragerea datelor din șiruri care corespund unui anumit șablon. În Python, pentru lucrul cu expresii regulate se folosește modulul încorporat **`re`**.

---

## **1. Ce sunt expresiile regulate?**

**Expresiile regulate** sunt șiruri care descriu șabloane pentru căutarea și prelucrarea textului. Aceste șabloane sunt formate din caractere obișnuite, precum și din caractere speciale (metacaractere), care stabilesc regulile de căutare.

Exemplu de expresie regulată simplă:

* **`abc`** — șablon pentru căutarea șirului „abc”.

Șabloanele mai complexe includ metacaractere, care permit realizarea unei căutări mai flexibile:

* **`^a`** — începutul șirului cu litera „a”.
* **`b$`** — sfârșitul șirului cu litera „b”.
* **`[a-z]`** — orice caracter din intervalul de la „a” la „z”.
* **`\d`** — orice cifră (echivalent cu `[0-9]`).
* **`\w`** — orice literă, cifră sau caracter de subliniere (echivalent cu `[a-zA-Z0-9_]`).

---

## **2. Modulul `re` în Python**

Pentru lucrul cu expresii regulate în Python se utilizează modulul **`re`**. Acest modul oferă mai multe funcții pentru căutare, înlocuire și analiză a șirurilor cu ajutorul expresiilor regulate.

### **2.1 Funcțiile de bază ale modulului `re`**

1. **`re.match(pattern, string)`** — încearcă să găsească o potrivire cu șablonul la începutul șirului. Returnează un obiect de potrivire dacă potrivirea este găsită, altfel — `None`.

   ```python
   import re
   result = re.match(r'abc', 'abcdef')
   if result:
       print("Match found:", result.group())
   else:
       print("No match")
   ```

   Rezultat:

   ```
   Match found: abc
   ```

2. **`re.search(pattern, string)`** — caută o potrivire cu șablonul în orice parte a șirului. Returnează un obiect de potrivire dacă potrivirea este găsită, altfel — `None`.

   ```python
   result = re.search(r'abc', 'xyzabcdef')
   if result:
       print("Search found:", result.group())
   else:
       print("No match")
   ```

   Rezultat:

   ```
   Search found: abc
   ```

3. **`re.findall(pattern, string)`** — găsește toate potrivirile ne-supracapuse ale șablonului în șir și le returnează sub forma unei liste.

   ```python
   result = re.findall(r'\d+', 'abc 123 def 456 ghi 789')
   print(result)
   ```

   Rezultat:

   ```
   ['123', '456', '789']
   ```

4. **`re.sub(pattern, repl, string)`** — înlocuiește toate potrivirile șablonului din șir cu șirul `repl`.

   ```python
   result = re.sub(r'\d+', '#', 'abc 123 def 456 ghi 789')
   print(result)
   ```

   Rezultat:

   ```
   abc # def # ghi #
   ```

5. **`re.split(pattern, string)`** — împarte șirul în funcție de potrivirile cu șablonul și returnează o listă de părți ale șirului.

   ```python
   result = re.split(r'\s+', 'abc 123 def 456 ghi 789')
   print(result)
   ```

   Rezultat:

   ```
   ['abc', '123', 'def', '456', 'ghi', '789']
   ```

---

## **3. Metacaractere și utilizarea lor**

Metacaracterele din expresiile regulate permit definirea unor șabloane mai complexe pentru căutarea și manipularea textului.

Există două seturi diferite de metacaractere:

* cele care sunt utilizate în interiorul parantezelor pătrate,
* cele care sunt utilizate în afara parantezelor pătrate

### **3.1 Metacaractere în afara parantezelor pătrate**

#### **1. `^` — Începutul șirului**

Metacaracterul `^` este utilizat pentru a indica începutul șirului. Acest lucru înseamnă că șablonul trebuie să coincidă cu începutul textului.

**Exemplu:**

```python
import re

result = re.match(r'^abc', 'abcdef')
print(result.group())  # abc
```

În acest exemplu, expresia regulată `^abc` verifică dacă șirul începe cu „abc”.

---

#### **2. `$` — Sfârșitul șirului**

Metacaracterul `$` este utilizat pentru a indica sfârșitul șirului. Șablonul trebuie să coincidă cu sfârșitul textului.

**Exemplu:**

```python
import re

result = re.match(r'abc$', 'abcdef')
print(result.group())  # abc
```

Aici expresia regulată `abc$` verifică dacă șirul se termină cu „abc”.

---

#### **3. `.` — Orice caracter (cu excepția liniei noi)**

Punctul `.` reprezintă orice caracter, cu excepția caracterului de linie nouă (`\n`). Acest lucru permite potrivirea șirurilor cu orice caractere în orice poziție.

**Exemplu:**

```python
import re

result = re.match(r'a.c', 'abc')
print(result.group())  # abc
```

Aici punctul din șablonul `a.c` corespunde oricărui caracter dintre „a” și „c”. În acest caz, se potrivește cu „abc”.

---

#### **4. `[]` — Clasă de caractere**

Parantezele `[]` sunt utilizate pentru a crea clase de caractere, care permit specificarea unui interval de caractere. În interiorul parantezelor pot fi enumerate caracterele care pot fi găsite în șir.

**Exemplu:**

```python
import re

result = re.match(r'[a-z]', 'b')
print(result.group())  # b
```

Aici `[a-z]` corespunde oricărui caracter din intervalul de la „a” la „z”. În acest exemplu, se potrivește cu caracterul „b”.

**Exemplu cu mai multe caractere:**

```python
result = re.match(r'[abc]', 'b')
print(result.group())  # b
```

Acest șablon caută oricare dintre caracterele „a”, „b” sau „c”.

---



# Lecție: **Expresii regulate în Python**

Expresiile regulate (sau **regex**) — sunt un instrument puternic pentru lucrul cu textul. Ele permit căutarea, înlocuirea, verificarea sau extragerea datelor din șiruri care corespund unui anumit șablon. În Python, pentru lucrul cu expresii regulate se utilizează modulul încorporat **`re`**.

---

## **1. Ce sunt expresiile regulate?**

**Expresiile regulate** — sunt șiruri care descriu șabloane pentru căutarea și procesarea textului. Aceste șabloane sunt formate din caractere obișnuite, precum și din caractere speciale (metacaractere), care stabilesc regulile de căutare.

Exemplu de expresie regulată simplă:

* **`abc`** — șablon pentru căutarea șirului „abc”.

Șabloanele mai complexe includ metacaractere, care permit realizarea unei căutări mai flexibile:

* **`^a`** — începutul șirului cu litera „a”.
* **`b$`** — sfârșitul șirului cu litera „b”.
* **`[a-z]`** — orice caracter din intervalul de la „a” la „z”.
* **`\d`** — orice cifră (echivalent cu `[0-9]`).
* **`\w`** — orice literă, cifră sau caracter de subliniere (echivalent cu `[a-zA-Z0-9_]`).

---

## **2. Modulul `re` în Python**

Pentru lucrul cu expresii regulate în Python se folosește modulul **`re`**. Acest modul oferă mai multe funcții pentru căutare, înlocuire și analiză a șirurilor cu ajutorul expresiilor regulate.

### **2.1 Funcțiile de bază ale modulului `re`**

1. **`re.match(pattern, string)`** — încearcă să găsească o potrivire cu șablonul la începutul șirului. Returnează un obiect de potrivire dacă potrivirea este găsită, altfel — `None`.

   ```python
   import re
   result = re.match(r'abc', 'abcdef')
   if result:
       print("Match found:", result.group())
   else:
       print("No match")
   ```

   Rezultat:

   ```
   Match found: abc
   ```

2. **`re.search(pattern, string)`** — caută o potrivire cu șablonul în orice parte a șirului. Returnează un obiect de potrivire dacă potrivirea este găsită, altfel — `None`.

   ```python
   result = re.search(r'abc', 'xyzabcdef')
   if result:
       print("Search found:", result.group())
   else:
       print("No match")
   ```

   Rezultat:

   ```
   Search found: abc
   ```

3. **`re.findall(pattern, string)`** — găsește toate potrivirile ne-suprapuse ale șablonului în șir și le returnează sub formă de listă.

   ```python
   result = re.findall(r'\d+', 'abc 123 def 456 ghi 789')
   print(result)
   ```

   Rezultat:

   ```
   ['123', '456', '789']
   ```

4. **`re.sub(pattern, repl, string)`** — înlocuiește toate potrivirile șablonului din șir cu șirul `repl`.

   ```python
   result = re.sub(r'\d+', '#', 'abc 123 def 456 ghi 789')
   print(result)
   ```

   Rezultat:

   ```
   abc # def # ghi #
   ```

5. **`re.split(pattern, string)`** — împarte șirul după potrivirile cu șablonul și returnează o listă de părți ale șirului.

   ```python
   result = re.split(r'\s+', 'abc 123 def 456 ghi 789')
   print(result)
   ```

   Rezultat:

   ```
   ['abc', '123', 'def', '456', 'ghi', '789']
   ```

---

## **3. Metacaractere și utilizarea lor**

Metacaracterele în expresiile regulate permit definirea unor șabloane mai complexe pentru căutarea și manipularea textului.

Există două seturi diferite de metacaractere:

* cele care sunt utilizate în interiorul parantezelor pătrate,
* cele care sunt utilizate în afara parantezelor pătrate

### **3.1 Metacaractere în afara parantezelor pătrate**

#### **1. `^` — Începutul șirului**

Metacaracterul `^` este utilizat pentru a indica începutul șirului. Aceasta înseamnă că șablonul trebuie să coincidă cu începutul textului.

**Exemplu:**

```python
import re

result = re.match(r'^abc', 'abcdef')
print(result.group())  # abc
```

În acest exemplu, expresia regulată `^abc` verifică dacă șirul începe cu „abc”.

---

#### **2. `$` — Sfârșitul șirului**

Metacaracterul `$` este utilizat pentru a indica sfârșitul șirului. Șablonul trebuie să coincidă cu sfârșitul textului.

**Exemplu:**

```python
import re

result = re.match(r'abc$', 'abcdef')
print(result.group())  # abc
```

Aici expresia regulată `abc$` verifică dacă șirul se termină cu „abc”.

---

#### **3. `.` — Orice caracter (cu excepția liniei noi)**

Punctul `.` reprezintă orice caracter, cu excepția caracterului de linie nouă (`\n`). Acest lucru permite potrivirea șirurilor cu orice caractere în orice poziție.

**Exemplu:**

```python
import re

result = re.match(r'a.c', 'abc')
print(result.group())  # abc
```

Aici punctul din șablonul `a.c` corespunde oricărui caracter dintre „a” și „c”. În acest caz, corespunde cu „abc”.

---

#### **4. `[]` — Clasă de caractere**

Parantezele `[]` sunt utilizate pentru a crea clase de caractere, care permit indicarea unui interval de caractere. În interiorul parantezelor pot fi enumerate caracterele care pot fi găsite în șir.

**Exemplu:**

```python
import re

result = re.match(r'[a-z]', 'b')
print(result.group())  # b
```

Aici `[a-z]` corespunde oricărui caracter din intervalul de la „a” la „z”. În acest exemplu, corespunde caracterului „b”.

**Exemplu cu mai multe caractere:**

```python
result = re.match(r'[abc]', 'b')
print(result.group())  # b
```

Acest șablon caută oricare dintre caracterele „a”, „b” sau „c”.

---

#### **5. `|` — Alegere condițională (SAU)**

Metacaracterul `|` permite crearea unei alegeri între mai multe variante. Acesta este echivalentul logic „SAU” în expresiile regulate.

**Exemplu:**

```python
import re

result = re.match(r'cat|dog', 'dog')
print(result.group())  # dog
```

În acest exemplu, expresia regulată `cat|dog` va corespunde fie cu „cat”, fie cu „dog”. În acest caz a coincis „dog”.

---

#### **6. `()` — Grupare și submăști**

Parantezele rotunde `()` sunt utilizate pentru a grupa părți ale expresiei, pentru a indica ce simboluri sau expresii trebuie procesate împreună. Acest lucru permite, de asemenea, capturarea grupurilor de potriviri.

**Exemplu:**

```python
import re

result = re.match(r'(abc)', 'abcdef')
print(result.group(1))  # abc
```

În acest exemplu, expresia `(abc)` capturează șirul „abc”, care devine apoi disponibil prin `group(1)`.

---

#### **7. `?` — 0 sau 1 apariție (cuantificator)**

Metacaracterul `?` este un cuantificator care indică faptul că simbolul sau grupul anterior poate apărea de 0 sau 1 ori.

**Exemplu:**

```python
import re

result = re.match(r'colou?r', 'color')
print(result.group())  # color
```

Aici expresia regulată `colou?r` corespunde atât cu „color”, cât și cu „colour”, deoarece litera „u” este opțională.

---

#### **8. `*` — 0 sau mai multe apariții (cuantificator)**

Metacaracterul `*` indică faptul că simbolul sau grupul anterior poate apărea de 0 sau mai multe ori.

**Exemplu:**

```python
import re

result = re.match(r'lo*', 'look')
print(result.group())  # loo
```

Aici expresia regulată `lo*` găsește un șir care începe cu „l”, urmat de 0 sau mai multe simboluri „o”. În exemplul „look” corespunde cu „loo”.

---

#### **9. `+` — 1 sau mai multe apariții (cuantificator)**

Metacaracterul `+` indică faptul că simbolul sau grupul anterior trebuie să apară cel puțin o dată sau de mai multe ori.

**Exemplu:**

```python
import re

result = re.match(r'lo+', 'look')
print(result.group())  # loo
```

În acest exemplu, expresia regulată `lo+` găsește „l”, urmat de una sau mai multe litere „o”.

---

#### **10. Transformarea cuantificatorilor lacomi în lenți**

Metacaracterul `?` este de asemenea utilizat pentru a transforma cuantificatorii „lacomi” (care capturează cât mai multe caractere) în „lenți”, care capturează cât mai puține caractere.

**Exemplu cu cuantificator lacom:**

```python
import re

result = re.match(r'<.*>', '<div>content</div>')
print(result.group())  # <div>content</div>
```

Aici `.*` capturează întregul șir, inclusiv „div”, deoarece este un cuantificator lacom.

**Exemplu cu cuantificator lent:**

```python
result = re.match(r'<.*?>', '<div>content</div>')
print(result.group())  # <div>
```

Adăugarea lui `?` face cuantificatorul lent, iar acesta capturează cât mai puține caractere, în acest caz doar primul tag `<div>`.

---

În expresiile regulate Python, în interiorul parantezelor pătrate sunt utilizate metacaractere speciale pentru crearea claselor de caractere și a intervalelor. Aceste metacaractere permit definirea caracterelor care pot fi găsite într-o anumită poziție din șir.

### **3.2 Metacaractere în interiorul parantezelor pătrate**

---

#### **1. `-` — Interval de caractere**

Metacaracterul `-` este utilizat pentru a desemna un interval de caractere. Intervalul poate fi numeric sau literal. Caracterele din interval pot fi reprezentate în ordine de la cel mai mic la cel mai mare.

**Exemplu:**

```python
import re

# Interval de la 'a' la 'z'
result = re.match(r'[a-z]', 'g')
print(result.group())  # g

# Interval de la '0' la '9'
result = re.match(r'[0-9]', '5')
print(result.group())  # 5
```

Aici `[a-z]` corespunde oricărui caracter de la „a” la „z”, iar `[0-9]` corespunde oricărui număr de la 0 la 9.

---

#### **2. `^` — Negare (când este primul simbol în paranteze)**

Dacă simbolul `^` se află pe prima poziție în parantezele pătrate, acesta inversează clasa de caractere, adică creează o clasă care corespunde oricărui caracter **cu excepția** celor enumerate în paranteze.

**Exemplu:**

```python
import re

# Corespunde oricărui caracter care nu este cifră
result = re.match(r'[^0-9]', 'a')
print(result.group())  # a

# Corespunde oricărui caracter care nu este litera 'a', 'b' sau 'c'
result = re.match(r'[^abc]', 'd')
print(result.group())  # d
```

Aici `[^0-9]` corespunde oricărui caracter care nu este cifră, iar `[^abc]` — oricărui caracter, cu excepția lui „a”, „b” și „c”.

---

#### **3. `[]` — Clasă de caractere**

Parantezele pătrate `[]` sunt utilizate pentru a crea clase de caractere, în care sunt enumerate caracterele dintre care unul trebuie să coincidă cu caracterul din șir.

**Exemplu:**

```python
import re

# Corespunde oricărui caracter care este fie 'a', fie 'b'
result = re.match(r'[ab]', 'a')
print(result.group())  # a

# Corespunde oricărui caracter care este literă sau cifră
result = re.match(r'[a-zA-Z0-9]', '1')
print(result.group())  # 1
```

În acest exemplu, `[ab]` corespunde oricărui simbol „a” sau „b”, iar `[a-zA-Z0-9]` — oricărui caracter din intervalele „a-z”, „A-Z” sau unei cifre de la „0” la „9”.

---

Aici `[\s]` corespunde oricărui caracter de spațiere, de exemplu spațiu, tabulație sau linie nouă.

#### **4. Secvențe speciale**

Secvențele speciale în expresiile regulate Python sunt simboluri care încep cu bara oblică inversă (`\`) și au o semnificație specială, permițând un control mai precis asupra caracterelor care vor corespunde șablonului vostru. Aceste secvențe simplifică crearea de pattern-uri și extind posibilitățile de căutare.

#### **1. `\f` — Săritură de pagină**

Metacaracterul `\f` corespunde caracterului de săritură de pagină. Acesta este un caracter special, utilizat în texte pentru a marca sfârșitul unei pagini (de exemplu, în formate vechi de documente).

**Exemplu:**

```python
import re

# Corespunde caracterului de săritură de pagină
result = re.match(r'\f', '\f')
if result:
    print("Săritură de pagină găsită.")
```

---

#### **2. `\n` — Trecere la linie nouă (Newline)**

Metacaracterul `\n` corespunde caracterului de trecere la linie nouă, care este utilizat în texte pentru a trece pe o linie nouă.

**Exemplu:**

```python
import re

# Corespunde caracterului de trecere la linie nouă
result = re.match(r'\n', '\n')
if result:
    print("Trecere la linie nouă găsită.")
```

#### **3. `\r` — Revenire de car (Carriage Return)**

Metacaracterul `\r` corespunde simbolului de revenire de car, care este utilizat pentru a muta cursorul la începutul liniei, fără a trece pe o linie nouă.

**Exemplu:**

```python
import re

# Corespunde simbolului de revenire de car
result = re.match(r'\r', '\r')
if result:
    print("Revenire de car găsită.")
```

---

#### **4. `\t` — Tabulație**

Metacaracterul `\t` corespunde simbolului de tabulație, care este utilizat pentru a crea indentări sau pentru alinierea textului în coloane.

**Exemplu:**

```python
import re

# Corespunde simbolului de tabulație
result = re.match(r'\t', '\t')
if result:
    print("Tabulație găsită.")
```

---

#### **5. `\d` — Cifră (Decimal Digit)**

Metacaracterul `\d` corespunde oricărui număr zecimal (cifră) de la 0 la 9.

**Exemplu:**

```python
import re

# Corespunde unei cifre
result = re.match(r'\d', '5')
if result:
    print("Cifră găsită.")
```

---

#### **6. `\D` — Nu este cifră (Non-digit)**

Metacaracterul `\D` corespunde oricărui simbol care nu este cifră.

**Exemplu:**

```python
import re

# Corespunde unui simbol care nu este cifră
result = re.match(r'\D', 'a')
if result:
    print("Nu este cifră găsită.")
```

---

#### **7. `\s` — Caracter de spațiere (Whitespace)**

Metacaracterul `\s` corespunde oricărui caracter de spațiere, inclusiv spațiu, tabulație, caracter de linie nouă, revenire de car și altele.

**Exemplu:**

```python
import re

# Corespunde unui caracter de spațiere
result = re.match(r'\s', ' ')
if result:
    print("Caracter de spațiere găsit.")
```

---

#### **8. `\S` — Caracter care nu este de spațiere (Non-whitespace)**

Metacaracterul `\S` corespunde oricărui caracter care **nu** este de spațiere.

**Exemplu:**

```python
import re

# Corespunde unui caracter care nu este de spațiere
result = re.match(r'\S', 'a')
if result:
    print("Caracter care nu este de spațiere găsit.")
```

---

#### **9. `\w` — Caracter de cuvânt (Word character)**

Metacaracterul `\w` corespunde oricărui caracter care este literă (majuscule sau minuscule), cifră sau caracter de subliniere (`_`).

**Exemplu:**

```python
import re

# Corespunde unui caracter de cuvânt
result = re.match(r'\w', 'a')
if result:
    print("Caracter de cuvânt găsit.")
```

---

#### **10. `\W` — Nu este caracter de cuvânt (Non-word character)**

Metacaracterul `\W` corespunde oricărui caracter care nu este literă, cifră sau caracter de subliniere (`_`).

**Exemplu:**

```python
import re

# Corespunde unui caracter care nu este de cuvânt
result = re.match(r'\W', '@')
if result:
    print("Nu este caracter de cuvânt găsit.")
```

În expresiile regulate Python există, de asemenea, secvențe speciale suplimentare care funcționează cu anumite poziții din șiruri. Aceste secvențe permit un control mai precis asupra locului unde trebuie să se afle caracterele pentru a corespunde șablonului dat.

### Secvențe speciale pentru expresii poziționale

---

#### **11. `\A` — Începutul șirului**

Metacaracterul `\A` este utilizat pentru a indica faptul că șablonul trebuie să corespundă doar la începutul întregului șir (fără a ține cont de modul multi-linie). Acesta este similar cu simbolul `^`, dar `\A` corespunde întotdeauna începutului șirului, spre deosebire de `^`, care poate funcționa diferit în contexte diferite, de exemplu în modul multi-linie.

**Exemplu:**

```python
import re

# Corespunde cu "start" doar la începutul șirului
result = re.match(r'\Astart', 'start here')
if result:
    print("Potrivire găsită la începutul șirului.")
```

---

#### **12. `\b` — Limită de cuvânt (word boundary)**

Metacaracterul `\b` indică limita unui cuvânt. El corespunde poziției dintre un caracter care face parte dintr-un cuvânt (literă, cifră sau caracter de subliniere) și un caracter care nu face parte dintr-un cuvânt (de exemplu, spațiu, punctuație sau început/sfârșit de șir).

**Exemplu:**

```python
import re

# Corespunde cu "word", dacă acesta se află la începutul sau la sfârșitul unui cuvânt
result = re.search(r'\bword\b', 'This is a word.')
if result:
    print("Potrivire găsită la începutul sau la sfârșitul cuvântului.")
```

**Notă:** `\b` funcționează și la limita șirului, dacă un cuvânt începe sau se termină acolo.

---

#### **13. `\B` — Nu este limită de cuvânt (non-word boundary)**

Metacaracterul `\B` corespunde oricărei poziții care **nu este** o limită de cuvânt. Aceasta înseamnă că simbolurile trebuie să fie în interiorul unui cuvânt, nu la începutul sau la sfârșitul acestuia.

**Exemplu:**

```python
import re

# Corespunde cu "word" în interiorul unui alt cuvânt, dar nu la început sau la sfârșit
result = re.search(r'\Bword\B', 'swordfish')
if result:
    print("Potrivire găsită în interiorul cuvântului.")
```

---

#### **14. `\Z` — Sfârșitul șirului**

Metacaracterul `\Z` corespunde sfârșitului șirului. Acesta este analog simbolului `$`, însă `\Z` va funcționa întotdeauna ca sfârșit de șir, în timp ce `$` poate funcționa diferit în modul multi-linie.

**Exemplu:**

```python
import re

# Corespunde cu "end" doar la sfârșitul șirului
result = re.search(r'end\Z', 'This is the end')
if result:
    print("Potrivire găsită la sfârșitul șirului.")
```

---

### **3.2 Cuantificatori**

Cuantificatorii indică de câte ori trebuie să se repete un element într-o expresie regulată.

* **`*`** — de 0 sau mai multe ori.

  ```python
  result = re.findall(r'lo*', 'look at this loop')
  print(result)  # ['lo', 'loo', 'loop']
  ```

* **`+`** — de 1 sau mai multe ori.

  ```python
  result = re.findall(r'lo+', 'look at this loop')
  print(result)  # ['loo', 'loop']
  ```

* **`?`** — de 0 sau 1 dată.

  ```python
  result = re.findall(r'lo?', 'look at this loop')
  print(result)  # ['lo', 'lo']
  ```

* **`{n}`** — exact de n ori.

  ```python
  result = re.findall(r'lo{2}', 'look at this looop')
  print(result)  # ['loo']
  ```

* **`{n, m}`** — de la n la m ori.

  ```python
  result = re.findall(r'lo{1,3}', 'look at this loooop')
  print(result)  # ['loo', 'loo']
  ```

---

## **4. Utilizarea grupurilor și a capturilor**

Expresiile regulate permit evidențierea grupurilor de simboluri care pot fi utilizate ulterior. Acest lucru se realizează cu ajutorul parantezelor rotunde.

### **4.1 Grupuri**

Gruparea permite extragerea părților din șirul care a coincis.

```python
result = re.match(r'(\d+)-(\d+)', '123-456')
print(result.groups())  # ('123', '456')
```

* **`group(0)`** — întregul șir.
* **`group(1), group(2), ...`** — grupurile corespunzătoare.

### **4.2 Grupuri ne-numerotate**

Dacă nu este necesar să fie returnat rezultatul pentru un anumit grup, pot fi utilizate grupuri ne-numerotate cu `?:`.

```python
result = re.match(r'(?:\d+)-(\d+)', '123-456')
print(result.groups())  # ('456',)
```

---

## **5. Exemplu de utilizare a expresiilor regulate**

Să presupunem că avem un șir și dorim să extragem toate adresele de email.

```python
import re

text = "Contact us at support@example.com or sales@company.org"
emails = re.findall(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,7}\b', text)

print(emails)
```

Rezultat:

```
['support@example.com', 'sales@company.org']
```

---

### **6. Afirmații în expresiile regulate (Lookahead și Lookbehind)**

Afirmațiile în expresiile regulate permit verificarea condițiilor care trebuie să fie îndeplinite înainte sau după poziția curentă din șir. Aceste afirmații nu consumă caractere din șir, ci doar verifică dacă simbolurile din anumite poziții corespund condițiilor. Afirmațiile pot fi **pozitive** sau **negative** și pot face referire la **textul următor** (lookahead) sau la **textul precedent** (lookbehind).

---

#### **1. Afirmație pozitivă (positive lookahead)**

Afirmația pozitivă, sau **lookahead**, verifică dacă după poziția curentă se află un anumit pattern. Aceasta se notează ca `(?=...)`, unde `...` este pattern-ul care trebuie să urmeze după poziția curentă.

**Exemplu:**

```python
import re

addresses = ['str. Nucului', 'str. Pushkin', 'Mateevici str', 'Kostrikin blvrd']
my_pattern = '.*(?=str$)'  # Lookahead pozitiv, verifică faptul că după "str" urmează sfârșitul șirului

for item in addresses:
    result = re.match(my_pattern, item)
    if result:
        print('I found it:', item)
    else:
        print('Nothing!')
```

**Explicație:**

* Pattern-ul `.*(?=str$)` caută orice simbol (`.*`), după care **trebuie obligatoriu** să urmeze textul `"str"`, iar șirul să se termine cu acest cuvânt (`$`).
* În acest exemplu, doar șirurile care se termină cu `"str"` vor fi potrivite cu succes.

**Rezultat:**

```
I found it: Mateevici str
Nothing!
Nothing!
Nothing!
```

---

#### **2. Afirmație negativă (negative lookahead)**

Afirmația negativă (sau **negative lookahead**) verifică faptul că după poziția curentă **nu urmează** un anumit pattern. Aceasta se notează ca `(?!...)`.

**Exemplu:**

```python
import re

addresses = ['str. Nucului', 'str. Pushkin', 'Mateevici str', 'Kostrikin blvrd']
my_pattern = '.*(?!str$)'  # Lookahead negativ, verifică faptul că nu urmează "str" la sfârșitul șirului

for item in addresses:
    result = re.match(my_pattern, item)
    if result:
        print('I found it:', item)
    else:
        print('Nothing!')
```

**Explicație:**

* Pattern-ul `.*(?!str$)` caută orice simbol (`.*`), după care nu trebuie să urmeze `"str"`, iar șirul nu trebuie să se termine cu `"str"`.
* În acest exemplu, șirurile care se termină cu `"str"` nu vor fi potrivite.

**Rezultat:**

```
I found it: str. Nucului
I found it: str. Pushkin
Nothing!
I found it: Kostrikin blvrd
```

---

#### **3. Afirmație pozitivă înainte (positive lookbehind)**

Afirmația pozitivă înainte (sau **lookbehind**) verifică dacă înaintea poziției curente se află un anumit pattern. Aceasta se notează ca `(?<=...)`.

**Exemplu:**

```python
import re

text = 'The quick brown fox jumps over the lazy dog'
my_pattern = '(?<=quick ).*'  # Lookbehind pozitiv, verifică faptul că înainte se află cuvântul "quick"

result = re.search(my_pattern, text)
if result:
    print('Found:', result.group())
else:
    print('Nothing!')
```

**Explicație:**

* Pattern-ul `(?<=quick ).*` caută tot ce urmează după cuvântul `"quick"`.
* Această afirmație verifică faptul că înaintea poziției curente se află cuvântul `"quick"`, iar tot ce urmează este capturat.

**Rezultat:**

```
Found: brown fox jumps over the lazy dog
```

---

#### **4. Afirmație negativă înainte (negative lookbehind)**

Afirmația negativă înainte (sau **negative lookbehind**) verifică faptul că înaintea poziției curente **nu se află** un anumit pattern. Aceasta se notează ca `(?<!...)`.

**Exemplu:**

```python
import re

text = 'The quick brown fox jumps over the lazy dog'
my_pattern = '(?<!quick ).*'  # Lookbehind negativ, verifică faptul că înainte nu se află "quick"

result = re.search(my_pattern, text)
if result:
    print('Found:', result.group())
else:
    print('Nothing!')
```

**Explicație:**

* Pattern-ul `(?<!quick ).*` caută tot ce nu se află imediat după cuvântul `"quick"`.
* În acest caz, el nu va captura textul care urmează după `"quick"`.

**Rezultat:**

```
Found: brown fox jumps over the lazy dog
```

---

## **7. Concluzie**

Expresiile regulate sunt un instrument puternic pentru lucrul cu textul. Ele permit crearea unor algoritmi flexibili și rapizi pentru căutare, înlocuire și extragere de informații. În Python, modulul **`re`** oferă toate instrumentele necesare pentru lucrul eficient cu expresiile regulate, iar utilizarea acestora poate simplifica semnificativ procesarea textului.
