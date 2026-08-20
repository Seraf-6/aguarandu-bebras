# Simulacro Aguarandú – Bebras

Material de entrenamiento para la **Olimpiada de Informática Aguarandú–Bebras** (OMAPA, Paraguay),
fase inicial. Incluye un simulacro web y cuadernillos imprimibles para las categorías
**Kilobyte** (4.º–6.º grado), **Megabyte** (7.º–9.º) y **Gigabyte** (7.º–9.º, con programación).

👉 **[Abrir el simulacro](https://seraf-6.github.io/aguarandu-bebras/)**

---

## Qué hay acá

| | |
|---|---|
| **Simulacro web** | Un desafío por pantalla, se puede avanzar y retroceder, marcar problemas para revisar, y el cronómetro está siempre visible. Las respuestas correctas aparecen **recién al terminar**, con la explicación de cada una. |
| **Banco de problemas** | 83 desafíos con enunciado, 4 opciones, respuesta, explicación, concepto de pensamiento computacional, nivel de dificultad y fuente. |
| **Cuadernillos PDF** | Uno por categoría: todos los desafíos del nivel + hoja de respuestas para el alumno + soluciones explicadas para el docente. |

### Formatos del simulacro

| Formato | Problemas | Tiempo |
|---|---|---|
| Simulacro oficial | 9 | 60 min |
| Entrenamiento corto | 5 | 25 min |
| Maratón | 15 | 75 min |
| Banco completo | todos los del nivel | sin límite |

### El código de la prueba

Antes de empezar, el simulacro muestra un **código de 4 caracteres**. Todos los que usen
el mismo código y la misma categoría reciben **exactamente los mismos problemas en el mismo orden**.
Anotá el código en el pizarrón y toda la clase rinde la misma prueba, aunque cada uno esté en su
propia computadora. Cambiando el código sale otra prueba distinta del mismo banco.

---

## Cómo actualizar el sitio publicado

El sitio ya está publicado en **https://seraf-6.github.io/aguarandu-bebras/**
(Settings → Pages, rama `main`, carpeta `/ (root)`).

Para actualizarlo, subí los archivos nuevos al repositorio: GitHub Pages vuelve a publicar
solo en 1–2 minutos. Los archivos que se sirven son `index.html`, `assets/`, `fichas/`,
`problems.json` y `.nojekyll` (este último es necesario para que Pages sirva las carpetas
tal cual, sin procesarlas con Jekyll).

---

## Cómo agregar o cambiar problemas

Todo el contenido vive en **`problems.json`**. Cada problema tiene esta forma:

```json
{
  "id": "kb-mi-problema",
  "nivel": "kilobyte",
  "titulo": "Título del desafío",
  "enunciado": "<p>Texto en HTML. Se puede usar [[IMG0]] para ubicar una figura.</p>",
  "imagenes": ["mi_figura.png"],
  "pregunta": "¿Qué se pregunta?",
  "opciones": ["Opción A", "Opción B", "Opción C", "Opción D"],
  "respuesta": 2,
  "explicacion": "<p>Por qué la respuesta correcta es esa.</p>",
  "concepto": "Grafos / recorridos",
  "dificultad": "media",
  "fuente": "De dónde salió",
  "incompleto": false
}
```

Detalles:

- `nivel`: `kilobyte`, `megabyte` o `gigabyte`.
- `respuesta`: índice de la opción correcta, **empezando en 0** (0 = A, 1 = B, 2 = C, 3 = D).
- `dificultad`: `facil`, `media` o `dificil`. El simulacro arma cada prueba
  con una mezcla de ~34 % fáciles, ~44 % medias y ~22 % difíciles, evitando repetir concepto.
- `imagenes`: nombres de archivos dentro de `assets/`. Si el enunciado contiene `[[IMG0]]`,
  `[[IMG1]]`, etc., la figura se inserta en ese punto; si no, va al final del enunciado.
- `incompleto: true` excluye el problema del simulacro y de los cuadernillos
  (se usa para el desafío «Muñeca nido de castor», al que le falta una imagen en la ficha original).

Después de editar `problems.json`, regenerá los archivos:

```bash
python3 src/fichas.py     # arma fichas/ficha-*.html
node scripts/pdf.mjs      # convierte esos HTML a PDF (necesita Playwright)
python3 src/build.py      # arma site/index.html con todo embebido
```

Si solo cambiaste texto y no querés regenerar los PDFs, alcanza con `python3 src/build.py`.

---

## Estructura

```
problems.json          banco de problemas (la única fuente de verdad)
assets/                figuras de los problemas
src/app.css            estilos del simulacro
src/app.js             lógica del simulacro
src/build.py           arma site/index.html embebiendo CSS + JS + banco
src/fichas.py          arma los cuadernillos HTML
scripts/pdf.mjs        convierte los cuadernillos a PDF
fichas/                cuadernillos generados (HTML y PDF)
site/                  ← esto es lo que se sube a GitHub Pages
```

---

## Sobre las fuentes

- **18 desafíos** provienen de las fichas oficiales *Ejercicios Kilobyte (2025)* y
  *Ejercicios Megabyte (2025)* publicadas por **OMAPA**. Sus enunciados e ilustraciones se
  reproducen para uso educativo sin fines de lucro, y cada uno indica su origen en el campo `fuente`.
  Las respuestas correctas no venían en esas fichas: fueron resueltas y verificadas para este material.
- **65 desafíos** son adaptaciones o variantes originales en estilo Bebras, escritas para este
  banco a partir de conceptos y formatos de tareas Bebras publicadas (Bebras Puerto Rico,
  Desafío Bebras Ñandú, Bebras México, Tarjetas Bebras Perú, entre otras). Cada uno declara
  en `fuente` si es adaptación de una tarea concreta o una variante original.
- Los 20 desafíos de la categoría Gigabyte tienen su pseudocódigo **traducido a Python y ejecutado**
  para confirmar la respuesta.

Bebras es una iniciativa internacional de pensamiento computacional
([bebras.org](https://www.bebras.org/)). En Paraguay la organiza
[OMAPA](https://www.omapa.org/proyectos/aguarandu/).

## Licencia

Material educativo de uso libre para docentes y estudiantes, sin fines de lucro.
Los contenidos de origen OMAPA pertenecen a sus autores.
