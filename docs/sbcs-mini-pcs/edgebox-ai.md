# 🖥️ EdgeBox AI

<span class="badge badge-green">In Stock</span>&nbsp;
<span class="badge badge-blue">Edge AI Computer</span>

> **AI inference where it matters — at the machine.** The EdgeBox AI is powered by the NVIDIA Jetson Orin NX, delivering up to 100 TOPS of AI performance in a compact, fanless enclosure. Run real-time object detection, quality inspection, and anomaly detection without sending data to the cloud.

---

## Quick Start

<div class="quick-start">
<h4>⚡ Running your first AI model in 20 minutes</h4>

1. Flash JetPack OS to the NVMe SSD
2. Connect power (12V DC), HDMI, and USB keyboard
3. Complete the NVIDIA initial setup wizard
4. Run the included ElephantAI demo (object detection on USB webcam)

</div>

---

## Technical Specifications

<table class="specs-table">
<tr><th colspan="2">AI & Compute</th></tr>
<tr><td>Module</td><td><strong>NVIDIA Jetson Orin NX 16GB</strong></td></tr>
<tr><td>AI Performance</td><td><strong>100 TOPS</strong></td></tr>
<tr><td>GPU</td><td>1024-core NVIDIA Ampere GPU</td></tr>
<tr><td>CPU</td><td>8-core ARM Cortex-A78AE @ 2.0 GHz</td></tr>
<tr><td>RAM</td><td>16 GB LPDDR5 (unified memory)</td></tr>
<tr><th colspan="2">Storage</th></tr>
<tr><td>NVMe Slot</td><td>M.2 2280 PCIe Gen 4 (up to 2TB)</td></tr>
<tr><td>eMMC</td><td>64 GB (OS)</td></tr>
<tr><th colspan="2">I/O</th></tr>
<tr><td>USB</td><td>4 × USB 3.2 Gen 2 (10 Gbps)</td></tr>
<tr><td>Ethernet</td><td>2 × 2.5GbE</td></tr>
<tr><td>Video In</td><td>2 × MIPI CSI-2 (4K camera)</td></tr>
<tr><td>Video Out</td><td>1 × HDMI 2.1, 1 × DP 1.4</td></tr>
<tr><td>Serial</td><td>1 × RS485, 1 × RS232</td></tr>
<tr><th colspan="2">Power & Physical</th></tr>
<tr><td>Input Voltage</td><td>12V DC (5.5/2.5mm barrel)</td></tr>
<tr><td>Typical Power</td><td>15–35W (AI workload dependent)</td></tr>
<tr><td>Dimensions</td><td>160 × 110 × 55 mm</td></tr>
<tr><td>Cooling</td><td>Passive aluminium heatsink (fanless)</td></tr>
<tr><td>Operating Temperature</td><td>-10°C to +55°C</td></tr>
</table>

---

## OS Setup

### Flash JetPack

The EdgeBox AI uses **NVIDIA JetPack 6.0** (Ubuntu 22.04 based):

```bash
# Use NVIDIA SDK Manager on a Linux host PC
# https://developer.nvidia.com/sdk-manager

# Or flash via USB with the included recovery cable
sudo ./flash.sh jetson-orin-nx-16 mmcblk0p1
```

!!! note "JetPack version"
    Always use JetPack 6.0 or later for Orin NX support. Earlier versions do not support the Orin architecture.

---

## AI Inference

### Run the ElephantAI demo

```bash
# Clone the demo repo
git clone https://github.com/elephantronics/edgebox-ai-demo
cd edgebox-ai-demo

# Install dependencies
pip3 install -r requirements.txt

# Run real-time object detection (YOLOv8)
python3 detect.py --source /dev/video0 --model yolov8n.engine
```

### Convert your own model to TensorRT

```bash
# Install torch2trt
pip3 install torch2trt

# Convert ONNX → TensorRT engine
trtexec --onnx=your_model.onnx \
        --saveEngine=your_model.engine \
        --fp16 \
        --workspace=4096
```

### Benchmark inference speed

| Model | Precision | FPS (EdgeBox AI) |
|---|---|---|
| YOLOv8n | FP16 | ~210 fps |
| YOLOv8m | FP16 | ~85 fps |
| YOLOv8x | FP16 | ~28 fps |
| ResNet-50 | INT8 | ~480 fps |

---

## Camera Input

=== "USB Camera"

    Any UVC-compatible USB camera works out of the box:

    ```python
    import cv2
    cap = cv2.VideoCapture(0)  # /dev/video0
    ret, frame = cap.read()
    ```

=== "MIPI CSI Camera"

    Connect a compatible MIPI camera (e.g. IMX477) to CSI port:

    ```python
    # GStreamer pipeline for CSI camera
    pipeline = (
        "nvarguscamerasrc ! "
        "video/x-raw(memory:NVMM),width=1920,height=1080,framerate=30/1 ! "
        "nvvidconv ! video/x-raw,format=BGRx ! videoconvert ! appsink"
    )
    cap = cv2.VideoCapture(pipeline, cv2.CAP_GSTREAMER)
    ```

---

## Troubleshooting

| Issue | Fix |
|---|---|
| High temperature warning | Check ambient temperature; ensure heatsink fins are unobstructed |
| TensorRT conversion fails | Ensure JetPack and TensorRT versions match; clear `/tmp/` cache |
| Camera not detected | Check USB port (use USB 3.2 port); try `v4l2-ctl --list-devices` |
