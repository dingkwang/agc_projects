# Product Requirements Document (PRD) - Video Generation MVP

## 1. MVP Video Generation using `veo3_video_generation.ipynb`

This section outlines the capabilities and requirements for the Minimum Viable Product (MVP) of video generation, leveraging the `veo3_video_generation.ipynb` notebook. This notebook demonstrates interaction with Google's Veo 3 model for generating high-quality videos from text and image prompts.

### 1.1. Introduction to Veo 3

Veo 3 on Vertex AI provides access to Google's advanced video generation capabilities. It creates videos with detailed visuals and realistic physics across various styles, supporting enhanced video quality from text and image prompts, and now includes dialogue and audio generation.

### 1.2. Prerequisites

To run the `veo3_video_generation.ipynb` notebook and utilize Veo 3, the following are required:

*   **Google Cloud Project:** An existing Google Cloud project with the Vertex AI API enabled.
*   **Google Gen AI SDK for Python:** Installation of the `google-genai` library.
    ```bash
    %pip install --upgrade --quiet google-genai
    ```
*   **Authentication:** If running in Google Colab, user authentication is necessary.
*   **Project Configuration:** Set `PROJECT_ID` and `LOCATION` variables within the notebook to your Google Cloud project details.

### 1.3. Core Functionality: Video Generation

The MVP focuses on two primary methods of video generation:

#### 1.3.1. Text-to-Video Generation

Users can generate videos by providing a text prompt. The process involves:

*   **Prompt Definition:** A detailed text description of the desired video content. The notebook includes an optional step to optimize prompts using Gemini, combining keywords for subject, action, scene, camera angles, movements, lens effects, style, and temporal elements.
*   **Audio Generation:** Option to include audio in the output video.
*   **Configurable Parameters:**
    *   `model`: `veo-3.0-generate-001` (standard quality) or `veo-3.0-fast-generate-001` (lower latency).
    *   `prompt`: The text prompt for video generation.
    *   `enhance_prompt`: Boolean to enable/disable prompt enhancement by the model.
    *   `generate_audio`: Boolean to enable/disable audio generation.
    *   `aspect_ratio`: e.g., "16:9".
    *   `number_of_videos`: Number of videos to generate (1 or 2).
    *   `duration_seconds`: Video duration (e.g., 8 seconds).
    *   `resolution`: e.g., "1080p" or "720p".
    *   `person_generation`: Controls generation of people (e.g., "allow_adult", "dont_allow").
*   **Output:** Generated video can be displayed directly in the notebook or stored in a specified Google Cloud Storage (GCS) bucket.

#### 1.3.2. Image-to-Video Generation

Users can generate videos by starting with an input image, with optional text prompts to guide motion and audio. The process involves:

*   **Starting Image:** Provide a local image file (e.g., `flowers.png` as in the example).
*   **Prompt Optimization (Optional):** Similar to text-to-video, Gemini can be used to combine image content with keywords for camera motion, subject animation, environmental animation, and audio.
*   **Configurable Parameters:**
    *   `model`: `veo-3.0-generate-preview`.
    *   `prompt`: Optional text prompt to guide motion and audio.
    *   `image`: The input image file.
    *   Other parameters (`enhance_prompt`, `generate_audio`, `aspect_ratio`, `number_of_videos`, `duration_seconds`, `resolution`, `person_generation`) are similar to text-to-video.
*   **Output:** Generated video can be displayed directly in the notebook.

## 2. Exploring `Wan-AI/Wan2.1-FLF2V-14B-720P-diffusers`

This section outlines the approach to exploring and running the `Wan-AI/Wan2.1-FLF2V-14B-720P-diffusers` model from Hugging Face.

### 2.1. Model Overview

`Wan-AI/Wan2.1-FLF2V-14B-720P-diffusers` is a model hosted on Hugging Face, likely designed for video generation or manipulation, given the "FLF2V" (Frame-Level Feature to Video) and "diffusers" in its name. The "720P" suggests its output resolution.

### 2.2. Approach to Running the Model

To run this model, the standard approach involves using the Hugging Face `diffusers` library in Python.

#### 2.2.1. Key Steps

1.  **Environment Setup:**
    *   Ensure Python is installed.
    *   Install the necessary libraries: `diffusers`, `transformers`, and potentially `accelerate` for optimized performance.
        ```bash
        pip install diffusers transformers accelerate
        ```
2.  **Model Loading:**
    *   Import `DiffusionPipeline` from `diffusers`.
    *   Load the model using its Hugging Face identifier.
        ```python
        from diffusers import DiffusionPipeline

        model_id = "Wan-AI/Wan2.1-FLF2V-14B-720P-diffusers"
        pipeline = DiffusionPipeline.from_pretrained(model_id)
        # If using a GPU, move the pipeline to GPU
        # pipeline.to("cuda")
        ```
3.  **Inference:**
    *   The specific input required for inference (e.g., text prompt, image, video frames) will depend on the model's design. Refer to the model card on Hugging Face for details.
    *   Typically, you would call the pipeline with your input.
        ```python
        # Example (replace with actual model input requirements)
        prompt = "A futuristic city at sunset"
        video_frames = pipeline(prompt).frames
        # Process or save video_frames
        ```
4.  **Review Hugging Face Model Card:**
    *   **Crucially**, visit the model's page on Hugging Face (`https://huggingface.co/Wan-AI/Wan2.1-FLF2V-14B-720P-diffusers`).
    *   The model card provides:
        *   Detailed usage instructions.
        *   Required dependencies beyond `diffusers`.
        *   Example code snippets for inference.
        *   Information on input/output formats.
        *   Any specific hardware requirements (e.g., GPU memory).
        *   Licensing information.

By following these steps and consulting the official Hugging Face model card, one can effectively explore and run the `Wan-AI/Wan2.1-FLF2V-14B-720P-diffusers` model.
