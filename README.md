# Case Study (CS3) - Classification of Dermal Medical Imaging
## Software 

Primary Software: Jupyter Notebook  
  
Add-on Packages: 
- os  
- numpy  
- pandas  
- matplotlib.pyplot  
- seaborn
- Image (from PIL)
- StratifiedKFold (from sklearn.model_selection)
- StandardScaler, OneHotEncoder, LabelEncoder (from sklearn.preprocessing)
- compute_class_weight (from sklearn.utils.class_weight)
- classification_report, confusion_matrix, f1_score (from sklearn.metrics)
- RandomForestClassifier (from sklearn.ensemble)
- tensorflow  
- keras (from tensorflow)
- layers (from tensorflow.keras)
- MobileNetV2 (from tensorflow.keras.applications)
- preprocess_input (tensorflow.keras.applications.mobilenet_v2)
- image (from tensorflow.keras.preprocessing)
- EarlyStopping (from tensorflow.keras.callbacks)
- ResNet50 (from tensorflow.keras.applications)
- preprocess_input (from tensorflow.keras.applications.resnet50)  

Platform: macOS

## Documentation Map

```
data/
└── metadata

scripts/
├── eda.ipynb
├── mobilenetv2_modeling_and_analysis.ipynb
└── resnet_model_and_analysis.ipynb

.gitignore
CS3_Hook_NicoM.pdf
CS3_Rubric_NicoM.pdf
LICENSE
README.md
```

## Instructions 

### i.) Pulling the Data  
- The data was obtained a dataset from the Harvard Dataverse called “The HAM10000 dataset, a large collection of multi-source dermatoscopic images of common pigmented skin lesions.” The dataset includes two zip files: HAM10000_images_part_1.zip and HAM10000_images_part_2.zip. These two files were unzipped and combined to create one large file which we used for our models. Each file had roughly 5,000 jpegs so the large combined file has over 10,000 jpegs. Due to the size of the combined file, the dataset is too large to upload onto github. Once the large file is created, the data can be stored locally and used to run the models. We also uploaded the metadata file to use for a multimodal model. The link to these files can be found here: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T

### Pre-Coding
- Download the required packages

### Metadata EDA  
1. Upload the dataset metadata and images folder  
2. Create a new colum that adds the image path (using the image_id column of the metadata) to the metadata  
3. Create a graph of the distribution of types of pigmented lesions save as an image to the outputs folder on Github  
4. Create a graph of the distribution of age and save as an image to the outputs folder on Github  
5. Create a graph of the distribution of of sex and save as an image to the outputs folder on Github  
6. Create a heatmap of the localization vs dx and save as an image to the outputs folder on Github  
7. Create a heatmap of the age vs dx and save as an image to the outputs folder on Github
8. Create a heatmap of the sex vs dx and save as an image to the outputs folder on Github  

- Feel free to explore additional combinations or relationships as you see fit!

### MobileNet Models
#### Cleaning 
1. Using the metadata with the image path added, check for missing values under columns: image_path, dx, and localization
2. Fill missing values for age with median
3. One-hot encode the localization column
4. Label encode the dx column
5. Define target variable to be the dx column and create a feature matrix with dx and image_path
#### Multimodal Classifier 
##### Stratified K-Fold Cross-Validation 
1. Convert boolean columns to integers (0, 1)
2. Create a stratified K-Fold cross-Validation
3. For each fold, split into training and validation set
4. Build fold dataset containing metadata features, image features, and labels
5. Append each fold dictionary to a fold list
##### Image Preprocessing and Feature Extraction  
1. Load pretrained CNN feature extractor MobileNetV2
2. Define load_and_preprocess_image to covert and resize images for model  
3. Define extract_features_batch for batch of images to load and preprocess images, run the images through the model, collect the feature vectors for the images, and stack all the results into one array  
##### Classifier  
1. Create lists for macro f1, classification reports, and confusion matrices  
2. For each fold, extract images features and extract metadata features  
3. Combine image and metadata features into one feature vector
4. Compute class_weight so that there is no class imbalance
5. Define the model and train with early stopping, class weights and validation data
##### Model Evaluation 
1. Compute the classifcation report with precision, recall, and f1 score, and macro f1 score and save as an image in classification_report folder in outputs folder on Github  
3. Create confusion matrix and save as an image in confusion matrices folder in outputs folder on Githib
#### Image-Only Classifier
(Repeat as above without metadata)
##### Stratified K-Fold Cross-Validation 
1. Create a stratified K-Fold cross-Validation
2. For each fold, split into training and validation set
3. Build fold dataset containing image features, and labels
4. Append each fold dictionary to a fold list
##### Image Preprocessing and Feature Extraction  
1. Load pretrained CNN feature extractor MobileNetV2
2. Define load_and_preprocess_image to covert and resize images for model  
3. Define extract_features_batch for batch of images to load and preprocess images, run the images through the model, collect the feature vectors for the images, and stack all the results into one array  
##### Classifier  
1. Create lists for macro f1, classification reports, and confusion matrices
2. Define class labels
4. For each fold split, extract images features
6. Compute class_weight so that there is no class imbalance
7. define the model and train with early stopping, class weights and validation data
##### Model Evaluation 
1. Compute the classifcation report with precision, recall, and f1 score, and macro f1 score and save as an image in classification_report folder in outputs folder on Github  
3. Create confusion matrix and save as an image in confusion matrices folder in outputs folder on Githib

### Resnet Models 
(structurally identical to MobileNetV2 model)
#### Cleaning 
1. Using the metadata with the image path added, check for missing values under columns: image_path, dx, and localization
2. Fill missing values for age with median
3. One-hot encode the localization column
4. Label encode the dx column
5. Define target variable to be the dx column and create a feature matrix with dx and image_path
#### Multimodal Classifier 
##### Stratified K-Fold Cross-Validation 
1. Convert boolean columns to integers (0, 1)
2. Create a stratified K-Fold cross-Validation
3. For each fold, split into training and validation set
4. Build fold dataset containing metadata features, image features, and labels
5. Append each fold dictionary to a fold list
##### Image Preprocessing and Feature Extraction  
1. Load pretrained CNN feature extractor ResNet50  
2. Define load_and_preprocess_image to covert and resize images for model  
3. Define extract_features_batch for batch of images to load and preprocess images, run the images through the model, collect the feature vectors for the images, and stack all the results into one array  
##### Classifier  
1. Create lists for macro f1, classification reports, and confusion matrices  
2. For each fold, extract images features and extract metadata features  
3. Combine image and metadata features into one feature vector
4. Compute class_weight so that there is no class imbalance
5. Define the model and train with early stopping, class weights and validation data
##### Model Evaluation 
1. Compute the classifcation report with precision, recall, and f1 score, and macro f1 score and save as an image in classification_report folder in outputs folder on Github  
3. Create confusion matrix and save as an image in confusion matrices folder in outputs folder on Githib
#### Image-Only Classifier
(Repeat as above without metadata)
##### Stratified K-Fold Cross-Validation 
1. Create a stratified K-Fold cross-Validation
2. For each fold, split into training and validation set
3. Build fold dataset containing image features, and labels
4. Append each fold dictionary to a fold list
##### Image Preprocessing and Feature Extraction  
1. Load pretrained CNN feature extractor MobileNetV2
2. Define load_and_preprocess_image to covert and resize images for model  
3. Define extract_features_batch for batch of images to load and preprocess images, run the images through the model, collect the feature vectors for the images, and stack all the results into one array  
##### Classifier  
1. Create lists for macro f1, classification reports, and confusion matrices
2. Define class labels
4. For each fold split, extract images features
6. Compute class_weight so that there is no class imbalance
7. define the model and train with early stopping, class weights and validation data
##### Model Evaluation 
1. Compute the classifcation report with precision, recall, and f1 score, and macro f1 score and save as an image in classification_report folder in outputs folder on Github  
3. Create confusion matrix and save as an image in confusion matrices folder in outputs folder on Githib

## Note

The dataset in which we used for this project includes it's own license concerning the contents of the data. The license can be found here: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T&version=4.0&selectTab=termsTab
