# **Qwen-Image-Edit-2511-LoRAs-Fast-Multi-Image-Rerun**

> A Gradio-based experimental demonstration for the Qwen/Qwen-Image-Edit-2511 model with lazy-loaded LoRA adapters supporting multi-image input editing. Users can upload one or more images (gallery format) and apply advanced edits such as pose transfer, anime conversion, or camera angle changes via natural language prompts. Features integrated Rerun SDK visualization for interactive side-by-side comparison of inputs and outputs, with downloadable results and persistent .rrd recordings.

## Features

- **Multi-Image Input**: Upload multiple images (e.g., reference pose + subject) for complex tasks like precise pose transfer.
- **Lazy LoRA Loading**: 3 specialized adapters (Photo-to-Anime, Multiple-Angles, Any-Pose) load only when selected to minimize memory usage.
- **Rerun Visualization**: Interactive viewer via `gradio-rerun` and `rerun-sdk`; logs all input images and final result; saves `.rrd` recordings in `tmp_rerun/`.
- **Download Support**: Direct download of generated output image.
- **Rapid Inference**: Flash Attention 3 enabled; 4-step default generations with bfloat16.
- **Auto-Resizing**: Preserves aspect ratio up to 1024px max edge (multiples of 8).
- **Custom Theme**: OrangeRedTheme with responsive layout and clean styling.
- **Examples**: 3 curated multi/single-image scenarios (anime style, angle change, pose transfer).
- **Queueing**: Up to 30 concurrent jobs.

**Note**: This is an experimental Space for the Qwen-Image-Edit-2511 model. For more stable performance, consider the [2509 version](https://huggingface.co/spaces/prithivMLmods/Qwen-Image-Edit-2509-LoRAs-Fast).

---

<img width="1418" height="773" alt="Screenshot 2025-12-27 at 21-55-31 Qwen-Image-Edit-2511-LoRAs-Fast - a Hugging Face Space by prithivMLmods" src="https://github.com/user-attachments/assets/11a0e2e6-61d6-40b9-9c6a-01c906912ef3" />

---

## Prerequisites

- Python 3.10 or higher.
- CUDA-compatible GPU (required for bfloat16 and Flash Attention 3).
- Stable internet for initial model/LoRA downloads.

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/PRITHIVSAKTHIUR/Qwen-Image-Edit-2511-LoRAs-Fast-Multi-Image-Rerun.git
   cd Qwen-Image-Edit-2511-LoRAs-Fast-Multi-Image-Rerun
   ```

2. Install dependencies:
   Create a `requirements.txt` file with the following content, then run:
   ```
   pip install -r requirements.txt
   ```

   **requirements.txt content:**
   ```
   git+https://github.com/huggingface/accelerate.git
   git+https://github.com/huggingface/diffusers.git
   git+https://github.com/huggingface/peft.git
   transformers==4.57.3
   huggingface_hub
   sentencepiece
   gradio-rerun
   torchvision
   supervision
   rerun-sdk
   kernels
   spaces
   hf_xet
   torch
   numpy
   av
   ```

3. Start the application:
   ```
   python app.py
   ```
   The demo launches at `http://localhost:7860`.

## Usage

1. **Upload Images**: Use the gallery to add one or more images (e.g., subject + pose reference).

2. **Select Adapter**: Choose from "Photo-to-Anime", "Multiple-Angles", or "Any-Pose".

3. **Enter Prompt**: Describe the desired edit (e.g., "Make the person in image 1 do the exact same pose of the person in image 2").

4. **Edit Image**: Click "Edit Image".

5. **Output**:
   - Interactive Rerun viewer showing all inputs and final result.
   - Download button for the generated PNG.
   - Recording saved as `.rrd` in `tmp_rerun/`.

### Supported Adapters

| Adapter           | Use Case                                      |
|-------------------|-----------------------------------------------|
| Photo-to-Anime   | Convert realistic photos to anime style       |
| Multiple-Angles  | Change camera viewpoint/angle                 |
| Any-Pose         | Transfer precise pose from reference image(s) |

## Examples

| Input Images                  | Prompt Example                                                                                             | Adapter     |
|-------------------------------|------------------------------------------------------------------------------------------------------------|-------------|
| examples/B.jpg                | "Transform into anime."                                                                                   | Photo-to-Anime |
| examples/A.jpeg               | "Rotate the camera 45 degrees to the right."                                                              | Multiple-Angles |
| examples/P1.jpg + examples/P2.jpg | "Make the person in image 1 do the exact same pose of the person in image 2. Changing style/background undesirable. Match head tilt, eye gaze, arms/legs position exactly." | Any-Pose |

## Rerun Viewer

- Logs paths: `images/input_0`, `input_1`, ..., `images/edited_result`.
- Supports zoom, pan, and comparison.
- Recordings persist in `tmp_rerun/` until manually cleared.

## Troubleshooting

- **Rerun Issues**: Ensure `gradio-rerun` and `rerun-sdk` installed; handles SDK version differences.
- **Adapter Loading**: First use downloads LoRA; monitor console.
- **OOM**: Reduce steps/resolution; clear cache with `torch.cuda.empty_cache()`.
- **Flash Attention Fails**: Fallback to default; requires compatible CUDA.
- **Gallery Input**: Supports filepaths, tuples, or PIL objects.
- **No Output**: Ensure at least one valid image uploaded.

## Contributing

Contributions welcome! Fork the repo, add new adapters to `ADAPTER_SPECS`, enhance Rerun logging, or improve multi-image handling, and submit PRs with tests.

Repository: [https://github.com/PRITHIVSAKTHIUR/Qwen-Image-Edit-2511-LoRAs-Fast-Multi-Image-Rerun.git](https://github.com/PRITHIVSAKTHIUR/Qwen-Image-Edit-2511-LoRAs-Fast-Multi-Image-Rerun.git)

## License

Apache License 2.0. See [LICENSE](LICENSE) for details.

Built by Prithiv Sakthi. Report issues via the repository.
