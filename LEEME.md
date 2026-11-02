# Control diario · Agencia Don Juan

Cuadro de operación para la reunión diaria (Ashly y Yadhira) + dashboard por cuenta.
La data vive en un Google Sheet; el HTML está en GitHub Pages.

## Instalación (10 minutos, una sola vez)

### 1. Google Sheet + Apps Script
1. Con hola@pablosaul.com crea un Google Sheet nuevo llamado **Control diario Don Juan**.
2. Menú **Extensiones → Apps Script**. Borra lo que haya y pega todo `Code.gs`.
3. Cambia la línea `const PIN = 'donjuan2026';` por el PIN que quieras darle al equipo.
4. Guarda, elige la función **setup** arriba y pulsa **Ejecutar**. Acepta los permisos.
   → Se crean las pestañas `Cuentas`, `Items`, `Historial` y `Reuniones`, con las 17 cuentas cargadas.
5. **Implementar → Nueva implementación → tipo App web**
   - Ejecutar como: **Yo**
   - Quién tiene acceso: **Cualquier persona**
6. Copia la URL que termina en `/exec`.

### 2. GitHub
1. Crea el repo (ej. `control-diario`) y sube `index.html`.
2. En `index.html`, busca `API_URL: ''` y pega la URL entre las comillas.
3. **Settings → Pages → Deploy from branch → main**.
   El cuadro queda en `https://pablosaul.github.io/control-diario/`.

Comparte el link y el PIN con Ashly y Yadhira. La primera vez cada una elige su nombre y todo lo que cambie queda firmado.

## Uso diario
- **Reunión de hoy, por editor / diseñador** (vista por defecto): aparece una tarjeta para Diego, Jairo, Richard y Adriana. En cada una se carga la tarea del día con **cliente + formato + nombre del video**; la fecha de entrega se llena sola con hoy. Con Enter se agrega y la fila queda lista para la siguiente tarea, conservando el cliente y el formato.
- Cada tarea queda guardada **en su marca**. Con el botón **Por marca** se ve lo mismo agrupado por cliente.
- Cada tarea lleva **fecha de inicio** y **fecha de entrega**. Si la entrega es anterior al inicio, el cuadro no deja guardarla.
- Cuando el editor o diseñador acaba, pulsa **✓ Terminada**. La tarea sale de su lista y pasa a "Terminadas en los últimos 7 días", donde se ve cuántos días tomó, si salió a tiempo o tarde y un botón **Reabrir** por si hubo un error.
- Etapas: Por hacer → En proceso → Revisión interna → Corrección → Terminado (→ Publicado). Lo que no se termina sigue apareciendo al día siguiente como atrasado.
- Si el Sheet ya estaba creado, la columna `fecha_inicio` se agrega sola al final de la pestaña Items con el primer guardado. Igual vuelve a pegar el `Code.gs` y crea una **nueva versión** de la implementación (Implementar → Gestionar implementaciones → editar → Nueva versión).
- **Acta**: quién asistió y los acuerdos del día.
- **Dashboard**: muestra un semáforo por cuenta, el avance contra la meta, la carga por persona, el embudo de producción, los bloqueos y los vencimientos de contrato. Al tocar una cuenta se abre su ficha con el historial de cambios.
- El cuadro se actualiza solo cada 90 segundos, así que las dos pueden trabajar a la vez.

## Cambiar cuentas, metas o fechas (desde el Sheet)
Pestaña **Cuentas**:
| columna | qué poner |
|---|---|
| meta | cantidad de contenidos |
| periodo_meta | `mes` = meta mensual · `contrato` = meta total entre inicio y fin · vacío = sin meta |
| dia_corte | día en que arranca el ciclo mensual (Kapek = 28). Vacío = mes calendario |
| inicio / fin | fechas del contrato (aaaa-mm-dd) |
| activa | `NO` para ocultar una cuenta sin borrarla |

Para agregar un cliente nuevo basta con añadir una fila. El equipo (`PRODUCCION`), las etapas, los formatos y los motivos de bloqueo están al inicio del `<script>` de `index.html`. Para sumar un editor nuevo, agrega una línea en `PRODUCCION`.

## Cómo se pinta el semáforo
- 🔴 algo lleva más de 2 días atrasado, o la cuenta va por debajo del 70 % del ritmo esperado de su meta
- 🟡 hay algo atrasado o bloqueado, o el ritmo está por debajo del 100 %
- 🟢 al día
- ⚪ todavía no hay registros
