## Week 2: Natural Language Processing and Word Embeddings

### Word Representation

So far, we represent words as vocabulory of words. Vocabulory could be 10,000 words long and each word in it is represented using one-hot encoding. One disadvantage of this is that each word is a thing in itself and it does'nt allow the algorithms to generalize the cross words.
Note that, the inner product of any two one-hot encoded vectors is zero. So, let's take an example: 

I want an Orange _______.

I want an Apple ________.

![wr1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2012-34-57.png)

The most likely word for the first and second blank space is 'juice'.
Even though the learning algorithm has learned the sentence that I want an Orange _juice_. Then the relationship between orange and apple is not as closer to any of the other words. Hence, the learning algorithm finds it difficult to recognize apple _juice_ is also as popular as orange _juice_. 

So, instead of one-hot representation, we can instead learn 'Featurized representation'. So, something like this:

![wr2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2012-41-37.png)

Let's say we take 300 features. Hence, e_5931 is 300 dimensional vector for the 'Man'. See the above figure. You can see that the probabilities/ numbers assigned with orange and apple are almost similar in most of the cases. Hence, this increases the probability of _juice_ being in the blank space for both of the sentences.

**Visualizing Word Embeddings:**
The representation that uses some sort of feauturized represntations in maybe a 300 dimensional space, these are called embeddings. For ex. the word 'Orange' is represnted as point in 300-dimensional space and hence is embedded in that space.The word 'Apple' is embedded to some other point in the same space. These features are visualized by mapping into much lower dimensional space. We can actually plot a 2D data and look at it. Word embeddings has been one of the most important ideas in NLP, in Natural Language Processing. 

![wr3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2012-56-01.png)


### Using Word Embeddings

In this video, you see how we can take these representations and plug them into NLP applications. Continuing with the named entity recognition example,
if you're trying to detect people's names. Given a sentence like Sally Johnson is an orange farmer, hopefully, you'll figure out that Sally Johnson is a person's name, hence, the outputs 1 like that. if you can now use the featurized representations, the embedding vectors that we talked about in the last discussion.
Then after having trained a model that uses word embeddings as the inputs, if you now see a new input, Robert Lin is an apple farmer.
Knowing that orange and apple are very similar will make it easier for your learning algorithm to generalize to figure out that Robert Lin is also a human.

!we1[](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-22-50.png)

A durian is a rare type of fruit, popular in Singapore and a few other countries.
But if you have a small label training set for the named entity recognition task,
you might not even have seen the word durian or
seen the word cultivator in your training set.
I guess technically, this should be a durian cultivator.
But if you have learned a word embedding that tells you that durian is a fruit,
so it's like an orange, and a cultivator, someone that cultivates is like a farmer,
then you might still be generalize from having seen an orange farmer in your
training set to knowing that a durian cultivator is also probably a person.
So one of the reasons that word embeddings will be able to do this is
the algorithms to learning word embeddings can examine very large text corpuses,
maybe found off the Internet.
So you can examine very large data sets, maybe a billion words,
maybe even up to 100 billion words would be quite reasonable.
So very large training sets of just unlabeled text. 

Now having discovered that orange and
durian are both fruits by reading massive amounts of Internet text,
what you can do is then take this word embedding and apply it to your named
entity recognition task, for which you might have a much smaller training set,
maybe just 100,000 words in your training set, or even much smaller. 

This allows us to use **Transfer Learning**  
where you take information you've learned from
huge amounts of unlabeled text that you can suck down essentially for
free off the Internet to figure out that orange, apple, and durian are fruits. 

![we2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-24-58.png)

![we3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-36-55.png)

![we4](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-38-02.png)


### Properties of Word Embeddings

One of the most fascinating properties of word embeddings is that they can also
help with analogy reasoning

![we5](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2013-59-42.png)

- 300D to 2D mapping for greater visualization

![we6](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2014-04-42.png)

Cosine similarity basically checks the inner product of the two vectors in t-swe space. More the inner product greater is the similarity.

![we7](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2014-10-04.png)

### Embedding Matrix

Now we shall see how to learn the word embeddings.
The big 300x10000 is the embedded matrix.

![l1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2014-20-45.png)


### Learning Word Embeddings

It turns out that Neural Network model is the small way of learning word embeddings. The hidden layers have their own parameters and the softmax at the end predicts the word 'juice'. 

![l2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2015-38-52.png)

![l3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2015-42-06.png)

### Word2Vec

If we want to predict the word within the window of +-10 words, then we define a context and a specified target. This is not an easy learning problem as there are many other words in a window of +-10 words. Embedding vector is obtained. 

![w1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2015-56-09.png)

This particular model is skip gram model because it skips some words according to the given context and the desired target.

Also, the disadvantage with softmax is that it's computationally heavy. Heirarchical Classification is good way to avoid this. Having a tree like this, the nodes can act just like a binary classification. Heirarchical softmax classifier doesn't nearly seem to be symmetrical. Usually the common words such as 'orange' or 'apple' are placed at the top 2/3 layers. However, the rare words such as 'durin' are placed at the much deeper nodes. This is one of the ways for speeding up the process.

![w2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2016-10-04.png)

### Negative Sampling

![ns1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2016-42-49.png)

This is just a modified way of learning algorithm and much more efficient than the skip gram model.'
For every positive examples, we have k negative examples for logistic regression type model. 

![ns2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2016-33-01.png)

![ns3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2016-42-38.png)

### GloVe Word Vectors

Not as popular as previous words. Symmetric relation between them if they appear in +-10 words of each other. X_ij is count of how close they appear w.r.t each other. Basically, the GloVe model minimizes the difference between :

![g1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2016-48-55.png)

We introduce the weighting term f_ij because we don't want log(X_ij) to be not equal to log(0). The other thing that this term f_ij does is:
rare words such as 'durin' are given more weight even though they do not appear as frequently as other similar words occur. Also, it does'nt give undue weight to the _Stop Words_ such as this, that, the, is, etc. which eventually hardly matter. 

In this GloVe model, theta and e are symmetrical.They eventually end up in the same optimization objective. One way to train the algorithm is to initialize theta and e
both uniformly around gradient descent to minimize its objective,
and then when you're done for every word,
to then take the average.
For a given words w,
you can have e final to be equal
to the embedding that was trained through this gradient descent procedure,
plus theta trained through this gradient descent procedure divided by two,
because theta and e in this particular formulation play
symmetric roles unlike the earlier models we saw in the previous videos.

![g2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-05-08.png)

![g3](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-12-10.png)

Correction:
![g4](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-18-39.png)

### Sentiment Classification
One of the challenges of sentiment classification
is you might not have a huge label training set for it.
But with word embeddings,
you're able to build good sentiment classifiers
even with only modest-size label training sets.

![sc1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-26-59.png)

the job of the RNN is to then compute
the representation at the last time step that allows you to predict Y-hat.
So this is an example of
a many-to-one RNN architecture which we saw in the previous week.
And with an algorithm like this,
it will be much better at taking word sequence into account and realize that "things are
lacking in good taste" is a negative review
and "not good" a negative review unlike the previous algorithm,
which just sums everything together into a big-word vector
mush and doesn't realize that "not good" has a very different meaning
than the words "good" or "lacking in good taste" and so on.
And so if you train this algorithm,
you end up with a pretty decent sentiment classification algorithm and
because your word embeddings can be trained from a much larger data set,
this will do a better job
generalizing to maybe even new words now that you'll see in your training set,
such as if someone else says,
"Completely absent of good taste,
good service, and good ambiance" or something,
then even if the word "absent" is not in your label training set,
if it was in your 1 billion or 100 billion word corpus used to train the word embeddings,
it might still get this right and generalize much better even to words that were in
the training set used to train the word embeddings but not
necessarily in the label training set
that you had for specifically the sentiment classification problem. 

![sc2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-30-07.png)

### Debiasing Word Embedding

For increasing accuracy, we have to make sure that our model is not biased to any of the feature. We shall see now how to eliminate those bias. (The bias is not the bias of NN here)

![db1](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-37-19.png)

Much more research is being carried out in the this field for reducing word debiasing

![db2](https://github.com/sharvaree1921/Audio_Controlled_Drone/blob/main/Images/Screenshot%20from%202021-05-28%2017-43-56.png)
