# Dataset Folder

This folder contains datasets used in the research paper. The datasets included are OCTA500, CORN, DRIVE, CHASEDB1, and DCA1. Please note that the images in these datasets may have undergone preprocessing steps, including cleaning and cropping. For example, CORN dataset has had overlapping samples between the training and testing sets removed; and some preprocessing like cropping for FOV has been applied.

## Dataset Details

### OCTA500 [1]
- **Images:** Contains the OCTA500 dataset images.
- **Supervised Labels:** Contains the corresponding fully supervised labels for the OCTA500 dataset.
- **Noisy Skeleton Annotations:** Contains the noisy skeleton annotations used in the paper for OCTA500 dataset.
- **h5 Files:** Contains h5 files with preprocessed images and their corresponding labels.
- **Note:** "Noisy Skeleton Annotations (only foreground)" is used for our method and is solely used for dilation to inpaint and obtain the background images. On the other hand, "Noisy Skeleton Annotations (both foreground and background)" are used for training other weakly supervised methods for comparison purposes. Same for CORN, DRIVE and CHASEDB1.
  
### CORN [2]
- **Images:** Contains the CORN dataset images.
- **Supervised Labels:** Contains the corresponding fully supervised labels for the CORN dataset.
- **Noisy Skeleton Annotations:** Contains the noisy skeleton annotations used in the paper for CORN dataset.
- **h5 Files:** Contains h5 files with preprocessed images and their corresponding labels.

### DRIVE [3]
- **Images:** Contains the DRIVE dataset images.
- **Supervised Labels:** Contains the corresponding fully supervised labels for the DRIVE dataset.
- **Noisy Skeleton Annotations:** Contains the noisy skeleton annotations used in the paper for DRIVE dataset.
- **h5 Files:** Contains h5 files with preprocessed images and their corresponding labels.

### CHASEDB1 [4]
- **Images:** Contains the CHASEDB1 dataset images.
- **Supervised Labels:** Contains the corresponding fully supervised labels for the CHASEDB1 dataset.
- **Noisy Skeleton Annotations:** Contains the noisy skeleton annotations used in the paper for CHASEDB1 dataset.
- **h5 Files:** Contains h5 files with preprocessed images and their corresponding labels.

### DCA1 [5]
- **Images:** Contains the DCA1 dataset images.
- **Supervised Labels:** Contains the corresponding fully supervised labels for the DCA1 dataset.
- **Noisy Skeleton Annotations:** Contains the noisy skeleton annotations used in the paper for DCA1 dataset. 
- **h5 Files:** Contains h5 files with preprocessed images and their corresponding labels.
- **Note:** We did not compare other weakly supervised segmentation methods on this dataset, so the Noisy Skeleton Annotations currently provided do not include the corresponding skeletons for the background category. However, you can easily obtain the background class skeletons by appropriately dilating the Noisy Skeleton of the foreground, inverting the grayscale (255-gray value), and then using the skeletonize operation in scikit-image to easily obtain the background class skeletons. Finally, add the background class skeletons to the foreground skeletons to obtain the complete skeletons, just like provided in other dataset folders.

You can easily visualize images from h5 files using code similar to the following example:

```python
from cv2 import imwrite
import h5py
import numpy as np
import cv2

# Specify the name of the h5 file and its path
name = '1'
data_path = './' + name + '.h5'

# Open the h5 file in read mode
img = h5py.File(data_path, 'r')

# Print the keys in the h5 file
print(img.keys())

# Access and print the shapes of the image and label datasets
print(img['image'].shape, img['label'].shape)
# print(img['image'].shape, img['label'].shape, img['scribble'].shape)


# Load image and label data from the h5 file
img_data = img['image'][:]
label = img['label'][:]

# Save the loaded image and label data as image files
cv2.imwrite('./' + name + '_img.png', img_data * 255.)
cv2.imwrite('./' + name + '_label.png', label * 127.)
# cv2.imwrite('./' + name + '_scribble.png', scribble*127.)


# Print information about the loaded image data
print(img_data)
print("Max pixel value:", np.max(img_data))
print("Min pixel value:", np.min(img_data))
print("Unique labels:", np.unique(label)) 
```

These datasets are provided here to facilitate the reproducibility of the research results presented in the paper. Please refer to the paper for details on how these datasets were used in the experiments.

- [1] Li, M., Zhang, Y., Ji, Z., Xie, K., Yuan, S., Liu, Q., Chen, Q., 2020. Ipn-v2 and octa-500: Methodology and dataset for retinal image segmentation. arXiv preprint arXiv:2012.07261.
- [2] Zhao, Y., Zhang, J., Pereira, E., Zheng, Y., Su, P., Xie, J., Zhao, Y., Shi, Y., Qi, H., Liu, J., et al., 2020. Automated tortuosity analysis of nerve fibers in corneal confocal microscopy. IEEE Trans. Med. Imaging 39 (9), 2725–2737.
- [3] Staal, J., Abràmoff, M.D., Niemeijer, M., Viergever, M.A., Van Ginneken, B., 2004. Ridge-based vessel segmentation in color images of the retina. IEEE Trans. Med. Imaging 23 (4), 501–509.
- [4] Fraz, M.M., Remagnino, P., Hoppe, A., Uyyanonvara, B., Rudnicka, A.R., Owen, C.G., Barman, S.A., 2012. An ensemble classification-based approach applied to retinal blood vessel segmentation. IEEE Trans. Biomed. Eng. 59 (9), 2538–2548.
- [5] Cervantes-Sanchez, F., Cruz-Aceves, I., Hernandez-Aguirre, A., HernandezGonzalez, M.A., Solorio-Meza, S.E., 2019. Automatic segmentation of coronary arteries in X-ray angiograms using multiscale analysis and artificial neural networks. Appl. Sci. 9 (24), 5507.
