# Bone-Histomorhometry

Bone histomorphometry allows quantitative evaluation of bone micro-architecture, bone formation, and bone remodeling by providing an insight to cellular changes. Histomorphometry plays an important role in monitoring changes in bone properties because of systemic skeletal diseases like osteoporosis and osteomalacia. Besides, quantitative evaluation plays an important role in fracture healing studies to explore the effect of biomaterial or drug treatment. However, until today, to our knowledge, bone histomorphometry remain time-consuming and expensive. Information obtained from both static and dynamic histomorphometry provides a valuable profile of bone turnover as well as mineralization and bone quality, features that can comprehensively be assessed with reliability only from a biopsy. Traditionally measurements performed with static and dynamic histomorphometry involve manual visual feature identification by trained professionals with creation of feature maps that are then quantitated by proprietary image analysis software programs (Osteomeasure™, Bioquant™). There is a high interoperability issue between pathologists drawing the feature maps. To overcome these drawbacks in manual process including the need for trained personnel engaging in a time-consuming process as well as potential subjectivity and both inter- and intra- operator variability we propose the development of an automated image analysis software based on a machine-learning algorithm that would create the feature maps for analysis.

In this project, we propose to exploit the emerging deep learning (DL) techniques to automate the analysis of histological images. Recently DL techniques have been widely used for medical imaging data of various modalities in radiology, such as diagnosis based on images of CT, Magnetic Resonance (MR), X-ray, and Positron Emission Tomography (PET). They have provided state-of-the-art performance for various tasks, e.g., aiding with diagnosis, predicting patients’ outcomes, decoding tumor phenotypes [4], and finding gene-protein signatures [3]. In particular, a special class of DL models, convolutional neural networks (CNNs), has achieved great success in medical imaging analysis. Various DL approaches based on CNNs have been proposed for learning feature representations, detecting lesions, classifying the images, and prognosticating treatment effects, in applications such as lung node and mass segmentation [5,6,7], nuclei detection on breast cancer histopathology images[8],  and medical image synthesis [9]. Despite the broad applications of DL techniques on medical imaging data, they remain to be exploited for histological images of bone biopsies. 

This project will develop an automated, high-performance, fast, validated software for bone histology and histomorphometry by exploring and exploiting the advantages of DL. Specifically, we will apply a contemporary CNN-based DL model, U-Net, which achieves state-of-the-art performance for various medical segmentation tasks. For example, the CNN-based U-Net achieves accurate, automatic tumor detection and segmentation task[10]; the tight frame U-Nets can effectively recover high-frequency edges in sparse view-CT[11].

# U-Net:

The UNET was developed by Olaf Ronneberger et al. for Bio Medical Image Segmentation. The architecture contains two paths. First path is the contraction path (also called as the encoder) which is used to capture the context in the image. The encoder is just a traditional stack of convolutional and max pooling layers. The second path is the symmetric expanding path (also called as the decoder) which is used to enable precise localization using transposed convolutions. Thus it is an end-to-end fully convolutional network (FCN), i.e. it only contains Convolutional layers and does not contain any Dense layer because of which it can accept image of any size[12]. Using U-net we build a semantic segmentation model on histomorphometric images of the patients. The goal of semantic image segmentation is to label each pixel of an image with a corresponding class of what is being represented. Because we’re predicting for every pixel in the image, this task is commonly referred to as dense prediction. One important thing to note is that we're not separating instances of the same class; we only care about the category of each pixel[13].

# Approach:

The first step in model building process is generating the labels for the images. The original images are annotated using the feature maps as the ground truth generated by the pathologist using  osteomeasure. The data set contained 9 patient feature maps each map divided into individual segments totaling to 142 images. Each image is annotated using ‘labelme’ annotation tool for semantic segmentation. The total number of classes present in the images were 12 including Bone, Void, Osteoid, Osteoblast Srf, Osteoblasts, Eroded surface, Osteclast Srf, Osteoclasts, Wall, Single label, Double Label, and Eroded depth. We selected the 4 dominant classes for this analysis which include one, Void, Osteoid, and the Osteclast Srf. The masks generated using the annotation tool were divided into train and test sets as labels along with the original images. A total of 80 images for were used for training and testing purpose where 60 were used for training and 20 were kept aside for testing. The pixel values for the image labels are changed to match close to each other for the model to converge faster. The u-net model is trained on the images for 2 epocs. Achieved a training accuracy of 97%.

# Results:

The model is tested on 20 images with 4 classes. The performance of the model can be estimated using accuracy and dice coefficient. While accuracy is easy to understand, it is not the best metric. When our classes are extremely imbalanced the accuracy could be really high whereas your model is returning a completely useless prediction. While on the other hand Dice coefficient  is better metric, simply put, the Dice Coefficient is 2 * the Area of Overlap divided by the total number of pixels in both images. The Dice coefficient is very similar to the IoU ranging from 0 to 1, with 1 signifying the greatest similarity between predicted and truth[14]. 


# References:

1.Faugere HMM. Atlas of Mineralized Bone Histology: Karger; 1986.

2.Malluche HH, Mawad H, Monier-Faugere MC. Bone biopsy in patients with osteoporosis. Curr Osteoporos Rep 2007;5:146-52.

3.Coroller T P, Grossmann P, Hou Y, et al. CT-based radiomic signature predicts distant metastasis in lung adenocarcinoma. Radiotherapy & Oncology, 2015, 114(3):345-350.

4. Aerts H J W L, Velazquez E R, Leijenaar R T H, et al. Decoding tumour phenotype by noninvasive imaging using a quantitative radiomics approach. Nature Communications, 2014, 4006.

5.Giger M L, Karssemeijer N, Schnabel J A. Breast image analysis for risk assessment, detection, diagnosis, and treatment of cancer. Annual Review of Biomedical Engineering, 2013, 15(1):327-357.

6.Dou Q, Chen H, Yu L, et al. Automatic Detection of Cerebral Microbleeds from MR Images via 3D Convolutional Neural Networks. IEEE Transactions on Medical Imaging, 2016, 35(5):1182-1195.

7. Anthimopoulos M, Christodoulidis S, Ebner L, et al. Lung Pattern Classification for Interstitial Lung Diseases Using a Deep Convolutional Neural Network. IEEE Transactions on Medical Imaging, 2016, 35(5):1207-1216.

8. Xu J, Xiang L, Liu Q, et al. Stacked Sparse Autoencoder (SSAE) for Nuclei Detection on Breast Cancer Histopathology Images. IEEE Trans Med Imaging, 2016, 35(1):119-130.

9. Dou Q, Chen H, Yu L, et al. Automatic Detection of Cerebral Microbleeds from MR Images via 3D Convolutional Neural Networks. IEEE Transactions on Medical Imaging, 2016, 35(5):1182-1195.

10. Ronneberger O, Fischer P, Brox T. U-Net: Convolutional Networks for Biomedical Image Segmentation. International Conference on Medical Image Computing and Computer-Assisted Intervention. Springer, Cham, 2015:234-241.

11. Han Y, Ye J C. Framing U-Net via Deep Convolutional Framelets: Application to Sparse-View CT. IEEE Transactions on Medical Imaging, 2018, 37(6):1418.

12. https://towardsdatascience.com/understanding-semantic-segmentation-with-unet-6be4f42d4b47

13. Olaf Ronneberger, Philipp Fischer, and Thomas Brox U-Net: Convolutional Networks for Biomedical Image Segmentation

14. https://towardsdatascience.com/metrics-to-evaluate-your-semantic-segmentation-model-6bcb99639aa2
