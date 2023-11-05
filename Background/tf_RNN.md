# RNN

**CONTENT COVERED**
- RNN
- LSTM
- Tokenizer
- Embedding Layer

## RNN
RNN is short for Recurrent Neural Network. Main job of RNN is processing input and output in a sequential manner.
RNN is a basic network of learning LSTM and Transformers.

![RNN](/X/Screenshot%20from%202023-09-04%2000-13-55.png)

All the neural networks we've learned about so far had one common feature: the values that passed through the hidden layers only moved in the direction of the output layer. However, **RNN has a unique characteristic where the result from the activation function in the hidden layer is not only sent towards the output layer but also sent back to the hidden layer as input for the next computation.**
Feedback from the former input change the weight of the networking according to the trend, or the change of value in sequencial input. At last predicting future value of the sequential data.

**Exploding/Vanishing Gradient Problem**
The vanishing and exploding gradient problems in RNNs (Recurrent Neural Networks) are specific instances of these issues that occur in the context of recurrent architectures. RNNs are particularly susceptible to these problems due to their sequential nature and the recurrent connections that exist within them.

## LSTM
LSTM is short for Long Short Term Memory network. Vanilla RNN is hard to train because of exploding/vanishing gradient problem. LSTM is type of RNN that is designmed to avoid the exploding/vanishing gradient problem.

![LSTM](/X/Screenshot%20from%202023-09-04%2007-57-50.png)
Instead of just using feedback from data just a step ahead, LSTM additionally uses all the data from a squence to predict the future value.

```
model = Sequential([
    Embedding(vocab_size, embedding_dim, input_length=max_length),
    Bidirectional(LSTM(64, return_sequences=True)),
    Bidirectional(LSTM(64)),
    Dense(32, activation='relu'),
    Dense(16, activation='relu'),
    Dense(1, activation='sigmoid'),
])
```

## Tokenizer
In NPL problem sentence must be changed into series of numbers in order to use it as a data to train the network. There are some steps to tokenize a sentence.

1. Split a sentence into token. Word token is often used but character token or sentence token can be used.
2. Make a token dictionary that maps token into number. In this process only tokens with most frequent appearance has to be saved in a dictionary and to prevent the `curse of dimension` value must be `one-hot-encoded`.

```
tokenizer = Tokenizer(num_words=vocab_size, oov_token = '<OOV>')
```

3. Lastly using token dictionary every sentence in a dataset can be changed into a series of number

```
tokenizer.fit_on_texts(train_sentences)
```

## Embedding layer
In NPL problem all data has to be `one-hot-encoded` to prevent making any relationship with the word that we do not want to make. 
![NPL data](/X/Screenshot%20from%202023-09-04%2008-18-34.png)

However, there is a problem of `one-hot-encoding` a data in NPL. Because there are more 0 then meaningful number, it is hard to train the network using this data. So Embedding layer change these series of number with lots of 0 into float number that is unique to every sentence.

```
x = Embedding(vocab_size, embedding_dim, input_length=max_length)
```