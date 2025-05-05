
# 🎨 Text-to-Image AI Generator (gRPC + Gradio)

A simple yet powerful Text-to-Image generation system using **DreamShaper 8** running locally on CPU. Built with **gRPC**, **Gradio**, and **Diffusers**, this project allows users to input a text prompt and generate stunning AI-generated images with customizable inference steps.

---

## 📁 Project Structure

```
.
├── app/
│   ├── imagegen.proto        # gRPC protobuf definition
│   ├── imagegen_pb2.py       # gRPC Python stubs (generated)
│   ├── imagegen_pb2_grpc.py  # gRPC server interface (generated)
│   └── server.py             # gRPC server with DreamShaper inference
├── gradio.py                 # Gradio frontend client
├── styles.css                # Custom CSS for Gradio interface
├── test.py                   # PyTest-based unit tests
├── requirements.txt          # Python dependencies
└── README.md                 # 📘 You're here!
```

---

## ⚙️ Setup Instructions

> ⚠️ Ensure you have Python 3.9+ and [VS Code](https://code.visualstudio.com/) installed.

1. **Clone the Repository**  
   ```bash
   git clone <your-repo-url>
   cd <project-folder>
   ```

2. **Install Dependencies**  
   ```bash
   pip install -r requirements.txt
   ```

3. **Download the Model**  
   - Model: [DreamShaper 8 (on CivitAI)](https://civitai.com/models/4384/dreamshaper)
   - Place the model in:
     ```
     /Project/Model/Dreamshaper 8/
     ```

4. **Generate gRPC Stubs (if not already included)**  
   ```bash
   python -m grpc_tools.protoc -I./app --python_out=./app --grpc_python_out=./app ./app/imagegen.proto
   ```

5. **Run the gRPC Server**  
   ```bash
   python app/server.py
   ```

6. **Launch the Gradio Frontend**  
   ```bash
   python gradio.py
   ```

---

## 🚀 Usage

### ✅ Generating an Image

- Launch the app in your browser.
- Enter a creative prompt (e.g., "A magical castle floating in the sky").
- Adjust the **inference steps** (more steps = better quality, slower).
- Click **Generate Image 🌟**.
- View and download your generated image!

> A copy of the last generated image is saved in `/frontend/generated/last_generated_image.png`.

---

## 🧠 Architecture Overview

```
+-----------------+          gRPC           +---------------------+
|  Gradio Client  |  <------------------>  |     gRPC Server      |
| (gradio.py)     |                        |  (server.py)         |
+-----------------+                        |  - DreamShaper Model |
                                           +---------------------+
```

- **gRPC Interface**: Defined in `imagegen.proto` with methods for image generation.
- **Server**: Loads the model using `diffusers` and handles prompt-to-image conversion.
- **Frontend**: Built with Gradio for interactive UI and styled with custom CSS.

---

## 🧪 Testing

Unit tests for the gRPC server are written using `pytest`.

```bash
pytest test.py
```

**Tests include:**
- Valid prompt image generation
- Empty prompt error handling
- Invalid step range handling
- Long prompt handling

---

## 🧰 Technologies Used

- `gRPC` - High-performance RPC framework
- `Diffusers` - HuggingFace inference pipelines
- `Gradio` - Quick UI for ML models
- `Pillow` - Image processing
- `PyTest` - Testing
- `Python 3.9+`

---

## 🧠 Model Information

- **Model**: DreamShaper 8
- **Source**: [CivitAI - DreamShaper 8](https://civitai.com/models/4384/dreamshaper)
- **Usage**: Loadable via `diffusers` with `AutoPipelineForText2Image`
- **Mode**: CPU-only for compatibility on all systems

---

## ⚠️ Limitations

- Runs on **CPU** → Slower generation (~15–60s/image depending on steps).
- Model path is **hardcoded** in `server.py` – update as needed.

---

## 📌 Future Improvements

- GPU acceleration support (e.g., CUDA).
- Image history panel in Gradio.
- Prompt templates or guidance features.
- Add watermarking or metadata embedding.
- Multi-image output or aspect ratio selection.

---

## 🙌 Acknowledgements

- [HuggingFace Diffusers](https://huggingface.co/docs/diffusers/index)
- [Gradio](https://www.gradio.app/)
- [gRPC](https://grpc.io/)
- [DreamShaper model creator](https://civitai.com/models/4384/dreamshaper)

---

## 📃 License

This project is for **academic use only** (AI4001/CS4063 – NLP Course).  
Do not distribute or deploy without appropriate license checks on the model.
