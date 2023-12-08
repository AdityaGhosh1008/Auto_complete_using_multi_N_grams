# Auto_complete_using_multi_N_grams
Auto complete system using multiple N grams ranked using pointwise mutual information
# Theory
Amongst classical machine learning techniques, N-grams is the most popular option for text
prediction/generation tasks. A thorough literature survey found out that using an N-grams model
along with PMI yielded the highest accuracy on the MSR dataset challenge. Hence, we embark on
implementing an N-grams model while enhancing its predictions using the PMI (Pointwise Mutual
Information) metric. We tweak our model to be generative rather than picking one out of a few
options available (as was the case with the MSR dataset and Hellaswag dataset)

Since we want to make an autocompletion model, we train the model on the “correct” endings
provided by the Hellaswag training dataset. The initial preprocessing steps involve dropping the
irrelevant columns (such as ind, source_id, split and split_type) and splitting the 4 ending options
into separate columns (labelled A0, A1, A2 and A3 respectively). We then use the correctly provided
label to find the “correct” ending and concatenate it with the context sentence provided to create the
final sentence. All columns other than ‘activity_label’ and the ‘Sentence’ columns are dropped. The
sentences are converted to lowercase and irrelevant words such as ‘[header’], ‘[title]’, ‘[step]’ and
‘[substep]’ are dropped. The words are lemmatised and different n-gram (unigram, bigram, trigram,
quadgram, pentagram, hexagram) tokens are created and their respective frequencies are calculated.
Input text when passed to a group of N-gram models which generate an array of predicted
outputs. We ten pass all these new predicted texts as input texts to the N-gram models to generate a
concatentaed output for each of the input texts. We repeat this process until the required length of the
sentence is reached (can be changed in code). This is sort of a brute force approach where we exhaust
all possible outputs that can be generated and use them further as inputs to find the best sentence
possible. In case a word is not present in the vocabulary of the model, we continue prediction by
randomly appending a word which does not change the context of the sentence. Since our task is of
sentence completion, we separate out the sentences which have ended with a fullstop (or a ‘<e>’
character) from those that still have scope to be completed. It is important to note that the sentences
without a fullstop will eventually terminate with one given we allow the length of the sentence to
increase. However, due to lack of resources (time and computational) we run the model for only
5-7 words. We finally rank the appropriateness of each sentence by calculating the PMI (Pointwise
Mutual Index) of each sentence.
