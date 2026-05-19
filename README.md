# PlantSimulator

**Editor visual de diagramas de proceso (PFD/P&ID) y simulador de alineaciones operativas para estaciones de bombeo y rebombeo de hidrocarburos.**

Cumple con simbología **ANSI/ISA-5.1 (2024)**. Diseñado para **operadores de planta e ingenieros de operaciones**: construye el diagrama de tu estación, define los servicios de cada línea y visualiza por dónde fluye el producto según el estado de válvulas y bombas.

> Desarrollado por **[Ing. Javier Gómez](https://github.com/ingjaviergomezm)** — Ingeniería de Operaciones.
> Probado sobre una estación real de rebombeo de crudo. La herramienta es *plant-agnostic*: sirve para cualquier estación cambiando el inventario.

---

## Para qué sirve

- **Dibujar el PFD/P&ID de la estación** con simbología estándar: tanques, bombas, válvulas, separadores, trampas de raspadores, sumideros, filtros, mezcladores, unidades LACT y conectores de frontera.
- **Definir servicios de tubería** (tipo de fluido) con código de color: Fase 1, Fase 2, ODL, Diluyente, etc.
- **Simular la ruta de flujo activa**: el simulador resalta por dónde pasa el producto según el estado normal de cada válvula/bomba, e identifica líneas sin camino completo.
- **Documentar alineaciones operativas** como base para checklists y procedimientos de sala de control.

No requiere instalación ni servidor: se abre en el navegador.

---

## Cómo se usa (guía rápida)

### 1. Abrir el editor
Abre el archivo del editor en un navegador moderno (Chrome o Edge recomendados). No necesita internet ni instalación.

### 2. Cargar el inventario de tu planta
Botón **📋 Plantilla** → sube el Excel con la lista de equipos/válvulas → *Reemplazar todo* o *Solo agregar nuevas*. Los componentes aparecen listos para ubicar.

### 3. Posicionar los equipos
- Pestaña **Por posicionar**: lista de componentes pendientes. Click en uno y luego click en el lienzo para ubicarlo.
- O arrástralos desde la **paleta** (panel izquierdo, sección *Equipos*).
- **Mover varios a la vez:** mantén **Ctrl** y haz click en varios equipos; luego arrastra cualquiera y se mueven juntos.
- Al arrastrar aparecen **guías de alineación** (líneas punteadas) que ayudan a alinear equipos entre sí.

### 4. Dibujar las tuberías
- Pulsa **P** (modo Tubería). Click en el puerto de un equipo, traza la línea (los segmentos salen ortogonales por defecto) y termina en otro equipo. **Doble-click** o **Enter** finaliza.
- **Reacomodar una tubería:** selecciónala y arrastra los puntos (codos) o los **tramos** (las barritas naranjas) para correrlos en horizontal/vertical.
- Donde dos tuberías se cruzan **sin conectarse**, automáticamente una **salta** sobre la otra (puente) para dejar claro que los flujos no se mezclan.

### 5. Asignar el servicio (tipo de fluido)
Panel izquierdo, **Servicios de tubería**. Para teñir una tubería: selecciónala y haz **click en el servicio** deseado — adopta su color al instante. Puedes crear, renombrar y recolorear servicios.

### 6. Simular el flujo
Botón **▶ Simular flujo**: resalta las tuberías con flujo activo (según el estado normal de válvulas/bombas) y atenúa el resto. Útil para verificar que una alineación tiene camino completo de origen a destino.

### 7. Guardar tu trabajo
- **Autoguardado** en el navegador (no se pierde al cerrar).
- **💾 Guardar como…**: exporta el proyecto a un archivo (eliges carpeta y nombre).
- **📂 Cargar proyecto**: reabre un proyecto guardado.

---

## Catálogo de equipos

| Equipo | Para qué |
|---|---|
| **Tanque / Vasija** | Almacenamiento; terminal de flujo. |
| **Separador (vertical / horizontal)** | Separación bifásica con demister y nivel de líquido. |
| **Sumidero** | Recolección de drenajes/aguas aceitosas. Trae por defecto **filtro canasta** a la entrada y **bomba** a la salida. |
| **Bomba (centrífuga / vertical / desplazamiento positivo)** | Propulsión; estado encendida/apagada/standby afecta la simulación. |
| **Trampa de recibo / despacho** | Recibo y lanzamiento de raspadores (pigs). La de recibo trae su **arreglo típico** (MOV de entrada, salida por el fondo y bypass). |
| **Filtro / Filtro canasta** | Filtración en línea. |
| **Mezclador en línea** | Mezclador estático (static mixer). |
| **Intercambiador** | Intercambio de calor. |
| **Unidad LACT** | Medición fiscal; brazos de medición con etiquetas editables. |
| **Carrotanque** | Origen/destino de producto en descargadero (vista normal o espejada). |
| **Origen / Destino (frontera)** | Por dónde entra o sale el producto del sistema (p.ej. ARAGUANEY, MONTERREY). Punto de partida del flujo. |
| **Brida ciega / tie-in** | Fin de línea físico; bloquea el flujo (la línea queda presurizada hasta ahí). |

Las **válvulas** (manuales HV, motorizadas MOV, control PCV/FCV, alivio PSV, shutdown SDV/ESDV, etc.) se dibujan con cuerpo *bowtie* horizontal y actuador arriba, y tienen un **estado en operación normal** (🔴 abierta · 🟢 cerrada · 🟡 disponible · ⚪ no aplica) que el simulador usa para calcular la ruta de flujo.

---

## Atajos de teclado

| Tecla | Acción |
|---|---|
| `V` | Modo selección |
| `P` | Modo dibujar tubería |
| `F` | Ajustar zoom al contenido |
| `Ctrl` + click | Sumar/quitar a la multi-selección |
| `Del` / `Backspace` | Eliminar lo seleccionado |
| `Esc` | Cancelar / deseleccionar |
| `Ctrl+Z` / `Ctrl+Y` | Deshacer / rehacer |
| Rueda del mouse | Zoom · Click+arrastrar vacío / `Alt`+arrastrar | Mover el lienzo (pan) |

---

## Convención de colores de estado (industria petrolera)

| Color | Estado | Significado |
|---|---|---|
| 🔴 Rojo | Abierta | Flujo activo — la línea está "caliente" |
| 🟢 Verde | Cerrada | Sin flujo — línea aislada |
| 🟡 Amarillo | Disponible | Control automático |
| ⚪ Gris | No aplica | Sin estado asignado |

> Nota: es la convención **inversa** al semáforo común. En operación petrolera el rojo indica "hay producto en movimiento", el verde "línea segura/aislada".

---

## Estado del proyecto

| Funcionalidad | Estado |
|---|---|
| Editor visual de PFD con simbología ANSI/ISA-5.1 | ✅ |
| Importador de inventario (Excel/CSV) | ✅ |
| Servicios de tubería + herramientas de edición | ✅ |
| Catálogo ampliado de equipos | ✅ |
| Motor de cálculo de ruta de flujo | ✅ |
| Importador de escenarios de alineación | 🚧 En desarrollo |
| Validación de coherencia entre escenarios | ⏳ Planeado |

---

## Aviso

Proyecto **privado** de uso interno. Este sitio publica únicamente la documentación / manual de usuario; **el código fuente no es público**. Para acceso a la herramienta, contactar al autor.

© Ing. Javier Gómez — [github.com/ingjaviergomezm](https://github.com/ingjaviergomezm)
