### Prerequisites

*   Python 3.x
*   TensorFlow/Keras (`pip install tensorflow`)
*   Matplotlib (`pip install matplotlib`)
*   NumPy (`pip install numpy`)

# Image Augmentation with Keras

This repository provides a simple yet effective Python script for augmenting images using the `tensorflow.keras` library's `ImageDataGenerator`. Image augmentation is a crucial technique in deep learning, used to artificially increase the size of a training dataset by applying various transformations to existing images. This helps improve the generalization ability of models and prevents overfitting.

This script uses the `ImageDataGenerator` class from Keras to perform the following augmentations:

*   **Rescaling:** Normalizes pixel values to the range [0, 1] (divides by 255).
*   **Shearing:** Applies a shear transformation to the image, distorting it along one axis.
*   **Zooming:** Zooms in or out on the image.
*   **Horizontal and Vertical Flipping:** Flips the image horizontally or vertically.
*   **Rotation:** Rotates the image by a random angle within a specified range.
*   **Horizontal and Vertical Shifts:** Shifts the image horizontally or vertically by a fraction of the image's width or height.

The script loads a single image, applies the specified augmentations, and displays a grid of 9 augmented images using `matplotlib`. It's easily adaptable to augment larger datasets by integrating it into your training pipeline (see the "Usage in a Training Loop" section).

## Getting Started

### Prerequisites

*   Python 3.x
*   TensorFlow/Keras (`pip install tensorflow`)
*   Matplotlib (`pip install matplotlib`)
*   NumPy (`pip install numpy`)

### Installation

1.  Clone the repository:

    ```bash
    git clone [invalid URL removed]
    ```

2.  Navigate to the repository directory:

    ```bash
    cd IMAGE-AUGMENTATION
    ```

### Usage

1.  Place the image you want to augment (e.g., `input_image.jpg`) in the same directory as the `image_augmenter.py` script.

2.  Run the script:

    ```bash
    python image_augmenter.py input_image.jpg
    ```
    If you do not specify an image, the script will look for `tim.jpg`

3.  The script will generate a Matplotlib window displaying 9 augmented versions of your input image.

### Usage in a Training Loop (Example)

To use this within a training loop for a larger dataset, you would typically use the `flow_from_directory` method of the `ImageDataGenerator`. Here's a basic example:

```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

datagen = ImageDataGenerator(
    rescale=1./255,
    shear_range=0.2,
    zoom_range=0.2,
    horizontal_flip=True
)

train_generator = datagen.flow_from_directory(
    'path/to/your/training/data', # Path to your training data directory
    target_size=(150, 150),       # Resize images to this size
    batch_size=32,                # Batch size
    class_mode='categorical'      # Or 'binary' depending on your problem
)

# Then use train_generator in your model's fit method:
# model.fit(train_generator, ...)
