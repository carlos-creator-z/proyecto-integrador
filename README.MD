# Portal Dimensional — Rick & Morty

Galería interactiva y responsiva de personajes de *Rick and Morty*. Construida con HTML5 semántico, CSS3 moderno y Vanilla JavaScript.

**API:** https://rickandmortyapi.com/api/character

---

## 🎯 Características principales

- **Galería responsiva** con grid adaptable (mobile-first).
- **Tema claro/oscuro** persistente en `localStorage` (clave: `'rm-theme'`).
- **Panel de detalle** interactivo al hacer click en una tarjeta.
- **Paginación** con botón "Cargar más".
- **Título clonado sobre Rick** — el encabezado aparece encima de su tarjeta.
- **Navegación por teclado** — Tab, Enter y Escape.
- **Accesibilidad** — ARIA labels, semantic HTML, lectores de pantalla.

---

## 📁 Estructura

```
proyecto integrador/
├── index.html    # HTML5 semántico
├── styles.css    # CSS3 responsivo con variables
├── index.js      # Lógica (Vanilla JS)
└── README.MD     # Esta documentación
```

---

## 🚀 Cómo usar

### Abrir directamente

1. Abre la carpeta `proyecto integrador`.
2. Haz doble click en `index.html` o arrastra al navegador.

### Con servidor local (recomendado)

**Python 3:**
```powershell
python -m http.server 8000
# Abre http://localhost:8000
```

**Node.js:**
```powershell
npm install -g http-server
http-server
```

---

## 🛠️ Tecnología

### HTML (`index.html`)

**Estructura semántica:**
- `<header>` — Logo, switch de tema, botón "Cargar más".
- `<main>` → `<section class="results-section">` — Contenedor principal.
- `<aside id="detail-panel">` — Panel de detalle (oculto por defecto).
- `<ul id="cards">` — Lista de tarjetas (generadas por JS).
- `<footer>` — Créditos.

**Elementos clave:**
| ID/Clase | Propósito |
|----------|-----------|
| `#theme-toggle` | Checkbox para tema claro/oscuro |
| `#theme-label` | Botón visible del tema |
| `#load-more` | Botón "Cargar más" |
| `#detail-panel` | Panel de detalle (hidden) |
| `#cards` | Contenedor de tarjetas |
| `.card` | Tarjeta individual |

### CSS (`styles.css`)

**Variables principales:**
```css
:root {
  --bg: #f6f9f3;           /* Fondo claro */
  --text: #0b2a0b;         /* Texto oscuro */
  --accent: #3be54a;       /* Verde neón */
  --accent-2: #7cc4ff;     /* Cyan */
  --transition: 300ms cubic-bezier(0.2, 0.8, 0.2, 1);
}

body.dark {
  --bg: #000000;           /* Negro puro */
  --text: #e6ffee;         /* Verde muy claro */
  --accent: #6dfc8b;       /* Verde más brillante */
}
```

**Grid de tarjetas:**
```css
.cards {
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  /* Se ajusta automáticamente: 2-4 columnas según ancho */
}
```

**Breakpoints:**
| Ancho | Columnas |
|-------|----------|
| < 641px | 2–3 |
| 641–900px | 3 |
| > 1025px | 4 |

### JavaScript (`index.js`)

**Constantes:**
```javascript
const API_BASE = 'https://rickandmortyapi.com/api/character';
const OWN_URL = 'https://rickandmorti.com/api/personajes';
const THEME_KEY = 'rm-theme';
```

**Funciones principales:**

| Función | Propósito |
|---------|-----------|
| `init()` | Inicializa todo (tema, primer fetch, listeners) |
| `initTheme()` | Lee tema de localStorage y lo aplica |
| `applyTheme(theme)` | Cambia tema y persiste en localStorage |
| `fetchCharacters()` | Obtiene personajes de la API |
| `renderCharacters(list)` | Renderiza tarjetas en el DOM |
| `createCard(character)` | Crea una tarjeta individual |
| `placeTitleAboveRick()` | Clona el título encima de la tarjeta de Rick |
| `showDetail(data)` | Muestra el panel de detalle |
| `hideDetail()` | Oculta el panel de detalle |

**Flujo principal:**
1. `DOMContentLoaded` → `init()`.
2. `initTheme()` — lee y aplica preferencia guardada.
3. `fetchCharacters()` — obtiene primera página.
4. Usuario interactúa:
   - Click tarjeta → `showDetail()`.
   - Click "Cargar más" → `fetchCharacters()` (siguiente página).
   - Toggle tema → `applyTheme()` + `localStorage.setItem()`.

---

## Requisitos

- **Navegador moderno** compatible con:
  - ES6+ (clases, arrow functions, async/await)
  - Fetch API
  - CSS Grid y Flexbox
  - CSS Custom Properties (variables)
  - localStorage
  - Clipboard API (para copiar URL)

- **Conexión a Internet** para consumir la API pública de Rick and Morty.

---

## Instalación y uso

### Opción 1: Abrir directamente el archivo (más simple)

1. Navega a la carpeta `proyecto integrador` en tu computadora.
2. Haz doble click en `index.html` o arrastra el archivo al navegador.

### Opción 2: Desde PowerShell (Windows)

```powershell
# En la carpeta del proyecto
start .\index.html
```

### Opción 3: Servir localmente (recomendado para desarrollo)

Si tienes Python instalado:

```powershell
# Python 3
python -m http.server 8000

# Luego abre http://localhost:8000 en el navegador
```

Si tienes Node.js:

```powershell
# Instala un servidor simple
npm install -g http-server

# En la carpeta del proyecto
http-server
```

---

## Documentación técnica

### HTML5 semántico

**Archivo:** `index.html`

#### Estructura general

```html
<body>
  <header class="site-header">
    <!-- Logo/marca y controles -->
  </header>
  <main class="container main-content">
    <section class="results-section">
      <!-- Panel de detalle y tarjetas -->
    </section>
  </main>
  <footer class="site-footer">
    <!-- Créditos -->
  </footer>
</body>
```

#### Componentes principales

| Elemento | ID/Clase | Descripción |
|----------|----------|-------------|
| `<header>` | `.site-header` | Contiene logo, switch de tema y botón "Cargar más". |
| `<h1>` | `.logo`, `.logo-series` | Título principal con sub-título. Estructura: `<span class="logo-sub">` y `<span class="logo-main">`. |
| `<nav>` | `.controls` | Navegación con controles: interruptor de tema y botones. |
| `<input>` | `#theme-toggle` | Switch checkbox para tema claro/oscuro (invisible, estilizado con CSS). |
| `<button>` | `#theme-label` | Botón visible que muestra el modo actual ("Modo Claro"/"Modo Oscuro"). |
| `<button>` | `#load-more` | Botón para cargar más personajes (paginación). |
| `<aside>` | `#detail-panel` | Panel de detalle del personaje seleccionado (oculto por defecto, `hidden`). |
| `<figure>` | `.detail-figure` | Contenedor para imagen ampliada del personaje en el panel. |
| `<ul>` | `#cards` | Lista no ordenada que contiene las tarjetas de personajes. |
| `<li>` | (generado por JS) | Elemento de lista que envuelve cada tarjeta. |
| `<article>` | `.card` | Tarjeta de personaje con imagen y nombre. |
| `<figure>` | Dentro de `.card` | Contenedor de imagen con `<figcaption>` para accesibilidad. |

#### Atributos de accesibilidad

- `aria-label`: Describe elementos interactivos (switch, botones).
- `aria-live="polite"`: Anuncia cambios en el área de estado (#status) a lectores de pantalla.
- `aria-pressed`: Indica el estado del botón de tema.
- `role="status"`: Marca el área de estado como una región activa.
- `tabindex="0"`: Hace que las tarjetas sean focuseables por teclado.

---

### CSS3 y variables

**Archivo:** `styles.css`

#### Organización de secciones

El archivo está organizado en 10 secciones numeradas:

1. **Variables y temas** — Definición de colores y transiciones.
2. **Estilos base** — Reset, tipografía, decoración del portal.
3. **Header y navegación** — Estilos del encabezado y logo.
4. **Botones** — Estados de botones (normal, hover, active).
5. **Interruptor de tema** — Estilos del switch y animaciones.
6. **Contenido principal** — Layout del área de resultados.
7. **Tarjetas** — Grid y estilos de cada tarjeta.
8. **Panel de detalle** — Estilos del panel lateral derecho.
9. **Utilidades** — Clases auxiliares (sr-only, btn-ghost).
10. **Media queries** — Estilos responsivos para diferentes breakpoints.

#### Variables CSS principales

```css
:root {
  /* Tema claro */
  --bg: #f6f9f3;              /* Fondo principal */
  --panel: #ffffff;            /* Fondo de paneles */
  --text: #0b2a0b;             /* Texto principal */
  --muted: #6b6b6b;            /* Texto secundario */
  --accent: #3be54a;           /* Color de acento (verde) */
  --accent-2: #7cc4ff;         /* Segundo acento (cyan) */
  --card-shadow: 0 6px 18px rgba(0, 0, 0, 0.08);
  --transition: 300ms cubic-bezier(0.2, 0.8, 0.2, 1);
}

body.dark {
  /* Tema oscuro */
  --bg: #000000;               /* Negro puro */
  --panel: #000000;
  --text: #e6ffee;             /* Verde muy claro */
  --muted: #9aa3a3;
  --accent: #6dfc8b;           /* Verde neón más brillante */
  --card-shadow: 0 10px 30px rgba(0, 0, 0, 0.7);
}
```

#### Grid de tarjetas

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 14px;
  /* Ajusta el número de columnas según el ancho disponible */
}
```

**Breakpoints responsivos:**

| Ancho | Columnas | Descripción |
|-------|----------|-------------|
| < 641px | 2–3 (automático) | Mobile-first |
| 641px–899px | 3 | Tablet |
| 900px–1024px | 3–4 (lado a lado con panel) | Layout hybrid |
| ≥ 1025px | 4 | Desktop completo |

#### Decoración visual

- **Portal circular:** Fondo decorativo con gradiente radial (`body::before`) que crea una atmósfera dimensional.
- **Sombras suaves:** Proporcionales al tema (más suaves en claro, más dramáticas en oscuro).
- **Transiciones:** Todas usan `--transition` para consistencia.

#### Clase especial: `.site-title-clone`

Estilos para el título clonado que aparece encima de la tarjeta de Rick:

```css
.site-title-clone {
  text-align: center;
  margin-bottom: 8px;
}
.site-title-clone .logo-main { font-size: 1.15rem; }
.site-title-clone .logo-sub { font-size: 0.85rem; }
.site-title-clone .logo-dot { display: none; }
```

---

### JavaScript y lógica

**Archivo:** `index.js`

#### Constantes globales

```javascript
const API_BASE = 'https://rickandmortyapi.com/api/character';
const OWN_URL = 'https://rickandmorti.com/api/personajes';
const THEME_KEY = 'rm-theme';
```

#### Selección de elementos DOM

Se cachean todos los elementos interactivos al inicio para mejorar rendimiento:

```javascript
const cardsEl = document.getElementById('cards');
const statusEl = document.getElementById('status');
const loadMoreBtn = document.getElementById('load-more');
const themeToggle = document.getElementById('theme-toggle');
const themeLabel = document.getElementById('theme-label');
const detailPanel = document.getElementById('detail-panel');
// ... más elementos
```

#### Funciones principales

##### 1. **applyTheme(theme)**

Aplica el tema seleccionado al documento y lo persiste en `localStorage`.

```javascript
function applyTheme(theme){
  if(theme === 'dark'){
    document.body.classList.add('dark');
    themeToggle.checked = true;
    themeLabel.textContent = 'Modo Oscuro';
    localStorage.setItem(THEME_KEY,'dark');
  } else {
    document.body.classList.remove('dark');
    themeToggle.checked = false;
    themeLabel.textContent = 'Modo Claro';
    localStorage.setItem(THEME_KEY,'light');
  }
}
```

**Parámetro:**
- `theme`: `'dark'` o `'light'`

**Efectos secundarios:**
- Cambia clase en `<body>`.
- Actualiza el estado del checkbox.
- Modifica el texto del botón.
- Guarda preferencia en `localStorage`.

##### 2. **initTheme()**

Lee la preferencia guardada en `localStorage` y la aplica. Añade listeners para cambios de tema.

```javascript
function initTheme(){
  const saved = localStorage.getItem(THEME_KEY);
  if(saved === 'dark') applyTheme('dark');
  else applyTheme('light');
  
  themeToggle.addEventListener('change', ()=>{
    applyTheme(themeToggle.checked ? 'dark' : 'light');
  });
  
  themeLabel.addEventListener('click', ()=>{
    const newTheme = document.body.classList.contains('dark') ? 'light' : 'dark';
    applyTheme(newTheme);
  });
}
```

**Flujo:**
1. Lee valor de `localStorage['rm-theme']`.
2. Si es `'dark'`, aplica tema oscuro; si no, aplica claro.
3. Asigna listeners al switch y botón.

##### 3. **setStatus(text)**

Actualiza el mensaje de estado visible para el usuario.

```javascript
function setStatus(text){
  statusEl.textContent = text || '';
}
```

**Casos de uso:**
- "Cargando personajes..."
- "Error al obtener datos..."
- "URL copiada al portapapeles"

##### 4. **createCard(character)**

Crea un elemento tarjeta a partir de los datos de un personaje.

```javascript
function createCard(character){
  const li = document.createElement('li');
  const article = document.createElement('article');
  article.className = 'card';
  
  // Almacenar datos del personaje en data-attributes
  article.dataset.name = character.name || '';
  article.dataset.image = character.image || '';
  article.dataset.status = character.status || '';
  article.dataset.species = character.species || '';
  article.dataset.gender = character.gender || '';
  article.dataset.origin = character.origin?.name || '';
  article.dataset.location = character.location?.name || '';
  article.dataset.episodes = (character.episode && character.episode.length) || 0;
  
  article.innerHTML = `
    <figure>
      <img src="${character.image}" alt="Imagen de ${character.name}" loading="lazy">
      <figcaption class="sr-only">Foto de ${character.name}</figcaption>
    </figure>
    <div class="card-body">
      <h3>${character.name}</h3>
    </div>
  `;
  
  article.tabIndex = 0;  // Focusable por teclado
  li.appendChild(article);
  return li;
}
```

**Entrada:**
- `character`: Objeto con propiedades de la API (name, image, status, etc.).

**Salida:**
- Elemento `<li>` con estructura completa de la tarjeta.

**Detalles técnicos:**
- Usa `data-*` attributes para almacenar información sin mostrarla en el DOM.
- `loading="lazy"` para optimizar carga de imágenes.
- `tabIndex = 0` hace la tarjeta navegable por teclado.

##### 5. **renderCharacters(list)**

Renderiza múltiples tarjetas de una vez usando `DocumentFragment` (más eficiente que appendChild múltiples).

```javascript
function renderCharacters(list){
  const fragment = document.createDocumentFragment();
  list.forEach(ch => fragment.appendChild(createCard(ch)));
  cardsEl.appendChild(fragment);
  placeTitleAboveRick();
}
```

**Optimización:** `DocumentFragment` no dispara reflows para cada elemento.

**Efecto adicional:** Llama a `placeTitleAboveRick()` después de renderizar.

##### 6. **placeTitleAboveRick()**

Busca la tarjeta de Rick y coloca una copia del título/subtítulo encima de su figura.

```javascript
function placeTitleAboveRick(){
  const headerTitle = document.querySelector('.logo-series');
  const headerTag = document.querySelector('.tag');
  if(!headerTitle || !headerTag) return;
  
  const articles = Array.from(cardsEl.querySelectorAll('article'));
  const rickArticle = articles.find(a => 
    a.dataset.name && a.dataset.name.toLowerCase().includes('rick')
  );
  if(!rickArticle) return;
  
  if(rickArticle.querySelector('.site-title-clone')) return;  // Evitar duplicados
  
  const wrapper = document.createElement('div');
  wrapper.className = 'site-title-clone';
  
  const titleClone = headerTitle.cloneNode(true);
  const tagClone = headerTag.cloneNode(true);
  
  titleClone.removeAttribute('id');
  tagClone.removeAttribute('id');
  
  wrapper.appendChild(titleClone);
  wrapper.appendChild(tagClone);
  
  const figure = rickArticle.querySelector('figure');
  if(figure) rickArticle.insertBefore(wrapper, figure);
}
```

**Lógica:**
1. Obtiene referencias al título original en el header.
2. Busca entre todas las tarjetas la que tenga "rick" en el nombre.
3. Si no existe, sale.
4. Si ya está clonado, no hace nada (evita duplicados).
5. Clona el título y lo inserta antes de la figura en la tarjeta de Rick.

##### 7. **async fetchCharacters()**

Realiza la petición HTTP a la API, maneja errores y paginación.

```javascript
async function fetchCharacters(){
  if(!nextUrl){
    setStatus('No hay más personajes para cargar.');
    loadMoreBtn.disabled = true;
    return;
  }
  
  try{
    setStatus('Cargando personajes...');
    loadMoreBtn.disabled = true;
    
    const res = await fetch(nextUrl);
    if(!res.ok) throw new Error(`HTTP ${res.status}`);
    const data = await res.json();
    
    if(Array.isArray(data.results)){
      renderCharacters(data.results);
    }
    
    nextUrl = data.info?.next || null;
    if(!nextUrl) loadMoreBtn.style.display = 'none';
    else loadMoreBtn.style.display = '';
    
    setStatus('');
  }catch(err){
    console.error('Error fetching characters:', err);
    setStatus('Error al obtener datos. Revisa la consola.');
  }finally{
    loadMoreBtn.disabled = false;
  }
}
```

**Manejo de errores:**
- `fetch()` rechaza si hay problema de red.
- `res.ok` valida que HTTP status sea 2xx.
- `try/catch/finally` asegura que el botón se re-habilite siempre.

**Paginación:**
- La API devuelve `data.info.next` (URL de la siguiente página) o `null` si no hay más.
- Se guarda en `nextUrl` para el próximo click del usuario.

##### 8. **showDetail(data)** y **showDetailFromArticle(article)**

Rellena y muestra el panel de detalle.

```javascript
function showDetailFromArticle(article){
  if(!article) return;
  const d = article.dataset;
  showDetail({
    name: d.name,
    image: d.image,
    status: d.status,
    species: d.species,
    gender: d.gender,
    origin: d.origin,
    location: d.location,
    episodes: d.episodes
  });
}

function showDetail(data){
  if(!detailPanel) return;
  detailImage.src = data.image || '';
  detailImage.alt = data.name || 'Imagen';
  detailName.textContent = data.name || '';
  detailDesc.textContent = `${data.name} es ${data.species || 'una entidad'}${data.gender ? ' de género ' + data.gender : ''}.`;
  detailStatus.textContent = data.status || '';
  detailSpecies.textContent = data.species || '';
  detailGender.textContent = data.gender || '';
  detailOrigin.textContent = data.origin || '';
  detailLocation.textContent = data.location || '';
  detailEpisodes.textContent = data.episodes || '0';
  detailPanel.hidden = false;
  detailPanel.focus();
}
```

**Descripción generada:** Como la API no incluye descripción libre, se genera una frase con los datos disponibles.

##### 9. **init()**

Función de inicialización que se ejecuta cuando el DOM está listo.

```javascript
function init(){
  initTheme();
  fetchCharacters();
  
  // Cambiar pathname (seguro)
  try{ history.replaceState({}, '', '/api/personajes'); }catch(e){ /* ignore */ }
  
  // Mostrar URL propia
  if(statusEl){ 
    const prev = statusEl.textContent; 
    statusEl.textContent = `URL propia: ${OWN_URL}`; 
    setTimeout(()=> statusEl.textContent = prev, 2000); 
  }
  
  // Copiar URL al portapapeles
  if(copyUrlBtn && ownUrlEl){
    copyUrlBtn.addEventListener('click', async ()=>{
      const text = ownUrlEl.href || OWN_URL;
      try{ 
        await navigator.clipboard.writeText(text); 
        setStatus('URL copiada al portapapeles'); 
        setTimeout(()=> setStatus(''), 1600); 
      }catch(e){ 
        setStatus('No se pudo copiar la URL'); 
      }
    });
  }
  
  // Listeners globales
  loadMoreBtn.addEventListener('click', ()=> fetchCharacters());
  cardsEl.addEventListener('click', (e)=>{
    const article = e.target.closest('article');
    if(!article) return;
    showDetailFromArticle(article);
  });
  cardsEl.addEventListener('keydown', (e)=>{
    if(e.key === 'Enter'){
      const article = e.target.closest('article');
      if(article) showDetailFromArticle(article);
    }
  });
  
  if(detailClose) detailClose.addEventListener('click', hideDetail);
  document.addEventListener('keydown', (e)=>{
    if(e.key === 'Escape') hideDetail();
  });
}
```

**Orden de ejecución:**
1. Inicializa tema desde `localStorage`.
2. Carga la primera página de personajes.
3. Intenta cambiar el pathname (sin cambiar origen).
4. Muestra URL propia brevemente.
5. Asigna todos los listeners de interacción.

---

## Almacenamiento persistente

### localStorage

**Clave:** `'rm-theme'`

**Valores posibles:** `'dark'` | `'light'`

**Uso:**
```javascript
// Guardar
localStorage.setItem('rm-theme', 'dark');

// Leer
const theme = localStorage.getItem('rm-theme');
```

**Comportamiento:**
- Se guarda cada vez que el usuario cambia de tema.
- Se lee al cargar la página en `initTheme()`.
- Persiste en el navegador incluso después de cerrar pestañas/sesiones.
- Específico por origen (protocolo + dominio + puerto).

---

## Accesibilidad y SEO

### Atributos ARIA

| Atributo | Elemento | Propósito |
|----------|----------|-----------|
| `aria-label` | Inputs, botones | Describe la función al lector de pantalla |
| `aria-live="polite"` | `#status` | Anuncia cambios de estado sin interrumpir |
| `aria-pressed` | `#theme-label` | Indica estado on/off del botón |
| `role="status"` | `#status` | Marca como región de estado |
| `role="region"` | `#detail-panel` | Agrupa contenido relacionado |

### Navegación por teclado

| Tecla | Acción |
|-------|--------|
| Tab | Navega entre elementos focusables |
| Enter (en tarjeta) | Abre panel de detalle |
| Escape (con detalle abierto) | Cierra panel de detalle |

### SEO básico

- `<meta name="description">` en el `<head>`.
- Encabezados semánticos (`<h1>`, `<h2>`, `<h3>`).
- Elementos semánticos (`<header>`, `<main>`, `<footer>`, `<article>`, `<figure>`).
- Atributos `alt` en imágenes.
- Estructura lógica del contenido.

---

## Responsividad

### Enfoque mobile-first

El CSS comienza con estilos para dispositivos móviles y se expande con media queries.

### Breakpoints

| Punto de quiebre | Ancho | Cambios |
|------------------|-------|---------|
| Mobile | < 641px | 2–3 columnas (automático), stack vertical |
| Tablet | 641px–899px | 3 columnas de tarjetas |
| Hybrid | 900px–1024px | Panel detalle + tarjetas lado a lado |
| Desktop | ≥ 1025px | 4 columnas, layout optimizado |

### Grid automático

```css
grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
```

Esta técnica permite que el navegador ajuste automáticamente el número de columnas sin necesidad de media queries adicionales.

### Viewport meta tag

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Asegura que la página se escale correctamente en dispositivos móviles.

---

## Flujo de la aplicación

```
┌─────────────────┐
│  Cargar página  │
└────────┬────────┘
         │
         ▼
┌──────────────────────────────┐
│  DOMContentLoaded o document │
│      ready?                  │
└────────┬─────────────────────┘
         │
         ▼
┌──────────────────────────────┐
│  init()                      │
├──────────────────────────────┤
│ 1. initTheme()               │
│    (lee localStorage)        │
│ 2. fetchCharacters()         │
│    (primera página)          │
│ 3. Asignar listeners         │
└────────┬─────────────────────┘
         │
         ▼
┌──────────────────────────────┐
│  Renderizar tarjetas         │
│  + placeTitleAboveRick()     │
└────────┬─────────────────────┘
         │
         ├─────► Usuario click en tarjeta ──┐
         │                                   │
         │      showDetailFromArticle()     │
         │      showDetail()                │
         │      detailPanel.hidden = false  │
         │                                   │
         │                    ◄──────────────┘
         │
         ├─────► Usuario click "Cargar más" ──┐
         │                                      │
         │       fetchCharacters()              │
         │       renderCharacters()             │
         │       placeTitleAboveRick()          │
         │                                      │
         │                     ◄────────────────┘
         │
         ├─────► Usuario toggle tema ──┐
         │                              │
         │       applyTheme()           │
         │       localStorage.setItem() │
         │                              │
         │                   ◄──────────┘
         │
         └─→ Loop
```

---

## Mejoras futuras

### Funcionalidades propuestas

1. **Buscador en tiempo real**
   - Filtrar personajes por nombre.
   - Debounce de 300ms para optimizar búsqueda.

2. **Filtros avanzados**
   - Por estado (vivo, muerto, desconocido).
   - Por especie.
   - Por género.
   - Combinaciones de filtros.

3. **Caché offline**
   - Usar IndexedDB para almacenar personajes localmente.
   - Permitir navegación sin conexión.

4. **Ordenamiento**
   - Alfabético, por ID, etc.

5. **Compartir personaje**
   - Link a redes sociales.
   - QR con datos del personaje.

6. **Comentarios/Ratings**
   - Guardar puntuación del usuario en un personaje (localStorage).

### Mejoras técnicas

1. **Minificación y bundling**
   - Usar Webpack o Vite para optimizar assets.
   - Minificar CSS y JS.

2. **Lazy loading mejorado**
   - Usar Intersection Observer para cargar tarjetas bajo demanda.

3. **Tests automáticos**
   - Unit tests con Jest.
   - Tests E2E con Cypress.

4. **Validación con TypeScript**
   - Tipado estricto de datos y funciones.

5. **Progressive Web App (PWA)**
   - Service Worker para offline.
   - Manifest para instalación en home screen.

6. **Analítica**
   - Rastrear interacciones con Google Analytics.

---

## Notas de desarrollo

### Depuración

Para ver mensajes de error o flujo:

```javascript
// En consola del navegador (F12)
console.log(character);  // Ver estructura de datos
localStorage.getItem('rm-theme');  // Ver tema guardado
```

### Performance

- Las imágenes usan `loading="lazy"` para cargar bajo demanda.
- Se cachean referencias a elementos DOM para evitar múltiples querys.
- Se usa `DocumentFragment` para renderizado en batch.

### Compatibilidad

Testeado en:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

---

## Créditos

- **API:** [Rick and Morty API](https://rickandmortyapi.com/)
- **Serie original:** *Rick and Morty* (Adult Swim)
- **Diseño e implementación:** Proyecto educativo

---

**Última actualización:** Diciembre 2025

Para más información o contribuciones, abre un issue o PR en el repositorio.
