
# Convolutional Neural Network for Medical Imaging Analysis - Abnormality detection in mammography


The objective of the final project is to perform abnormality classification in mammography using Convolutional Neural Networks

## Original Dataset:
The dataset we will focus on is **CBIS DDSM: Curated Breast Imaging Subset of Digital Database for Screening Mammography**
The original data along with a detailed description of the collection and the policies about usage and citation can be found here: https://wiki.cancerimagingarchive.net/display/Public/CBIS-DDSM

This collection is freely available to browse, download, and use for commercial, scientific and educational purposes as outlined in the [Creative Commons Attribution 3.0 Unported License](https://creativecommons.org/licenses/by/3.0/).


A description of the dataset is provided in:
> Lee, Rebecca Sawyer, et al. "A curated mammography data set for use in computer-aided detection and diagnosis research." Scientific data 4 (2017): 170177. URL:
https://www.nature.com/articles/sdata2017177



The original images are in DICOM format, the standard format for the communication and management of medical imaging information and related data.

You can find images related to a sample from the original dataset at the following URLs:
- [full mammograms](https://github.com/alerenda/computational_intelligence_project/blob/master/a.jpeg)
- [ROI of abnormality](https://github.com/alerenda/computational_intelligence_project/blob/master/c.png)
- [patches of abnormality](https://github.com/alerenda/computational_intelligence_project/blob/master/b.png)
 

Please notice that:
- Full images have a high resolution, e.g. 3000x4000
- Full images and patches are grayscale images with a depth of 16bit

### Two-classes Classification problem
There are two types of abnormalities
- calcifications:  tiny deposits of calcium that appear as bright spots in mammograms
- masses: space-occupying lesions seen in more than one projection


### Further description of abnormalities

[Here](https://wiki.cancerimagingarchive.net/display/Public/CBIS-DDSM#510bc7863f3042f59a27301f1f4b6bef), several csv files are provided with the description of each image. The fields are the following
 - patient_id, breast density, left or right breast, image view, abnormality id, abnormality type, calc type, calc distribution, assessment, pathology, subtlety, image file path, cropped image file path, ROI mask file path
 
This description enables another **optional** task: **diagnosis classification**.
In the original dataset each abnormality is labeled as:
- Benign without callback (i.e. no additional films or biopsy was done to make the benign finding)
- Benign
- Malignant

## Dataset as it is provided:

Dealing with original dataset is critical since full images are high resolution and the DICOM format is not natively supported in keras.

Indeed, preprocessing steps have been performed to provide only the patches images in a proper format.

**You are provided with numpy arrays containing images and labels from training and test sets.**

The following operations have been performed.
- images of patches were selected from the original dataset
- images of patches were loaded and resized to different shapes (512x512 - 224x224 - 150x150) using OpenCV resize function: `cv2.resize(img, dsize=(shape, shape), interpolation=cv2.INTER_NEAREST)`
- numpy arrays of labels and images were saved:
  - train_lab.npy
  - train_img_150.npy
  - train_img_224.npy
  - train_img_512.npy
  - public_test_lab.npy
  - public_test_img_150.npy
  - public_test_img_224.npy
  - public_test_img_512.npy
- labels are encoded as follows:
  - Masses vs Calcification Classification:
    - 'MASSES' label = 0
    - 'CALCIFICATIONS' label = 1
  - Malignant, Benign, Benign_without_callback Classification:
    - 'MALIGNANT' label = 0
    - 'BENIGN_WITHOUT_CALLBACK' label = 1
    - 'BENIGN'  label = 2

**You will be able to load the arrays using `numpy load` function.**




 ## Project Aims and Requirements
 
 

The project is inspired to the work described in 
 > [1] Xi, P.  Shu, C.,  Goubran, R., Abnormality Detection in Mammography using Deep Convolutional Neural Networks, 13th IEEE International Symposium on Medical Measurements and Applications, MeMeA 2018; Universita La SapienzaRome; Italy; 11 June 2018 through 13 June 2018; Category numberCFP18MEA-USB; Code 138764
 





### Basic delivery

1. Analysis of the state of the art techniques related with the case study (at least [1]) 

2. Development of a classification model for discriminating between masses and calcification [**CNN.ipynb**]
  - Design and development of an ad-hoc CNN architecture (training from scratch).

3. Development of a classification model for discriminating between masses and calcification.  [**CNN-PT.ipynb**]
  - Usage of a pre-trained state-of-the-art architecture
 
4. Demonstrate mastery of deep learning base concepts:
  - hyperparameters search and evaluation of underfitting / overfitting in this case study
  - application of regularization techniques

5. Development of a composite classifier (Ensemble of Neural Networks) to boost classification performance  [**ENSEMBLE.ipynb**]


**The submission of yuor projects will consist in the following files**:
- [**CNN.ipynb**] a notebook file (ipynb) for the solution with the CNN from scratch architecture, adequately described and commented.
- [**CNN-PT.ipynb**] a notebook file (ipynb) for the solution with the pre-trained architecture, adequately described and commented.
- [**ENSEMBLE.ipynb**] a notebook file (ipynb) for the solution with the ensemble, adequately described and commented:
  - the file will load *different*, already trained, models (or their prediction) and will compute the output of the composite classifier. 
- [**REPORT.pdf**] The report should include:
  - A brief description of the state of the art
  - A detailed description of the proposed solutions, highlighting the motivation behind the performed choices, with commented figures and plots.
    - E.g.: 
        - *simple model -> accuracy curves obtained on a validation set allows to observe underfitting*
        - *more complex model -> accuracy curves obtained on a validation set allows to observe overfitting*
        - *application of these regularization techniques: ... *
        - *performed these hyperparameters search: ...*
        - *hyperparameters chosen according to ...*
        
   
  
  
  
  
  






### Optional delivery:  
**In addition to** the basic delivery:
- Usage of trained CNN to perform localization task
  - inspired to [1] and / or Lecture Notebook: 9_Visualizing_what_Convnets_learn 
  - it is an open issue: we will consider positively any attempt to cope with this problem even if no positive results are achieved (provided that they are properly justified).
- Development of a classification model for diagnosis: discriminating between Benign without callback, Benign, Malignant

### Particularly appreciated:
- Usage of algorithms, techniques and architectures that were not presented during the course
- Creativity!
- High performance models:
  - Do not fit your model (params or hyperparams) on the provided *public test set*: your notebook will be tested replacing the *public test set* with a *private test set*. The leaderboard will be published on the course site.
  

# References
- Dataset:
  -  Rebecca Sawyer Lee, Francisco Gimenez, Assaf Hoogi , Daniel Rubin  (2016). Curated Breast Imaging Subset of DDSM. The Cancer Imaging Archive. http://dx.doi.org/10.7937/K9/TCIA.2016.7O02S9CY

  - Rebecca Sawyer Lee, Francisco Gimenez, Assaf Hoogi, Kanae Kawai Miyake, Mia Gorovoy & Daniel L. Rubin. A curated mammography data set for use in computer-aided detection and diagnosis research. Scientific Data volume 4, Article number: 170177 (2017) (link)

  - Clark K, Vendt B, Smith K, Freymann J, Kirby J, Koppel P, Moore S, Phillips S, Maffitt D, Pringle M, Tarbox L, Prior F. The Cancer Imaging Archive (TCIA): Maintaining and Operating a Public Information Repository, Journal of Digital Imaging, Volume 26, Number 6, December, 2013, pp 1045-1057. (paper)

- Related work:
  - Xi, P.  Shu, C.,  Goubran, R., Abnormality Detection in Mammography using Deep Convolutional Neural Networks, 13th IEEE International Symposium on Medical Measurements and Applications, MeMeA 2018; Universita La SapienzaRome; Italy; 11 June 2018 through 13 June 2018; Category numberCFP18MEA-USB; Code 138764
