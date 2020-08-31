# Generate TV Scripts

In this project, we'll generate our own Seinfeld TV scripts using RNNs. We'll be using a Seinfeld dataset of scripts from 9 seasons. The Neural Network we'll build will generate a new, "fake" TV script.

## Rubrics

This project meets all the specifications, which are:

### All Required Files and Tests
- [x] The project submission contains the project notebook, called “dlnd_tv_script_generation.ipynb”.
- [x] All the unit tests in project have passed.

### Pre-processing Data
- [x] The function `create_lookup_tables` create two dictionaries:

    - Dictionary to go from the words to an id, we'll call vocab_to_int
    - Dictionary to go from the id to word, we'll call int_to_vocab
    
    The function `create_lookup_tables` return these dictionaries as a tuple (vocab_to_int, int_to_vocab).

- [x] The function `token_lookup` returns a dict that can correctly tokenizes the provided symbols.

### Batching Data
- [x] The function `batch_data` breaks up word id's into the appropriate sequence lengths, such that only complete sequence lengths are constructed.
- [x] In the function `batch_data`, data is converted into Tensors and formatted with TensorDataset.
- [x] Finally, `batch_data` returns a DataLoader for the batched training data.

### Build the RNN
- [x] The RNN class has complete `__init__`, `forward`, and `init_hidden` functions.
- [x] The RNN must include an LSTM or GRU and at least one fully-connected layer. The LSTM/GRU should be correctly initialized, where relevant.

### RNN Training
- [x] Enough epochs to get near a minimum in the training loss, no real upper limit on this. Just need to make sure the training loss is low and not improving much with more training.
- [x] Batch size is large enough to train efficiently, but small enough to fit the data in memory. No real “best” value here, depends on GPU memory usually.
- [x] Embedding dimension, significantly smaller than the size of the vocabulary, if you choose to use word embeddings
- [x] Hidden dimension (number of units in the hidden layers of the RNN) is large enough to fit the data well. Again, no real “best” value.
- [x] n_layers (number of layers in a GRU/LSTM) is between 1-3.
- [x] The sequence length (seq_length) here should be about the size of the length of sentences you want to look at before you generate the next word.
- [x] The learning rate shouldn’t be too large because the training algorithm won’t converge. But needs to be large enough that training doesn’t take forever.
- [x] The printed loss should decrease during training. The loss should reach a value lower than 3.5.
- [x] There is a provided answer that justifies choices about model size, sequence length, and other parameters.

### Generate TV Script
- [x] The generated script can vary in length, and should look structurally similar to the TV script in the dataset. It doesn’t have to be grammatically correct or make sense.

## Results

### Model Performance

The model hyperparameters are decided by trial-and-error method. The table below shows the documentation of hyperparameters used on the training process for the first up to fourth trial.

|    PARAMETERS   |   1st   |   2nd   |   3rd   |   4th   |
|:---------------:|:-------:|:-------:|:-------:|:-------:|
| sequence_length |    8    |    16   |    16   |    16   |
|    batch_size   |    32   |    32   |    64   |   128   |
|    num_epochs   |    3    |    3    |    6    |    6    |
|  learning_rate  |   0.01  |  0.001  |  0.001  |  0.001  |
|  embedding_dim  |   512   |   512   |   512   |   400   |
|    hidden_dim   |   256   |   256   |   256   |   256   |
|     n_layers    |    2    |    2    |    3    |    3    |
|     **LOSS**    | 5.48253 | 4.30486 | 3.69230 | 3.45619 |
|     **TIME**    |37min 51s|48min 46s|71min 57s|52min 29s|

Parameters:
- `sequence_length`: length (words) of a sequence (sentence).
- `batch_size`: training batch size
- `num_epochs`: number of epochs to train for
- `learning_rate`: learning rate for an Adam optimizer
- `embedding_dim`: embedding dimension; smaller than the `vocab_size`
- `hidden_dim`: hidden dimension of RNN
- `n_layers`: number of layers/cells in RNN

Results:
- **LOSS**: training loss printed at the end of epoch
- **TIME**: time taken to train the model (tracked using `%%time`)

### Generated scripts

With the network trained and saved, WE'll use it to generate a new, "fake" Seinfeld TV script, for example:

    george: i was not going to get a good time.

    george: i think it was a little good idea to be a little chat.

    elaine: i was a little cop.

    sidra: oh, that's a good idea. i don't know what the name is.

    jerry: i think it was the most deal.

    elaine: no.

    george: you know...

    jerry: no! no.

    jerry: oh, that's the way of you, huh, but the result of the trial.

    george: what is that?

    kramer: yeah.

    george: oh, come on, let's go down to you.

    jerry: yeah.

    hoyt: you know, you were going to be a lot of the business.

    jerry: what about the defendants, and the next day is robbing a year of $85.

    hoyt: and i think you were a little. i mean, i think we could be a little good.

    george: i don't know what to say.

    jerry: i can't find that anymore.

    george: i don't know.

    jerry: i can't find this anymore.

    kramer: no, no, no, no.

    jerry: you know, i was just going to be.

    sidra: no one is the only way to the airport.

    kramer: well, i think it's so bad.

    jerry: no.

    kramer: well, i know. i think you would. i think i was a little good.

    kramer: well, you can go down.

    george: oh, that's the good.

    hoyt: the whole, i think it's the first one who had no time to be swarming.

    jerry: oh, i think it's a little cop.

    jerry: i don't know.

    elaine: i don't know, but you want to get it out of the plane.

    kramer: i think i was a good.

    jerry: i was a virgin.

    elaine: yeah, yeah, i know.

    george: so?

    kramer: well, i don't have a lot of a thing of you.

    george: so, you know, that is your fault. you were in the mood of the contest.

    elaine: oh.

    george: so, i can't do that. it's a good man.

    elaine: well, you know, the other time, i have a lot of time.

    jerry: so, the whole thing is in

Notes: the TV script is not perfect. It's ok if the TV script doesn't make perfect sense, but it should look like alternating lines of dialogue.