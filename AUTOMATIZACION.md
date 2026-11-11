# Publicación automática — instrucciones para la tarea programada

Esta tarea corre dos veces al día (mañana y tarde, hora del centro de México) y publica en despiertapuebla.com.mx.

## 1. Buscar las noticias
- Busca en la web las noticias más importantes de las últimas 12 horas en Puebla (capital, zona metropolitana y los 217 municipios), en México y en el mundo.
- Prioridad: Puebla > Nacional > Política > Economía > Internacional > Deportes > Entretenimiento > Tecnología > Educación.
- Medios locales: El Sol de Puebla, e-consulta, Municipios Puebla, Diario Cambio, La Jornada de Oriente, Milenio Puebla, El Popular, Poblanerías, Intolerancia Diario, Status Puebla, Puebla Online, Ángulo 7, Hipócrita Lector, Quadratín Puebla. Nacionales: Uno TV, Infobae México, Milenio, El Universal, La Jornada, Reforma, Excélsior, El Financiero, Expansión, Proceso. Abre las notas para confirmar los datos.
- Antes de escribir, lee los títulos de `content/notas/` de los últimos 2 días y **no repitas** una nota que ya existe. Si un tema avanzó, escribe una nota nueva con el dato nuevo.

## 2. Escribir 20 notas
Crea **exactamente 20** archivos nuevos en `content/notas/`, uno por nota, con nombre `AAAA-MM-DD-titular-en-minusculas-con-guiones.json` (máximo 70 caracteres después de la fecha) y este formato:

```json
{
  "titulo": "Titular claro, en tus palabras",
  "seccion": "puebla",
  "fecha": "2026-11-11T06:20",
  "resumen": "Dos o tres frases con los hechos: qué pasó, dónde, cifras y quién lo dijo.",
  "cuerpo": "",
  "imagen_tema": "catedral",
  "imagen": "",
  "credito": "",
  "fuentes": [{ "medio": "El Sol de Puebla", "enlace": "https://..." }],
  "destacada": false,
  "autor": "Redacción"
}
```

Reglas:
- `seccion`: puebla, nacional, politica, economia, internacional, entretenimiento, tecnologia, educacion o deportes. Al menos 8 de las 20 deben ser de `puebla`. Notas de política o educación locales (Congreso del Estado, Ayuntamiento, BUAP, SEP Puebla) pueden ir en `politica` o `educacion`.
- `fecha`: la hora de la ejecución (hora del centro). Usa minutos distintos para conservar el orden de importancia (la más importante con la hora más reciente).
- Marca `"destacada": true` en las 4 más importantes; de preferencia, al menos 2 de Puebla.
- `imagen_tema`: una de las claves de `assets/imagenes.js` que corresponda al tema o lugar (por ejemplo `popo` para el volcán, `buap` para la universidad, `ruta` para transporte, `autopista` para la México-Puebla, `estadio_pue` para el Club Puebla, `ayuntamiento` para el gobierno municipal, `industria` para Volkswagen, Audi y la industria automotriz, `cholula`, `atlixco`, `tehuacan`, `sierra` para la Sierra Norte, `campo` para el campo poblano). Si ninguna encaja, usa `catedral` o `centro` para Puebla y `zocalo` para el país.
- **Redacta todo con tus propias palabras.** No copies frases de los medios; como máximo, una cita breve (menos de 15 palabras) entre comillas si la frase exacta importa.
- **No inventes datos.** Cada cifra, nombre o fecha debe estar en la fuente enlazada. Si una fuente solo da el titular, escribe una nota breve con eso.
- Cada nota lleva al menos una fuente con su enlace real.
- Temas delicados (violencia, salud, política): tono neutral, sin adjetivos ni opiniones.

## 3. Actualizar los datos del día
Edita `content/hoy.json` (mismo formato que ya tiene):
- `fecha` ("Miércoles 11 de noviembre de 2026") y `actualizado` (hora).
- `clima`: máxima, mínima, pronóstico, lluvia y viento de la ciudad de Puebla (SMN / Conagua). `ahora` solo si tienes la temperatura actual de una fuente. `aire` y `aire_estado` (ok, warn, bad) si la Secretaría de Medio Ambiente del estado publica el índice.
- `popocatepetl`: fase del Semáforo de Alerta Volcánica (`fase`, por ejemplo "Amarillo Fase 2"; `color`: verde, amarillo o rojo) y el resumen del último reporte del Cenapred (exhalaciones, minutos de tremor, explosiones, caída de ceniza y si opera el Aeropuerto de Puebla). Si no hay reporte nuevo, deja el anterior.
- `municipios`: 5 o 6 municipios (San Andrés Cholula, Atlixco, Tehuacán, Teziutlán, Huauchinango, San Martín Texmelucan).
- `vialidades`: autopista México-Puebla, Arco Poniente / Periférico Ecológico, Vía Atlixcáyotl, bulevar 5 de Mayo y líneas 1, 2 y 3 de RUTA, solo con reportes confirmados.
- `avisos`: cortes de agua de Agua de Puebla, obras, alertas de Protección Civil, ceniza del Popocatépetl o trámites con fecha límite.
- `agenda`: eventos, ferias y manifestaciones anunciadas para el día.
Si no encuentras un dato, quita esa fila o deja el anterior; no lo inventes.

## 4. Revisar y publicar
1. Ejecuta `node scripts/build.mjs`. Si marca errores, corrígelos.
2. Confirma que hay 20 archivos nuevos y que ninguno repite una nota anterior.
3. Haz commit en `main` con el mensaje `Noticias del AAAA-MM-DD (mañana|tarde)` y push. Netlify publica solo.
4. Envía al usuario un mensaje corto: cuántas notas se publicaron, los 4 titulares destacados y cualquier problema.
