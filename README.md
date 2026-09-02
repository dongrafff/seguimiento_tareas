# 17 · GitHub Seguimiento

Copia web del proyecto **01 Seguimiento_tareas**, montable en **GitHub Pages** con las
tareas guardadas directamente en el repo (`data/datos.json`). Así **no hay que importar
nada cada vez que se abre**: al cargar la app, baja tus tareas de GitHub; al cambiarlas,
se suben solas.

## Cómo funciona

- `index.html` es una sola página (misma app que antes) con un módulo de sincronización añadido.
- **Fuente de verdad:** el archivo `data/datos.json` del repo (mismo formato que los respaldos `datos_T3.json`).
- Al abrir: carga desde GitHub → si no está configurado, usa carpeta/localStorage como antes.
- Al guardar cualquier cambio: se programa una subida a GitHub (con *debounce*, no satura la API).

## Despliegue en 4 pasos

1. **Crear el repo** vacío en GitHub (público o privado), p.ej. `seguimiento-tareas`.
2. **Subir este proyecto**:
   ```bash
   git add -A && git commit -m "Seguimiento de tareas con sync a GitHub"
   git branch -M main
   git remote add origin https://github.com/<TU_USUARIO>/seguimiento-tareas.git
   git push -u origin main
   ```
3. **Activar GitHub Pages** en el repo: `Settings → Pages → Source = Deploy from a branch`
   (o esperar al primer deploy del workflow `.github/workflows/pages.yml`, que publica solo `index.html` + `data/`).
4. Abrir la URL de Pages (`https://<TU_USUARIO>.github.io/seguimiento-tareas/`) y, en la barra de datos,
   clic en **⚙️ GitHub** → llenar *Owner*, *Repo* y un **token**, botón **Guardar y probar**.

> La primera vez que guardas desde la app se crea actualiza `data/datos.json` con tus tareas.
> El repo ya trae un `data/datos.json` semilla (16 tareas del T3) — puedes editarlo o dejarlo.

## Token de GitHub (necesario para *guardar*)

La **lectura** funciona sin token si el repo es público; para **escribir** desde la app
hace falta un token con permiso `Contents`:

- **Fine-grained PAT (recomendado):** `Settings → Developer settings → Fine-grained tokens`
  - *Access:* solo el repo `seguimiento-tareas`.
  - *Permissions:* **Contents → Read and write**.
  - Copia el token (`github_pat_…`) y pégalo en el modal ⚙️ GitHub.
- El token vive **solo en tu navegador** (localStorage) — no queda committeado.

## Archivos

| Ruta | Rol |
|---|---|
| `index.html` | La app + módulo de sync con GitHub |
| `data/datos.json` | Tus tareas (fuente de verdad, se actualiza sola) |
| `.github/workflows/pages.yml` | Publica la app en GitHub Pages |

## Notas / límites

- El token se guarda por navegador; cada equipo debe configurarlo una vez.
- Imágenes muy grandes (>~400 KB como dataURL) se refieren a `imagenes/<uid>.png` para no inflar el repo.
- Para empezar de cero en otro equipo: basta abrir la URL y poner owner/repo/token — las tareas ya están ahí.
