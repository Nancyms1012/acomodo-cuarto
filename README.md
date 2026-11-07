# Acomodo del cuarto

Planificador para probar distintas formas de acomodar los muebles de mi cuarto, con las medidas reales y sin instalar nada.

Página publicada: https://nancyms1012.github.io/acomodo-cuarto/planner.html

## Páginas

| Archivo | Qué es |
|---|---|
| `planner.html` | Planificador interactivo. Se arrastran los muebles sobre el plano a escala. |
| `index.html` | Propuesta NUEVA del acomodo (estática), con enlace al planificador. |
| `actual.html` | Acomodo ACTUAL (estático), para comparar. |

Todo es HTML, CSS y JavaScript en un solo archivo por página. No hay dependencias ni paso de compilación.

## Cómo usar el planificador

- **Mover:** arrastra un mueble (mouse o dedo).
- **Seleccionar:** toca el mueble. Arriba se ve su nombre y medidas.
- **Rotar:** botón "Rotar" (gira el mueble 90° alrededor de su centro y lo mantiene dentro del cuarto). Las medidas no cambian: solo se intercambian el ancho y el alto dibujados. Si rotado no cabe en el cuarto, avisa y no lo gira.
- **Espacio libre:** la barra azul de arriba muestra el espacio libre del cuarto en m² y en % (descontando muebles, puerta y división, sin contar dos veces lo que se solapa). Al seleccionar un mueble muestra además cuántos cm hay libres a su izquierda, derecha, arriba y abajo hasta lo más cercano (otro mueble, la división o la pared), y dibuja esas distancias en el plano con líneas amarillas. Se actualiza mientras arrastras.
- **Cuadrícula 10 cm:** botón "Cuadricula 10 cm". Líneas finas cada 10 cm y más marcadas cada 50 cm.
- **Imán:** botón "Iman". Al arrastrar, ajusta el mueble a múltiplos de 10 cm, o lo pega a la pared opuesta si queda a menos de 5 cm. Para medidas exactas usa "Medidas".
- **Cotas:** botón "Cotas" muestra u oculta las líneas de medida en los bordes de cada mueble (ancho arriba, alto a la izquierda, en cm), igual que las de las paredes. Se actualizan al rotar o cambiar medidas.
- **Medidas:** botón "Medidas", o doble toque sobre el mueble, o "Medidas" en la lista. Permite cambiar nombre, largo, ancho y posición (X, Y). El mueble se mantiene dentro del cuarto.
- **Fijar/Soltar:** bloquea o libera un mueble. Un mueble fijo no se arrastra ni se rota. Solo la TV está fija por defecto.
- **+ Agregar:** crea un mueble nuevo con nombre, largo, ancho y categoría.
- **Eliminar:** quita el mueble seleccionado (si está fijo, primero hay que soltarlo).
- **Lista:** panel con todos los muebles y sus medidas.
- **Reset:** vuelve a la distribución inicial. Borra los cambios guardados.
- **Exportar:** descarga un `.txt` con la posición de cada mueble.

Cada mueble muestra su nombre y sus medidas (ancho × alto en cm, tal como se ve en el dibujo). Con las cotas encendidas, las medidas van en líneas sobre los bordes. Los muebles muy pequeños (por ejemplo la TV, de 50 × 6 cm) pueden mostrar solo la medida, o nada; el nombre y la medida siempre están en el tooltip al pasar el mouse. La preferencia de cotas se guarda en el navegador (`roomPlannerCotas`).

## Medidas del cuarto

El plano está dibujado a escala en centímetros.

- Pared de arriba (balcón y puerta): 220 cm.
- Pared de abajo (cama): 224 cm.
- Paredes izquierda y derecha: 300 cm en la mitad de la puerta y 284 cm en la mitad de la cama (584 cm en total).
- La división es un pedazo de pared de 75 × 10 cm que sale de la pared derecha.
- La pared de arriba es un balcón con cortina (franja de 28 cm en el dibujo).

El detalle de los muebles y las decisiones están en [CONTEXTO.md](CONTEXTO.md).

## Datos guardados

El planificador guarda los cambios en el navegador (`localStorage`), así que solo se ven en el mismo navegador y equipo.

| Clave | Contenido |
|---|---|
| `roomPlanner` | Lista de muebles con sus medidas y posiciones |
| `roomPlannerNextId` | Siguiente id para muebles nuevos |
| `roomPlannerPercheroLibre` | Marca de una migración que soltó el perchero de pared |
| `roomPlannerPuerta75` | Marca de la migración que agregó la puerta de 75 × 75 |
| `roomPlannerCotas`, `roomPlannerGrid`, `roomPlannerSnap` | Preferencias de cotas, cuadrícula e imán |

Si se cambian las posiciones iniciales en el código, quien ya tenga datos guardados sigue viendo los viejos hasta pulsar Reset.

## Probar en local

Abre `planner.html` en el navegador. No necesita servidor.

## Publicar

El sitio se publica con GitHub Pages desde la rama `main`. Al hacer push a `main`, la página se actualiza en uno o dos minutos. Para ver el cambio, recarga con Ctrl+F5.

```
git add planner.html
git commit -m "Descripción del cambio"
git push origin main
```

## Respaldos relacionados

- Editor interactivo anterior (archivo único, sin GitHub): `Documents\CUARTO-PLANO\cuarto-interactivo.html`.
- Notas de la conversación original: `Documents\CUARTO-PLANO\NOTAS-CUARTO.md`.
