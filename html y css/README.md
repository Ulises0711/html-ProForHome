# ProForHome · Portal de Servicios Profesional y Clasificados de Oficios

**Segundo Parcial Práctico · Interfaz del Usuario 2026 · Caso 9**  
**Alumno:** Ulises · **Modalidad:** individual

ProForHome es una plataforma que conecta a personas que necesitan un arreglo en su casa con profesionales independientes de **plomería, electricidad, pintura y gas**. El usuario busca un profesional por rubro y zona, revisa su perfil y le pide un presupuesto con un formulario guiado.

---

## Entregables

| Entregable | Enlace / ubicación |
|---|---|
| Prototipo en Figma (lectura + prototipo) | https://www.figma.com/design/c8KjLABo5nEKzqMNUO1nQI |
| Sitio publicado (Netlify) | https://magnificent-pixie-838c6f.netlify.app |
| Código fuente (GitHub) | _(pegar acá el enlace del repositorio, si se sube)_ |
| Sitio en carpetas | Carpeta `html y css` (este README está adentro) |
| Documentación de heurísticas | Este documento, sección **Heurísticas de Nielsen aplicadas** |

> Para ver el prototipo interactivo en Figma: abrir el enlace, tocar **▶ Present** y elegir el flujo **"Caso 9 · Móvil"** o **"Caso 9 · Escritorio"**.

---

## 1. Cobertura de la consigna del Caso 9

| Requerimiento | Sitio web | Prototipo Figma |
|---|---|---|
| **Directorio de profesionales:** búsqueda por rubro y zona, listado con valoración en estrellas | `index.html`: filtros por rubro y zona que muestran u ocultan tarjetas; 6 profesionales con foto, estrellas, tarifa y especialidades | Pantalla *01 Directorio*; filtros convertidos en componentes interactivos (la opción elegida queda marcada) |
| **Perfil profesional:** galería de trabajos, opiniones, zona de cobertura, tarifa de visita | `perfil.html`: galería con 4 fotos reales de trabajos, opiniones con estrellas, panel lateral con cobertura y tarifa | Pantalla *02 Perfil* |
| **Solicitud de presupuesto:** formulario guiado, detalles adjuntos y confirmación de envío | `solicitud.html` (5 pasos numerados, adjunto de fotos) → `confirmacion.html` | Pantallas *03 Solicitud* y *04 Confirmación*; opciones, franja horaria e interruptor de urgencia interactivos |
| Flujo completo y cerrado | `mis-solicitudes.html`: seguimiento de pedidos con estados y cancelación con confirmación | Pantalla *05 Mis solicitudes*; navegación conectada entre las 5 pantallas |

---

## 2. Prototipo en Figma

### 2.1 Cómo se construyó

1. **Diseño inicial en Google Stitch:** pantallas móviles de directorio, perfil, solicitud y confirmación. Las pantallas de inicio de sesión, registro y recuperación de contraseña que había generado Stitch se quitaron del proyecto final, para concentrar el prototipo en el flujo que pide la consigna: buscar un profesional, ver su perfil y pedir un presupuesto.
2. **Desarrollo del sitio en HTML y CSS** a partir de ese diseño, adaptado a Argentina (bandera, código +54, zonas de CABA, precios en pesos).
3. **Publicación en Netlify** e **importación a Figma** con el plugin *html.to.design*, en dos tamaños: **390 px (celular)** y **1440 px (escritorio)**.
4. **Organización del archivo**, creación del **sistema de diseño**, **componentes interactivos** y **conexión del flujo**.

### 2.2 Organización del archivo

| Sección | Contenido |
|---|---|
| **1 · Pantallas móvil (390 px)** | `Móvil / 01 Directorio` → `05 Mis solicitudes` |
| **2 · Pantallas escritorio (1440 px)** | `Escritorio / 01 Directorio` → `05 Mis solicitudes` |
| **3 · Sistema de diseño** | Variables, componentes con variantes de estado y componentes interactivos |
| **4 · Componentes importados** | Componentes generados por la importación (botones, chips, menú, tarjetas), con variante *hover* |

### 2.3 Variables (tokens de diseño)

Colección **"ProForHome · Tokens"**: los mismos valores que `estilos.css`, para que el diseño y el código sean consistentes. Cada variable tiene su nombre CSS como *code syntax* (por ejemplo `var(--teal)`).

| Grupo | Variables | Uso |
|---|---|---|
| Marca | `navy`, `navy-hover` | Cabecera, títulos, texto principal |
| Acción | `teal`, `teal-hover`, `teal-presionado`, `teal-claro` | Botón principal, selección, éxito |
| Valoración | `ambar`, `ambar-claro`, `ambar-texto` | Solo estrellas y estado "En revisión" |
| Error / peligro | `rojo`, `rojo-hover`, `rojo-presionado`, `rojo-claro` | Errores y acciones destructivas |
| Neutros | `fondo`, `blanco`, `azul-suave`, `azul-medio`, `gris-claro`, `texto`, `texto-suave`, `gris`, `borde`, `borde-fuerte` | Fondos, textos y bordes |
| Radios | `radio/normal` (8), `radio/grande` (16), `radio/pildora` (999) | Esquinas de botones, tarjetas y chips |

### 2.4 Componentes y variantes de estado

| Componente | Variantes | Para qué sirve |
|---|---|---|
| **Botón** | 4 tipos (Primario, Secundario, Contorno, Peligro) × 5 estados (Default, Hover, Presionado, Foco, Deshabilitado) = **20** | Todas las acciones del sitio; texto editable |
| **Chip de filtro** | Default, Hover, Seleccionado, Foco | Filtros de rubro y zona |
| **Estado de solicitud** | En revisión, Presupuesto recibido, Finalizada, Cancelada | Etiquetas de *Mis solicitudes* (color **e** ícono) |
| **Campo de texto** | Vacío, Hover, Foco, Completo, Error | Formulario de solicitud; el estado Error muestra el mensaje debajo |
| **Estrellas** | Valor 5, 4, 3 | Valoración de los profesionales |

### 2.5 Componentes interactivos (prototipo)

En la web, el navegador recuerda qué opción marcó el usuario. La importación a Figma trae solo una imagen fija de cada pantalla, así que estos grupos se rehicieron como **componentes interactivos**: cada uno tiene una variante por opción y, al hacer clic, **cambia a la variante con esa opción marcada** (se comporta como un botón de radio). Existen en versión móvil y escritorio.

| Pantalla | Componente | Opciones |
|---|---|---|
| Directorio | **Filtro rubro** | Todos, Plomería, Electricidad, Pintura, Gas |
| Directorio | **Filtro zona** | Todas, Caballito, Palermo, Almagro, Flores |
| Solicitud | **Tipo de problema** | Fuga / rotura, Desagüe tapado, Calefón / caldera, Grifería, Inspección |
| Solicitud | **Franja horaria** | Mañana, Tarde, Noche |
| Solicitud | **Despacho urgente** | Interruptor Sí / No, con animación |

### 2.6 Flujo interactivo

```
Directorio ──► Perfil ──► Solicitud ──► Confirmación ──► Mis solicitudes
    ▲            │            │               │                │
    └────────────┴────────────┴───────────────┴────────────────┘
        (logo, menú superior y "← Volver" en todas las pantallas)
```

| Desde | Acción | Destino |
|---|---|---|
| Directorio | "Ver perfil" / "Pedir presupuesto" | Perfil / Solicitud |
| Perfil | "Solicitar presupuesto", "Pedir presupuesto" / "Ver otros profesionales" | Solicitud / Directorio |
| Solicitud | "Enviar solicitud a Mike" / "Cancelar" | Confirmación / pantalla anterior |
| Confirmación | "Ver mis solicitudes" / "Volver al directorio" | Mis solicitudes / Directorio |
| Mis solicitudes | "Ver perfil", "Ver presupuesto", "Pedir de nuevo", "Buscar otro profesional" | Perfil, Solicitud, Directorio |
| Todas | Logo, menú "Profesionales" / "Mis solicitudes", "← Volver" | Directorio / Mis solicitudes / atrás |

Hay **46 conexiones por versión** (móvil y escritorio) y dos puntos de inicio: **"Caso 9 · Móvil"** y **"Caso 9 · Escritorio"**.

---

## 3. Sitio web (HTML + CSS)

### 3.1 Cómo verlo

- **En línea:** https://magnificent-pixie-838c6f.netlify.app
- **En la computadora:** abrir `index.html` con doble clic. No necesita instalación ni JavaScript.

### 3.2 Estructura de carpetas

```
html y css/
├── index.html              01 · Directorio de profesionales (filtros por rubro y zona)
├── perfil.html             02 · Perfil profesional (galería, opiniones, cobertura, tarifas)
├── solicitud.html          03 · Formulario guiado de pedido de presupuesto
├── confirmacion.html       04 · Confirmación de envío al profesional
├── mis-solicitudes.html    05 · Seguimiento de solicitudes (con cancelación confirmada)
├── estilos.css             Hoja de estilos única, ordenada en secciones y comentada
├── imagenes/               Fotos de profesionales y de trabajos realizados
└── README.md               Esta documentación
```

### 3.3 Imágenes

| Imagen | Dónde aparece |
|---|---|
| `plomero.jpeg` | Foto de Mike Tremblay (directorio, perfil, solicitud, mis solicitudes) |
| `electricista.webp` / `electricista2.webp` | Fotos de Elena Rostova / Julián Peralta |
| `gasista.jpeg` / `gasista2.jpeg` | Fotos de Marcos Herrera / Lucas Fernández |
| `pintor2.jpg` | Foto de David Chen |
| `tuboG`, `tuboR`, `grifo`, `grifoR` | Galería *Trabajos previos verificados* del perfil |
| `contructor.jpeg` | Sección *Garantía ProForHome* del directorio |
| `pintor.jpeg` | Foto de *Trabajo terminado* en Mis solicitudes |

Todas las imágenes tienen **texto alternativo (`alt`)** que describe la foto y **carga diferida (`loading="lazy"`)**. Se recortan con `object-fit: cover` para que no se deformen.

### 3.4 Responsive

- Diseño **mobile first**: se escribe primero para celular y se amplía con `@media` a 720 px (tablet) y 1040 px (escritorio).
- Etiqueta `viewport`, imágenes fluidas y cuadrículas (`grid`) con `minmax(0, 1fr)`.
- El listado pasa de 1 columna (celular) a 2 (tablet) y 3 (escritorio). El perfil pasa a dos columnas con panel lateral.
- Verificado sin scroll horizontal en 320, 360, 390, 768 y 1280 px.

---

## 4. Heurísticas de Nielsen aplicadas

| # | Heurística | Ejemplo en el sitio | Ejemplo en Figma |
|---|---|---|---|
| 1 | Visibilidad del estado del sistema | Chip activo en verde, pasos numerados, pantalla de confirmación | Variantes *Seleccionado*, *Foco*, *Presionado*; filtros interactivos |
| 2 | Coincidencia con el mundo real | Rubros, zonas, precios en pesos y +54 de Argentina | Textos y etiquetas iguales al sitio |
| 3 | Control y libertad del usuario | "← Volver", "Cancelar", logo y menú en todas las páginas | Acciones *Back* y navegación a inicio |
| 4 | Consistencia y estándares | Una sola hoja de estilos con variables | Colección de variables y componentes reutilizables |
| 5 | Prevención de errores | Validación de campos y confirmación para cancelar | Variante *Error* del campo y *Deshabilitado* del botón |
| 6 | Reconocer en lugar de recordar | Opciones visibles como chips y tarjetas | Grupos de selección con todas las opciones a la vista |
| 8 | Diseño estético y minimalista | Una acción principal por pantalla | Jerarquía de botones Primario / Secundario / Contorno |

### 4.1 Visibilidad del estado del sistema
El usuario siempre sabe dónde está y qué pasó con su acción.

- El menú marca la página actual (`aria-current="page"` y fondo resaltado).
- En los filtros, el chip activo queda en verde y la lista de profesionales cambia al instante. En Figma, los filtros son componentes interactivos que muestran la opción elegida.
- El formulario muestra el avance (*Tu pedido › Confirmación › Respuesta del profesional*) y tiene secciones numeradas del 1 al 5.
- Al enviar, `confirmacion.html` avisa que el pedido llegó, con número de referencia y los próximos pasos.
- En *Mis solicitudes*, cada pedido tiene una etiqueta de estado (*En revisión*, *Presupuesto recibido*, *Finalizada*, *Cancelada*) con color e ícono, para que no dependa solo del color.
- Botones, chips y campos responden con *hover*, *presionado* y un aro de **foco** visible al navegar con el teclado. En Figma están documentados como variantes.

### 4.2 Coincidencia entre el sistema y el mundo real
- Lenguaje cotidiano en español rioplatense: "Pedí un presupuesto", "¿Qué problema tenés?", "Calefón", "Destapaciones".
- Datos locales: barrios de CABA, precios en pesos argentinos y teléfono con código **+54**.
- Íconos conocidos: estrellas para valoración, ✓ para verificado, ⏳ para "en revisión".

### 4.3 Control y libertad del usuario
- Siempre hay una salida: "← Volver al directorio / al perfil", botón "Cancelar" en el formulario, logo y menú en todas las pantallas.
- El pedido se puede cancelar **antes** de enviarlo (formulario) y **después** (*Mis solicitudes*, con confirmación).
- En el prototipo, "Volver" y "Cancelar" usan la acción *Back* de Figma, que regresa a la pantalla anterior.

### 4.4 Consistencia y estándares
- Una sola hoja de estilos (`estilos.css`) con **variables de color** compartidas por todas las páginas. En Figma, la misma paleta está como **variables**, con los mismos nombres.
- La cabecera, el pie y los botones son iguales en todas las pantallas. En Figma son **componentes** reutilizados.
- Convenciones de la web: el logo lleva al inicio, el ámbar se usa solo en estrellas y el rojo solo en errores y acciones destructivas.

### 4.5 Prevención de errores
- Validación de campos en el formulario: `required`, `minlength="20"`, `maxlength="500"`, `type="date"` y `type="tel"` con `pattern`.
- Los errores aparecen recién cuando el usuario sale del campo (`:user-invalid`), con borde rojo y un texto que explica cómo corregirlos. En Figma corresponde a la variante **Error** del *Campo de texto*.
- Para cancelar una solicitud hay que confirmar ("¿Cancelar esta solicitud? No se puede deshacer"), y la opción segura queda a la vista.
- La zona se elige de una lista con los barrios donde hay cobertura, en lugar de escribirla.

### 4.6 Reconocer en lugar de recordar
- Los filtros muestran todas las opciones como chips, así no hay que escribir nada.
- El tipo de problema y la franja horaria son tarjetas seleccionables, y la elegida queda marcada.
- La tarjeta del profesional se repite arriba del formulario, para saber a quién se le está escribiendo.
- La confirmación repite el resumen de lo enviado.

### 4.7 Diseño estético y minimalista
- Hay **una acción principal por pantalla**, en verde. Las secundarias van en estilo suave o de contorno; en Figma son los tipos *Primario*, *Secundario* y *Contorno* del componente Botón.
- La jerarquía tipográfica es clara: *Plus Jakarta Sans* para títulos e *Inter* para textos, con espacios en escala de 4/8 px.
- Cada tarjeta muestra solo lo necesario para decidir: foto, valoración, tarifa base y especialidades.

---

## 5. Accesibilidad

- Enlace "Saltar al contenido" al principio de cada página.
- Estructura semántica: `header`, `nav`, `main`, `section`, `article`, `footer`. Los filtros son `fieldset` con `legend`.
- Texto alternativo en todas las imágenes y `aria-label` en las estrellas (por ejemplo, "Valoración 4,9 de 5").
- Aro de foco visible para usar el sitio con el teclado.
- Contraste de texto adecuado sobre los fondos de la paleta.
- Botones y chips de por lo menos 44–48 px de alto, cómodos para tocar con el dedo.

---

## 6. Decisiones y límites

- **Sin JavaScript:** los filtros, el modal de cancelación y los avisos funcionan solo con CSS (`:has()`, `:target`, `:user-invalid`). Requiere un navegador actualizado (Chrome, Edge, Firefox o Safari recientes).
- **Es un prototipo estático:** los datos son de ejemplo y el formulario no se guarda en un servidor.
- **Sin cuenta de usuario:** se quitaron las pantallas de inicio de sesión, registro y recuperación de contraseña. El prototipo empieza directamente en el directorio de profesionales.
- **Perfil único:** todos los botones "Ver perfil" llevan al perfil de ejemplo de Mike Tremblay.
- **En Figma, los filtros cambian de aspecto pero no ocultan tarjetas:** mostrar cada combinación de filtros requeriría una pantalla por combinación. En el sitio web sí filtran.
- **"Cancelar solicitud" en Figma:** la ventana de confirmación existe solo en el sitio web, porque no se importó.

---

## 7. Herramientas utilizadas

| Herramienta | Uso |
|---|---|
| **Google Stitch** | Diseño inicial de las pantallas móviles |
| **HTML5 y CSS3** | Desarrollo del sitio responsive (editor de código) |
| **Netlify** | Publicación del sitio |
| **Figma + html.to.design** | Importación de las pantallas, sistema de diseño, componentes y prototipo |
| **Claude (asistente de IA)** | Apoyo en el código, la organización del archivo de Figma y esta documentación |
