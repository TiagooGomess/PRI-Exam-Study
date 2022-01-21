# Vector Model

## Some definitions

-   Term: A token is an instance of a sequence of characters in some particular document that are grouped together as a useful semantic unit for processing.
-   Type: A type is the class of all tokens containing the same character sequence.
-   Term: A term is a type that is included in the IR system’s dictionary. Rather than being exactly the tokens that appear in the document, they are usually derived from them by various normalization processes

## Stemming and Lemmatization

-   Stemming usually refers to a crude heuristic process that chops off the ends of words, and often includes the removal of derivational affixes.
-   Lemmatization usually refers to doing things properly with the use of a vocabulary and morphological analysis of words, normally aiming to remove inflectional endings only and to return the base or dictionary form of a word, which is known as the lemma.
-   If confronted with the token `saw`, stemming might return just `s`, whereas lemmatization would attempt to return either `see` or `saw` depending on whether the use of the token was as a verb or a noun.
-   Stemming increases recall while harming precision.
-   Stemming can increase the retrieved set without increasing the number of relevant documents.
-   Stemming can only increase the retrieved set, which means increased or unchanged recall.
-   Stemming decreases the size of the vocabulary.
-   Stemming should be invoked at indexing time and when processing a query.

## What is the bag of words model for a document?

-   A bag of words is a representation of text that describes the occurrence of words within a document. We just keep track of word counts and disregard the grammatical details and the word order. It is called a "bag" of words because any information about the order or structure of words in the document is discarded.
-   In this view of a document, known in the literature as the bag of words model, the exact ordering of the terms in a document is ignored but the number of occurrences of each term is material (in contrast to Boolean retrieval). We only retain information on the number of occurrences of each term. Thus, the document "Mary is quicker than John" is, in this view, identical to the document "John is quicker than Mary". Nevertheless, it seems intuitive that two documents with similar bag of words representations are similar in content.

## What is… term frequency, collection frequency, document frequency, inverse document frequency?

-   Term frequency (`tf`): weight is equal to the number of occurrences of term `t` in document `d`. It's denoted `tf-td`, where `td` denotes the term and the document in order.
-   Collection frequency (`cf`): total number of occurrences of a term in the collection
-   Document frequency (`df-t`): number of documents in the collection that contain a term `t`
-   In trying to discriminate between documents for the purpose of scoring it is better to use a document-level statistic (such as the number of documents containing a term) than to use a collection-wide statistic for the term (document frequency is better than collection frequency).
-   Inverse document frequency (`idf`): numerical statistic that is intended to reflect how important a word is to a document in a collection
-   Denoting the total number of documents in a collection by `N`, we define the inverse document frequency (`idf`) of a term `t` as follows:
    -   ![](https://i.imgur.com/LOYlzHK.png)
    -   Thus the `idf` of a rare term is high, whereas the `idf` of a frequent term is likely to be low.

## How do you calculate tf-idf weights?

-   The `tf-idf` weighting scheme assigns to term `t` a weight in document `d` given by:
    -   ![](https://i.imgur.com/5rYXPSC.png)
-   In other words, `tf-idf t,d` assigns to term `t` a weight in document `d` that is:
    -   highest when `t` occurs many times within a small number of documents (thus lending high discriminating power to those documents)
    -   lower when the term occurs fewer times in a document, or occurs in many documents (thus offering a less pronounced relevance signal)
    -   lowest when the term occurs in virtually all documents

## How do you rank documents in the vector model?

-   At this point, we may view each document as a vector with one component corresponding to each term in the dictionary, together with a weight for each component that is given by:
    -   ![](https://i.imgur.com/5rYXPSC.png)
-   For dictionary terms that do not occur in a document, this weight is zero
-   Overlap score measure: the score of a document `d` is the sum, over all query terms, of the number of times each of the query terms occurs in `d`. We can refine this idea so that we add up not the number of occurrences of each query term t in d, but instead the tf-idf weight of each term in d.
    -   ![](https://i.imgur.com/JsYqtH2.png)

## Questions

Why is the `idf` of a term always finite?

-   The `idf` of a term is equal to the logarithm of the number of documents in a collection `N` divided by the document frequency of the term `df`. Because `N` is always finite, and `df` >= 1, then the `idf` of a term is always finite.

<hr>

What is the `idf` of a term that occurs in every document? Compare this with the use of stop word lists.

-   Term occurs in every document => `df = N`
-   `idf = log(N/df) = log(N/N) = log(1) = 0`
-   For a word that occurs in every document, putting it on the stop list has the same effect as idf weighting: the word is ignored.

<hr>

Consider the table of term frequencies for 3 documents denoted Doc1, Doc2, Doc3:

![](https://i.imgur.com/OV3NGl4.png)

Compute the `tf-idf` weights for the terms `car`, `auto`, `insurance`, `best`, for each document, using the `idf` values from the following figure:

![](https://i.imgur.com/AuoyoYY.png)

-   For `Doc1`:
    -   `tf-idf(car) = tf(car) * idf(car) = 27 * 1.65 = 44.55`
    -   `tf-idf(auto) = tf(auto) * idf(auto) = 3 * 2.08 = 6.24`
    -   `tf-idf(insurance) = tf(insurance) * idf(insurance) = 0 * 1.62 = 0`
    -   `tf-idf(best) = tf(best) * idf(best) = 14 * 1.5 = 21`
-   For `Doc2`:
    -   `tf-idf(car) = tf(car) * idf(car) = 4 * 1.65 = 6.6`
    -   `tf-idf(auto) = tf(auto) * idf(auto) = 33 * 2.08 = 68.64`
    -   `tf-idf(insurance) = tf(insurance) * idf(insurance) = 33 * 1.62 = 53.46`
    -   `tf-idf(best) = tf(best) * idf(best) = 0 * 1.5 = 0`
-   For `Doc3`:
    -   `tf-idf(car) = tf(car) * idf(car) = 24 * 1.65 = 39.6`
    -   `tf-idf(auto) = tf(auto) * idf(auto) = 0 * 2.08 = 0`
    -   `tf-idf(insurance) = tf(insurance) * idf(insurance) = 29 * 1.62 = 46.98`
    -   `tf-idf(best) = tf(best) * idf(best) = 17 * 1.5 = 25.5`

<hr>

Can the `tf-idf` weight of a term in a document exceed 1?

-   Yes, as we can see in the exercise above.

<hr>
