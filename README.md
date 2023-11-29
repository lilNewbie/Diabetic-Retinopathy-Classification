# Diabetic Retinopathy Classification

This repository contains a summary of my approaches to Image Classification on the Diabetic Retinopathy [Dataset](https://www.kaggle.com/datasets/amanneo/diabetic-retinopathy-resized-arranged)

## Preprocessing
- Resizing to image height and width of 224 pixels
- A variation of Ben Graham's [Preprocessing](https://www.kaggle.com/code/ratthachat/aptos-eye-preprocessing-in-diabetic-retinopathy#2.-Try-Ben-Graham's-preprocessing-method.)
- Using convertScaleAbs() function from OpenCV
- Up-sampling the training dataset by merging images
- Preprocessing using the ImageDataGenerator from Keras
