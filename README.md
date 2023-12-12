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

Sample Image produced - 

![merged_preprocess](https://github.com/lilNewbie/Diabetic-Retinopathy-Classification/assets/90834922/0d35bcb3-9af3-4a41-b593-f79851b8ce9b)


## Approaches

### **Using Transfer Learning with the Up-sampling Approach**
I used CNN models obtained from [Keras Applications](https://email-with-gpt-by-lilnewbie.streamlit.app/) and used the pre-trained weights of these models. I removed the existing classifier and added my own classifier to it.

These models were then trained on the up-sampled data.

### **The Machine Learning Approach**
The Machine Learning Approach involves the use of supervised Machine Learning algorithms to classify the flattened images into their respective classes.

Using Machine Learning methods on the 224×224×3 images was not possible due to the sheer size of the dataset produced when the images are flattened. Compressing the images to a smaller resolution would result in a loss of data.

Thus, I passed the 224×224×3 images through a pre-trained CNN model and took the outputs from the final CNN layer of the model. 

The output dimensions were 7×7×512. To reduce dimensionality, I took the mean across the last channel to get a 7×7 output per image.

These outputs were then flattened and added to a dataframe which was then used to train the classifiers.

I used a total of 5000 images from the up-sampled and preprocessed dataset resulting in a dataset having 50 columns (49 features from the flattened output and 1 target column) and 5000 rows.

### **The Ensemble Approach** 
The Ensemble Approach involved the use of three CNN models which were trained on the up-sampled dataset separately. 

These models were then run on the test-data and the probabilities of the predictions of each model were used to compute a weighted mean of probabilities. This weighted mean was used to predict the class of the image.

The weights were assigned according to the performances of the models on the validation set.

This approach worked the best when compared to the other approaches.
