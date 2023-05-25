# Visual-Question-Answering
Computer Vision (CV) and Natural Language Processing
(NLP) were combined in this project to understand the yes/no
questions and answer them regarding images. A simple pretrain CNN (dense, dropout, and add layer) was used for the
text embedding (GOTO [text embeding program](https://github.com/Afsaneh-Karami/Visual-Question-Answering/blob/master/VQAClassifier_baseline/SentenceEmbeddingGenerator.py)).<br/>
For the CV, different CNN encoders (shallow
and deep) like, Inceptionv3, ResNet50, NASNetMobile, MobileNetV2, Transformer, and the CNN in base code were applied and compared their accuracy, Precision, Recall, Balanced Accuracy, and F-measure (GOTO [program](https://github.com/Afsaneh-Karami/Visual-Question-Answering/blob/master/VQAClassifier_baseline/VQAClassifier_baseline.py)).<br/>
For all CNN except the transformer,
Imagenet-trained weight was implemented. In the following,
the reasons for choosing them were explained.<br/> 
* Inception
concatenates parallel convolutional layers to capture features
at multiple scales and resolutions and improve the accuracy in
image recognition tasks, especially for images with little
details and low resolution like this project (224*224).<br/>
* ResNet
employs a ”bottleneck” design, which avoids overfitting by
reducing the number of parameters with skip connections.
They also transfer information from shallower layers to deeper
layers (preserve information) and enable the network to learn
identity maps. So it can extract complex features from low-resolution images. <br/>
* NASNet CNN automatically searches
through possible network architectures to find the optimal one
for a specific task using techniques such as reinforcement
learning. So, it can adapt its architecture based on image
resolution, training data number, and some hyperparameters,
such as learning rate and activation functions. Its adaptability
help to capture meaningful visual features from images with
lower resolution. <br/>
* MobileNetV2 is a shallow CNN efficient for this project because this VQA task is relatively easy.
MobileNetV2 uses linear bottlenecks, and it can prevent the
loss of important information during the feature extraction
process. <br/>
* The Transformer architecture is designed on the self-attention mechanism, paying attention to the sequence of
information, their position and relation. It enables the
transformer to focus on relevant parts of the input data and
extract complex relations between them, so be able to model
long-range dependencies. The self-attention mechanism allows
the transformer architecture to be parallelisable, making it
more computationally efficient. The image was divided
into some patches, flattened embedded patches and added
the position information to them, then fed to the encoder
block of the transformer. In the encoder, some self-attention mechanisms and normalisation are applied. Finally,
Feedforward Neural Networks process the self-attention output
and generate the final representations of the input sequence (128-dimensional embedding vector).
## result and discussion
Different hyperparameters were tested for the transformer,
like learning rate, dropout rate, batch size, patch size, number
of heads, and number of transformer layers. Based on the result
of this project, for low-resolution images and medium levels of
detail, it is better to have a larger patch size with meaningful
features in each patch (size 32). As the training dataset has a
different distribution than the validation and test data, choosing
a big batch size is better for getting more data for each
training epoch, which increases the chance of getting a more
diverse image and may be better matched with validation
and test data. The projection-dim was chosen 286 based on
trial and error. It represents each patch to a self-attention
mechanism, which should include an important parameter of
each patch. The number of head and transformer layers were
3 and 4, respectively, based on the resolution and detail of
the image. In all the different CNN plot, there is a significant
distance between the training and validation accuracy curve.
At first, I thought it was a variance problem and tried some
regulation, dropout, and low dimensional CNN with low
parameters. But, it could not mitigate the gap between the
training and validation. It means the reason for the lower
validation accuracy was data mismatched, not overfitting. To
confirm the data mismatched problem, 1000 images of training
were selected randomly and copied to validation data, which
increased the validation accuracy by 8.2%(For MobileNetV2).
Following figures and Table I show the result of training and
validation for different CNN and hyperparameters. MobileNet
had the lowest parameters and highest scores. All CNN except
NASNet and MobileNet were more robust in recognising the
No answer correctly until the Yes response (high specificity
and lower recall). Inception and ResNet are two deep CNN
and logically need lower epochs to train. The transformer had
the most oscillation in the validation process. Based on the
result, the VQA task does not require deep CNN.<br/>
![basemodel](https://github.com/Afsaneh-Karami/Visual-Question-Answering/assets/78735911/a58eacc4-f4fd-4acf-ac80-89e3a4790190)


