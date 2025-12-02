<img width="722" height="404" alt="image" src="https://github.com/user-attachments/assets/a97c044a-04f1-4ad9-8381-85b6ed4c5f85" /># 🦅 Eagle Vision Alert System
### Real-Time AI Violence Detection & IoT Alerting System

**Eagle Vision** is an intelligent surveillance solution designed to detect violent activities in real-time and automatically dispatch alerts to authorities. By integrating Deep Learning (CNNs) with embedded hardware (ESP32-CAM & GSM Modules), this project eliminates the need for constant human monitoring in sensitive areas like schools, ATMs, and public transport hubs.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Model Performance](#-model-performance)
- [Hardware Setup](#-hardware-setup)
- [Installation & Usage](#-installation--usage)
- [Future Scope](#-future-scope)

---

## 🧐 Overview
Traditional surveillance is passive, relying on human operators who may miss critical events. Eagle Vision automates this process by:
1.  **Capturing** live video streams via ESP32-CAM.
2.  **Processing** frames using a fine-tuned CNN model (ResNet50/Xception).
3.  **Detecting** violence with high accuracy.
4.  **Alerting** authorities immediately via SMS (GSM Module) and Telegram (with image proof).

---

## 🌟 Key Features
* **Real-Time Detection:** Processes video frames on the fly to detect aggression or physical violence.
* **Dual Alert Mechanism:**
    * **SMS:** Sends immediate text alerts via SIM800L GSM Module.
    * **Telegram:** Sends a photo snapshot of the incident via Telegram API.
* **Edge Integration:** Lightweight architecture designed for low-cost hardware implementation.
* **High Accuracy:** Trained on a curated dataset of 6,000 frames (Hockey Fight, Classroom Fight, and Surveillance datasets).

---

## 🏗 System Architecture

The system follows a hybrid IoT-AI workflow:

1.  **Input:** ESP32-CAM streams live video over Wi-Fi to the central processing unit (PC/Laptop).
2.  **Processing:** A Python script fetches frames, preprocesses them (resize to 224x224), and passes them through the trained Deep Learning model.
3.  **Inference:** The model classifies the frame as "Violence" or "Non-Violence".
4.  **Action:**
    * If **Violence** is detected:
        * Python script triggers the **Telegram Bot** to send an image.
        * Python script sends a serial signal to the **Arduino Uno**.
        * Arduino commands the **SIM800L** to send an SMS.


<img width="1157" height="637" alt="image" src="https://github.com/user-attachments/assets/9c3bc754-6c96-42df-b891-cb5633ce9cb5" />

---

## 🛠 Tech Stack

### Software
* **Language:** Python 3.x, C++ (Arduino)
* **Libraries:** OpenCV, TensorFlow/Keras, NumPy, Serial
* **Models:** ResNet50, Xception, EfficientNetB0
* **APIs:** Telegram Bot API

### Hardware
* **Camera:** ESP32-CAM
* **Controller:** Arduino Uno
* **Communication:** SIM800L GSM Module
* **Power:** DC-DC Buck-Boost Converter (to stabilize voltage)

---

## 📊 Model Performance

We trained and tested three major architectures. While ResNet50 had the best raw accuracy, **Xception** was selected for deployment due to its superior speed and stability in real-time video inference.

| Model | Accuracy (Offline) | Precision | Recall | Inference Speed | Verdict |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ResNet50** | **94.71%** | 0.951 | 0.942 | ~125ms | Best Accuracy |
| **Xception** | 92.31% | 0.958 | 0.885 | **~140ms** | **Best Real-Time Performance** |
| **EfficientNetB0**| 50.00% | 0.500 | 1.00 | ~86ms | Failed to converge |

---

## 🔌 Hardware Setup



* **ESP32-CAM:** Configured as a Web Server to stream video.
* **Arduino <-> SIM800L:** Connected via SoftwareSerial.
* **Arduino <-> PC:** Connected via USB Serial for receiving detection triggers.

<img width="626" height="274" alt="image" src="https://github.com/user-attachments/assets/5cfb8b06-91c2-49ef-b427-2f3a97a7cc0c" />

<img width="722" height="404" alt="image" src="https://github.com/user-attachments/assets/a96ff417-f268-4703-b2ee-e7c1cecaa9f2" />

---

## 🚀 Installation & Usage

1.  **Clone the Repository**
    ```bash
    git clone [https://github.com/Pinakhi7/eagle-vision.git](https://github.com/Pinakhi7/eagle-vision.git)
    cd eagle-vision
    ```

2.  **Hardware Setup**
    * Upload the `esp32_cam_stream.ino` code to your ESP32-CAM.
    * Upload the `gsm_alert_system.ino` code to your Arduino Uno.
    * Verify the GSM module has a valid SIM card and power.

3.  **Run the AI Detection**
    * Install dependencies: `pip install -r requirements.txt`
    * Update the `IP Address` in the python script to match your ESP32-CAM.
    * Run the inference script:
    ```bash
    python real_time_detection.py
    ```

---

## 🔮 Future Scope
* **Temporal Analysis:** Implementing LSTM (Long Short-Term Memory) networks to analyze video sequences rather than single frames for better context.
* **Audio Integration:** Adding audio sensors to detect screams or loud crashes.
* **Edge Optimization:** Converting models to TensorFlow Lite for running fully on edge devices without a PC.

---

### 📝 Credits
Developed as a Capstone Project exploring the intersection of Computer Vision and IoT for public safety.
