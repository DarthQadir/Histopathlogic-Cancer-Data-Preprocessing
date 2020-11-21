
<h3 align="center">
This repository serves as a guide to preparing  <a href="https://www.kaggle.com/c/histopathologic-cancer-detection"> Kaggle's Histopathologic Cancer detection challenge's </a>  data.
  <br></br>
</h3>

**A thorough tutorial with explanations can be found [here](https://towardsdatascience.com/data-preparation-guide-for-detecting-histopathologic-cancer-detection-7b96d6a12004)**
<br><br>

The Jupyter Notebook contains 4 sections:

1. How to download the dataset off Kaggle.
2. How to augment images
3. How to balance target distributions
4. How to structure the data for Keras Model Training

<br>


<h3 align='center'> How to download the dataset off Kaggle. </h3>

Kaggle provides a wonderful API one can use to directly download their dataset. This section of the notebook provides code which you can use to download data off Kaggle. It is applicable to any Kaggle dataset but I showcase its usage for the Histopathologic Cancer data.

*Command line code for downloading the dataset*
<br><br>

```
! kaggle competitions download -c histopathologic-cancer-detection
```

<br>

<h3 align='center'> How to augment images </h3>

Image augmentation is important so our machine learning models are able to generalize more easily. This section of the notebook provides a function which can be used to augment images with rotations, contrast changes, brightness changes etc.

*Function used for image augmentation*
<br><br>
```
readCroppedImage(path, augmentations = True,ORIGINAL_SIZE=96, CROP_SIZE=90, RANDOM_ROTATION=3, RANDOM_SHIFT = 2,RANDOM_BRIGHTNESS = 7, RANDOM_CONTRAST = 5,
RANDOM_90_DEG_TURN=1):
```
                    
<h3 align='center'>How to balance target distributions</h3>

In our training dataset, we need to make sure that the distribution of our classes if equal. This ensures that our model learns how to classify each class equally well. If we don't do this, our model may only work really well on the class with more datapoints, while failing at classifying other classes.

*Code for a 60% training, 20% testing, and 20% validation data split*
<br><br>
```
df_train, df_val, df_test = np.split(df_data.sample(frac=1), [int(.6*len(df_data)), int(.8*len(df_data))])
```


<h3 align='center'>How to structure the data for Keras Model Training</h3>

In case datasets are too big to fit in our memory, we use generators. Generators pass our data in batches instead of all at once; and they also require your data to be structured in a specific way to work. This section includes code on how to create such a directory structure.


<br><br>
*Below is the directory structure that a keras generator needs for the cancer detection dataset*
```
- Training data folder
  - a_no_tumor_tissue folder
  
  - b_has_tumor_tissue folder
  
- Testing data folder
  - a_no_tumor_tissue folder
  - b_has_tumor_tissue folder
  
- Validation data folder
  - a_no_tumor_tissue folder
  - b_has_tumor_tissue folder
 
  ```
