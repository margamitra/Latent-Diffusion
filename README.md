# Latent Diffusion Model README

This project implements a **Latent Diffusion Model (LDM)** for **text-to-image generation**. It utilizes **UNet** architecture and **Variational Autoencoders (VAE)** to create high-quality images from textual descriptions. The model works by transforming textual prompts into embeddings and then refining latent variables through a denoising process to generate realistic images.

## The Basic Workflow

The Latent Diffusion Model workflow operates through several key stages to convert text prompts into images. Here is a step-by-step breakdown of the process:

### 1. **Textual Input Preprocessing**
   The user provides textual prompts, which describe the image they wish to generate. These prompts are processed by a **text encoder** (CLIP model), which transforms the text into a fixed-dimensional embedding that will guide the image generation process.

   - **Text Encoding**: The text prompts are tokenized and passed through the encoder to obtain embeddings representing the semantic meaning of the input.

### 2. **Latent Space Representation**
   Instead of directly working in image space, the model operates in a **latent space**. This is achieved using a **Variational Autoencoder (VAE)**, which encodes images into a compact latent representation, and later decodes them back into the image space.

   - **Latent Encoding**: If an image is provided, it is encoded into its latent representation using the VAE encoder.
   - **Latent Sampling**: For fresh generation, random noise is initialized in the latent space to begin the image creation process.

### 3. **Diffusion Process in Latent Space**
   The core of the image generation process lies in the **diffusion** mechanism. Starting from random noise, the model iteratively refines the latent variables through multiple **denoising steps**. This process uses the **UNet architecture** to predict and remove noise at each step.

   - **Noise Addition**: At each diffusion step, noise is added to the latent variables to simulate how images become corrupted by noise.
   - **Denoising with UNet**: The **UNet** architecture, known for its encoder-decoder structure, progressively denoises the latents, refining them step-by-step into a coherent image.
     - The UNet helps both in **upsampling** the features in the lower-resolution latent space and in **decoding** to produce final image details from the noisy latent input.

### 4. **Guided Generation with Classifier-Free Guidance**
   To ensure that the generated image closely aligns with the text prompt, **classifier-free guidance** is applied during the denoising process. This technique steers the generation process to adhere more strongly to the prompt's semantics without requiring a separate classifier.

   - **Class Guidance**: The guidance term \( g \) controls how strongly the text embedding influences the final image generation.

### 5. **Final Image Decoding**
   After several denoising steps, the final latent representation is passed through the **VAE decoder** to transform it back into image space. The result is the generated image.

   - **Image Output**: The latent representation is decoded into an image, followed by necessary post-processing like scaling and normalization.

### 6. **Visualization**
   As the image is being generated, intermediate images can be saved and visualized at various diffusion steps to track the progress of the model. This feature helps to understand how the latent variables evolve over time.

## Key Components
- **Text Encoder (CLIP)**: Converts textual prompts into embeddings.
- **VAE (AutoencoderKL)**: Encodes images into a latent space and decodes them back into image space.
- **UNet**: Denoises and refines the latent variables, progressively increasing the image's resolution.
- **Classifier-Free Guidance**: Guides the generation process based on the text embedding.
- **Latent Diffusion**: The iterative process that refines random latent variables to generate high-quality images.

## Results
![image](https://github.com/user-attachments/assets/744f08d2-2767-4c47-a800-65159e6abff0)
### Prompt: 
"An otter wearing sunglasses relaxing on a floating tube in a swimming pool, on a sunny day."
![image](https://github.com/user-attachments/assets/45879d63-914e-4152-932a-69909362efa8)
### Prompt: 
"A cute blue-green space rover like wall-E with cute eyes, lost on a strange planet,cool earth tones"


