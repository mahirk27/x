# Case-Study Documentation

## Overview
This is a simple task that requires creating a workflow using **ComfyUI** that takes an input image and
generates a Van Gogh style version of it using Stable Diffusion and ControlNet. This workflow includes image style transfer techniques and advanced models to show my ability to work with ComfyUI

## Getting Started
### Prerequisites
- Python 3.10
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [ComfyUI-Manager](https://github.com/ltdrdata/ComfyUI-Manager)
- [Van Gogh Diffusion-V1](https://civitai.com/models/91/van-gogh-diffusion)
- [ControlNet Models (Canny, Depth, Sketch)](https://huggingface.co/TencentARC/T2I-Adapter)
- [4x-UltraSharp Upscaler](https://civitai.com/models/116225/4x-ultrasharp)
- [KJ-Nodes for Image Processing](https://github.com/kijai/ComfyUI-KJNodes)

### Setting up  the Project
1. Setting up the environment:
   - Create a virtual environment with **Python 3.10**
   - Activate the virtual environment to prevent conflicts
2. Installation:
   - Install ComfyUI from source in your virtual environment
   - Install ComfyUI-Manager
   - Download custom model weights and place them under **ComfyUI/models/checkpoints**
   - Load custom workflow
   - Install the missing nodes via ComfyUI-Manager or Install them from sources provided
3. Usage:
   - Select an input image.
   - Configure hyperparameters of ControlNet models and Custom Stable Diffusion Model(currently using recommended model parameters provided by the owner of Diffusion model)
   - Select positive and negative prompts referring to [Diffusion Model Card](https://huggingface.co/dallinmackay/Van-Gogh-diffusion)
   - Run the workflow

## Workflow
To provide a clearer explanation of the workflow, it has been divided into three sections.

### Section 1:

![Custom Model Configuration](/workflow_imgs/workflow_img0.png)
Here we can select Custom Diffusion Models Hyperparameters. Also we can decide batch size and generated image resolution.

### Section 2: 
![Custom Model Configuration](/workflow_imgs/workflow_img1.png)
Here we used T2I-Adapter's ControlNet models for consistent img2img style transfer all the parameters can be changed using ComfyUI. Here are the ones selected are Canny, Depth and Sketch but we can use segmentation or pose models too according to the user's requirements. Also added a module that handles image normalization and resizing. Normalization node is not connected anywhere since the results are better without using it.

### Section 3:
![Custom Model Configuration](/workflow_imgs/workflow_img2.png)
Here we used 4x-Ultrasharp's upscaler to successfully increase the resolution of the generated image or enhace the images quality.

## Example Images
![custom input image](/input_images/input_img0.jpeg)

![custom output image](/ouput_images/output_img0.png)

![custom input image](/input_images/input_img4.jpg)

![custom output image](/ouput_images/output_img4.png)

## Troubleshooting
1. Missing nodes after loading the workflow
   -Use the ComfyUI Manager to download and install any missing nodes or modules.
   -Check the workflow file for dependencies or specific models(ControlNet, Van-Gogh-Diffusion, 4x-Upscaler) that need to be installed.
2.  Output Image Quality is Poor or Inaccurate
   -Double-check the positive and negative prompts to ensure they accurately describe the desired style. It is espacially important to add "lvngvnct," to beginning of the positive prompt as its referred at the model card.
   -Verify that output of Diffusion model is connected to 4x-Upscaler.
   -If you are receiving mostly yellow faces and mostly blue areas, add them to your negative prompt like referred at model card.
   -Ensure the seed, sampler, and scheduler parameters are set appropriately for the task.
3.  Slow Processing Times
   -Decrease the number of steps, reduce the batch size, or lower the resolution of input images.
   -Ensure your drivers (especially GPU drivers) are up-to-date.
   -Adjust the ControlNet workflow to reduce processing time.
        


