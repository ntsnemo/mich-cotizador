# Datos para cotizaciones e itinerarios (Google Sheet o TSV)

La app carga **destinos, condiciones y hoteles** desde **Google Sheets** (recomendado) o desde los archivos TSV en esta carpeta como respaldo. Las columnas deben coincidir con el documento base (BaseCotizador / Sheet).

El mismo documento puede tener más pestañas (itinerarios, imágenes, etc.); están documentadas más abajo para mantener el mismo estándar de columnas. Hoy la app **solo carga** Destinos, Condiciones y Hoteles.

---

## Opción A: Google Sheet

Si está configurado el ID del documento en `index.html` (SHEET_CONFIG), la app intenta cargar desde el Sheet. Para que funcione:

1. **Publicar el documento en la web**  
   En el Google Sheet: *Archivo > Compartir > Publicar en la web*. Elige “Hojas del documento” o “Documento completo”, formato **Valores separados por comas (.csv)**. Pulsa “Publicar”. Sin este paso la app no puede leer los datos.

2. **Pestañas que usa la app (cotizador)**  
   El GID sale de la URL al abrir cada pestaña:
   - **Destinos** → GID `0`
   - **Condiciones** → GID `1889365118`
   - **Hoteles** → GID `1598531904`

3. **Columnas**  
   Deben ser exactamente las indicadas más abajo para cada hoja.

Los cambios en el Sheet se ven en la app **después de recargar la página**.

---

## Opción B: Archivos TSV (respaldo)

Si el Sheet no está publicado o falla la red, la app carga desde los TSV de esta carpeta. Usa las mismas columnas que en el documento base.

---

## Columnas por hoja (match con el documento base)

### Cotizador (la app carga estas 3)

### 1. Destinos

| Columna      | Uso |
|-------------|-----|
| **id**      | Identificador: texto (orlando, universal, california, paris, crucero-disney, crucero-otros, nickelodeon, xcaret) o número del 1 al 8 (1 = Orlando, 2 = Universal, …). |
| **nombre**  | Nombre mostrado del destino (ej. "🏰 Disney World · Orlando"). La app no rellena el selector con esto; es informativo. |
| **imagen_url** | URL de la imagen del destino. |
| **gradiente**  | CSS para la tarjeta, ej. `linear-gradient(135deg,#1a1a6e,#4b2583,#c33f91)`. |

Si en el Sheet o TSV añades la columna **agente_titulo** (ej. "Agente Disney✨"), la app la usará; no está en el documento base.

---

### 2. Condiciones

| Columna | Uso |
|--------|-----|
| **destino_id** | Mismo valor que **id** en Destinos (texto o número 1–8). |
| **condiciones** | Texto principal de pago/cancelación que aparece en la cotización. |
| **condiciones_eventos_especiales** | Opcional. Texto para eventos especiales (ej. Star Wars Nite en California); se usa cuando el usuario marca el checkbox de evento especial. Puedes usar `\n` para saltos de línea. |

---

### 3. Hoteles

| Columna | Uso |
|--------|-----|
| **destino_id** | Destino del hotel (orlando, universal, california, paris, xcaret). Texto o número 1–8. |
| **nombre_hotel** | Nombre exacto del hotel como aparece en el selector. |
| **categoria** | Etiqueta (Value, Moderate, Deluxe, Prime Value, Preferred, Disney, etc.). La app deduce la clase CSS si no usas **categoria_css**. |
| **imagen_url** | URL de una imagen del hotel. Si está vacía, solo se muestra la categoría; si la URL falla, se oculta la imagen. |
| **optgroup** | Etiqueta del grupo en el desplegable (ej. "⭐ Value Resorts", "🏨 Good Neighbor Hotels"). |

Si añades la columna **categoria_css** (ej. `cat-premier`, `cat-deluxe`), la app la usará en lugar de deducirla de **categoria**; no está en el documento base.

El orden de las filas en el archivo es el orden en el selector de hoteles.

---

### Otras hojas del documento (referencia; la app no las carga aún)

Estas pestañas están en el mismo documento (BaseCotizador / Sheet). Si más adelante la app las usa, las columnas deben coincidir con esta tabla.

#### 4. ImagenesItinerarios

| Columna       | Uso |
|---------------|-----|
| **template_id** | Identificador del itinerario al que pertenece la imagen. |
| **url_imagen**  | URL de la imagen. |

---

#### 5. Itinerarios

| Columna     | Uso |
|-------------|-----|
| **id**      | Identificador del itinerario. |
| **titulo**  | Título del itinerario. |
| **hotel**   | Hotel asociado. |
| **cover_url** | URL de la imagen de portada. |
| **gradient** | CSS del gradiente (ej. linear-gradient(...)). |
| **orden**   | Orden de aparición. |

---

#### 6. ItinerarioDias

| Columna       | Uso |
|---------------|-----|
| **template_id** | Identificador del itinerario. |
| **dia_orden**   | Número de día (orden). |
| **titulo**      | Título del día. |
| **icono**       | Icono o emoji del día. |
| **tipo**        | Tipo de día (ej. crucero, parque, viaje). |

---

#### 7. ItinerarioActividades

| Columna       | Uso |
|---------------|-----|
| **template_id** | Identificador del itinerario. |
| **dia_orden**   | Día al que pertenece la actividad. |
| **orden**       | Orden de la actividad dentro del día. |
| **hora**        | Hora (ej. "9:00 AM"). |
| **descripcion** | Texto de la actividad. |

---

#### 8. ItinerarioTips

| Columna       | Uso |
|---------------|-----|
| **template_id** | Identificador del itinerario. |
| **dia_orden**   | Día al que pertenece el tip. |
| **orden**       | Orden del tip. |
| **texto**       | Contenido del tip. |

---

#### 9. ItinerarioDocs

| Columna       | Uso |
|---------------|-----|
| **template_id** | Identificador del itinerario. |
| **orden**       | Orden del documento. |
| **icono**       | Icono o emoji. |
| **titulo**      | Título del documento. |
| **descripcion** | Descripción o texto. |
