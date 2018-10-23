# YODO You-Only-Diagnose-Once

Using YOLOv2 to detect pneumonic patches in CXR images using the dataset from [RSNA kaggle Pneumonai Detection Challenge](https://www.kaggle.com/c/rsna-pneumonia-detection-challenge).

#### The process
1. Use a pretrained [CheXNet](https://arxiv.org/abs/1711.05225) model as a backbone feature extractor for the YOLOv2 model.
2. Fine tune the model for classifying the 3 cases we have in our dataset (Normal, Opacity, No Opacity/ Not Normal)
3. Add three additional convolutional layers to the model after fine funing to end up with the detcetion layer (shape: $7\times7\times5\times5$)
4. Train the 3 convolutional layers with freezing the weights of the rest of the network and then finetune the whole network.
5. Because of the infrequent presence of the pneumonic patches in the dataset, I used a dynamic method for weighting the loss that gives higher weight for missing a pneumonic patch by computing the weights for each training patch separately. 

It is a simple model without augmentation or ensampling and still gives good results (top 50% in the competition).

**Note**: I don't provide data exploratory code in this notebook as there are already multiple kernels on the competiotion page on Kaggle that did marvelous job in this regard.

**Credits**: Code I used in the Notebook
1. Loading dicom images https://www.kaggle.com/jonnedtc/cnn-segmentation-connected-components
2. YOLOv2 implementation https://github.com/experiencor/keras-yolo2
3. Weights for a pretrained ChexNet model https://github.com/brucechou1983/CheXNet-Keras