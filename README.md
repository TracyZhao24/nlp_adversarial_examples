## Set up your environment
Create a Python virtual environment with Python 3.8.10 and install the dependencies specified in `requirements.txt`
```
pip install -r requirements.txt
```
Verify that tensorflow version 2.13.0 and keras version 2.13.1 are installed.
```
pip freeze
```

## Download the datasets
1) Download the Imdb dataset for sentiment analysis task
```
./download_dataset.sh
```

2) Download the SNLI dataset for textual entailment task
```
bash download_snli_data.sh
```

3) Download the glove vector embeddings (used by the model)
```
 ./download_glove.sh 
```

4) Download the counter-fitted vectors (used by our attack)
```
./download_counterfitted_vectors.sh 
```

## Attacking Sentiment Analysis model
1) Build the vocabulary and embeddings matrix.
```
python build_embeddings.py
```

That will take a minute, and it will tokenize the dataset and save it to a pickle file. It will also compute some auxiliary files like the matrix of the vector embeddings for words in our dictionary. All files will be saved under `aux_files` directory created by this script.

2) Download the Google language model.
```
./download_googlm.sh
```

3) Pre-compute the distances between embeddings of different words (required to do the attack) and save the distance matrix.

```
python compute_dist_mat.py 
```
4) Run the attack in the [`IMDB_AttackDemo.ipynb`](IMDB_AttackDemo.ipynb) Jupyter notebook. The sentiment analysis model has already been trained and the checkpoints are included. 

(Optional) To re-train the sentiment analysis model:
```
python train_model.py
```


## Attacking Textual Entailment model

The model we are using for our experiment is the SNLI model of [Keras SNLI Model](https://github.com/Smerity/keras_snli) .

1) Pre-compute the embedding matrix 
```
python nli_compute_dist_matrix.py
```

3) Run the attack using the [`NLI_AttackDemo.ipynb`](NLI_AttackDemo.ipynb) Jupyter notebook. The textual entailment model has already been trained and the checkpoints are included. 

(Optional) To re-train the NLI model:
```
python snli_rnn.py
```