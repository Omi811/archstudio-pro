# 🏛️ ArchStudio PRO — 3D Architecture, CAD Bridge & Spatial Intelligence Workspace

[![Live Cloud App](https://img.shields.io/badge/Live_Cloud_App-Active-10b981?style=for-the-badge)](https://ais-pre-iv5bjg2c3ptul7pzpsg7ib-641552886067.asia-northeast1.run.app)
[![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-omi811.github.io-f59e0b?style=for-the-badge)](https://omi811.github.io/archstudio-pro/)
[![GitHub Profile](https://img.shields.io/badge/GitHub-@Omi811-181717?style=for-the-badge&logo=github)](https://github.com/Omi811)

**ArchStudio PRO** is an Apple-grade, spatial intelligence and 3D architectural workspace engineered for **interior designers, architects, visualizers, and turnkey construction clients**. It unifies real-time Three.js PBR 3D visualization, live mesh & VRAM telemetry, automated batch 3D optimization, universal CAD/DCC interoperability (**Autodesk 3ds Max, Blender 4.x, Trimble SketchUp, and Autodesk AutoCAD**), 6-phase Work Breakdown Structures (WBS), and itemized Bill of Quantities (BOQ) estimation in a single Cupertino-inspired web application.

---

## 🌐 Live Links

* **Instant Cloud Live App:** [https://ais-pre-iv5bjg2c3ptul7pzpsg7ib-641552886067.asia-northeast1.run.app](https://ais-pre-iv5bjg2c3ptul7pzpsg7ib-641552886067.asia-northeast1.run.app)
* **GitHub Pages Production URL:** [https://omi811.github.io/archstudio-pro/](https://omi811.github.io/archstudio-pro/)
* **GitHub Repository:** [https://github.com/Omi811/archstudio-pro](https://github.com/Omi811/archstudio-pro)

---

## ✨ Core Features & Modules

### 1. 🧊 Interactive 3D Studio Pro (Three.js WebGL PBR)
* **Composite Procedural Architectural Room:** 25+ individual 3D architectural and furniture sub-meshes (`Room_Floor_Slab`, `Coffee_Table_Fluted_Base`, `Sofa_Seat_Cushions`, `Brushed_Brass_Tray`, `Lamp_Spun_Cone_Shade`, `Window_Clear_Glazing`).
* **Real-Time Style Presets:** Switch seamlessly between **Modern Japandi**, **Industrial Loft**, **Scandinavian Minimal**, and **Luxury Contemporary**.
* **Atmospheric Lighting Simulation:** Toggle **Daylight Sun**, **Golden Hour Sunset**, and **Night Architectural Cove & Accent Lighting** with ACESFilmic tone mapping and `RoomEnvironment` IBL reflections.
* **Camera Framing & Calipers:** Smooth exponentially damped camera transitions across **Isometric 3D**, **Top-Down Plan**, and **Eye-Level** views, plus live dimensional caliper overlays.
* **Direct Scene Exporters:** 1-click export to `.GLTF`, `.OBJ`, and high-resolution client render `.PNG` snapshots.

### 2. 🔍 3D Asset Inspector & Universal File Ingestion Hub
* **Scene Telemetry:** Live polygon/triangle counter (`△`), vertex counter, draw call tracking, and estimated GPU Texture VRAM usage (including $\times 1.33$ mipmap chain overhead).
* **Live PBR Shader Controls:** Select any 3D component in the viewport or inspector list to adjust **Roughness** ($0–100\%$), **Metalness** ($0–100\%$), **Base Albedo Hex Color**, and **Wireframe Mode** in real time.
* **Universal File Ingestion (`*/*`):** Drag and drop any project file format with automatic software classification and 1-click **Ask AI** technical audit:
  * **3D Formats:** `.glb`, `.gltf`, `.obj`, `.fbx`, `.stl`, `.ply`, `.3ds`
  * **CAD & BIM Suites:** `.dwg`, `.dxf`, `.skp`, `.blend`, `.max`, `.ifc`, `.rvt`
  * **2D Blueprints & Site Photos:** `.png`, `.jpg`, `.jpeg`, `.webp`, `.svg`
  * **Costing & BOQ Spreadsheets:** `.csv`, `.xlsx`, `.xls`
  * **Specifications & Quotes:** `.pdf`, `.docx`, `.txt`

### 3. ⚡ Batch 3D Processing & Mesh Optimizer
* **Multi-File Queue:** Simultaneously optimize multiple `.OBJ` and `.GLB` 3D assets.
* **Automated Polygon Reduction:** Configurable decimation ratio ($10\%$ to $85\%$), hard triangle ceiling limits, UV seam preservation, and choice of **Quadric Error Metrics (QEM)**, **Planar Edge Collapse**, or **Boundary Preserving** decimation.
* **Automated Texture Compression:** Compress textures to **Basis Universal (`KTX2`)**, **WebP**, or **JPEG/PNG Crush** with max resolution clamping ($1024\text{px}$, $2048\text{px}$, $4096\text{px}$).
* **1-Click Export:** Download individual optimized `.OBJ`/`.GLTF` files and a complete JSON optimization audit manifest.

### 4. 🔗 Universal CAD & 3D DCC Bridge
Zero-distortion script and geometry generators tailored for all 4 major desktop architectural suites:
* **Autodesk 3ds Max (`.ms` MaxScript & `.OBJ`):** Generates parametric room boxes, `Physical_Camera` with 35mm architectural lens, and system unit scaling (`#Inches` / `#Generic`).
* **Blender 4.x (`.py` Python & `.GLTF`):** Generates an automated `bpy` script with **Principled BSDF** shader nodes, metric scaling, and 3-point architectural area lighting.
* **Trimble SketchUp Pro (`.rb` Ruby Console & `.SKP`):** Automates floor slab and wall group creation with organized tags/layers.
* **Autodesk AutoCAD (`.DXF` ASCII):** Live compliant ASCII `.DXF` generator pre-configured with **AIA National CAD Standard layers** (`A-WALL`, `A-FURN`, `A-DIM`).

### 5. 🗓️ 6-Phase WBS Timeline & 📊 BOQ Pro Calculator
* **Work Breakdown Structure (WBS):** Interactive 6-phase critical-path schedule covering Schematic Design, Demolition & Civil, MEP & HVAC, False Ceiling, Factory Millwork, and Handover Snagging.
* **Bill of Quantities (BOQ) Estimator:** Dynamic cost calculator scaling across **Standard**, **Premium**, and **Ultra-Luxury** material tiers with CSV export.
* **Materials & Surfaces Matrix:** Side-by-side comparison of **Sintered Stone (Dekton)**, **Engineered Quartz**, **Full-Body Porcelain Slabs**, **Natural Italian Statuario Marble**, and **Marine-Grade IS-710 BWR Plywood**.

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend Framework** | React 19 + TypeScript + Vite 8 (`base: './'` for static & subpath hosting) |
| **3D Engine** | Three.js (`WebGLRenderer`, `RoomEnvironment`, `GLTFExporter`, `OBJExporter`, `GLTFLoader`, `OBJLoader`) |
| **Styling & UI** | Tailwind CSS 4 (Cupertino dark titanium & frosted glass aesthetic) + Lucide Icons |
| **Backend & AI Proxy** | Node.js + Express (`server.ts`) + `@google/genai` (with Google Search grounding & standalone static fallback) |
| **Testing** | Node.js native test runner (`tsx --test`) — 26 unit tests covering BOQ, WBS, CAD Bridge, Asset Inspector, Batch Optimizer & GitHub Pages |

---

## 🚀 Local Development & Testing

```bash
# 1. Install dependencies
npm install

# 2. Start the full-stack development server on http://localhost:3000
npm run dev

# 3. Run the complete unit test suite (26 tests)
npx tsx --test src/utils/architectureLogic.test.ts src/utils/cadBridgeLogic.test.ts src/utils/assetInspectorLogic.test.ts src/utils/batchOptimizerLogic.test.ts src/utils/githubPagesLogic.test.ts

# 4. Type-check and build the static production bundle (./dist)
npm run lint
npm run build
```

---

## 📦 Publishing to GitHub Pages (`@Omi811`)

This repository includes a pre-configured GitHub Actions workflow (`.github/workflows/deploy.yml`), relative asset paths (`base: './'` in `vite.config.ts`), `public/.nojekyll`, and `public/404.html`.

### Option A: 1-Click In-App Auto-Publish
1. Click the green **Publish / Live Link** button in the top navigation bar.
2. Copy the 8-digit GitHub Device Code and authorize at [https://github.com/login/device](https://github.com/login/device).
3. The server automatically creates `Omi811/archstudio-pro`, pushes the compiled `dist/` bundle to `gh-pages`, and activates `https://omi811.github.io/archstudio-pro/`.

### Option B: Standard Git Push (Automated via GitHub Actions)
```bash
git init
git add .
git commit -m "feat: publish ArchStudio PRO 3D & CAD Workspace to GitHub Pages"
git branch -M main
git remote add origin https://github.com/Omi811/archstudio-pro.git
git push -u origin main
```
In your GitHub repository **Settings → Pages → Source**, select **GitHub Actions** (or **Deploy from a branch → `gh-pages`**).

---

## 📄 Additional Documentation
* See [**`ARCHITECTURE.md`**](./ARCHITECTURE.md) for deep-dive technical specifications on the 3D PBR pipeline, CAD file generators, VRAM formulas, and static deployment architecture.
