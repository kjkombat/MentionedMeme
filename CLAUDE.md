# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

MentionedMeme is an image manipulation project focused on generating variations of the famous "Brazil Mentioned" K-On anime meme. The goal is to generate small fractions of the image (bottle cap, background, dress elements) rather than regenerating the entire image through AI diffusion models, preserving the meme's comedic element.

## Development Environment Setup

This project uses `uv` for Python package management:

```bash
# Create virtual environment
uv venv

# Install dependencies
uv pip install -r requirements.txt
```

## Dependency Management

- `requirements.in`: Source file listing direct dependencies (opencv-python, numpy, pillow, matplotlib)
- `requirements.txt`: Auto-generated pinned dependencies via pip-compile
- To update dependencies: modify `requirements.in` and run `pip-compile requirements.in`

## Code Architecture

### Primary Development: Jupyter Notebook

The main development work is in `mentionedmeme.ipynb`, which contains:

1. **Image Loading Utilities**:
   - `load_image()`: Loads images using PIL and converts to numpy arrays
   - `load_and_pad_image()`: Loads images with OpenCV and pads them to target dimensions with transparent borders

2. **Image Manipulation Functions**:
   - `overlay_image(source, overlay, bbox)`: Core function that performs alpha-blended image overlay
     - Takes source image, overlay image, and bounding box (x, y, width, height)
     - Handles alpha channel masking for transparent overlays
     - Performs linear blending: `blended = roi * (1 - mask) + resized_overlay * mask`
   - `calc_dim_resize()`: Resizes images to target dimensions

3. **Visualization**:
   - `display_image()`: Uses matplotlib to display images in notebook

### Current Implementation Status

Working example demonstrates:
- Loading a source K-On image (`images/source_pic.png`)
- Overlaying a transparent Texas cap (`images/aus_cap.png`)
- Positioning overlay using ROI coordinates (Region of Interest)
- Alpha blending with masking for natural-looking composites

### Key Technical Details

- Images are handled in RGB format (PIL) or BGR format (OpenCV) depending on function
- Alpha channel (4th channel) is used for transparency masking
- Coordinate system: `(x, y, width, height)` for bounding boxes
- ROI extraction enables precise overlay positioning on source images

## Running the Code

Primary workflow is through Jupyter notebook:
```bash
jupyter notebook mentionedmeme.ipynb
```

The `main.py` file is currently a placeholder and not part of the active development workflow.

## Images Directory

Contains source images and overlay elements (gitignored). Working example uses:
- `source_pic.png`: Base K-On character image
- `texas-cap-transparent.png`: Overlay element with alpha channel
