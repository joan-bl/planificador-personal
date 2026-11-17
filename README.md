# Planificador personal para iPad 2

**Web:** https://joan-bl.github.io/planificador-personal/

Web app de un solo archivo (`index.html`) para usar en un **iPad 2 (A1395, iOS 9.3.5 / 9.3.6)** fijo en el escritorio o en la pared. Tiene un diseño inspirado en el calendario de iCloud.

## Qué tiene

| Pestaña | Para qué |
|---|---|
| **Calendario mensual** | Toca un día para añadir eventos (con hora opcional). Los eventos culturales salen en azul y los normales en verde. |
| **Planificador semanal** | Franjas de búsqueda de empleo, gimnasio y hobby. Cada toque en una franja cambia su tipo: Empleo → Gimnasio → Hobby → Libre. La rutina matutina y la comida son fijas. Arriba se ve el recuento (meta de gimnasio: 3 días). "Reiniciar semana" pide un segundo toque para confirmar. |
| **Lista de tareas** | Tareas con prioridad de 1 a 3 estrellas, ordenadas por prioridad, y filtros (Todas, Pendientes, Completadas). |

## Notas técnicas (por qué está hecho así)

Safari de iOS 9 es muy antiguo, así que la app evita todo lo que no soporta:

- **CSS escrito a mano, sin Tailwind ni ninguna librería externa.** El script de Tailwind por CDN no funciona en iOS 9.
- **Sin CSS Grid**, que llegó con iOS 10.3. La maqueta usa flexbox (con prefijos `-webkit-`).
- **JavaScript ES5**: nada de `let`, `const`, funciones flecha ni template literals.
- **Fecha en español hecha a mano**, porque iOS 9 no tiene `Intl`.
- **Rendimiento en el iPad 2:**
  - **Toque rápido:** el click se lanza en cuanto se levanta el dedo, sin la espera de unos 300 ms de Safari, y `touch-action: manipulation` se aplica a todos los elementos. Los campos de texto mantienen su comportamiento normal.
  - En el planificador semanal, cada toque **actualiza solo esa franja** en lugar de reconstruir la tabla entera.
- **Zonas táctiles de 44 px como mínimo** y **pantalla completa** al abrirla desde el icono de inicio.

### Datos

Se guardan en el `localStorage` de Safari, solo en ese iPad. No hay servidor ni cuenta.

| Clave | Contenido |
|---|---|
| `ipad_month_events` | Eventos por día: `{ "2026-11-17": { events: [{ time, text, cultural }] } }` |
| `ipad_weekly_schedule` | Plan semanal: `{ "10:00 - 12:00": [7 valores, de lunes a domingo] }` |
| `ipad_tasks` | Tareas: `[{ id, title, completed, priority }]` |

Safari guarda estos datos para cada dominio (`joan-bl.github.io`). Si se borran los datos de Safari, se pierde todo. En modo privado no se guarda nada.

Para cambiar las franjas horarias por defecto, edita `defaultSchedule` en el `<script>`. Después, en la app, pulsa "Reiniciar semana".

## Publicar cambios

Esta carpeta es el repositorio [`joan-bl/planificador-personal`](https://github.com/joan-bl/planificador-personal), publicado con GitHub Pages desde la rama `main`. Para actualizar la web:

```bash
git add -A
git commit -m "Describe el cambio"
git push
```

GitHub tarda uno o dos minutos en publicar. En el iPad, cierra la app del todo (deslízala hacia arriba en el selector de apps) y vuelve a abrirla.

## Instalar en el iPad

1. En **Safari**, abre https://joan-bl.github.io/planificador-personal/
2. Toca **Compartir** (el cuadrado con la flecha) → **Añadir a pantalla de inicio**.
3. Ábrela siempre desde ese icono.

## Licencia

MIT.
