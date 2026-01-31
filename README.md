# KitaKo - Image Recognition for Road and Infrastructure

## Features

- **Multiple Input Sources**: Supports images, image folders, video files, USB cameras
- **Real-time Detection**: Live inference with FPS display
- **Customizable Resolution**: Set custom display resolution for inference
- **Recording Capability**: Record detection results to video file
- **Object Counting**: Displays the number of detected potholes per frame

## Project Structure

```
KitaKo/
├── yolo_detect.py              # Main detection script
├── my_model.pt                 # Pre-trained YOLO model
├── README.md                   # This file
├── labeled dataset for training/   # Training dataset with labels
├── pothole_image_data/         # Additional pothole image data
│   └── Pothole_Image_Data/
├── test images and vids/       # Test images and videos
└── train and results/          # Training outputs
    ├── args.yaml               # Training arguments
    ├── results.csv             # Training metrics
    └── weights/
        ├── best.pt             # Best model weights
        └── last.pt             # Last checkpoint weights
```

## Requirements

- Python 3.8+
- OpenCV (`cv2`)
- NumPy
- Ultralytics YOLO

### Optional (for Raspberry Pi)
- picamera2

## Installation

1. Clone or download this repository

2. Create and activate a conda environment:
   ```bash
   conda create -n KitaKo_Potholes python=3.9
   conda activate KitaKo_Potholes
   ```

3. Install dependencies:
   ```bash
   pip install opencv-python numpy ultralytics
   ```

## Usage

### Basic Command Structure
```bash
python yolo_detect.py --model <model_path> --source <input_source> [options]
```

### Arguments

| Argument | Description | Required | Default |
|----------|-------------|----------|---------|
| `--model` | Path to YOLO model file | Yes | - |
| `--source` | Input source (image, folder, video, usb, picamera) | Yes | - |
| `--thresh` | Minimum confidence threshold (0-1) | No | 0.5 |
| `--resolution` | Display resolution (WxH format) | No | Source resolution |
| `--record` | Record output to video file | No | False |

### Examples

**Detect from USB Camera:**
```bash
python yolo_detect.py --model my_model.pt --source usb0 --resolution 1280x720
```

**Detect from Video File:**
```bash
python yolo_detect.py --model my_model.pt --source potholes2.mp4
```

**Detect from Image:**
```bash
python yolo_detect.py --model my_model.pt --source test_image.jpg
```

**Detect from Image Folder:**
```bash
python yolo_detect.py --model my_model.pt --source "test images and vids"
```

**Record Detection Results:**
```bash
python yolo_detect.py --model my_model.pt --source usb0 --resolution 1280x720 --record
```

## Keyboard Controls (During Inference)

| Key | Action |
|-----|--------|
| `Q` | Quit the program |
| `S` | Pause inference (press any key to resume) |
| `P` | Save current frame as `capture.png` |

## Output

- **Real-time Display**: Bounding boxes around detected potholes with confidence percentages
- **FPS Counter**: Displays average frame rate (for video/camera sources)
- **Object Count**: Shows number of detected objects per frame
- **Recording**: Saves as `demo1.avi` when `--record` flag is used

## Training

The model was trained using the Ultralytics YOLO framework. Training configuration and results are stored in the `train and results/` directory:

- `args.yaml` - Training hyperparameters and configuration
- `results.csv` - Training metrics (loss, mAP, etc.)
- `weights/best.pt` - Best performing model checkpoint
- `weights/last.pt` - Final model checkpoint
