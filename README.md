# ComfyUI-RMBG

A ComfyUI custom node designed for advanced image background removal and object segmentation, utilizing multiple models including RMBG-2.0, INSPYRENET, BEN, SAM, and GroundingDINO.

$${\color{red}If\ this\ custom\ node\ helps\ you\ or\ you\ like\ my\ work,\ please\ give\ me⭐on\ this\ repo!}$$
$${\color{red}It's\ a\ greatest\ encouragement\ for\ my\ efforts!}$$

## News & Updates
- 2024/12/23: Update ComfyUI-RMBG to v1.3.0 with new Segment node ( [update.md](https://github.com/1038lab/ComfyUI-RMBG/blob/main/update.md#v140-20241222) )
![rmbg v1.3.0](https://github.com/user-attachments/assets/7607546e-ffcb-45e2-ab90-83267292757e)

  - Added text-prompted object segmentation
  - Support both tag-style ("cat, dog") and natural language ("a person wearing red jacket") prompts
  - Multiple models: SAM (vit_h/l/b) and GroundingDINO (SwinT/B) (as always model file will be downloaded automatically when first time using the specific model)
  - This update requires install requirements.txt

- 2024/12/12: Update Comfyui-RMBG ComfyUI Custom Node to v1.2.2 ( [update.md](https://github.com/1038lab/ComfyUI-RMBG/blob/main/update.md#v122-20241212) )
![RMBG1 2 2](https://github.com/user-attachments/assets/cb7b1ad0-a2ca-4369-9401-54957af6c636)

- 2024/12/02: Update Comfyui-RMBG ComfyUI Custom Node to v1.2.1 ( [update.md](https://github.com/1038lab/ComfyUI-RMBG/blob/main/update.mdv121-20241202) )
![GIF_TO_AWEBP](https://github.com/user-attachments/assets/7f8275d5-06e5-4880-adfe-930f045df673)

- 2024/11/29: Update Comfyui-RMBG ComfyUI Custom Node to v1.2.0 ( [update.md](https://github.com/1038lab/ComfyUI-RMBG/blob/main/update.md#v120-20241129) )
![RMBGv1 2 0](https://github.com/user-attachments/assets/4fd10123-6c95-4f9e-8d25-fdb39b5fc792)

- 2024/11/21: Update Comfyui-RMBG ComfyUI Custom Node to v1.1.0 ( [update.md](https://github.com/1038lab/ComfyUI-RMBG/blob/main/update.md#v110-20241121) )
![comfyui-rmbg version compare](https://github.com/user-attachments/assets/2d23cf42-ca74-49e5-a8bf-9de377bd71aa)

## Features
- Background Removal (RMBG Node)
  - Multiple models: RMBG-2.0, INSPYRENET, BEN
  - Various background options
  - Batch processing support
  
- Object Segmentation (Segment Node)
  - Text-prompted object detection
  - Support both tag-style and natural language inputs
  - High-precision segmentation with SAM
  - Flexible parameter controls

![RMBG Demo](https://github.com/user-attachments/assets/f3ffa3c4-5a21-4c0c-a078-b4ffe681c4c4)

## Installation

### Method 1. install on ComfyUI-Manager, search `Comfyui-RMBG` and install
install requirment.txt in the ComfyUI-RMBG folder
  ```bash
  ./ComfyUI/python_embeded/python -m pip install -r requirements.txt
  ```

### Method 2. Clone this repository to your ComfyUI custom_nodes folder:
  ```bash
  cd ComfyUI/custom_nodes
  git clone https://github.com/1038lab/ComfyUI-RMBG
  ```
  install requirment.txt in the ComfyUI-RMBG folder
  ```bash
  ./ComfyUI/python_embeded/python -m pip install -r requirements.txt
  ```

### 3. Manually download the models:
- The model will be automatically downloaded to `ComfyUI/models/RMBG/` when first time using the custom node.
- Manually download the RMBG-2.0 model by visiting this [link](https://huggingface.co/briaai/RMBG-2.0/tree/main), then download the files and place them in the `/ComfyUI/models/RMBG/RMBG-2.0` folder.
- Manually download the INSPYRENET models by visiting the [link](https://huggingface.co/1038lab/inspyrenet), then download the files and place them in the `/ComfyUI/models/RMBG/INSPYRENET` folder.
- Manually download the BEN model by visiting the [link](https://huggingface.co/PramaLLC/BEN), then download the files and place them in the `/ComfyUI/models/RMBG/BEN` folder.
- Manually download the SAM models by visiting the [link](https://huggingface.co/1038lab/sam), then download the files and place them in the `/ComfyUI/models/SAM` folder.
- Manually download the GroundingDINO models by visiting the [link](https://huggingface.co/1038lab/GroundingDINO), then download the files and place them in the `/ComfyUI/models/grounding-dino` folder.

## Usage
### RMBG Node
![RMBG](https://github.com/user-attachments/assets/cd0eb92e-8f2e-4ae4-95f1-899a6d83cab6)

### Optional Settings :bulb: Tips
| Optional Settings    | :memo: Description                                                           | :bulb: Tips                                                                                   |
|----------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Sensitivity**      | Adjusts the strength of mask detection. Higher values result in stricter detection. | Default value is 0.5. Adjust based on image complexity; more complex images may require higher sensitivity. |
| **Processing Resolution** | Controls the processing resolution of the input image, affecting detail and memory usage. | Choose a value between 256 and 2048, with a default of 1024. Higher resolutions provide better detail but increase memory consumption. |
| **Mask Blur**        | Controls the amount of blur applied to the mask edges, reducing jaggedness. | Default value is 0. Try setting it between 1 and 5 for smoother edge effects.                    |
| **Mask Offset**      | Allows for expanding or shrinking the mask boundary. Positive values expand the boundary, while negative values shrink it. | Default value is 0. Adjust based on the specific image, typically fine-tuning between -10 and 10. |
| **Background**      | Choose output background color | Alpha (transparent background) Black, White, Green, Blue, Red |
| **Invert Output**      | Flip mask and image output | Invert both image and mask output |
| **Performance Optimization** | Properly setting options can enhance performance when processing multiple images. | If memory allows, consider increasing `process_res` and `mask_blur` values for better results, but be mindful of memory usage. |

### Basic Usage
1. Load `RMBG (Remove Background)` node from the `🧪AILab/🧽RMBG` category
2. Connect an image to the input
3. Select a model from the dropdown menu
4. select the parameters as needed (optional)
3. Get two outputs:
   - IMAGE: Processed image with transparent, black, white, green, blue, or red background
   - MASK: Binary mask of the foreground

### Parameters
- `sensitivity`: Controls the background removal sensitivity (0.0-1.0)
- `process_res`: Processing resolution (512-2048, step 128)
- `mask_blur`: Blur amount for the mask (0-64)
- `mask_offset`: Adjust mask edges (-20 to 20)
- `background`: Choose output background color
- `invert_output`: Flip mask and image output
- `optimize`: Toggle model optimization

### Segment Node
1. Load `Segment (RMBG)` node from the `🧪AILab/🧽RMBG` category
2. Connect an image to the input
3. Enter text prompt (tag-style or natural language)
4. Select SAM and GroundingDINO models
5. Adjust parameters as needed:
   - Threshold: 0.25-0.35 for broad detection, 0.45-0.55 for precision
   - Mask blur and offset for edge refinement
   - Background color options

<details>
<summary><h2>About Models</h2></summary>

## RMBG-2.0
RMBG-2.0 is is developed by BRIA AI and uses the BiRefNet architecture which includes:
- High accuracy in complex environments
- Precise edge detection and preservation
- Excellent handling of fine details
- Support for multiple objects in a single image
- Output Comparison
- Output with background
- Batch output for video
The model is trained on a diverse dataset of over 15,000 high-quality images, ensuring:
- Balanced representation across different image types
- High accuracy in various scenarios
- Robust performance with complex backgrounds

## INSPYRENET
INSPYRENET is specialized in human portrait segmentation, offering:
- Fast processing speed
- Good edge detection capability
- Ideal for portrait photos and human subjects

## BEN
BEN is robust on various image types, offering:
- Good balance between speed and accuracy
- Effective on both simple and complex scenes
- Suitable for batch processing

## SAM
SAM is a powerful model for object detection and segmentation, offering:
- High accuracy in complex environments
- Precise edge detection and preservation
- Excellent handling of fine details
- Support for multiple objects in a single image
- Output Comparison
- Output with background
- Batch output for video

## GroundingDINO
GroundingDINO is a model for text-prompted object detection and segmentation, offering:
- High accuracy in complex environments
- Precise edge detection and preservation
- Excellent handling of fine details
- Support for multiple objects in a single image
- Output Comparison
- Output with background
- Batch output for video
</details>


## Requirements
- ComfyUI
- Python 3.10+
- Required packages (automatically installed):
  - torch>=2.0.0
  - torchvision>=0.15.0
  - Pillow>=9.0.0
  - numpy>=1.22.0
  - huggingface-hub>=0.19.0
  - tqdm>=4.65.0
  - transformers>=4.35.0
  - transparent-background>=1.2.4

## Credits
- RMBG-2.0: https://huggingface.co/briaai/RMBG-2.0
- INSPYRENET: https://github.com/plemeri/InSPyReNet
- BEN: https://huggingface.co/PramaLLC/BEN
- SAM: https://huggingface.co/facebook/sam-vit-base
- GroundingDINO: https://github.com/IDEA-Research/GroundingDINO
- Created by: [1038 Lab](https://github.com/1038lab)

## License
GPL-3.0 License
