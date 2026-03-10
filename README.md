# El Arte de hacer Commits en GitHub

En el mundo profesional, el historial de Git es la bitácora del proyecto. Cuando nos unamos a trabajar en equipo, es vital que cualquier desarrollador entienda qué cambió en el código sin tener que leerlo línea por línea. 

Para lograr esto, en este equipo utilizaremos el estándar de la industria llamado **Conventional Commits**.

---

## 1. La Estructura Base

Todo commit debe seguir exactamente este formato:

> `<type>(<scope>): <subject>`
>
> `<body>`
>
> `<footer>`

*(Nota: El `scope`, `body` y `footer` son opcionales. El `type` y el `subject` son estrictamente obligatorios).*

---

## 2. Los Tipos de Commit (`<type>`)

### Los 10 Clásicos (Estándar de la Industria)
* **`feat`**: (Feature) Nueva funcionalidad aportada al sistema.
* **`fix`**: (Fix) Corrección de un error o bug.
* **`docs`**: (Documentation) Cambios exclusivos en la documentación (README, Swagger, Javadoc).
* **`style`**: (Style) Formato de código (espacios, comas faltantes) que no afecta la lógica.
* **`refactor`**: (Refactor) Reestructuración de código que no añade features ni arregla bugs.
* **`test`**: (Test) Añadir pruebas faltantes o modificar las existentes.
* **`chore`**: (Chore) Tareas de mantenimiento, como actualizar dependencias.
* **`perf`**: (Performance) Cambios que mejoran el rendimiento del sistema o consultas.
* **`build`**: (Build) Cambios que afectan el sistema de compilación (Maven, npm, Vite).
* **`ci`**: (Continuous Integration) Cambios en archivos de configuración de integración continua o despliegue.

### Código y Arquitectura
* **`revert`**: (Revert) Revertir un commit anterior que introdujo problemas.
* **`clean`**: (Clean) Eliminar código muerto, comentarios innecesarios o logs de consola.
* **`remove`** / **`rm`**: (Remove) Eliminar un archivo o una funcionalidad deprecada por completo.
* **`rename`**: (Rename) Renombrar variables, métodos o nombres de archivos para mayor claridad.
* **`move`**: (Move) Mover archivos de un directorio a otro (ej. mover utilitarios a `/utils`).
* **`types`**: (Types) Cambios específicos en las interfaces o tipos estáticos (TypeScript).
* **`mock`**: (Mock) Añadir datos falsos o simular respuestas para desarrollo local.
* **`wip`**: (Work In Progress) Trabajo en progreso (solo para ramas locales al pausar el trabajo).

### Frontend y UI
* **`ui`**: (User Interface) Cambios visuales o de diseño puro.
* **`asset`**: (Asset) Añadir o actualizar recursos estáticos (imágenes, fuentes, iconos, logos).
* **`a11y`**: (Accessibility) Mejoras de accesibilidad web.
* **`i18n`**: (Internationalization) Configuración o adición de traducciones.
* **`lint`**: (Lint) Arreglar errores de formato marcados por el linter (ESLint / Prettier).
* **`seo`**: (SEO) Mejoras de etiquetas meta para indexación.

### Backend, Base de Datos y Seguridad
* **`sec`** / **`security`**: (Security) Parches o corrección de vulnerabilidades de seguridad.
* **`db`**: (Database) Cambios en la estructura de la base de datos (scripts de migración).
* **`seed`**: (Seed) Inserción de datos iniciales o de prueba a la base de datos.
* **`config`**: (Config) Cambios en archivos de configuración del framework.
* **`env`**: (Environment) Actualización o documentación de variables de entorno.

### Operaciones y Despliegue
* **`deploy`**: (Deploy) Scripts o configuraciones para subir el proyecto a producción.
* **`release`**: (Release) Commit especial para marcar una nueva versión del software (ej. `release: v1.0.0`).
* **`hotfix`**: (Hotfix) Parche de emergencia aplicado directamente sobre el código en producción.

---

## 3. El Contexto (`<scope>`)

El `(<scope>)` (alcance o contexto) es una herramienta visual para indicar rápidamente qué parte exacta del proyecto fue modificada. 

**Reglas de oro para el Scope:**
1. Siempre va entre paréntesis: `(modulo)`.
2. Se escribe en minúsculas.
3. Debe ser corto (1 o 2 palabras máximo).
4. Es **opcional**. Si un cambio afecta a todo el proyecto (ej. actualizar la versión del framework), simplemente no lo uses.

### Scopes sugeridos por Arquitectura:

**Backend (Spring Boot / Java):**
* Por dominio: `(reservations)`, `(docks)`, `(trucks)`, `(waiting-list)`.
* Técnicos: `(db)`, `(auth)`, `(security)`, `(api)`.

**Frontend (Angular / TypeScript):**
* Por módulo: `(ollas)`, `(solicitudes)`, `(entregas)`, `(dashboard)`.
* Técnicos: `(services)`, `(forms)`, `(routing)`.

**Frontend (Vue 3 / JavaScript):**
* Por funcionalidad: `(reportes)`, `(sla)`, `(historial)`.
* Técnicos: `(components)`, `(utils)`, `(state)`.

> **¿Cuándo NO usar Scope?**
> No uses scope si tu cambio afecta a muchísimos archivos o al proyecto entero.
> * Incorrecto: `chore(todo): update dependencies`
> * Correcto: `chore: update dependencies`

---

## 4. El Asunto (`<subject>`)

Es la descripción corta de lo que hiciste. Tiene 3 reglas de oro para todo el equipo:

1. **Verbo en imperativo:** Escribe como si estuvieras dando una orden. Usa `add`, no `added` ni `adding`. Usa `fix`, no `fixed`.
2. **Todo en minúscula:** Salvo nombres propios como JWT, ID, HTML o clases específicas.
3. **Sin punto final:** No pongas un `.` al final de la oración.

---

## 5. Ejemplos Prácticos por Tecnología

Para que quede clarísimo, aquí tienen ejemplos aplicados a lo que cada uno está haciendo en sus laboratorios:

### Backend (Spring Boot / Java)
* `feat(reservations): add validation for truck and dock load compatibility`
* `fix(db): correct column name for weight capacity in trucks table`
* `refactor(services): move overlapping logic to a dedicated validator class`
* `chore(flyway): add migration script v3 for operational closures`

### Frontend (Angular / TypeScript)
* `feat(solicitudes): implement FormArray for dynamic items in the request form`
* `fix(services): resolve forkJoin synchronization issue when saving dispatches`
* `style(dashboard): update padding and grid layout for statistics cards`
* `ci(vercel): add configuration file for static angular deployment`

### Frontend (Vue 3 / JavaScript)
* `feat(reportes): add computed property to calculate SLA due dates`
* `fix(state): correct issue where deleted report stayed on screen`
* `refactor(utils): extract date formatting logic to an external js module`
* `docs(readme): update instructions to run the vue app with vite`

---

## 6. Commits Complejos (Con Body)

Si hiciste un cambio complejo que requiere explicación del **por qué**, no lo resumas mal. Usa un commit de múltiples líneas:

```text
fix(auth): fix token expiration issue on concurrent requests

The interceptor was failing to refresh the token when two HTTP 
calls were made at the exact same millisecond. Added a queue 
system to hold requests until the new token is available.

Resolves: #89
```
---

## Autor y derechos de uso

Autor: Diego Avalos ☕

Documento elaborado con fines educativos.
Uso libre para proyectos académicos, citando la fuente.
