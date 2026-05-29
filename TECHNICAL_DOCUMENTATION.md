# FindDinFilm - Teknisk Dokumentation

## 📋 Projektoverview

**FindDinFilm** er en webtilpasset filmfinderplatform designet til at hjælpe brugere med at søge efter film og få overblik over tilgængelige film på forskellige streamingservices. Platformen er bygget som en statisk frontend-applikation med integration til Firebase/Firestore.

**Projektmål:** At skabe en brugervenlig interface, hvor danskere nemt kan søge efter film og få information om tilgængelighed.

---

## 🏗️ Arkitektur

### Struktur

```
FindDinFilm/
├── frontpage.html           # Landingsside & søgepunkt
├── login.html              # Loginformular
├── createuser.html         # Registreringsside
├── profilepage.html        # Brugerprofil
├── sorting.html            # Filmsortering & browsing
├── API_search.html         # API-søgefunktionalitet
├── usersettings.html       # Brugerindstillinger
├── style.css               # Globalt CSS stylesheet
├── Data.json               # Konfigurationsfil
├── firebase.json           # Firebase-konfiguration
├── firestore.rules         # Firestore sikkerhedsregler
├── cookie-consent.html     # Cookie-consentbanner
├── hello world.py          # (Hjælpefil)
└── FilmImages/             # Mapper til filmplakater
```

### Frontend-teknologier
- **HTML5** - Semantisk markup
- **CSS3** - Design med CSS-variabler (dark/light mode support)
- **JavaScript** - Interaktivitet og DOM-manipulation (inline i HTML)

### Backend & Database
- **Firebase** - Backend-tjeneste
- **Firestore** - NoSQL database for film-, bruger- og streamingdata
- **Firebase Rules** - Sikkerhedskonfiguration defineret i `firestore.rules`

---

## 🎨 Design & Styling

### CSS-arkitektur

Hele applikationen bruger et centralt **`style.css`** stylesheet med følgende features:

#### Tema & Farvepalette
- **Dark mode (default)**
  - Baggrund: `#0b3252` (mørkebluet)
  - Tekst: `#efeded` (næsten hvidt)
  - Accent: `#00aaff` (himmelblå)
  - Grænse: `#0077ff` (dyb blå)

- **Light mode** (CSS-klasse `.light-mode` på `<html>`)
  - Baggrund: `#f5ede7` (beige)
  - Tekst: `#1a1a1a` (næsten sort)
  - Accent: `#c4956a` (guld)
  - Grænse: `#d4a574` (sand)

#### Layout-komponenter

| Komponent | Beskrivelse |
|-----------|-----------|
| **Header** | Sticky navigation med logo og loginlink |
| **Navigation** | Horisontale links + mobil-toggle |
| **Hero Section** | Gradientbaggrund med stor overskrift |
| **Grid Layout** | 3-kolonne grid for cards (responsive: 2 på tablet, 1 på mobil) |
| **Sidebar** | 25% venstreside med navigation (på profilepage, sorting) |
| **Main Content** | 75% højreside med primært indhold |
| **Featured Films** | 5-kolonne grid af filmplakater (responsive) |
| **Search Bar** | Input felt med søgeknap |
| **Footer** | Dark-mode footer med links |

#### Responsiv design
- **Desktop:** ≥ 901px
- **Tablet:** 600px - 900px  
- **Mobil:** < 600px

---

## 📄 Sidestruktur

### 1. **frontpage.html** - Landingsside
**Formål:** Første indtastpunkt, søgefunktionalitet, featured films

**Komponenter:**
- Header med navigationsmenu
- Button-container (Forside, Søgemaskine, Min Side)
- Søgebar med intro-tekst
- 5 featured filmslots (filmplakater)

**Funktionalitet:**
- `openFilmModal()` - Åbner filmdetaljer i modal
- Dynamisk filmvisning baseret på `FilmImages/`-mappen

---

### 2. **login.html** - Brugerlogin
**Formål:** Autentificere eksisterende brugere

**Formularfelter:**
- Email/Brugernavn
- Adgangskode
- "Husk mig" checkbox
- "Glemt adgangskode" link

**Styling:** Centreret boks med blå border, dark-mode farver

---

### 3. **createuser.html** - Brugerregistrering
**Formål:** Nye brugere opretter konto

**Formularfelter:**
- Navn
- Email
- Adgangskode (med valideringskrav)
- Bekræf adgangskode
- Vilkår & betingelser checkbox

---

### 4. **profilepage.html** - Brugerprofil
**Formål:** Brugerindstillinger, favoritter, historik

**Layout:**
- Sidebar med profilnavigation
- Main content med brugerdata
- Sekskaber til watchlists, historik m.m.

---

### 5. **sorting.html** - Filmgalleri & Filter
**Formål:** Browse og filter film

**Features:**
- Filterbar (efter genre, år, rating osv.)
- Grid-display af filmplakater
- Søgefunktionalitet i stedet for pagination

---

### 6. **API_search.html** - API-søgningsside
**Formål:** Avanceret søgning, integration med tredjepartsfilm-APIs

**Features:**
- Avanceret søgefiltre
- Viser filmoplysninger fra eksterne kilder

---

### 7. **usersettings.html** - Brugerindstillinger
**Formål:** Tilpassede præferencer

**Muligheder:**
- Tema (dark/light mode toggle)
- Notifikationsindstillinger
- Privatlivsindstillinger

---

### 8. **cookie-consent.html** - Cookie-banner
**Formål:** GDPR-kompatibel cookie-consenthåndtering

---

## 🔐 Database-schema (Firestore)

### Collection: `users`
```json
{
  "uid": "string",
  "name": "string",
  "email": "string",
  "role": "admin|user",
  "createdAt": "timestamp",
  "preferences": {
    "theme": "dark|light",
    "notifications": "boolean"
  }
}
```

### Collection: `films`
```json
{
  "filmId": "string",
  "title": "string",
  "year": "number",
  "genre": ["string"],
  "rating": "number",
  "description": "string",
  "poster": "url",
  "platforms": ["netflix", "disney+", "hbo+", ...]
}
```

### Collection: `watchlists`
```json
{
  "userId": "string",
  "films": ["filmId1", "filmId2", ...],
  "createdAt": "timestamp"
}
```

---

## 🔒 Sikkerhed

### Firestore Rules (`firestore.rules`)

```firebase
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Kun autentificerede brugere kan læse egne data
    match /users/{userId} {
      allow read, write: if request.auth.uid == userId;
    }
    
    // Film er offentligt læsbar
    match /films/{filmId} {
      allow read: if true;
      allow write: if request.auth.token.admin == true;
    }
  }
}
```

### Bedste praksis
- ✅ Hashed adgangskoder (Firebase Authentication håndterer dette)
- ✅ HTTPS for al datakommunikation
- ✅ CORS headers for API-sikkerhed
- ✅ Cookie-consent overholdelse (GDPR)

---

## 🎯 Konfiguration

### `Data.json` - Sitemetadata
```json
{
  "siteName": "FindDinFilm",
  "theme": "dark",
  "version": 1,
  "users": [
    { "name": "Christian", "role": "admin" }
  ]
}
```

### `firebase.json` - Firebase-konfiguration
```json
{
  "firestore": {
    "rules": "firestore.rules"
  }
}
```

---

## 🔄 Workflows

### Bruger-workflow (Login/Registrering)
```
frontpage.html
    ↓
login.html (eksisterende bruger)
    ↓
Firebase Auth
    ↓
profilepage.html (profil + watchlist)
```

### Film-søgnings-workflow
```
frontpage.html (søgbar)
    ↓
Søgning sendes til JavaScript-funktion
    ↓
Firestore query ('films' collection)
    ↓
Resultater vises i grid
```

---

## 📱 Responsive Design

### Breakpoints
- **Desktop (> 900px):** Full 3-kolonne layout
- **Tablet (600-900px):** 2-kolonne grid
- **Mobil (< 600px):** 1-kolonne stakkede elementer, mobil menu

### Mobile-menu
```javascript
.menu-toggle {
  display: block; // Kun på mobil
}

nav ul.active {
  display: flex; // Vises når toggle klikkes
}
```

---

## 🚀 Deployment

### Hosting
- **Firebase Hosting** (anbefalet)
- **GitHub Pages** (statisk)
- **Netlify** (kontinuert deployment)

### Deploy steps (Firebase)
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

---

## 🔧 Vedligeholdelse

### Filer der kræver opdatering
| Fil | Årsag | Hyppighed |
|-----|-------|-----------|
| `Data.json` | Brugerkonfiguration | Ved behov |
| `firestore.rules` | Sikkerhedsopdateringer | Efter ændringer i schema |
| `style.css` | Designopdateringer | Løbende |
| HTML-filer | Indhold & layout | Løbende |

### Browser-kompatibilitet
- ✅ Chrome/Chromium (seneste 2 versioner)
- ✅ Firefox (seneste 2 versioner)
- ✅ Safari (seneste 2 versioner)
- ✅ Edge (seneste 2 versioner)

---

## 📚 Dependencies

| Teknologi | Formål | Version |
|-----------|--------|---------|
| Firebase | Backend & Auth | (Latest) |
| Firestore | Database | Integreret i Firebase |
| HTML5 | Markup | Native |
| CSS3 | Styling | Native |
| JavaScript (ES6+) | Interaktivitet | Native |

---

## 🐛 Debugging

### Console logging
Åbn DevTools (F12) → Console for fejlmeldinger

### Firestore-fejlfinding
```javascript
db.collection('films').get().then(snapshot => {
  console.log(snapshot.docs);
});
```

### CSS-debugging
- Inspector Tool (F12) → Elements tab
- Network tab for at tjekke stylesheet-indlæsning

---

## 📞 Support & Kontakt

**Projektansvarlig:** Christian (Admin)  
**Repository:** `M6-Design-af-it-baserede-systemer---F26`  
**Seneste opdatering:** 2026-05-29

---

## 📜 Licens & Vilkår

Denne dokumentation gælder for FindDinFilm-projektet under M6-kurset (AAU).

