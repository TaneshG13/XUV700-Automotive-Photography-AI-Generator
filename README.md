# Realistic Car Compositing with Stable Diffusion & ControlNet

This project demonstrates a professional workflow for creating photorealistic automotive advertisements using generative AI. The core task was to place a specific car model, the **Mahindra XUV700**, into nine distinct scenes across three Indian locations, ensuring maximum visual fidelity and brand accuracy.

This repository documents the **No-LoRA Inpainting and Compositing** method used to achieve these results.

![Showcase Banner](results/banner_placeholder.jpg) ## Table of Contents
- [Project Goal](#project-goal)
- [Rationale for Method](#rationale-for-method)
- [The Final Workflow](#the-final-workflow)
- [Technology Stack](#technology-stack)
- [Setup & Installation](#setup--installation)
- [Usage Guide](#usage-guide)
- [Showcase of Results](#showcase-of-results)
- [Future Improvements](#future-improvements)
- [Acknowledgments](#acknowledgments)

## Project Goal

The primary objective was to generate nine photorealistic images of a **silver Mahindra XUV700** in three distinct locations:
1.  **Mumbai:** The Bandra-Worli Sea Link
2.  **Jaipur:** In front of the Hawa Mahal
3.  **Nagpur Region:** A road in the Tadoba Forest

The key evaluation criteria were realism, consistency across the image set, and perfect accuracy to the source car model.

## Rationale for Method

A **No-LoRA Inpainting and Compositing** workflow was deliberately chosen over LoRA fine-tuning for two strategic reasons:
1.  **Guaranteed Model Accuracy:** By using cutouts from the official reference photos, the car's brand identity—its precise shape, grille, and details—is 100% accurate in every image. This eliminates the risk of generative "hallucinations" or model inaccuracies.
2.  **Demonstration of Compositing Skills:** This method showcases essential skills in digital compositing, lighting, and shadow work, which are critical for professional commercial imagery. It proves an ability to seamlessly blend real and AI-generated elements.

## The Final Workflow

The project was executed using a methodical, multi-stage process that combines AI generation with digital art techniques.

1.  **Asset Preparation:**
    * High-quality source images of the car were used to create transparent `.png` cutouts.
    * These cutouts were then used to generate corresponding **Depth Maps** for use with ControlNet.

2.  **Background Generation:**
    * The `txt2img` function was used with the `sd_xl_base_1.0.safetensors` model.
    * **ControlNet (Depth Model)** guided the AI to generate a scene with perspective and space that perfectly matched the intended car's shape and angle.

3.  **Compositing:**
    * The generated background and the corresponding car cutout were combined in an external image editor (e.g., Photoshop, GIMP).

4.  **Inpainting for Realism:**
    * The composite image was taken into the `Inpaint` tab for a two-pass blending process to add realistic shadows and environmental lighting.

## Technology Stack

* **Core Framework:** [AUTOMATIC1111's Stable Diffusion Web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
* **Primary Model:** `sd_xl_base_1.0.safetensors`
* **Key Extension:** `sd-webui-controlnet` by Mikubill
* **ControlNet Models:** `sdxl_canny_mid.safetensors`, `sdxl_depth_mid.safetensors`
* **Image Editor:** Any editor that supports layers and transparency (e.g., Adobe Photoshop, GIMP).

## Setup & Installation

To replicate this environment:

1.  Install the Automatic1111 Web UI.
2.  Install the `sd-webui-controlnet` extension from the `Extensions` tab.
3.  Download the `sd_xl_base_1.0.safetensors` checkpoint and place it in the `models/Stable-diffusion` folder.
4.  Download the SDXL-compatible ControlNet models ('mid' versions of Canny and Depth) and place them in the `extensions/sd-webui-controlnet/models` folder.
5.  Restart the Web UI.

## Usage Guide

1.  **Prepare Assets:** Create your car `.png` cutouts and `.png` depth maps.
2.  **Generate Background:** Use `txt2img` with a detailed prompt and the appropriate ControlNet depth map to generate a background scene.
3.  **Composite:** Combine the background and the corresponding car cutout in an image editor.
4.  **Inpaint:** Use the `Inpaint` tab to add shadows and lighting for the final touch.

### Example Prompt for Background Generation
```prompt
(masterpiece, best quality, ultra-realistic photograph), the road on the Bandra-Worli Sea Link in Mumbai with an empty space for a car, bright afternoon sun from the top-right creating soft shadows, shot on a Sony A7III with a 35mm lens, sharp focus
