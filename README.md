# Silhouette Tracker: Real-Time Human Pose Estimation with CUDA Acceleration

*A real-time human pose estimation pipeline, fully configured within an isolated Conda environment for effortless setup, reproducibility, and portability.*

## Available Documentation / Доступная документация

- [English Documentation](README.md) (current document / текущий документ)
- [Документация на русском языке](README_RU.md)

## Project Structure

```
silhouette-tracker/
├── .env.example    # Configuration template
├── SBOMs/          # Dependency metadata
├── app/            # Application source code
├── models/         # YOLOv8 models
└── videos/         # Input video files
```

## Quick Start

### I. Prerequisites

| Component | Requirement |
| :--- | :--- |
| **Package Manager** | [`Micromamba`](https://github.com/mamba-org/mamba) |
| **Operating System** | GNU/Linux-based system |
| **Architecture** | `x86_64` |
| **Hardware** | NVIDIA GPU with a driver supporting CUDA >= 12.6.3 |
| **Development Tools** *(Optional)* | [`conda-lock`](https://github.com/conda/conda-lock) and [`pip-licenses`](https://github.com/raimon49/pip-licenses) |

> **Note:**  
> These are not strict requirements, but rather the baseline environment where the code is 
guaranteed to run out of the box. Alternative setups are possible but may require manual 
configuration.

### II. Clone the Repository

```bash
git clone https://github.com/snegoviol/silhouette-tracker.git
cd silhouette-tracker
```

### III. Create and Activate Virtual Environment

```bash
micromamba env create -p ./.venv -f SBOMs/conda-linux-64-lock.yml
micromamba activate ./.venv
```

### IV. Prepare Data

Models and videos are not included in the repository due to size limitations. To download the models, run:

```bash
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8n-pose.pt   && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8s-pose.pt   && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8m-pose.pt   && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8l-pose.pt   && \
wget -P models/ https://github.com/ultralytics/assets/releases/download/v8.2.0/yolov8x-pose.pt  
```

Add any video to the `videos/` directory. For demonstration, you can download videos from [Pexels Free Stock Videos](https://www.pexels.com/videos/).  
For example: [Mother and daughter with face masks at the park by Gustavo Fring from Pexels](https://www.pexels.com/video/mother-and-daughter-with-face-masks-at-the-park-4265036/).

### V. Configure via `.env`

1. Create `.env` file from template:

    ```bash
    cp .env.example .env
    ```

2. Edit `.env` in any text editor (e.g., `nano`, `VSCode`):

    ```bash
    nano .env
    ```

3. Configure parameters: the file is divided into sections — modify values according to your needs. For example:

    ```bash
    # === MODEL CONFIGURATION ===
    MODEL_NAME=yolov8m-pose.pt
    CONFIDENCE=0.8

    # === VIDEO CONFIGURATION ===
    VIDEO_NAME=example-pexels.mp4

    # === DISPLAY SETTINGS ===
    DISPLAY_WIDTH=1020
    DISPLAY_HEIGHT=720

    # === PATH CONFIGURATION ===
    MODELS_DIR=models
    VIDEOS_DIR=videos
    ```

### VI. Run the Application

```bash
python -m app.main
```

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).
