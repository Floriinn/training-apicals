# Axios vs Fetch - Ghid de Comparație

## 📋 Fișiere

- **`script.js`** - Implementări cu **AXIOS** (libraria folosită în proiectul acesta)
- **`script-fetch.js`** - Implementări cu **FETCH API** (API nativ al browserului)

---

## 🔍 Diferențe Principale

### 1. **Cerere POST - Login**

#### ✅ Cu Axios:

```javascript
const response = await axios.post("http://localhost:8090/api/user/login", {
  email,
  password,
});
```

#### ✅ Cu Fetch:

```javascript
const response = await fetch("http://localhost:8090/api/user/login", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ email, password }),
});
const data = await response.json();
```

**Observații:**

- Axios transformă automat obiectele în JSON
- Fetch necesită `JSON.stringify()` manual și header-ul explicit
- Fetch nu aruncă eroare automat pentru status != 2xx

---

### 2. **Cerere GET - Să obțin toți utilizatorii**

#### ✅ Cu Axios:

```javascript
const response = await axios.get("http://localhost:8090/api/user/");
```

#### ✅ Cu Fetch:

```javascript
const response = await fetch("http://localhost:8090/api/user/");
const data = await response.json();
```

**Observații:**

- Axios returnează direct datele în `response.data`
- Fetch necesită `response.json()` extra

---

### 3. **Cerere DELETE - Șterg un utilizator**

#### ✅ Cu Axios:

```javascript
const response = await axios.delete(`http://localhost:8090/api/user/${id}`);
```

#### ✅ Cu Fetch:

```javascript
const response = await fetch(`http://localhost:8090/api/user/${id}`, {
  method: "DELETE",
});
const data = await response.json();
```

---

### 4. **Cerere PATCH - Actualizez departamentul**

#### ✅ Cu Axios:

```javascript
const response = await axios.patch(
  `http://localhost:8090/api/user/${id}/department`,
  {
    idDepartment,
  },
);
```

#### ✅ Cu Fetch:

```javascript
const response = await fetch(
  `http://localhost:8090/api/user/${id}/department`,
  {
    method: "PATCH",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ idDepartment }),
  },
);
const data = await response.json();
```

---

## 📊 Tabel Comparativ

| Caracteristică       | Axios                                  | Fetch                    |
| -------------------- | -------------------------------------- | ------------------------ |
| **Tip**              | Librărie externă                       | API nativ                |
| **Import**           | `<script src="axios.min.js"></script>` | Integrat în browser      |
| **Sintaxă JSON**     | Automată                               | Manual (JSON.stringify)  |
| **Response data**    | `response.data`                        | `await response.json()`  |
| **Gestionare erori** | Auto la status != 2xx                  | Manual (`response.ok`)   |
| **Timeout**          | Suportă nativ                          | Necesită AbortController |
| **Interceptori**     | Suportă nativ                          | Necesită custom logic    |
| **Mărime**           | ~12KB                                  | 0KB (nativ)              |
| **Browser support**  | IE9+                                   | IE (nu suportă)          |

---

## ✅ Avantaje Axios

1. **Sintaxă mai simplă** - Nu trebuie JSON.stringify
2. **Gestionare erori automată** - Orice status !== 2xx e eroare
3. **Interceptori** - Pentru middleware-uri
4. **Timeout** - Configurat ușor
5. **XSRF Protection** - Automată
6. **Cancelarea requesturilor** - Suportă nativ

---

## ✅ Avantaje Fetch

1. **Nativ în browser** - Nu trebuie librărie
2. **Mai mic** - Fără dependență externă
3. **Performanță** - Puțin mai rapid
4. **Standard web** - Part din ES6+
5. **Controlul complet** - Dacă vrei mai multă flexibilitate

---

## 🚀 Cât de Instalez Axios?

În `front-end/package.json` este deja instalat! Doar asigură-te că incluzi:

```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

Sau din `node_modules`:

```html
<script src="../node_modules/axios/dist/axios.min.js"></script>
```

---

## 💡 Recomandări

- **Pentru training** → Folosește **Axios** (mai simplu de învățat)
- **Pentru proiecte mari** → **Axios** (mai putere)
- **Pentru proiecte mici** → **Fetch** (fără dependență)
- **Pentru IE support** → **Axios** (Fetch nu merge pe IE)

---

## 🔧 Error Handling - Comparație

### Cu Axios:

```javascript
try {
  const response = await axios.post(url, data);
  // cod
} catch (error) {
  console.error(error.response?.data); // Direct la date eroare
}
```

### Cu Fetch:

```javascript
try {
  const response = await fetch(url, {
    method: "POST",
    body: JSON.stringify(data),
  });
  if (!response.ok) {
    const errorData = await response.json();
    throw new Error(errorData.message);
  }
  // cod
} catch (error) {
  console.error(error.message);
}
```

---

## 📝 Utilizare în Proiect

Proiectul folosește **Axios** în `script.js`. Toate funcțiile sunt gata pentru a fi apelate din HTML:

```html
<!-- Login -->
<form onsubmit="event.preventDefault(); loginUser(email.value, password.value)">
  <input type="email" id="email" required />
  <input type="password" id="password" required />
  <button type="submit">Login</button>
</form>

<!-- Signup -->
<form
  onsubmit="event.preventDefault(); signUpUser(email.value, password.value)"
>
  <input type="email" id="email" required />
  <input type="password" id="password" required />
  <button type="submit">Sign Up</button>
</form>
```

---

## 🎓 Concluzii

✨ **Axios este mai ușor de folosit** pentru training și proiecte serioase.
🌐 **Fetch este nativ și suficient** pentru aplicații simple.

Ambele lucrează perfect! Alege pe baza preferințelor și necesităților proiectului.
