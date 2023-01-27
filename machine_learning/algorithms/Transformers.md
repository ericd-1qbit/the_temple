https://towardsdatascience.com/what-are-vision-transformers-and-how-are-they-important-for-general-purpose-learning-edd008545e9e


The concept of transformers originated in Natural Language Processing (NLP) applications, whereby the task is to understand the text and draw meaningful conclusions


Typical Transformer Architecture
► Text is split into a set of words called tokens.
► Each token is converted into an encoded/embedded vector (e.g. word2vec)
► The position of the word in the sequence is encoded using position embedding [1] and integrated with the word embedding.
► The embeddings are fed into the Transformer encoder.
► The encoder has a Multi-Layer Self-Attention Network (MSP) which assigns weights to tokens based on their relative importance in the sentence, hence embedding the context.
► A Multi-layer Perceptron (MLP) network follows the MSP and encodes the output from the attention network.
► There are multiple MSP and MLP blocks along with Norm layers inside the encoder.
► A final MLP-Head Layer is added outside the encoder network which provides the logits. Logits can be converted to probabilities by applying an activation layer (e.g. softmax).


As we can see that the architecture of a transformer network is generic because the encoder output is not constructed for a specific task (e.g. classification) but rather it provides a general encoding that can be used for a multitude of applications by adding a corresponding MLP Head. This is why transformers are useful in transfer learning and are promising for achieving a general-purpose learning goal.


Vision Transformers

- similar to text transformers with slight adjustment to account for image
-  input image is split into a set of image patches, called _visual token_
-  visual tokens are embedded into a set of encoded vectors of fixed dimension
- visual tokens are embedded into a set of encoded vectors of fixed dimension. The position of a patch in the image is embedded along with the encoded vector and fed into the transformer encoder network
- ![[Pasted image 20230126155909.png]]
multiple blocks in the ViT encoder and each block consists of three major processing elements: _Layer Norm_, _Multi-head Attention Network (MSP)_ and _Multi-Layer Perceptrons (MLP)_. _Layer Norm_ keeps the training process on track and let model adapt to the variations among the training images. _MSP_ is a network responsible for generation of attention maps from the given embedded visual tokens. These attention maps help network focus on most important regions in the image such as object(s). The concept of attention maps is same as the one found in the traditional computer vision literature (e.g. saliency maps and alpha-matting).

_MLP_ is a two-layer classification network with GELU (_Gaussian Error Linear Unit_) at the end. The final MLP block, also termed as _MLP head_ is used as an output of the transformer. An application of _softmax_ on this output can provide classification labels

applications of transformers: very generic, find them in almost all vision related tasks

**Image Classification (Image -> Label)**'
- competing with CNN in some aspects
**Image Captioning (Image -> Sentence)**'

**3.3.** **Contrastive Language-Image Pre-Training (Image <-> Text Snippet)**
A more advanced application of _ViTs_ is the learning of association that exists between an image and a piece of text. This is the application where the true ability of generalizability is required because it requires an abstract representation of both the text as well as the image. This can be achieved by training two separate transform encoders for text snippet and the image. The encoded image as well as the text features can then be compared for their respective similarity by constructing a cosine-similarity matrix. A relevant implementation for such transformer model is proposed in CLIP (Contrastive Language-Image Pre-Training)

 text snippets as well as the images are encoded into a set of text and image feature vectors respectively by using the pre-trained ViT