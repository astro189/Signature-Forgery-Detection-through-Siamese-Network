# Signature-Forgery-Detection-through-Siamese-Network
<h3>What are Siamese Networks?</h3>
<p>The basic idea behind Siamese networks is to have two identical subnetworks, often called "twins," that share the same architecture and weights. Each input (such as an image, text, or any other data representation) is passed through these twin networks, producing embeddings or feature vectors. These embeddings are then compared using a similarity metric such as Euclidean distance or cosine similarity to determine the similarity or dissimilarity between the inputs.

Siamese networks are trained using pairs of inputs along with their corresponding labels indicating whether they are similar or dissimilar. During training, the network learns to minimize the distance between embeddings of similar inputs while maximizing the distance between embeddings of dissimilar inputs. This learning process helps the network develop a representation space where similar inputs are closer together and dissimilar inputs are farther apart.</p>

<h3>Signature forgery detection</h3>

<p>Forgery detection is one of the major applications for the siamese network, in this project we focus on the <a href="https://arxiv.org/abs/1707.02131">SigNet</a> paper as a base reference for our model. The project involves the following steps.</p>

<li>Dataset Preparation</li>
<li>Base model</li>
<li>Twin model architecture and Training</li>
<li>Evaluation of the model</li>

<h4>Dataset Preparation</h4>
<p>The dataset for training a siamese netowrk involes pairs of positive and negative images, hence intially we need to convert our dataset of images into these pairs of images. Follwing which we have implmented a custom datagenerator to get for the batch wise pair image generation during training, considerably reducing the memory requirement due to loading only a single batche of images at once as well as speeding up the training process. 
</p>

<p>The following preprocessing steps are applied to each image for maintaining a standard representation:</p>
<li>Resize: All images are resized to (155,220), the input size of the model</li>
<li>Grayscaling: Removing color channels for faster model training</li>
<li>Binarization: Converting images to binary form through OTSU thresholding</li>
<li>Normalization of pixels: Subtracting by mean and dividing by std of pixel values</li>
<li>Dataset Split: Training images->18565, Validation images->4641</li>
<br>

<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Preprocessed%20negative.png" alt="Negative Pairs"></p>
<p align="center"><b>Negative Pairs</b></p>
<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Preprocessed%20positive.png" alt="Positive Pairs"></p>
<p align="center"><b>Positive Pairs</b></p>

<h4>Base Model</h4>
<p>The base model is based on a sequential CNN architecture with MaxPooling, the final layer of the model however is a 128 elements vector which is our encoding of the images.</p>

<h5>Base Model Parameters</h5>
<li>Input shape: (155, 220)</li>
<li>Batch size: 64</li>
<li>Layer activations: Relu</li>
<li>Total parameters for training: 83269056</li>

<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Model%20visualization.png" alt="Base Model", width=600px></p>
<p align="center"><b>Base Model</b></p>


<h4>Twin Model Architecture and Training </h4>

<p>The twin model architecture is what represents a siamese network each individual image from our pair of images is run through the model to generate each of there encoding and training using the contrastive loss function to increase the distance between negative encoded pairs and decrease the distance between positive encoded pairs. The weights are shared between the two twin models</p>


<h5>Training Parameters</h5>
<li>Loss: Contrastive loss</li>
<li>Optimizer: RMSProp</li>
<li>Metrics: Accuracy</li>
<li>Epochs: 30</li>
<li>Training time: 4 Hours</li>

<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Final%20Model.png" alt="Siamese Network", width=600px></p>
<p align="center"><b>Siamese Network</b></p>

<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Screenshot%202024-03-16%20132506.png" alt="Contrastive Loss", width=600px></p>
<p align="center"><b>Contrastive Loss</b></p>

<h4>Model Evaluation</h4>
<p>The model is tested on two seperate datasets, one taken from the dataset used for training and the second one is a self created signature dataset. It model shows generalized outcome for both negative as well as positive pairs of images. Performance of the model can still be improved through use of methods such as cross validation, I will try and implement such methods in the fututre and report back any changes.</p>

<h5>Validation Classification Report</h5>
<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Screenshot%202024-03-16%20140824.png" alt="classification report", width=400px></p>
<p align="center"><b>Validation Classification Report</b></p>


<h5>Test Set</h5>

<h6>Evaluation Metric</h6>

<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Test%20eval.png" alt="Test Evaluation Metric", width=400px></p>
<p align="center"><b>Test Evaluation Metric</b></p>

<h6>Confusion Matrix</h6>

<br>
<p align="center"><img src="https://github.com/astro189/Signature-Forgery-Detection-through-Siamese-Network/blob/main/Readme_img/Confusion%20Matrix.png" alt="Test Evaluation Metric", width=400px></p>
<p align="center"><b>Confusion Matrix</b></p>











