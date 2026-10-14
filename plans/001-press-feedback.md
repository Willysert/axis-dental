# 001 — Respuesta instantánea al tocar botones

Commit base: 2db62e4 · Archivo: `index.html` (solo el bloque `<style>`)

## Problema
Ningún elemento tocable tiene efecto de "presionado". Los botones tardan 0.25 s en cambiar de color, y los enlaces de la barra de la portada no cambian de forma suave al pasar el dedo.

## Valores objetivo
- Presionado: `transform: scale(0.97)` en `:active`, transición `transform 160ms ease-out`.
- Cambios de color/fondo: 160 ms, `ease`.
- Botón flotante de WhatsApp: `scale(0.94)` en `:active` (su hover ya es 1.06).
- Celdas de servicios: `scale(0.98)` en `:active` (son más grandes; un efecto mayor se vería exagerado).

## Pasos
1. `.btn`: cambiar `transition` a `background 160ms ease, color 160ms ease, border-color 160ms ease, transform 160ms ease-out`. Añadir `.btn:active { transform: scale(0.97); }` DESPUÉS de las reglas `:hover` (para que gane sobre `translateY(-1px)`).
2. `.wa-float`: `transition: transform 160ms ease-out`; añadir `.wa-float:active { transform: scale(0.94); }` después del `:hover`.
3. `.svc-cell`: `transition: background 160ms ease, transform 160ms ease-out`; añadir `.svc-cell:active { transform: scale(0.98); }`.
4. `.hero-nav a`: añadir `transition: color 160ms ease, transform 160ms ease-out` y `.hero-nav a:active { transform: scale(0.97); }`.

## Fuera de alcance
Hover solo para mouse, FAQ, barra superior, aparición de secciones, foto de portada, reduced-motion (puntos 2–7 de la auditoría). No tocar HTML ni JS.

## Verificación
- Mantener el clic sobre un botón: se achica al instante y vuelve al soltar.
- Con "reducir movimiento" activo, no hay escala (la regla global ya anula transiciones).
