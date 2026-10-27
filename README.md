<h1><img width="64px" src="ai_diffusion/icons/logo-128.png"> Generative AI <i>for Krita 5</i></h1>

> [!WARNING]
> **This Krita 5 (Qt5) port is in maintenance mode and no longer actively developed.**
> It continues as **[Diffusion for Krita](https://github.com/SHoogstad/diffusion-for-krita)**: one download for
> Krita 5.3 and Krita 6, with Runpod GPU support and new models. Please switch to it via the
> [new releases page](https://github.com/SHoogstad/diffusion-for-krita/releases) and report problems
> [there](https://github.com/SHoogstad/diffusion-for-krita/issues).
>
> This repository won't get new features. It may still get the occasional minor fix
> (for example a ComfyUI update for the local server), with no promises on timing.

> [!IMPORTANT]
> **This is an unofficial port** of [**Acly/krita-ai-diffusion**](https://github.com/Acly/krita-ai-diffusion)
> back to **Krita 5.x (PyQt5)**, with a few additions of my own.
> All credit for the plugin goes to [Acly](https://github.com/Acly) and the upstream contributors.
> Upstream moved to Qt6 / Krita 6 starting with version 1.54; this fork keeps new upstream
> releases running on **Krita 5.3** stable.
>
> Please report problems with this build [**here**](https://github.com/SHoogstad/krita-ai-diffusion-qt5/issues),
> not upstream. If you're on Krita 6, use the [original plugin](https://github.com/Acly/krita-ai-diffusion) instead.

⭳ [Download (this fork)](https://github.com/SHoogstad/krita-ai-diffusion-qt5/releases) | 🔀 [What's different](#fork) | ✨[Features](#features) | 🖼️[Gallery](#gallery) | 📖[User Guide (upstream)](https://docs.interstice.cloud) | 🏠 [Original project](https://github.com/Acly/krita-ai-diffusion)

## <a name="fork"></a> What's different in this fork

### Krita 5 port
* PyQt6 → PyQt5 (`QAction` back in `QtWidgets`, etc.), and the version check accepts Krita 5.x.
* Krita 5 doesn't expose its `DoubleSliderSpinBox` to Python, so the plugin has its own version for
  the strength and settings sliders: drag the bar to change the value, or double-click it to type one. **Krita 5.3 is the target and the tested version.**
* Otherwise the code stays as close to upstream as possible. New upstream releases are merged and
  ported again.

### Updates come from this fork
* The built-in updater checks **this repository's** GitHub releases, not upstream's, so it never
  offers you a Qt6-only build. Downloads are verified against the SHA-256 digest that GitHub publishes.
* **Configure ▸ Plugin ▸ Include Pre-releases** opts in to pre-release builds. If you installed a
  pre-release, you keep getting newer pre-releases.

### Extra models (1.55)
Not available upstream (yet), included since 1.55:
* **MOSS-Image**: text-to-image with a Qwen3.5-9B text encoder. **Regions** are converted to
  MOSS's JSON layout boxes (bounding box + caption per region), and region prompts with quoted text
  (e.g. a neon sign saying `"OPEN"`) become text boxes. Needs ComfyUI 0.42 or newer.
* **Fibo 2** (Dev, generate + edit) and **Fibo 2 Edit** (Edit Turbo, 4 steps). Prompts go through
  `TextEncodeFibo2`, so the text encoder also sees the edit and reference images. Reference images are
  called `<image_N>` in instructions. Large canvases are generated at about 1 MP (the training resolution)
  and then upscaled, which avoids duplicated limbs. Needs ComfyUI master.
* Both use the Flux 2 VAE and are detected by filename. They only show up if the connected ComfyUI
  supports them; otherwise you get an "update ComfyUI" hint.

### Versioning
Release tags look like `v<plugin version>-krita5.3`, for example `v1.54.1-krita5.3`. The plugin version
follows upstream (fork-only features bump the minor version, as in 1.55), and the suffix names the **target Krita version**, not a build number.

| Release | Based on | Channel |
|---|---|---|
| `v1.55.3-krita5.3` | upstream 1.54 + MOSS-Image / Fibo 2, slider fix | stable (latest) |
| `v1.55.2-krita5.3` | upstream 1.54 + MOSS-Image / Fibo 2 | previous stable |
| `v1.55.0`, `v1.55.1` | same, earlier builds | pre-release |
| `v1.54.1-krita5.3` | upstream 1.54 | older stable |

---

## About the plugin (from upstream)

This is a plugin to use generative AI in image painting and editing workflows
from within Krita. Visit
[**www.interstice.cloud**](https://www.interstice.cloud) for an introduction. Learn how to use it on
[**docs.interstice.cloud**](https://docs.interstice.cloud). The guides apply to this port as well,
except for installation and updates (see below).

The main goals of this project are:
* **Precision and Control.** Creating entire images from text can be unpredictable.
  To get the result you envision, you can restrict generation to selections,
  refine existing content with a variable degree of strength, focus text on image
  regions, and guide generation with reference images, sketches, line art,
  depth maps, and more.
* **Workflow Integration.** Most image generation tools focus heavily on AI parameters.
  This project aims to be an unobtrusive tool that integrates and synergizes
  with image editing workflows in Krita. Draw, paint, edit and generate seamlessly without worrying about resolution and technical details.
* **Local, Open, Free.** We are committed to open source models. Customize presets, bring your
  own models, and run everything local on your hardware. Cloud generation is also available
  to get started quickly without heavy investment.  

[![Watch video demo](media/screenshot-video-preview.webp)](https://youtu.be/Ly6USRwTHe0 "Watch video demo")

## <a name="features"></a> Features

* **Inpainting**: Use selections for generative fill, expand, to add or remove objects
* **Live Painting**: Let AI interpret your canvas in real time for immediate feedback. [Watch Video](https://youtu.be/AF2VyqSApjA?si=Ve5uQJWcNOATtABU)
* **Upscaling**: Upscale and enrich images to 4k, 8k and beyond without running out of memory.
* **Diffusion Models**: Flux 2, Z-Image, Stable Diffusion 1.5, XL, Illustrious
* **Edit Models**: Make modifications to images via text instructions
* **ControlNet**: Scribble, Line art, Canny edge, Pose, Depth, Normals, Segmentation, +more
* **IP-Adapter**: Reference images, Style and composition transfer, Face swap
* **Regions**: Assign individual text descriptions to image areas defined by layers.
* **Job Queue**: Queue and cancel generation jobs while working on your image.
* **History**: Preview results and browse previous generations and prompts at any time.
* **Strong Defaults**: Versatile default style presets allow for a streamlined UI.
* **Customization**: Create your own presets - custom checkpoints, LoRA, samplers and more.

## <a name="installation"></a> Getting Started

See the [Plugin Installation Guide](https://docs.interstice.cloud/installation) for instructions.

A concise (more technical) version is below:

### Operating System

Windows, Linux, MacOS

#### Hardware support

To run locally a powerful graphics card with at least 6 GB VRAM (NVIDIA) is
recommended. Otherwise generating images will take very long or may fail due to
insufficient memory!

<table>
<tr><td>NVIDIA GPU</td><td>supported via CUDA (Windows/Linux)</td></tr>
<tr><td>AMD GPU</td><td>supported via ROCm (Windows/Linux)</td></tr>
<tr><td>Intel GPU</td><td>supported via XPU (Windows/Linux)</td></tr>
<tr><td>Apple Silicon</td><td>MPS on macOS 14+</td></tr>
<tr><td>CPU</td><td>supported, but very slow</td></tr>
</table>


### Installation

1. Install [Krita](https://krita.org/) **5.3** (5.2 may work; on Krita 6 use [upstream](https://github.com/Acly/krita-ai-diffusion/releases/latest) instead).
1. Download `krita_ai_diffusion-<version>-krita5.3.zip` from [this fork's releases](https://github.com/SHoogstad/krita-ai-diffusion-qt5/releases).
   It replaces the upstream plugin if that's installed (same `ai_diffusion` folder). Your settings and server stay.
2. Start Krita and install the plugin via Tools ▸ Scripts ▸ Import Python Plugin from File...
    * Point it to the ZIP archive you downloaded in the previous step.
    * Check [Krita's official documentation](https://docs.krita.org/en/user_manual/python_scripting/install_custom_python_plugin.html) for more options.
3. Restart Krita and create a new document or open an existing image.
4. To show the plugin docker: Settings ‣ Dockers ‣ AI Image Generation.
5. In the plugin docker, click "Configure" to start local server installation or connect.

> [!NOTE]
> If you encounter problems please check the [FAQ / list of common issues](https://docs.interstice.cloud/common-issues) for solutions.
>
> If an issue is specific to this Krita 5 build (Qt errors, updater, MOSS-Image / Fibo 2), report it
> [on this fork](https://github.com/SHoogstad/krita-ai-diffusion-qt5/issues). Before opening an issue upstream,
> check that it also happens with the original plugin on Krita 6. Please note that official Krita channels are **not** the right place to seek help with
> issues related to this extension!

### _Optional:_ Custom ComfyUI Server

The plugin uses [ComfyUI](https://github.com/comfyanonymous/ComfyUI) as backend.
As an alternative to the automatic installation, you can install it manually or
use an existing installation. If the server is already running locally before
starting Krita, the plugin will automatically try to connect. Using a remote
server is also possible this way.

Please check the list of [required extensions and models](https://docs.interstice.cloud/comfyui-setup) to make sure your installation is compatible.

### _Optional:_ Object selection tools (Segmentation)

If you're looking for a way to easily select objects or remove background in the
image, there is a [separate plugin](https://github.com/Acly/krita-ai-tools)
which adds AI segmentation tools.


## Contributing

Fixes for the Krita 5 port are welcome here. Make feature work against
[upstream](https://github.com/Acly/krita-ai-diffusion) where possible, and it will reach this fork with the next merge.
See the [contributing guide](CONTRIBUTING.md).

## <a name="gallery"></a> Gallery

_Live painting with regions (Click for video)_
[![Watch video demo](media/screenshot-regions.png)](https://youtu.be/PPxOE9YH57E "Watch video demo")

_Inpainting on a photo using a realistic model_
<img src="media/screenshot-2.png">

_Reworking and adding content to an AI generated image_
<img src="media/screenshot-1.png">

_Adding detail and iteratively refining small parts of the image_
<img src="media/screenshot-3.png">

_Modifying the pose vector layer to control character stances (Click for video)_
[![Watch video demo](media/screenshot-5.png)](https://youtu.be/-QDPEcVmdLI "Watch video demo")

_Control layers: Scribble, Line art, Depth map, Pose_
![Scribble control layer](media/control-scribble-screen.png)
![Line art control layer](media/control-line-screen.png)
![Depth map control layer](media/control-depth-screen.png)
![Pose control layer](media/control-pose-screen.png)

## Technology

* Image generation: [Stable Diffusion](https://github.com/Stability-AI/generative-models), [Flux](https://blackforestlabs.ai/)
* Diffusion backend: [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
* Inpainting: [ControlNet](https://github.com/lllyasviel/ControlNet), [IP-Adapter](https://github.com/tencent-ailab/IP-Adapter)

## License & credits

Original plugin © [Acly](https://github.com/Acly) and contributors, licensed under [GPL-3.0](LICENSE).
This port is distributed under the same license. It is not affiliated with or endorsed by the upstream project or Interstice.
