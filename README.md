# Translator_using_Transformers

Transformers are a type of deep learning model that has gained significant attention and popularity, particularly in the field of natural language processing (NLP). The architecture of transformers was introduced in a 2017 paper called "Attention is All You Need" by Vaswani et al., and it has since revolutionized various NLP tasks. The architecture is shown below,the details of which can be found below:-

![transformer](https://github.com/madarshb19/Translator_using_Transformers/assets/70708225/fc03d9eb-0707-4f28-bfae-b6f681451e3e)


The key idea behind transformers is the use of self-attention mechanisms, which allow the model to focus on different parts of the input sequence when making predictions. This attention mechanism is crucial in capturing relationships between words or tokens in a sequence, enabling the model to understand dependencies and long-range interactions.

The architecture of transformers consists of two main components: the encoder and the decoder. The encoder processes the input sequence and converts them into abstract vector embeddings, while the decoder generates the output sequence. Both the encoder and decoder are composed of multiple identical layers stacked on top of each other.

At the beginning of the model, the input sequence is represented as a set of embeddings. Each token in the sequence is transformed into a vector representation known as the input embedding. These embeddings capture the semantic meaning of the tokens and provide a foundation for the subsequent layers. Since transformers don't have inherent sequential information like recurrent neural networks (RNNs), positional encoding is added to convey the position of each token in the input sequence. The positional encodings are added to the input embeddings, allowing the model to differentiate between tokens based on their relative positions.

![inputembedding](https://github.com/madarshb19/Translator_using_Transformers/assets/70708225/32f490f2-8434-4488-b5c8-05d154cf6073)

The encoder is composed of multiple layers where each encoder layer has two sub-layers: a multi-head self-attention layer and a position-wise fully connected feed-forward network.

a. Self-Attention layer: The self-attention mechanism allows the model to weigh the importance of different tokens in the input sequence. It computes a weighted sum of the embeddings of all tokens, with the weights determined by the similarity between tokens. The positional embeddings are passed on into three different Linear layers and three new matrices are learnt: Query (Q), Key (K), and Value(V). The Q and K matrices undergo a dot product to create a score matrix. This matrix determines how much focus one word must put on other words. The scores matrix is then scaled down by a factor of \sqrt{d_{k}} where the d_{k} represents the dimensions of the key array. The scaling is performed to ensure stable gradients during backpropagation as matrix multiplications cause coefficients to explode. The scaled scores undergo a softmax to obtain the attention weights matrix. This attention weight matrix is then multiplied with the Value vector (V) which passes through a final linear layer to get the output of the self attention layer.  

b. Feed-Forward Network: After the self-attention mechanism, a feed-forward network is applied independently to each position in the sequence. It consists of two linear transformations with a non-linear activation function in between, such as the Rectified Linear Unit (ReLU). This feed-forward network helps the model learn complex interactions between tokens.

