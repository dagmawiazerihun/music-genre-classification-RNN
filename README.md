# Music Genre Classification using Naive Bayes and RNN

This program utilizes Naive Bayes classification on the [Million Song Dataset](http://millionsongdataset.com/) to classify songs in 2 given genres. It displays to the console the top 10 classifying words and the classifier's accuracy on 
the test portion of the dataset (20%). Then, we compare this ML model to a TensorFlow RNN, for which we also print the accuracy.

## Command Line Argument

This program takes one optional command line argument, which specifies the number of records in the final table. The number of tracks included for a given record limit is roughly an order of magnitude less than the limit. This is used to 
optimize performance. On a ~2018 Dell Laptop with 4 cores and 8 threads, running with all rock and metal songs and 100,000 records in the MSD took ~200 seconds, or ~3.33 minutes. We have found that 100,000 records is optimal for testing 
as it provides a balance of speed and accuracy. Other genre combinations we tried took up to ~325 seconds, likely due to the RNN model not activating the early stopping procedure because the error had not significantly neutralized before 
all epochs were run.

## Program Workflow

The program attaches several databases from the MSD, extracts relevant columns, and then extracts the bag of words and genre tags for each record (track) such that it is already formatted to be run on the NLTK naive bayes model. Then, the 
data is reformatted into a pandas dataframe containing per record a genre tag in the 0th column and in subsequent columns each column represents a lyric in the generated corpus of songs, and each cell is a boolean indicating its presence 
in the given track. From this we can easily extract the genre label and a vector of word presences using basic list comprehension.

## Findings

We ran this program using 100k records on several different genre combinations, and the findings can help indicate which genres are similar in lyrical structure (more similar genres are harder to accurately classify) and which genres are 
more distinct than others (we found rap was very easily identifiable.)

## RNN Model

The RNN has several layers, namely an embedding layer, an LSTM layer, and a Dense layer, all feeding into 2 final neurons which indicate genre. Details about these layer types can be found in the in-line code comments or in the final 
report attached in this directory.

