# SKILL.md — Structured AI Development Workflow

> Este archivo define el proceso de desarrollo que Claude debe seguir
> ESTRICTAMENTE en todos los proyectos. Léelo siempre antes de empezar.

---

## PASO 1 — ANÁLISIS CONCEPTUAL ✅ COMPLETADO

Antes de escribir ningún código:

- Analizar la descripción completa del proyecto
- Identificar los objetivos principales
- Identificar los posibles desafíos técnicos
- Proponer una arquitectura de alto nivel
- Explicar el razonamiento con claridad

**Resultado:** PWA 100% frontend, IndexedDB, coste cero, mobile-first.

---

## PASO 2 — PREGUNTAS DE ACLARACIÓN ✅ COMPLETADO

Preguntas resueltas:

- **Plataforma**: Móvil principal, compatible tablet/ordenador
- **Coste**: Cero absoluto — solo tecnologías gratuitas
- **Hosting**: GitHub Pages (https://flochamonche.github.io/ENGPRO/)
- **Almacenamiento**: IndexedDB local + export/import JSON manual
- **Estilo visual**: Azules suaves (día), tema oscuro (noche)
- **Backend**: No — todo en JS vanilla en el navegador
- **Sincronización**: Manual vía export/import JSON (OneDrive, USB, etc.)
- **Privacidad**: Datos 100% locales en el dispositivo

---

## PASO 3 — MOCKUP DE INTERFAZ DE USUARIO ✅ COMPLETADO

Mockup visual interactivo entregado en `mockup.html`:

- Pantalla de documentos (3 modos de entrada)
- Pantalla de revisión de vocabulario
- Pantalla del diccionario con búsqueda y filtros
- Pantalla del módulo de aprendizaje (4 modos + filtro por temas)
- Pantalla de ajustes (tema, backup, configuración)
- Navegación inferior con 4 secciones

**Aprobado por el usuario antes de implementar.**

---

## PASO 4 — IMPLEMENTACIÓN DE LA APLICACIÓN ✅ COMPLETADO

App implementada en archivo único `index.html` con:

- 3 modos de entrada: archivo (PDF/DOCX/TXT), pegar texto, foto/OCR
- Parser inteligente para bases de datos estructuradas
- Detección automática de listas vs texto continuo
- Traducción automática (MyMemory API) + significados (Dictionary API)
- Diccionario con búsqueda, filtros, aciertos/fallos, edición, eliminación
- 4 modos de aprendizaje con SM-2 y filtro por temas
- 96 términos precargados en 7 categorías
- Export/import JSON con fusión inteligente
- Tema día/noche persistente
- PWA instalable en móvil

**Desplegado en:** https://flochamonche.github.io/ENGPRO/

---

## PASO 5 — ITERACIÓN Y MEJORAS (ACTIVO)

Workflow para nuevas funcionalidades:

1. El usuario propone una mejora o reporta un problema
2. Claude analiza el impacto y propone solución
3. Implementar el cambio mínimo necesario
4. Probar antes de hacer push
5. Commit + push a GitHub (auto-deploy en Pages)

**Reglas para iteraciones:**
- No romper funcionalidad existente
- Paso a paso: una mejora por ciclo
- Preguntar ante la duda
- Mantener todo en un solo archivo HTML
- Push solo cuando el usuario confirme
