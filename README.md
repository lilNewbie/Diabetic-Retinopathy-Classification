# Diabetic Retinopathy Classification

This repository contains a summary of my approaches to Image Classification on the Diabetic Retinopathy [Dataset](https://www.kaggle.com/datasets/amanneo/diabetic-retinopathy-resized-arranged)

## Preprocessing
- Resizing to image height and width of 224 pixels
- A variation of Ben Graham's [Preprocessing](https://www.kaggle.com/code/ratthachat/aptos-eye-preprocessing-in-diabetic-retinopathy#2.-Try-Ben-Graham's-preprocessing-method.)
- Using convertScaleAbs() function from OpenCV
- Up-sampling the training dataset by merging images
- Preprocessing using the ImageDataGenerator from Keras

### Up-sampling methods used
- Random Flipping
- Using a duplicate
- Merging two images
### Merging function
* The **Merge function** merges two similar images belonging to the same class. 
* Each image is named as 'xxxxx_left.jpg' or 'xxxxx_right.jpg'. Similarity of the image is decided using the filename to identify left and right eyeballs. 
* The two chosen images are added using the [cv2.addWeighted()](https://docs.opencv.org/4.x/d2/de8/group__core__array.html#gafafb2513349db3bcff51f54ee5592a19) function.
