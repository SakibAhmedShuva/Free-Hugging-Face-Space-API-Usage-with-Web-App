# Hugging Face Space API Wrapper with Flask

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.0.3-black.svg)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Hugging Face](https://img.shields.io/badge/HF-Powered%20by%20Hugging%20Face-yellow.svg)](https://huggingface.co/)

This project provides a simple yet powerful Flask-based web application that acts as a backend API to generate images using any public or private Hugging Face Gradio Space. It abstracts the direct interaction with the `gradio_client`, saves the generated images locally, and returns a public URL, making it easy to integrate image generation into your own applications.

![image](https://github.com/user-attachments/assets/2b825b8c-5bad-4ca5-b9ce-0d52c4969093)


![image](https://github.com/user-attachments/assets/2f01c79e-e474-4481-abb4-9c1de9bb33ef)


## ✨ Features

- **Simple API Endpoint**: A single POST endpoint to generate images from a text prompt
- **Universal HF Space Compatibility**: Connect to any Gradio-based image generation Space by simply changing an environment variable
- **Local Image Caching**: Automatically saves generated images to a static directory
- **Public URL Generation**: Returns a direct, publicly accessible URL for each generated image
- **Prompt Enhancement**: Includes a basic prompt enhancer to improve the quality of generated images
- **Easy Configuration**: Setup is managed entirely through a `.env` file. No code changes needed to get started
- **Frontend Included**: A basic HTML/JavaScript frontend is provided in `templates/index.html` to test the API

## 🚀 How It Works

The application follows a simple workflow:

1. A user sends a prompt to the `/api/v1/generate-image` endpoint
2. The Flask server receives the request and enhances the prompt with cinematic and high-quality keywords
3. It uses the `gradio_client` library to connect to the specified Hugging Face Space using your API token
4. The client sends the enhanced prompt to the HF Space, which generates an image
5. The HF Space returns a temporary local file path for the generated image
6. The Flask server reads this image file, saves it permanently to its own `static/generated_images` directory
7. Finally, the server returns a JSON response containing the public URL of the newly saved image

## 🛠️ Setup and Installation

Follow these steps to get the application running on your local machine.

### Prerequisites

- Python 3.8+
- A Hugging Face Account
- A Hugging Face User Access Token with read permissions

### 1. Clone the Repository

```bash
git clone https://github.com/SakibAhmedShuva/Free-Hugging-Face-Space-API-Usage-with-Web-App.git
cd Free-Hugging-Face-Space-API-Usage-with-Web-App
```

### 2. Create a Virtual Environment

It's highly recommended to use a virtual environment to manage dependencies.

```bash
# For Windows
python -m venv venv
venv\Scripts\activate

# For macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a file named `.env` in the root directory of the project. Copy the contents of the example below and fill in your own values.

#### `.env` Example

```env
# --- Hugging Face Configuration ---

# The name of the Hugging Face Space you want to use (e.g., "stabilityai/stable-diffusion-3-medium-diffusers")
GRADIO_HF_SPACE_NAME="multimodalart/stable-diffusion-v1-4"

# Your Hugging Face User Access Token (https://huggingface.co/settings/tokens)
HF_TOKEN="hf_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# (Optional) The specific API name in the Gradio app if it's not the default.
# Most of the time, you can leave this commented out.
# GRADIO_API_NAME="/run"
```

### 5. Run the Application

```bash
flask run
```

The application will start on `http://127.0.0.1:5000` by default. You can open this URL in your browser to see the example frontend or start making requests to the API.

## 📦 API Usage

The core of this project is its API endpoint for image generation.

### Endpoint Details

- **URL**: `/api/v1/generate-image`
- **Method**: `POST`
- **Headers**: `Content-Type: application/json`

### Request Body

```json
{
  "prompt": "a majestic lion wearing a crown, studio lighting"
}
```

### Example cURL Request

```bash
curl -X POST http://127.0.0.1:5000/api/v1/generate-image \
-H "Content-Type: application/json" \
-d '{"prompt": "a majestic lion wearing a crown, studio lighting"}'
```

### Responses

#### Success Response (200 OK)

The server will respond with the original prompt and the URL of the generated image.

```json
{
  "imageUrl": "http://127.0.0.1:5000/static/generated_images/f8b2a1c1-5e7e-4b2a-8c9d-1e2f3a4b5c6d.png",
  "prompt": "a majestic lion wearing a crown, studio lighting"
}
```

#### Error Response (500 Internal Server Error)

If the Hugging Face service fails or is misconfigured.

```json
{
  "error": "Internal Server Error",
  "message": "The image generation service failed. Details: <error message from the service>"
}
```

## 📁 Project Structure

```
.
├── static/
│   └── generated_images/   # Generated images are stored here
├── templates/
│   └── index.html          # Simple frontend for testing
├── .env                    # Your local environment variables (you must create this)
├── app.py                  # The main Flask application logic
├── requirements.txt        # Python dependencies
└── README.md               # This file
```

## 🤝 Contributing

Contributions are welcome! If you have suggestions for improvements or find a bug, please feel free to:

1. Fork the repository
2. Create a new feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📜 License

This project is distributed under the MIT License. See the `LICENSE` file for more information.

---

<div align="center">
  <strong>Made with ❤️ and powered by Hugging Face 🤗</strong>
</div>
