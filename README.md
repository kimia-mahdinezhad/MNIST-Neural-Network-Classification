# MNIST Neural Network Classification
This report delves into the outcomes and analysis of the exercise at hand, which comprises two distinct parts. The first segment involves the design and analysis of a model for the identification of handwritten numbers. In the second part, we evaluate the effects of selectively removing certain classes from the training data and examine the resulting predictions and observations.

## Part I

In this exercise, you will be tasked with classifying the MNIST dataset using a neural network. To access the code for data loading and network implementation, you can refer to the code provided during the exercise solving sessions. Your objectives in this exercise include:

1. Investigating the impact of altering the number of layers on the network's performance.
2. Examining the effects of modifying the number of neurons within the hidden layers.
3. Analyzing the consequences of changing the optimizer.

Upon achieving the best output, you will proceed to calculate various performance metrics for the optimal network, including:

- **Accuracy**
- **Recall**
- **Precision**
- **ROC curve** (for each class against all others)
- **Learning curve**

**Answer**
In this exercise, the model was built using the MNIST dataset, which adheres to the Standards of the National Institute of Modified Technology. This dataset comprises 70,000 examples of handwritten figures in the English language format, with 60,000 samples used for training and the remaining 10,000 samples allocated for testing. All the samples are in black and white, presented as large 28 x 28 pictures. 

Notably, the dataset is not divided into a Train-Validation-Test format. This choice allows for more effective cross-study comparisons and better performance evaluation among different models. Additionally, it ensures a more substantial amount of data available for the training portion, which is particularly beneficial for educational and training applications of this dataset.

The model was constructed using the Keras library, employing the Sequential Model Classification approach. It consists of fully connected layers. To identify the most suitable configuration, several experiments were conducted, and the results of each study, along with observations, are documented. The primary model configuration corresponds to the setting recommended on Kaggle.

| Loss Value | Accuracy Value | Model Configuration |
|------------|----------------|---------------------|
| 0.0090     | 0.9971         | Initial State       |
| 0.0077     | 0.9980         | Reducing Layers     |
| 0.0082     | 0.9970         | Increasing Layers   |
| 0.0089     | 0.9971         | Reduced Neurons in Hidden Layer |
| 0.0060     | 0.9980         | Increased Neurons in Hidden Layer |
| 0.3067     | 0.9143         | Optimizer Changed to Adagrad |
| 0.0097     | 0.9968         | Optimizer Changed to Nadam |
| 0.0063     | 0.9992         | Optimizer Changed to Adamax |
| 0.0015     | 0.9995         | Optimizer Changed to RMSprop |

As we observed above, the best model is described as below:
- 3 Dense Layers with Activation Relu and 256 Neurons
- 1 Dense Layer with Softmax Activation and 10 Neurons
- RMSprop Optimizer, Batch Size 128, Epochs 20

Subsequently, the following performance parameters for the best model on the test data were evaluated:

- Accuracy for the best model: 0.982
- Recall for the best model: 0.98202587781796
- Precision for the best model: 0.9819508254130177
- ROC curve for each class in the form of "Rest vs One" is provided for classes 0 and 9.

ROC curve diagram for digit 0 compared to other digits and ROC curve diagram for digit 9 compared to other digits are included.
![](https://github.com/kimia-mahdinezhad/MNIST-Neural-Network-Classification/blob/main/Media/1.png)
![](https://github.com/kimia-mahdinezhad/MNIST-Neural-Network-Classification/blob/main/Media/2.png)

The Learning curve graph contains Accuracy values for each epoch, while the Loss values for each epoch are shown in the Loss curve.
![](https://github.com/kimia-mahdinezhad/MNIST-Neural-Network-Classification/blob/main/Media/3.png)
![](https://github.com/kimia-mahdinezhad/MNIST-Neural-Network-Classification/blob/main/Media/4.png)

## Part II

In this section, you will utilize the network architecture established in the first part. However, instead of training on the entire dataset, you will restrict training to only the data associated with the first 5 classes (i.e., digits 0 to 4). Subsequently, you will evaluate the network's performance on the data of the second set of 5 classes. 

You will also examine how the network behaves when confronted with a new class, based on the output of the neurons in the final layer. The question is whether the network's performance aligns with your expectations.

Given the results, consider proposing a solution for detecting outlier data from the network's output. Note that an actual implementation is not required; a textual description of your proposed approach will suffice.

**Answer**
In this section, we employ the data for the classes of numbers 5 to 9 as the test data, having been removed from the training data. The goal is to assess the model's performance on classes it has not seen during training. Since these numbers were not included in the initial training, the model cannot precisely identify them, but it can predict that digits 5 to 9, sharing similarities with digits 0 to 4, may be placed in the latter class.

To identify these categories, the states of the first part of the model that were incorrectly categorized as "Others" are considered, and the highest-numbered class is used as a prediction. It's important to note that the incorrect categorization may result from peculiar handwriting or variations in pixel patterns. Clear and normally written numbers are correctly categorized, while these predictions are purely speculative and not entirely dependable. The results of these predictions are as follows:

- The number 5 is most frequently identified as the number 3.
- The number 6 is predominantly identified as the number 1.
- The number 7 is most frequently recognized as the number 2.
- The number 8 is most frequently classified as the number 2.
- The number 9 is primarily identified as the number 4.

![](https://github.com/kimia-mahdinezhad/MNIST-Neural-Network-Classification/blob/main/Media/5.png)

For model creation, all samples of digits 0 to 4 are grouped as train data, and digits 5 to 9 as test data. The previous model is trained on this new data. This division is specific to this example to avoid the model learning certain classes. The results of applying the model to the selected dataset are displayed in the images. However, since no data from classes 5 to 9 were included in the training data, the accuracy for these classes is zero. 

- The number 5 is most frequently identified as the number 3.
- The number 6 is predominantly recognized as the number 4.
- The number 7 is most frequently classified as the number 3.
- The number 8 is primarily identified as the number 3.
- The number 9 is mostly identified as the number 4.

![](https://github.com/kimia-mahdinezhad/MNIST-Neural-Network-Classification/blob/main/Media/6.png)

The key issue with the examined model is its inability to accurately identify classes 5 to 9. It mistakenly assumes these numbers are similar to the ones it saw during training. To address this problem and enhance class detection and the declaration of uncertainty in classifying, it's possible to assign another class to unknown data. A threshold can be applied to determine whether or not to classify data into a certain class. This approach can improve the model's accuracy and reliability, especially for unseen data.
