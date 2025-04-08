

# 📄 Project : Lane Detection using OpenCV

## 🛣️ Overview

This project is a simple yet effective implementation of a **lane detection system** using Python and OpenCV. It is designed to process video input and identify the lane lines on roads in real time, which is a fundamental step in developing autonomous vehicle systems and driver-assist technologies.

---

## 📌 Objectives

- Detect and highlight lane lines from road videos.
- Understand and implement fundamental computer vision techniques.
- Create a modular and readable Python program using OpenCV.

---

## 🔧 System Requirements

- **Python**: Version 3.x
- **Libraries**:
  - OpenCV (`opencv-python`)
  - NumPy

### Installation

Install the required packages using pip:

```bash
pip install opencv-python numpy
```

---

## 📁 Project Structure

```
lane-detection/
│
├── lane_detection.py       # Main Python script
├── D:/deverse/ND_19.mp4    # Input video file (update path as needed)
└── README.md               # Project description and setup guide
```

---

## 🧠 Methodology

### 1. **Grayscale Conversion**

To reduce computational complexity, each frame is converted from RGB to grayscale using:
```python
gray = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
```

### 2. **Gaussian Blur**

Blurring is applied to smooth the image and reduce noise:
```python
blur = cv2.GaussianBlur(gray, (5, 5), 0)
```

### 3. **Canny Edge Detection**

Edges are detected using the Canny algorithm:
```python
edges = cv2.Canny(blur, 50, 150)
```

### 4. **Region of Interest (ROI)**

A polygonal mask is applied to focus on the road area:
```python
height = image.shape[0]
polygons = np.array([[(100, height), (1180, height), (600, 400)]])
```

### 5. **Hough Line Transform**

Lines are detected from the edge image using the Probabilistic Hough Transform:
```python
lines = cv2.HoughLinesP(cropped_edges, rho=2, theta=np.pi / 180, threshold=100, minLineLength=40, maxLineGap=5)
```

### 6. **Display Detected Lines**

Detected lines are drawn on a blank image and overlaid on the original frame:
```python
combo = cv2.addWeighted(frame, 0.8, line_image, 1, 1)
```

---

## 🧪 How to Run

1. Replace the video path in `cv2.VideoCapture()` with your own local path:
   ```python
   cap = cv2.VideoCapture("D:\\deverse\\ND_19.mp4")
   ```

2. Run the script:
   ```bash
   python lane_detection.py
   ```

3. The lane-detected video will be displayed. Press `q` to quit.

---

## 🧾 Sample Output

- The script shows a real-time overlay of green lines indicating detected lanes.
- Lines are detected within the defined triangular ROI.
- ![image](https://github.com/user-attachments/assets/c1280163-fcfa-4136-80cf-c92e5c2bd138)


---

## 💡 Enhancements (Future Scope)

- Lane line averaging and extrapolation for more stable detection.
- Color filtering to isolate yellow/white lanes.
- Integration with object detection to avoid vehicles.
- Curved lane detection using polynomial fitting.
- Real-time steering suggestions for autonomous navigation.

