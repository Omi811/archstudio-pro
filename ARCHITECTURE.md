# 📐 ArchStudio PRO — Technical Architecture & Engineering Specification (`ARCHITECTURE.md`)

This document details the internal engineering architecture, mathematical models, 3D rendering pipeline, and CAD interoperability specifications powering **ArchStudio PRO**.

---

## 1. System Architecture Overview

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                        ArchStudio PRO Client (React 19)                     │
├──────────────────┬──────────────────┬──────────────────┬────────────────────┤
│  3D Studio Pro   │ 3D Asset & File  │  Batch 3D Mesh   │   Universal CAD    │
│  (Three.js PBR)  │ Inspector Panel  │  Optimizer Modal │   Bridge Studio    │
└────────┬─────────┴────────┬─────────┴────────┬─────────┴─────────┬──────────┘
         │                  │                  │                   │
         ▼                  ▼                  ▼                   ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                   Decoupled Pure TypeScript Domain Modules                  │
│  • assetInspectorLogic.ts  (VRAM, triangle/vertex counters, file classifier)│
│  • batchOptimizerLogic.ts  (QEM decimation, KTX2/WebP compression metrics)  │
│  • cadBridgeLogic.ts       (AutoCAD DXF, 3ds Max .ms, Blender .py, SKP .rb) │
│  • architectureLogic.ts    (6-phase WBS critical path, BOQ rate calculator) │
│  • githubPagesLogic.ts     (GitHub Pages URL builder & static AI engine)    │
└──────────────────────────────────────┬──────────────────────────────────────┘
                                       │
         ┌─────────────────────────────┴─────────────────────────────┐
         ▼ (Cloud / Full-Stack Mode)                                 ▼ (GitHub Pages Static Mode)
┌─────────────────────────────────────────┐       ┌─────────────────────────────────────────┐
│ Express Server (server.ts)              │       │ Standalone Browser Runtime              │
│ • POST /api/chat (@google/genai)        │       │ • Relative Asset Loader (base: './')    │
│ • POST /api/github/device/start         │       │ • Client-Side Architectural AI Engine   │
│ • POST /api/github/auto-publish         │       │ • Local Blob Exporters (.GLTF/.OBJ/.DXF)│
└─────────────────────────────────────────┘       └─────────────────────────────────────────┘
```

---

## 2. 3D Rendering & Asset Inspection Pipeline

### 2.1 Physically Based Rendering (PBR) Setup
* **Tone Mapping:** `THREE.ACESFilmicToneMapping` with `toneMappingExposure = 1.15` for photorealistic highlight roll-off.
* **Environment Lighting:** Procedural `RoomEnvironment` processed through `THREE.PMREMGenerator` for realistic metallic and dielectric specular reflections without external HDR network bottlenecks.
* **Shadow Mapping:** `THREE.PCFShadowMap` with $2048 \times 2048$ shadow map resolution and radial canvas contact shadows under furniture plinths.
* **Exponential Camera Damping:** Orbital and preset camera transitions use frame-rate independent exponential smoothing:
  $$\alpha = 1 - e^{-k \cdot \Delta t}$$

### 2.2 Texture VRAM & Geometry Memory Estimation (`src/utils/assetInspectorLogic.ts`)
* **Texture VRAM Calculation:** Given texture dimensions $(W \times H)$ and channel depth $C \in \{3, 4\}$, including the standard mipmap pyramid overhead ($\approx 33\%$):
  $$\text{VRAM}_{\text{texture}} = \text{round}\left(W \times H \times C \times 1.33\right) \text{ bytes}$$
* **Vertex Buffer Memory:** Calculated at $32\text{ bytes/vertex}$ (Position `vec3` $12\text{B}$ + Normal `vec3` $12\text{B}$ + UV `vec2` $8\text{B}$).

---

## 3. Automated Batch 3D Optimization (`src/utils/batchOptimizerLogic.ts`)

The Batch Processing engine processes queues of `.OBJ`, `.GLB`, `.GLTF`, and `.FBX` files simultaneously:
1. **Polygon Decimation:** Applies target reduction ratio $r \in [0.10, 0.85]$ and optional hard triangle ceiling $T_{\max}$:
   $$T_{\text{opt}} = \max\left(4, \min\left(T_{\text{orig}}, \lfloor T_{\text{orig}} \cdot (1 - r) \rfloor, T_{\max}\right)\right)$$
2. **Texture Supercompression:** Models GPU transcoding savings across **Basis Universal (`KTX2`)**, **WebP**, and **JPEG/PNG Crush**, plus resolution clamping ($1024^2$, $2048^2$, $4096^2$).

---

## 4. CAD & 3D Software Interoperability Standards (`src/utils/cadBridgeLogic.ts`)

| Target Suite | Native Format | Coordinate System | Layer / Node Standard |
| :--- | :--- | :--- | :--- |
| **Autodesk AutoCAD** | `.DXF` (ASCII `AC1015`) | 2D Plan ($X, Y$ Inches) | AIA Layers: `A-WALL` (Color 4), `A-FURN` (Color 2), `A-DIM` (Color 1) |
| **Autodesk 3ds Max** | `.ms` (MaxScript) & `.OBJ` | Z-Up (`#Inches`) | `Box` primitives, `Physical_Camera` (35mm lens), Directional Sun |
| **Blender 4.x** | `.py` (`bpy`) & `.GLTF` | Z-Up (`METRIC` $1.0\text{m}$) | `ShaderNodeBsdfPrincipled` PBR materials + 35mm Camera |
| **Trimble SketchUp** | `.rb` (Ruby API) & `.SKP` | Z-Up (Feet/Inches) | `Sketchup.active_model.entities` grouped with `ArchStudio_Room` tag |

---

## 5. GitHub Pages Static Readiness

To ensure zero-config compatibility with GitHub Pages (`https://omi811.github.io/archstudio-pro/`):
1. **`vite.config.ts`:** Sets `base: './'` so all bundled assets load relatively regardless of repository subpath.
2. **`public/.nojekyll`:** Prevents GitHub Pages' Jekyll processor from ignoring underscore-prefixed files.
3. **`public/404.html`:** Preserves Single-Page Application (SPA) routing on direct subpath refreshes.
4. **`.github/workflows/deploy.yml`:** Builds the production bundle on Ubuntu with Node 22 and deploys via `actions/deploy-pages@v4`.
