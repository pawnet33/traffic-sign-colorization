# Traffic Sign Image Colorization

## Project Overview

This project focuses on automatic colorization of grayscale traffic sign images using deep learning. Two convolutional autoencoder architectures are implemented and compared to evaluate different approaches to image reconstruction.

The models learn to predict color information from grayscale images while preserving their original structure and details.

## Dataset

The project uses the **German Traffic Sign Recognition Benchmark (GTSRB)** dataset.

- Training set: 26,640 images
- Test set: 12,630 images
- Image resolution: 64 × 64 pixels

Images are resized to 64 × 64 pixels before being used for training.

## Methodology

The colorization task is performed in the CIELAB color space:

- **L channel** – represents image lightness and is used as model input.
- **a and b channels** – represent color information and are used as prediction targets.

This approach separates image structure from color information, allowing the models to focus on predicting colors while retaining the original luminance.

## Models

Two convolutional autoencoder architectures are implemented using a shared encoder:

**1. Transposed Convolution Autoencoder**
- Convolutional encoder with four downsampling layers.
- Decoder based on transposed convolutions.
- Reconstructs the color channels from the grayscale input.

**2. Interpolation + Convolution Autoencoder**
- Uses the same encoder architecture.
- Decoder combines bilinear interpolation with standard convolutional layers.
- Gradually increases spatial resolution to reconstruct the color channels.

## Training

Both models are trained using the following configuration:

| Parameter | Value |
|---|---|
| Optimizer | Adam |
| Learning rate | 0.001 |
| Loss function | L1 Loss |
| Epochs | 10 |
| Batch size | 64 |
| Image size | 64 × 64 |

Training is performed using PyTorch.

## Results

Both architectures demonstrate stable convergence during training.

| Model | Initial Loss | Final Loss |
|---|---:|---:|
| Transposed Convolution AE | 0.05300 | 0.02403 |
| Interpolation + Convolution AE | 0.05285 | 0.02713 |

The Transposed Convolution Autoencoder achieves a lower final training loss and converges faster.

Visual comparison on test images shows no substantial differences between the two approaches.

The models also generalize reasonably well to external images resembling the training dataset. However, their performance decreases on images from significantly different environments.

## Technologies

- Python
- PyTorch
- Torchvision
- NumPy
- Matplotlib
- scikit-image
- Pillow
- Jupyter Notebook

## How to Run

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

2. Install the required libraries:

   ```bash
   pip install torch torchvision numpy matplotlib scikit-image pillow jupyter
   ```

3. Open the notebook:

   ```bash
   jupyter notebook traffic-sign-colorization.ipynb
   ```

4. Run the notebook cells sequentially.

The GTSRB dataset is downloaded automatically by Torchvision.

## Project Structure

```text
traffic-sign-colorization/
│
├── traffic-sign-colorization.ipynb
├── README.md
└── data/
```

## Conclusion

This project demonstrates two different approaches to image colorization using convolutional autoencoders. The experiments show that both architectures can learn to reconstruct color information from grayscale traffic sign images, with the Transposed Convolution approach achieving a lower training loss.
