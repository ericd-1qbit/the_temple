# Convolutional Neural Networks

##### Reading: Dynamic Graph CNN for Learning on Point Clouds
- arXiv:1801.07829

- Point Clouds (PC) are a geometric representation of data in particular in computer graphics (or vision). This paper combines successes in CNN with point cloud representation.
- Point clouds do not possess topological infoirmation. The authors introduce a NN module called EdgeConv which allows CNN application on PC.
- Paper considers PC classification and segmentation. 
- EdgeConv is an NN operation which captures local geometric structures in the PC, which remain invariant under permutations. Learns edge features, i.e. relations between points and their neighbors. This approach is based on PointNet.

Related Work:
Handcrafted Features:
extrinsic descriptors use coordinates of PC in 3D space
intrinsic descriptors interpret 3d shape as manifold with a discretized metric
like mesh.
Deep Learning on Geometry: CNN for geometric data
Geometric generative models: adapt VAE, GAN to non-euclidean setting of PC.
Problem is the comparison between input and output, as there is no canonical
order.
Dynamic Graph CNN - DGCNN
- construct a local neighborhood graph
- apply convolution-like operations on graph edges
- An edge is a nonlinear function from a pair of points to real numbers and
learnable parameters.

DGCNN approach for PC
-Edge Convolution
from input points in PC (can also be PC of features in subsequent layer)
-Dynamic Graph Update
Multilayer Perceptron (MLP)

- Properties
	- permutation invariance
because operation based on max() which is symmetric under permutations
-- translation invariance
partially true, as paper choice enables switching off translation dependency
-Comparison to existing methods

Evaluation
- Classification
-- Model Complexity
-- ModelNet40 experiments

- part segmentation
each point in a PC classified into a predefined set of categories
- indoor scene segmentation

Discussion
- new operatopr for learning on PC
- local geometric features important in 3D classification tasks
Figures:
F1 - nice example how algorithm finds "semantic" features in PC
Basically, it decomposes the PC into similar looking objects and marks their
classification in "distance"

F2 - own note: looks similar to RBM? compare this
This being used in HEP: jet reconstruction.

In this paper, we present a new approach for machine
learning on jets. The core of this approach is to treat
jets as particle clouds, i.e., unordered sets of particles.
Based on this particle cloud representation, we introduce
ParticleNet, a network architecture tailored to jet tagging tasks. The performance of the ParticleNet ar
chitecture is compared with alternative deep-learning architectures, including the jet image–based ResNeXt-50
model, the particle sequence–based P-CNN model and
the particle set–based PFN model. On both the top
tagging and the quark-gluon tagging benchmarks, ParticleNet achieves state-of-the-art performance and im
proves significantly over existing methods. Although the
very deep image–based ResNeXt-50 model also shows significant performance improvement over shallower models
like P-CNN and PFN on the top-tagging benchmark, indicating that deeper architectures can generally lead to better performance, the gain with the ParticleNet architecture is more substantial. Moreover, the high performance is achieved in a very economical way as the number of trainable parameters is a factor of 4 (56) lower in
ParticleNet (ParticleNet-Lite) compared to ResNeXt-50.

Such lightweight models are particularly useful for applications in high-energy physics experiments, esp
ecially for
online event processing in which low latency and memory
consumption is critical.
While we only demonstrate the power of the particle
cloud representation in jet tagging tasks, we think that
it is a natural and generic way of representing jets (and
even the whole collision event) and can be applied to a
broad range of particle physics problems. Applications
of the particle cloud approach to, e.g., pileup identification, jet grooming, jet energy calibration, etc., would be
particularly interesting and worth further investigation.


##### Reading: Jet Tagging via Particle Clouds
arXiv:1902.08570v3

Quark- and gluon-jet separation important for physics at LHC. This paper treats
jets as unordered set of particles, which is different than most approaches
seeing them as ordered structure. This leads to the analogon to point clouds in
3D space used in computer vision - a \emph{particle cloud}. They use the Dynamic
Graph CNN from the other paper (Dynamic graph cnn for learning on
point clouds).  This approach here outperforms state of the art tools!
Jet representation as images comes naturally, given the way they are detected.
Calorimeter cells can be seen as image pixels, their values corresponding to the
deposited energy. This has been well studied and understood using relatively
shallow CNN. Deeper structures might improve things. CNN offer computational
disadvantages and complications when using more information than just
calorimeter.

Another way of representing jets is through their constituent particles. For
deep learning this
requires to order constituents somewhow, commonly according to their transverse
momentum. This is an arbitrary choice and may imply some suboptimal choice.

Jets seen as particle clouds - an unordered, permutation invariant set -  seem
more natural choice. Point clouds are irregular distributed points in space,
with an underlying internal structure, just like jets. 
  
Convolution is the extraction of features from an input image and can be
understood as the subsequent application of functions. For a pixelised image, it
would map the original pixels onto a smaller dimensional image, preserving
relationships between original pixels 

CNN extremely successful. Key features for their success: 
- convolutional operation exploits translational symmetry of images (shared
kernels across full image). This reduces the number of parameters to be learned
and improves learning, as each weight uses full image. 

- hierarchical approach: convolutions are stacked. subsequent layers learn
different structures of images, from shallow layers learning neighbouring
relations to deep layers learning global properties. 
Here, combine CNN and point cloud. Convolutional operation needs some local
patch to operate - not given in point cloud and needs to be defined.

Furthermore, the convolution form needs to be modified on point clouds to
respect permutation invariance.

That's why they introduce EdgeConv in that aforementioned paper - Edge
Convolution. Each point in the cloud is a vertex in a graph, the connection of
each point with its k nearest neighbours are the edges. This defines a local
patch. With that, the EdgeConv operation is defined. It can be understood as a
perceptron operating on the point and its k neighbours.

These perceptrae can be stacked, making a deep learning structure possible. This stackability also means that the distances learned by the EdgeConv operation change with each layer. The parameters of the Network are thereby updated. This results in a Dynamic Graph CNN.

ParticleNet is an adaption of the EdgeConv and DGCNN structures. 
One Building block is the EdgeConv operation. This operation goes as follows:
- find k neartes neighbors (k is a hyperparameter)
- construct edge features from the "features" (?)
- feed to 3 layer multilayer perceptron - linear layer, batch norm,lisation and ReLU.

Approach outperforms state of the art technology!
  
Q: 
- How is the cloud permutation invariant? 
- Fig 1: features as input to edge features?
- adaptive learning rate observed before? (p4)
-- warm up
-- cyclical
-- depending on optimiser
-- ADAM not necessary, since it is adaptive. check it!
- cross entropy loss is constructed how? what's the truth info?
- input to algorithm given by kinematic variables?