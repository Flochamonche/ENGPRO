# CLAUDE.md — Eng-Pro Vocabulary App

## Descripción del proyecto
PWA (Progressive Web App) para construir y gestionar vocabulario profesional inglés–español, con módulo de aprendizaje adaptativo y repetición espaciada. 100% frontend, coste cero.

## Estado actual: v1.0 FUNCIONAL
La app está implementada y operativa en un único archivo `index.html`.

## Stack tecnológico (DEFINITIVO)
- **Frontend**: HTML5, CSS3, JavaScript vanilla — archivo único (`index.html`)
- **Almacenamiento**: IndexedDB (local, persistente, offline)
- **NLP**: Extracción de vocabulario en JS (sin backend Python)
- **Librerías externas** (CDN, gratuitas):
  - pdf.js — extracción de texto de PDF
  - mammoth.js — extracción de texto de DOCX
  - Tesseract.js — OCR para fotos/imágenes
- **APIs gratuitas** (sin clave):
  - MyMemory API — traducción automática EN→ES
  - Free Dictionary API — significados en inglés
- **PWA**: manifest.json + sw.js (instalable en móvil, offline)
- **Hosting**: GitHub Pages (gratuito)
- **Coste**: CERO

## Arquitectura
```
[3 modos de entrada]
  ├── Archivo (PDF/DOCX/TXT)
  ├── Pegar texto (copiar/pegar)
  └── Foto/OCR (cámara o galería)
        ↓
[Detección automática de formato]
  ├── Base datos estructurada (===) → Parser directo con categorías
  └── Texto libre → Extracción NLP (frecuencia, bigramas, trigramas)
        ↓
[Traducción y significado automáticos] (MyMemory + Dictionary API)
        ↓
[Revisión por usuario] (aceptar/rechazar/editar + aceptar todos)
        ↓
[IndexedDB] → vocabulary, learning, documents, config
        ↓
[Módulo de aprendizaje] (SM-2, 4 modos, filtro por temas)
        ↓
[Exportar/Importar JSON] (backup prioritario)
```

## Estructura de archivos
```
Engpro/
├── index.html        ← App completa (HTML + CSS + JS embebidos)
├── manifest.json     ← Configuración PWA
├── sw.js             ← Service Worker (cache offline)
├── mockup.html       ← Mockup visual de referencia
├── Data Base.txt     ← Base de datos inicial (96 términos)
├── CLAUDE.md         ← Este archivo
├── SKILL.md          ← Workflow de desarrollo
├── Eng-Pro .docx     ← Spec original
└── Skills.docx       ← Skills original
```

## Módulos implementados

### 1. Ingesta de documentos — 3 modos
- **Archivo**: PDF (pdf.js), DOCX (mammoth.js), TXT
- **Pegar texto**: área de texto para copiar/pegar contenido
- **Foto/OCR**: cámara o galería → Tesseract.js extrae texto
- Detección automática de base de datos estructurada vs texto libre
- Deduplicación: no repite términos ya existentes ni subconjuntos

### 2. Extracción y ranking de vocabulario
- Análisis de frecuencia, filtrado de stopwords y palabras básicas
- Detección de bigramas/trigramas (expresiones multipalabra)
- Puntuación por sufijos profesionales (-tion, -ment, -ness, etc.)
- Eliminación de duplicados y subconjuntos entre candidatos
- Parser especial para bases de datos con formato estructurado (secciones ===)

### 3. Traducción automática
- MyMemory API: traducción EN→ES gratuita
- Free Dictionary API: significado/definición en inglés
- Se buscan automáticamente al extraer candidatos
- Los que ya traen traducción (del parser) solo buscan significado
- Campos editables por el usuario antes de guardar

### 4. Revisión guiada
- Tarjetas con: término, contexto, traducción, significado, categoría
- Botones: aceptar / rechazar por término
- Botones: aceptar todos / rechazar todos (para bases de datos)
- Categoría auto-asignada desde el parser, editable
- Barra de progreso de revisión

### 5. Diccionario
- Búsqueda por texto (inglés o español)
- Filtros por categoría (chips dinámicos)
- Detalle/edición de cada término (modal)
- Eliminar términos individuales
- Indicador de dificultad (fácil/media/difícil)

### 6. Aprendizaje adaptativo
**4 modos:**
- Opción múltiple (EN → ES)
- Escribir respuesta
- Completar frase en contexto
- Reverso (ES → EN)

**Características:**
- Algoritmo SM-2 (repetición espaciada)
- Filtro por temas: selección múltiple o todos
- Racha y contador de sesión
- Barra de progreso
- Comparación flexible (Levenshtein) en modo escritura
- Solo usa términos con traducción en modos que la requieren

### 7. Datos y backup (PRIORIDAD MÁXIMA)
- Exportar: descarga JSON completo (vocabulario + progreso + documentos)
- Importar: fusión inteligente sin duplicados, con versionado
- Aviso visual si llevas días sin exportar
- Formato JSON legible y portable (OneDrive, USB, email...)

### 8. Temas visuales
- Modo día: azules suaves sobre fondo claro (#F0F4F8)
- Modo noche: azules sobre fondo oscuro (#0F172A)
- Toggle persistente (se guarda en IndexedDB)

### 9. Base de datos precargada
- 96 términos incluidos de fábrica (primer uso)
- 7 categorías: Technical Engineering, Corporate & Management, Connectors, Phrase Bank (3 sub), Presentations (3 sub), Director-Level, Fillers
- Se cargan automáticamente solo la primera vez

## Esquema IndexedDB
```
vocabulary: { id, term_en, term_es, meaning, example_sentences, source_document, category, date_added, difficulty_score }
learning:   { vocab_id, last_reviewed, next_review, ease_factor, interval_days, correct_count, incorrect_count }
documents:  { id, filename, upload_date, word_count, terms_extracted }
config:     { key, value }
```

## Instrucciones para Claude
- **Leer siempre SKILL.md antes de escribir código nuevo**
- Mantener todo en un único archivo HTML (index.html)
- Comentarios del código en **español**
- Mobile-first, responsive
- Coste CERO: solo APIs y librerías gratuitas
- La base de datos del usuario es PRIORITARIA: nunca perder datos
- Funciones pequeñas, claras y bien nombradas
- Ante la duda, preguntar antes de asumir

## Restricciones clave
- Sin frameworks (React, Vue, Angular)
- Sin costes recurrentes
- Sin servicios externos de pago
- Funcionar offline en la medida de lo posible
- Datos locales (IndexedDB), exportación manual para sincronizar

## Preferencias del usuario
- Uso principal desde **móvil**, pero compatible con tablet/ordenador
- Tema día con **azules suaves**, tema noche disponible
- La base de datos acumulada es **oro** — protección máxima
- Prefiere ir **paso a paso**: implementar, probar, iterar
- Comunicación en **español**
- Los archivos .docx contienen la info original, no es necesario revisarlos

## Historial de problemas resueltos
- **Cache del navegador**: el usuario abría el archivo desde otra carpeta (ENGApp vs Engpro)
- **Quiz mostraba opciones en inglés**: corregido filtrando solo términos con traducción
- **Términos duplicados en extracción**: añadido filtro de subconjuntos y deduplicación contra DB
- **Scripts bloqueantes**: movidos a carga `defer` para no bloquear renderizado
- **file:// protocol**: CORS bloquea manifest.json y Service Worker en local (normal, funciona al hostear)
