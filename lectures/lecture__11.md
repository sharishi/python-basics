# 📘 **Curs: Crearea și utilizarea endpoint-urilor web**

---

# Capitolul 1. Introducere în API și aplicații web

## 1.1. Ce este un API?

**API (Application Programming Interface)** — este un interfață de comunicare între programe.

* Imaginați-vă: aveți un server care stochează date și un client (browser, aplicație mobilă) care vrea să obțină aceste date.
* API descrie **regulile de comunicare** între ele: ce cereri pot fi făcute și ce răspuns să se aștepte.

Exemple:

* magazin online: API returnează lista produselor, adaugă o comandă, schimbă starea unei comenzi
* messenger: API obține lista mesajelor, trimite un mesaj nou

**Ideea:** în loc ca clientul și serverul să „trage” fișiere unul de la altul, API oferă **interacțiune structurată, predictibilă și sigură**.

---

## 1.2. Cereri HTTP: baza API

API folosește de obicei **protocolul HTTP**. Metode principale:

| Metodă | Scop                                |
| ------ | ----------------------------------- |
| GET    | Obține date                         |
| POST   | Creează date noi                    |
| PUT    | Actualizează complet date existente |
| PATCH  | Actualizează parțial date existente |
| DELETE | Șterge date                         |

Exemplu:

* GET `/users` → obține lista utilizatorilor
* POST `/users` → creează un utilizator nou
* GET `/users/5` → obține utilizatorul cu ID = 5

Datele se transmit prin:

* Parametrii URL (`/users/5`)
* Parametrii Query (`/users?age=25`)
* Corpul cererii (de obicei JSON pentru POST/PUT)

---

# Capitolul 2. Ce este FastAPI

FastAPI — este un **framework Python pentru crearea aplicațiilor web și API**.

### Caracteristici principale:

1. **Rapiditate** — rulează pe server asincron Uvicorn, suportă async/await
2. **Simplitate** — endpoint-urile sunt descrise ca funcții normale
3. **Validarea datelor** — prin tipuri Python și Pydantic
4. **Autodocumentare** — Swagger UI și ReDoc sunt generate automat
5. **Funcționalități moderne** — suport WebSockets, Dependency Injection, Background Tasks

**Ideea:** în loc să faci manual parsing-ul cererilor HTTP, FastAPI face asta automat, verifică datele, returnează JSON și generează documentație.

---

# Capitolul 3. Ce este un endpoint

**Endpoint** — este URL-ul prin care clientul interacționează cu serverul.

Exemple:

| URL         | Metodă | Descriere                          |
| ----------- | ------ | ---------------------------------- |
| /           | GET    | Pagina principală                  |
| /users      | GET    | Obține toți utilizatorii           |
| /users      | POST   | Creează un utilizator nou          |
| /users/{id} | GET    | Obține utilizator după ID          |
| /users/{id} | PUT    | Actualizează datele utilizatorului |
| /users/{id} | DELETE | Șterge utilizatorul după ID        |

**Ideea:** fiecare endpoint este un punct de intrare în aplicație, un „port” pentru cereri și răspunsuri.

---

# Capitolul 4. Instalarea FastAPI și Uvicorn

Pentru a lucra cu FastAPI, instalați:

```bash
pip install fastapi uvicorn
```

* **FastAPI** — framework-ul
* **Uvicorn** — server ASGI, rulează aplicația și gestionează cererile HTTP

După instalare, puteți crea aplicații web și API complete în Python.

---

# Capitolul 5. Aplicație minimă cu un endpoint

Creați fișierul `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()  # creăm instanța aplicației

@app.get("/")
def read_root():
    return {"message": "Hello, FastAPI!"}
```

### Explicații:

* `app = FastAPI()` — creează aplicația care va gestiona cererile
* `@app.get("/")` — decorator: „pentru GET pe URL `/`, apelează această funcție”
* `read_root()` — funcția-endpoint, returnează un dicționar, FastAPI îl convertește automat în JSON

### Lansare:

```bash
uvicorn main:app --reload
```

* `main` — numele fișierului fără `.py`
* `app` — obiect FastAPI
* `--reload` — serverul se va reîncărca automat la schimbări

Accesați [http://127.0.0.1:8000](http://127.0.0.1:8000)

Rezultat:

```json
{"message": "Hello, FastAPI!"}
```

---

# Capitolul 6. Endpoint-uri cu parametri
# 📘 **Curs: Crearea și utilizarea endpoint-urilor web (continuare)**

---

# Capitolul 6. Endpoint-uri cu parametri

## 6.1. Parametri de cale (Path Parameters)

Endpoint-urile pot primi variabile direct din URL:

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id, "name": f"User {user_id}"}
```

* `user_id` din URL-ul `/users/5` va fi transmis funcției
* FastAPI convertește automat string-ul în `int`
* Dacă se transmite o valoare care nu este număr, FastAPI returnează eroarea 422

**Exemplu cerere:** `GET /users/5`
**Răspuns:**

```json
{"user_id": 5, "name": "User 5"}
```

---

## 6.2. Parametri de interogare (Query Parameters)

Parametrii de interogare se transmit prin `?` în URL:

```python
@app.get("/items/")
def get_items(skip: int = 0, limit: int = 10):
    return {"skip": skip, "limit": limit}
```

**Exemplu cerere:** `/items/?skip=5&limit=20`
**Răspuns:**

```json
{"skip": 5, "limit": 20}
```

**Ideea:** parametrii de query sunt utili pentru filtre, paginare și căutare.

---

# Capitolul 7. Cereri POST și validarea datelor

Pentru cererile POST, datele se trimit în **corpului cererii** (de obicei JSON).

FastAPI folosește **Pydantic** pentru validarea și tipizarea datelor.

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    name: str
    age: int

@app.post("/users/")
def create_user(user: User):
    return {"message": f"User {user.name} created!", "user": user}
```

**Exemplu corp cerere JSON:**

```json
{
  "name": "Ivan",
  "age": 25
}
```

**Răspuns server:**

```json
{
  "message": "User Ivan created!",
  "user": {"name": "Ivan", "age": 25}
}
```

### Explicație:

* `User` — model de date care definește câmpurile așteptate
* FastAPI verifică automat tipurile (`str`, `int`) și prezența câmpurilor obligatorii
* Dacă datele sunt incorecte → FastAPI returnează o eroare cu explicații

---

# Capitolul 8. Documentație automată

FastAPI generează automat **Swagger UI** și **ReDoc**:

* Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
* ReDoc: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

Se pot testa endpoint-urile direct din browser, trimite cereri GET/POST și vizualiza răspunsurile.

---

# Capitolul 9. Concluzii și idei cheie

1. **Endpoint** — punctul de intrare în aplicația server
2. **FastAPI** permite crearea rapidă a endpoint-urilor cu cod minim
3. **GET și POST** sunt principalele metode HTTP, dar se pot folosi și PUT, PATCH, DELETE
4. **Parametrii de cale, parametrii de query și JSON în corpul cererii** oferă flexibilitate în manipularea datelor
5. **Autodocumentarea** este un instrument puternic pentru testarea și interacțiunea cu API-ul
6. Crearea unei aplicații web cu FastAPI în esență înseamnă **crearea unui API**, care poate fi folosit de frontend, aplicații mobile sau alte servere
