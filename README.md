# 🧠 PixelBrain: Multi-Stage Intelligent Photo Editing

PixelBrain is an advanced AI photo-editing ecosystem that moves beyond static presets. It utilizes a "Multi-Stage Intelligence" architecture to analyze images technically, contextually, and emotionally before making creative editing decisions.

---

## 🔗 Project Links

* **Live Deployment, Source & Code:** [Hugging Face Spaces - PixelBrain](https://huggingface.co/spaces/devrajsaini/PixelBrain/tree/main)
* **Model Training & Datasets (Kaggle):**
    * [CNN: Indoor vs. Outdoor Classification](https://www.kaggle.com/code/devrajnsut/indoor-outdoor)
    * [CNN: Day vs. Night Classification](https://www.kaggle.com/code/devrajnsut/day-night)
    * [CNN: Weather Condition Analysis](https://www.kaggle.com/code/devrajnsut/weather)

---

## 🛠️ The Architecture (How it Works)

PixelBrain processes an image through four distinct intelligence layers:

### 1. The Vision Layer (Custom CNNs)
The base layer consists of three custom-trained Convolutional Neural Networks (CNNs) developed on Kaggle. These models categorize the environment:
* **Environment:** Indoor vs. Outdoor
* **Temporal:** Day vs. Night
* **Atmospheric:** Weather conditions (Sunny, Cloudy, Rainy, etc.)

### 2. The Semantic & Affective Layer
* **YOLOv8:** Performs object detection to identify specific subjects (e.g., pizza, pets, vehicles, mountains).
* **DeepFace:** Performs facial analysis to detect human emotions (Happiness, Sadness, Anger, etc.) and gender.

### 3. The Logic Layer (AI Brain)
All metadata from the previous layers is structured into a complex prompt and sent to the **Perplexity Sonar LLM**. The LLM acts as a "Senior Creative Director," weighing technical flaws (blur/darkness) against artistic potential to return a final list of filters.



### 4. Persistence Layer
To overcome the ephemeral nature of cloud spaces, every prediction is logged locally to a CSV and immediately synchronized to a [Hugging Face Dataset](https://huggingface.co/datasets/devrajsaini/llm_prediction_nature) using the `huggingface-hub` API.

---

## ✨ Key Features

* **Emotional Grading:** Automatically suggests 'warm' or 'happy' filters when joy is detected in faces.
* **Technical Rescue:** Identifies underexposed (dark) or shaky (blurry) photos and applies corrective filters (`brighten`, `deblur`) only when needed.
* **Contextual Intelligence:** Automatically triggers `savory` filters for food items and `cool` or `vintage` filters for modern or historical architecture.
* **Persistent Analytics:** Real-time data logging to the cloud for performance monitoring and future model fine-tuning.

---

## 🎨 Filter Logic Examples

| Scenario | Detected Metadata | Recommended Filter(s) |
| :--- | :--- | :--- |
| **Beach Sunset** | Outdoor, Day, Sunny, Sand, Water | `['warm', 'happy']` |
| **Night Street** | Outdoor, Night, Car, Street Light | `['brighten', 'cool']` |
| **Pizza Party** | Indoor, Food, People, Happy | `['savory', 'happy']` |
| **Old Church** | Outdoor, Cloudy, Architecture | `['vintage_tv', 'grayscale']` |

---

## 💻 Tech Stack

* **Backend:** Python 3.11, FastAPI, Uvicorn
* **Deep Learning:** TensorFlow, Keras (Custom CNNs), Ultralytics (YOLOv8)
* **Facial Analysis:** DeepFace
* **LLM Integration:** Perplexity AI API (Sonar)
* **Deployment:** Docker, Hugging Face Spaces
* **Storage:** Hugging Face Datasets API

---

## 🚀 Installation & Local Setup

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/your-username/PixelBrain.git](https://github.com/your-username/PixelBrain.git)
    cd PixelBrain
    ```

2.  **Environment Variables:**
    Create a `.env` file in the root directory:
    ```text
    PERPLEXITY_API_KEY=your_perplexity_key
    HF_TOKEN=your_huggingface_write_token
    DATASET_REPO_ID=devrajsaini/llm_prediction_nature
    ```

3.  **Run with Docker:**
    ```bash
    docker build -t pixelbrain .
    docker run -p 7860:7860 pixelbrain
    ```

---
