# SuperSplat Viewer


# 🚀 Visor de Gaussian Splatting (PlayCanvas Modificado)

Este proyecto es una aplicación web de visualización 3D construida utilizando la tecnología de PlayCanvas, específicamente una modificación del visor [SuperSplat Viewer](https://github.com/playcanvas/supersplat-viewer).

Permite a los usuarios cargar y visualizar modelos 3D en formatos compatibles, como Gaussian Splats (.splat) o .ply, directamente desde su máquina local.

## 🛠️ Modificaciones Realizadas

El código original ha sido modificado para:
1.  **Habilitar Carga Local:** Añadir un botón y la lógica de JavaScript para que el usuario pueda subir sus propios archivos de datos (.splat, .ply).
2.  **Inicio Vacío:** Deshabilitar la carga del modelo por defecto (`scene.compressed.ply`) para evitar errores 404 y empezar con un visor vacío.
3.  **Despliegue Vercel:** Ajustar los comandos de build para un despliegue exitoso en Vercel.

## 📝 Agradecimientos y Créditos

Este proyecto se basa en el código fuente abierto del equipo de PlayCanvas.

**Repositorio Original:**
* **Nombre:** PlayCanvas SuperSplat Viewer
* **URL:** [https://github.com/playcanvas/supersplat-viewer](https://github.com/playcanvas/supersplat-viewer)
* **Autor:** El equipo de PlayCanvas

Agradecemos al equipo de PlayCanvas por crear y compartir esta valiosa herramienta.


# SuperSplat Viewer

[![NPM Version](https://img.shields.io/npm/v/@playcanvas/supersplat-viewer)](https://www.npmjs.com/package/@playcanvas/supersplat-viewer)
[![NPM Downloads](https://img.shields.io/npm/dw/@playcanvas/supersplat-viewer)](https://npmtrends.com/@playcanvas/supersplat-viewer)
[![License](https://img.shields.io/npm/l/@playcanvas/supersplat-viewer)](https://github.com/playcanvas/supersplat-viewer/blob/main/LICENSE)
[![Discord](https://img.shields.io/badge/Discord-5865F2?style=flat&logo=discord&logoColor=white&color=black)](https://discord.gg/RSaMRzg)
[![Reddit](https://img.shields.io/badge/Reddit-FF4500?style=flat&logo=reddit&logoColor=white&color=black)](https://www.reddit.com/r/PlayCanvas)
[![X](https://img.shields.io/badge/X-000000?style=flat&logo=x&logoColor=white&color=black)](https://x.com/intent/follow?screen_name=playcanvas)

| [User Manual](https://developer.playcanvas.com/user-manual/gaussian-splatting/editing/supersplat/import-export/#html-viewer-htmlzip) | [Blog](https://blog.playcanvas.com) | [Forum](https://forum.playcanvas.com) |

This is the official viewer for [SuperSplat](https://superspl.at).

<img width="1114" height="739" alt="supersplat-viewer" src="https://github.com/user-attachments/assets/15d2c654-9484-4265-a279-99acb65e38c9" />

The web app compiles to a simple, self-contained static website.

The app supports a few useful URL parameters (though please note these are subject to change):
- `&settings=url` - specify the URL of the `settings.json` file (default is `./settings.json`)
- `&content=url` - specify the URL of the `scene.compressed.ply` file (default is `./scene.compressed.ply`)

Additional options:
- `&noui` - hide UI
- `&noanim` - start with animation paused
- `&poster=url` - show an image while loading the scene content
- `&ministats` - show the runtime CPU (and on desktop, GPU) performance graphs
- `&skybox=url` - specify an equirectangular skybox image for the skybox

The web app source files are available as strings for templating when you import the package from npm:

```ts
import { html, css, js } from '@playcanvas/supersplat-viewer';

// logs the source of index.html
console.log(html);

// logs the source of index.css
console.log(css);

// logs the source of index.js
console.log(js);
```

## Local Development

To initialize a local development environment for SuperSplat Viewer, ensure you have [Node.js](https://nodejs.org/) 18 or later installed. Follow these steps:

1. Clone the repository:

   ```sh
   git clone https://github.com/playcanvas/supersplat-viewer.git
   cd supersplat-viewer
   ```

2. Install dependencies:

   ```sh
   npm install
   ```

3. Start the development build and local web server:

   ```sh
   npm run develop
   ```

4. Open your browser at http://localhost:3000.

## Settings Schema

The `settings.json` file has the following schema (defined in TypeScript and taken from the SuperSplat editor):


```typescript
type AnimTrack = {
    name: string,
    duration: number,
    frameRate: number,
    target: 'camera',
    loopMode: 'none' | 'repeat' | 'pingpong',
    interpolation: 'step' | 'spline',
    smoothness: number,
    keyframes: {
        times: number[],
        values: {
            position: number[],
            target: number[],
        }
    }
};

type ExperienceSettings = {
    camera: {
        fov?: number,
        position?: number[],
        target?: number[],
        startAnim: 'none' | 'orbit' | 'animTrack',
        animTrack: string
    },
    background: {
        color?: number[]
    },
    animTracks: AnimTrack[]
};
```

### Example settings.json

```json
{
  "background": {"color": [0,0,0,0]},
  "camera": {
    "fov": 1.0,
    "position": [0,1,-1],
    "target": [0,0,0],
    "startAnim": "orbit"
  }
}
```
