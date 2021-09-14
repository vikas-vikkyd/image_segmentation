# Solution Flow

The task is for semantic image segmentation to label each pixel of image to correct labels (1 for road and 0 for not road). For this problem implemented Unet architecture which first downsample the image and then upsample to original size, in between we use skip-connections which helps in gradient vanishing problem.

# Preprocessing
Solution contains different functions to prepare data for Training.

get_image_path()- Map image with their absolute path. Example output: ['image1.png', './content/training/input/image1.png']

map_input_output()- To Map input image to masked out. [input_image, input_image_path, output_image, output_image_path]

preprocessing()- To decode and resize the image to desired shape. Resize the images to (224*224)

get_training_dataset()- To create Batched dataset for training. Created a batch of 32 examples.

get_validation_dataset()- To created Batched dataset for validation

# Model
Implemented a Unet model which has mainly three sections: encoder, bottleneck and decoder.

Encoder - Encoder has four encoder blocks, each encoder block consists of two Conv layers (64, 128, 256, 512) followed by MaxPooling layer(2*2). Downsampling of image is because of MaxPooling layer Conv layer is to extract different features from image.

Decoder- Decoder part of model consists of Conv2DTranspose to upsample the image followed by concatenate layer (skip connection) to overcome gradient vanishing problem and Dropout layer to overcome any overfitting problem.

# Training
Optimized binary cross entropy (we have just two classes 0 and 1) using Adam with learning rate 0.001 and trained for 50 epochs.

![image](https://user-images.githubusercontent.com/29758488/133234145-ffcf4853-8702-482e-bf85-9e195b465b89.png)
![image](https://user-images.githubusercontent.com/29758488/133234264-da2d53a4-0b66-4b27-ab72-3e9c8ee5e7d8.png)

# Evaluation
Made prediction on provided testing images and saved the masked images.
Calculated different evaluation metrics like accuracy, precision, recall and IOC for each images and final mean for all test images are below:

Accuracy: 0.945

Precision: 0.6167

Recall: 0.5771

IOU: 0.4264
