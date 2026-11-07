# Contexto del proyecto

Documento de respaldo: explica de dónde sale cada medida y decisión para poder retomar el proyecto sin la conversación original.

## Origen

- El proyecto nació el 9 de julio de 2026 en una sesión de Kiro (workspace PAGINA CICLISMO + HIGHVISION-WEB) titulada "Hola! Esta vez quiero que seas un tipo disenador de interiores y arquitecto...".
- Objetivo: reordenar el cuarto, que se siente saturado, y probar distribuciones con las medidas reales.
- Se pidió reemplazar la cómoda pequeña por un espejo de pie para fotos de outfit.
- Primero se hicieron planos estáticos (`Documents\CUARTO-PLANO\cuarto-*.html`) con propuestas A, B y C. Después se pasó a un editor interactivo, y finalmente a este repositorio en GitHub Pages.

## Geometría del cuarto

Sistema de coordenadas del planificador (centímetros):

- X: horizontal, 0 en la pared izquierda y 224 en la derecha.
- Y: vertical, 0 arriba (balcón y puerta) y 584 abajo (pared de la cama).
- Todo el cuarto mide 224 × 584 cm.

Mitades:

| Mitad | Largo | Ancho | Qué hay |
|---|---|---|---|
| Mitad 2 (arriba) | 300 cm | 220 cm | Puerta, balcón, perchero de pie, mesa de adorno y los muebles grandes de la pared izquierda |
| Mitad 1 (abajo) | 284 cm | 224 cm | Cama, mesa de noche, gavetero |

- La división está a Y = 300. Es un pedazo de pared de 75 × 10 cm que sale de la pared derecha (ocupa Y 290–300, X 149–224). El resto del cuarto está abierto entre las dos mitades.
- La pared de arriba es un balcón: no hay pared ni ventana, solo una cortina. En el dibujo es una franja de 28 cm.
- La puerta es corrediza (75 cm en el dibujo, arriba a la derecha). Se puede cambiar el lado de apertura.
- El dibujo usa 224 cm de ancho para todo el cuarto. En la mitad de la puerta el ancho real es 220 cm; esos 4 cm no se dibujan, solo se rotulan en la pared de arriba.

## Muebles y medidas

Medidas en cm. En el código: `largo` es la medida horizontal y `ancho` la vertical cuando `rotated: false`. Con `rotated: true` se intercambian.

| # | Mueble | Largo × ancho | Posición inicial (x, y) | Dibujado (horizontal × vertical) |
|---|---|---|---|---|
| 2 | Perchero de pie | 30 × 30 | 130, 38 | 30 × 30 |
| 3 | Mesa de adorno | 80 × 40 | 45, 32 | 80 × 40 |
| 4 | Estante grande | 90 × 45 | 0, 42 | 45 × 90 |
| 5 | Cómoda grande | 130 × 43 | 0, 135 | 43 × 130 |
| 6 | Escritorio | 120 × 60 | 0, 268 | 60 × 120 |
| 7 | Gavetero verde | 41 × 36 | 0, 543 | 36 × 41 |
| 8 | Cama | 195 × 145 | 39, 389 | 145 × 195 |
| 9 | Mesa de noche | 38 × 28 | 186, 546 | 28 × 38 |
| 10 | TV (fija) | 50 × 6 | 170, 302 | 50 × 6 |
| 11 | Estante blanco | 61 × 30 | 178, 310 | 30 × 61 |
| 13 | Perchero de pared | 180 × 50 | 174, 100 | 50 × 180 |
| 14 | Cómoda pequeña | 63 × 40 | 184, 25 | 40 × 63 |

Notas sobre las medidas:

- Las medidas de los muebles las dio la usuaria. La mesa de noche es 38,5 × 28 y la cómoda grande 43,5 × 130; en el código están redondeadas.
- El perchero de pared es un espacio de 180 × 50 cm donde se cuelga ropa. Por eso el mueble se llama "Perchero de pared".
- Las posiciones iniciales vienen del plano aprobado en el editor interactivo. Los ajustes de solapes (mesa de adorno a x=45, cómoda pequeña a y=25, perchero de pared a y=100) se hicieron en el planificador y se comprobaron por código: ningún mueble se sale del cuarto ni se solapa.
- La cama más el gavetero y la mesa de noche ocupan 209 de los 224 cm del fondo. Entre la cama y la división quedan 89 cm.

## Distribución actual del cuarto

Según la descripción de la usuaria:

- **Pared de arriba (balcón):** mesa de adorno y perchero de pie.
- **Pared derecha, de arriba hacia abajo:** cómoda pequeña, perchero de pared, división, estante blanco con la TV.
- **Pared del fondo:** mesa de noche en la esquina, cama y gavetero.
- **Pared izquierda, de abajo hacia arriba:** escritorio (a la altura de la división), cómoda grande, estante grande.

## Reglas y decisiones

- Solo la TV es un mueble fijo. El perchero de pared dejó de ser fijo el 7 de noviembre de 2026 y ahora se puede mover, quitar o volver a fijar con el botón "Fijar/Soltar".
- La cama no puede quedar pegada a las paredes de los lados: necesita espacio para poner cosas a cada lado (unos 38 cm). Las propuestas deben respetar las medidas reales.
- Se descartó una propuesta (P4) porque la cama taparía todo el cuarto.
- La cómoda pequeña se quiere eliminar. En el código sigue existiendo como mueble que se puede quitar.
- La TV está colocada junto a la división, sobre el estante blanco. En la conversación original también se dijo que la TV estaba en la pared del fondo. Si no es ahí, hay que corregirla.

## Estructura del código (`planner.html`)

- `ROOM_ANCHO`, `ROOM_LARGO`, `DIVISION_Y`, `ANCHO_MITAD_2`, `DIVISION_LARGO`, `DIVISION_GROSOR`: geometría del cuarto.
- `DEFAULT_FURNITURE`: muebles iniciales. Cada uno tiene `id`, `name`, `largo`, `ancho`, `x`, `y`, `rotated`, `locked`, `category`.
- `renderRoom()`: dibuja paredes, medidas, división, puerta, balcón y muebles. Calcula `SCALE` según el espacio disponible.
- `startDrag`, `onDrag`, `endDrag`: arrastre con mouse y táctil. Los muebles se mantienen dentro del cuarto.
- `openEditModal`, `saveEdit`: edición de nombre, medidas y posición.
- `toggleLockSelected`, `rotateSelected`, `deleteSelected`, `addFurniture`: acciones de la barra.
- `saveToLocal` y `loadFromLocal`: persistencia en `localStorage` y migración del perchero.

## Historial de cambios

| Fecha | Cambio |
|---|---|
| 9 jul 2026 | Primeros planos, propuestas y editor interactivo (sesión original) |
| 7 nov 2026 | Perchero de pared deja de ser fijo; botón Fijar/Soltar; migración de datos guardados |
| 7 nov 2026 | Medidas en cada pared |
| 7 nov 2026 | Dimensiones corregidas: cama de pie, división de 75 cm, puerta y balcón a escala, posiciones sin solapes |
| 7 nov 2026 | Medidas visibles en cada mueble y edición de medidas, nombre y posición |

## Pendientes e ideas

- Aviso cuando dos muebles se solapan.
- Aviso cuando la cama queda a menos de 38 cm de una pared lateral.
- Agregar el espejo de pie que reemplazaría a la cómoda pequeña (se puede crear con "+ Agregar", por ejemplo 50 × 12 cm).
- Confirmar la ubicación de la TV.
- Opción de guardar varias distribuciones con nombre (ahora solo hay una guardada en el navegador).

## Respaldos y fuentes

- Sesión original de Kiro: `C:\Users\Nathalia Wong\.kiro\sessions\fc1f3c25865c5666\513f0179-c648-4c26-aeed-ab51cc671a0e\messages.jsonl`.
- Editor interactivo previo y planos: `C:\Users\Nathalia Wong\Documents\CUARTO-PLANO\`.
- Repositorio: https://github.com/Nancyms1012/acomodo-cuarto (antes `nancyms1012`; GitHub redirige).
