# Signature-Forgery-Detection-through-Siamese-Network
<h3>What are Siamese Networks?</h3>
<p>The basic idea behind Siamese networks is to have two identical subnetworks, often called "twins," that share the same architecture and weights. Each input (such as an image, text, or any other data representation) is passed through these twin networks, producing embeddings or feature vectors. These embeddings are then compared using a similarity metric such as Euclidean distance or cosine similarity to determine the similarity or dissimilarity between the inputs.

Siamese networks are trained using pairs of inputs along with their corresponding labels indicating whether they are similar or dissimilar. During training, the network learns to minimize the distance between embeddings of similar inputs while maximizing the distance between embeddings of dissimilar inputs. This learning process helps the network develop a representation space where similar inputs are closer together and dissimilar inputs are farther apart.</p>

<h3>Signature forgery detection</h3>

<p>Forgery detection is one of the major applications for the siamese network, in this project we focus on the <a href="https://arxiv.org/abs/1707.02131">SigNet</a> paper as a base reference for our model. The project involves the following steps.</p>

<li>Dataset Preparation</li>
<li>Base model</li>
<li>Final model architecture</li>
<li>Training and Evaluation of the model</li>

<h4>Dataset Preparation</h4>
<p>The dataset for training a siamese netowrk involes pairs of positive and negative images, hence intially we need to convert our dataset of images into these pairs of images. Follwing which we have implmented a custom datagenerator to get for the batch wise pair image generation during training, considerably reducing the memory requirement due to loading only a single batche of images at once as well as speeding up the training process. </p>

<h4>Base Model</h4>
<p>The base model is based on a sequential CNN architecture with MaxPooling, the final layer of the model howver is a 128 elements vector which is our encoding of the images. the model has the following parameters </p>

<li>Input shape: (155, 220)</li>
<li>Batch size: 32</li>
<li>Layer activations: Relu</li>

