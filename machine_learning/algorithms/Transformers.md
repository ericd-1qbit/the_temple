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
