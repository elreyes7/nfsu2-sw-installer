# nfsu2-sw installer (ES / EN)

🌐 **Web Installer / Instalador Web:** [https://elreyes7.github.io/nfsu2-sw-installer/](https://elreyes7.github.io/nfsu2-sw-installer/)

*[🇪🇸 Español](#español) | [🇺🇸 English](#english)*

---

<a name="español"></a>
## 🇪🇸 Español

Página instaladora para **nfsu2-sw** (`nfsu2x`), el port nativo de **Need for Speed: Underground 2** (Xbox original) para **Nintendo Switch**:  
👉 **[https://elreyes7.github.io/nfsu2-sw-installer/](https://elreyes7.github.io/nfsu2-sw-installer/)**

Le entregas tu propia copia del juego de Xbox original (una imagen de disco — volcado completo o XISO — o la carpeta del disco extraído con su `default.xbe`) y genera un archivo `.zip` listo para extraer en `sdmc:/switch/`. Todo se ejecuta localmente en tu navegador: los archivos de tu juego nunca salen de tu computadora.

Este proyecto está inspirado y adaptado a partir de `defjam-sw-installer` / `the-simpsons-game-nx-installer` y `nfsmw-nx-installer` de StevensND: mantiene el flujo de tres pasos, lectura de imágenes XISO en el navegador y generación de paquetes ZIP64 en streaming de varios GB directo a disco.

### Qué hace

1. **Detecta y valida `default.xbe`** (dentro de la imagen XISO `.iso`/`.xiso`, o dentro de la carpeta seleccionada) para la versión NTSC-U de Xbox (Title ID `4541006F`).
2. **Incluye el ejecutable de Switch (`nfsu2x-vulkan.nro` / `nfsu2x.nro`)** descargado desde la sección de *Releases* (o cargado localmente).
3. **Genera el archivo `nfsu2x_env.txt` optimizado para consola** (con `NFSU2_NO_LOG=1` y `RECOMP_NX_PROFILE=0` para evitar escrituras constantes en la microSD, escala `1.5x`, pantalla ancha `16:9`, decodificador `NFSU2_NATIVE_VP6=1` y perfiles de reloj).
4. **Construye el paquete `.zip` en streaming (ZIP64):**
   * **Instalación completa (`nfsu2x.zip`):** Empaqueta el ejecutable `.nro`, `nfsu2x_env.txt` y todos los archivos del disco bajo `switch/nfsu2x/game/`.
   * **Actualización (`nfsu2x-update.zip`):** Empaqueta únicamente el ejecutable `.nro` y la configuración `nfsu2x_env.txt` sin volver a copiar los archivos del juego.

### Estructura del repositorio

| Ruta | Contenido |
| :--- | :--- |
| `index.html` | Interfaz web bilingüe (Español / Inglés), lector de imágenes XISO de Xbox y empaquetador ZIP64 en streaming |
| `release/` / *Releases* | Binarios compilados (`nfsu2x-vulkan.nro`, `nfsu2x.nro`) y plantilla de configuración `nfsu2x_env.txt` |
| `.github/workflows/deploy.yml` | Flujo de GitHub Actions que descarga el `.nro` desde *Releases* (superando el límite web de 25 MB) y publica el sitio en GitHub Pages |

### Despliegue y cómo subir el `.nro` (> 25 MB)

La interfaz web de GitHub impide subir archivos mayores a 25 MB directamente al código, por lo que **el archivo `.nro` no se sube arrastrándolo a la pestaña Code**:

1. Ve a la sección **Releases** de tu repositorio (`https://github.com/elreyes7/nfsu2-sw-installer/releases/new`) y sube allí tu `nfsu2x-vulkan.nro` / `nfsu2x.nro` (GitHub Releases permite archivos de hasta **2 GB** desde el navegador).
2. El flujo de trabajo en `.github/workflows/deploy.yml` descarga automáticamente el `.nro` de tu último Release y lo inyecta en GitHub Pages al publicar la página (configura *Settings > Pages > Build and deployment > Source: GitHub Actions*).

### Licencia y avisos legales

Distribuido bajo licencia **GPL-3.0** (`LICENSE`), al igual que `nfsmw-nx-installer` y `defjam-sw-installer`.

*Need for Speed™: Underground 2* © 2004 Electronic Arts Inc. Este es un proyecto fan no oficial y no está afiliado, respaldado ni patrocinado por Electronic Arts Inc., Microsoft ni Nintendo. Este sitio no aloja ni distribuye imágenes de disco ni archivos originales del juego.

---

<a name="english"></a>
## 🇺🇸 English

The web installer page for **nfsu2-sw** (`nfsu2x`), the native **Nintendo Switch** port of **Need for Speed: Underground 2** (original Xbox):  
👉 **[https://elreyes7.github.io/nfsu2-sw-installer/](https://elreyes7.github.io/nfsu2-sw-installer/)**

You give it your own copy of the original Xbox game (a disc image — full dump or XISO — or the extracted disc folder with its `default.xbe`) and it gives you a `.zip` ready to extract into `sdmc:/switch/`. Everything runs in your browser: the game files never leave your computer.

Adapted from `defjam-sw-installer` / `the-simpsons-game-nx-installer` and `nfsmw-nx-installer` by StevensND: the same three steps, in-browser Xbox XISO disc reader, and streaming ZIP64 writer capable of packaging several GB straight to disk.

### What it does

1. **Finds `default.xbe`** (inside the `.iso`/`.xiso` disc image, or inside the chosen folder) for the Xbox NTSC-U release (Title ID `4541006F`).
2. **Bundles `nfsu2x-vulkan.nro` / `nfsu2x.nro`** fetched from the repository's *Releases* (or provided locally).
3. **Generates a console-optimized `nfsu2x_env.txt`** (`NFSU2_NO_LOG=1` and `RECOMP_NX_PROFILE=0` to prevent SD card stuttering, `1.5x` resolution scale, `16:9` widescreen, native `NFSU2_NATIVE_VP6=1`, and clock profiles).
4. **Streams the `.zip` package (ZIP64):**
   * **First installation (`nfsu2x.zip`):** Bundles the `.nro` executable, `nfsu2x_env.txt` settings, and all disc files under `switch/nfsu2x/game/`.
   * **Update package (`nfsu2x-update.zip`):** Bundles only the `.nro` executable and `nfsu2x_env.txt` without copying the game files again.

### Layout

| Path | Contents |
| :--- | :--- |
| `index.html` | Single-file web interface (Spanish & English), Xbox XISO reader, and streaming ZIP64 packager |
| `release/` / *Releases* | Switch binaries (`nfsu2x-vulkan.nro`, `nfsu2x.nro`) and default `nfsu2x_env.txt` |
| `.github/workflows/deploy.yml` | GitHub Actions workflow that pulls the `.nro` asset from *Releases* and deploys the site to GitHub Pages |

### Deployment

The `.nro` binary is over 25 MB, so it is not uploaded through GitHub's web file editor. Instead, it is attached as a Release asset in `elreyes7/nfsu2-sw-installer`. The workflow in `.github/workflows/deploy.yml` downloads the `.nro` from the latest release and publishes the complete site to GitHub Pages. Pages must be set to deploy from **GitHub Actions** (*Settings > Pages > Source*).

### Licence

GPL-3.0 (`LICENSE`), as `nfsmw-nx-installer` and `defjam-sw-installer`.

*Need for Speed™: Underground 2* © 2004 Electronic Arts Inc. This is an unofficial fan project, not affiliated with or endorsed by Electronic Arts, Microsoft, or Nintendo.
