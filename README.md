
# Synthetic Crack Image Generation using Diffusion Models

This project focuses on generating synthetic images of wall cracks using four distinct generative models based on diffusion principles. These models allow efficient and high-quality data augmentation for structural analysis, deep learning training, and defect detection in civil infrastructure.

## Models Used

### 1. **DDPM (Denoising Diffusion Probabilistic Model)**
A standard diffusion model trained to learn the forward and reverse process of noise corruption. Operates in pixel space.

- **Resolution:** 64×64
- **Architecture:** U-Net with attention and sinusoidal time embedding
- **Dataset:** Custom crack image dataset
- **Training Epochs:** 400
- **Accuracy:** ~66% acceptable generation quality

### 2. **LDM (Latent Diffusion Model)**
Instead of operating on pixels directly, LDM applies the diffusion process to a compressed latent space, reducing compute costs significantly.

- **Core Components:** VAE encoder/decoder, U-Net, diffusion scheduler
- **Advantage:** Enables high-resolution generation while being computationally efficient
- **Use Case:** Efficient manipulation and generation of 512×512 crack images

### 3. **DIT (Diffusion Transformer using Stable Diffusion)**
A latent diffusion model that incorporates a Transformer-based text encoder (e.g., CLIP) for prompt-based conditioning.

- **Main Components:** VAE, U-Net with cross-attention, Text Encoder
- **Prompt Example:** "Crack on a concrete wall"
- **Scheduler:** PNDM, K-LMS, Heun Discrete, or DPM Solver
- **Efficiency:** Leverages latent space and textual prompts for flexible control

### 4. **LCM-LoRA (Latent Consistency Model with Low-Rank Adaptation)**
A fine-tuned extension of the LDM model designed for fast image generation with high fidelity using few-step inference.

- **Built on:** Stable Diffusion with LoRA tuning
- **Training Tool:** kohya_ss
- **Sampling Steps:** Typically 2–3 for good results
- **Performance:** Achieves high-quality crack generation with descriptive prompts

## How to Run

Each model comes with separate inference and training scripts or pipelines. Ensure the required libraries are installed (e.g., `diffusers`, `transformers`, `torch`), and follow the respective model documentation for usage.

Example for LCM-LoRA:
```python
# Enter prompt
prompt = "Vertical crack on an old painted wall"
image = pipe(prompt, num_inference_steps=3, guidance_scale=7.5).images[0]
image.show()
```

## Results

The models can generate realistic and diverse crack patterns. Some require multiple inference steps to achieve optimal results, especially with detailed prompts. Example outputs include:

- "Sunlight shining on a cracked wall"
- "Water drain damage on concrete with split cracks"
- "Vertical fissures on aging concrete facade"

## Conclusion

By combining traditional and latent diffusion techniques, this project enables robust synthetic data generation tailored to civil infrastructure applications. Each model presents trade-offs between speed, quality, and flexibility.

## License

This project is licensed for academic and research purposes. For commercial use, please contact the author.
