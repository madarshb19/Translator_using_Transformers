# Translator_using_Transformers

Transformers are a type of deep learning model that has gained significant attention and popularity, particularly in the field of natural language processing (NLP). The architecture of transformers was introduced in a 2017 paper called "Attention is All You Need" by Vaswani et al., and it has since revolutionized various NLP tasks. The architecture is shown below,the details of which can be found below:-

![transformer](https://github.com/madarshb19/Translator_using_Transformers/assets/70708225/fc03d9eb-0707-4f28-bfae-b6f681451e3e)


The key idea behind transformers is the use of self-attention mechanisms, which allow the model to focus on different parts of the input sequence when making predictions. This attention mechanism is crucial in capturing relationships between words or tokens in a sequence, enabling the model to understand dependencies and long-range interactions.

The architecture of transformers consists of two main components: the encoder and the decoder. The encoder processes the input sequence and converts them into abstract vector embeddings, while the decoder generates the output sequence. Both the encoder and decoder are composed of multiple identical layers stacked on top of each other.

At the beginning of the model, the input sequence is represented as a set of embeddings. Each token in the sequence is transformed into a vector representation known as the input embedding. These embeddings capture the semantic meaning of the tokens and provide a foundation for the subsequent layers. Since transformers don't have inherent sequential information like recurrent neural networks (RNNs), positional encoding is added to convey the position of each token in the input sequence. The positional encodings are added to the input embeddings, allowing the model to differentiate between tokens based on their relative positions.

![inputembedding](https://github.com/madarshb19/Translator_using_Transformers/assets/70708225/32f490f2-8434-4488-b5c8-05d154cf6073)

The encoder is composed of multiple layers where each encoder layer has two sub-layers: a multi-head self-attention layer and a position-wise fully connected feed-forward network.

a. Multi-Head Attention layer: The self-attention mechanism allows the model to weigh the importance of different tokens in the input sequence. It computes a weighted sum of the embeddings of all tokens, with the weights determined by the similarity between tokens. The positional embeddings are passed on into three different Linear layers and three new matrices are learnt: Query (Q), Key (K), and Value(V). The Q and K matrices undergo a dot product to create a score matrix. This matrix determines how much focus one word must put on other words. The scores matrix is then scaled down by a factor of $d_k^1/2$ where the d_k represents the dimensions of the key array. The scaling is performed to ensure stable gradients during backpropagation as matrix multiplications cause coefficients to explode. The scaled scores undergo a softmax to obtain the attention weights matrix. This attention weight matrix is then multiplied with the Value vector (V) which passes through a final linear layer to get the output of the self attention layer. Each self attention layer is performed multiple times using the same Q,K and V values where each layer is called as a head. Ideally, we would expect each head to learn different and unique representations of the input.



b. Feed-Forward Network: The output of the multi-head attention layer is then added to the input (i.e,the positional embeddings). This is known as residual connection. This connections helps in training the network properly by better flow of gradients through the network. The output of the residual connection then goes through a Layer Normalization layer which helps in reducing training time. It is then passed through a Feedforward network consisting of Linear layer -> ReLu -> Linear followed by another residual connection and Layer normalization.



The decoder uses the initial output of training data and learns to generate new sequences for new inputs. Similiar to encoders,the decoders also consist of multihead attention layers but firstly,there are two of these layers and secondly, the working of these layers slightly differ compared to the encoders. Since the decoder is autoregressive, we have to ensure that the tokens which it uses to train do not exceed that of the current word. For example, in the sentence 'Typing this is taking forever' , the word 'is' should not have access to 'taking' and 'forever'. It is similiar to how test set is not touched during training in machine learning tasks. This prevention is done by applying a look-ahead mask. The look ahead mask is a matrix where the diagonals and the lower traingular part are 0 and the rest are negative infinity.In the first layer, after the scaled scores are obtained in a similiar manner to that of encoders, this scaled score matrix is added to the look ahead mask matrix to obtain the masked scores. Upon applying the softmax function on this,the future tokens after the current word would have zero weights. For the second layer,the Q,K matrices are the outputs of the encoder while V is the output of the first attention layer of the decoder. The output of the second layer is passed through a linear and softmax layer and the final output consists of Nx1 array representing class labels where N is the vocabulary size and each element represents probabilities of different tokens in the vocabulary as the output sequence.



