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

## Questions in section 6.2

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

## Vector space model

-   Representation of a set of documents as vectors in a common vector space
-   It is fundamental to a host of information retrieval operations ranging from scoring documents on a query, document classification and document clustering
-   To compensate for the effect of document length, the standard way of quantifying the similarity between two documents `d1` and `d2` is to compute the cosine similarity of their vector representations `V(d1)` and `V(d2)`:
    -   ![](https://i.imgur.com/oFBGm9q.png)
    -   where the numerator represents the dot product (also known as inner product) of the vectors `V(d1)` and `V(d2)`, while the denominator is the product of their Euclidean lengths.
    -   This formula can rewritten to:
        -   ![](https://i.imgur.com/Mp8z7sK.png)
        -   where:
        -   ![](https://i.imgur.com/70RstbV.png)
        -   and:
        -   ![](https://i.imgur.com/DAbE0QJ.png)
    -   Thus, `sim(d1, d2)` can be viewed as the dot product of the normalized versions of the two document vectors
    -   This measure is the cosine of the angle `θ` between the two vectors, shown in the following figure:
    -   ![](https://i.imgur.com/IGlfRhp.png)
-   What use is the similarity measure `sim(d1, d2)`?
    -   Given a document `d`, consider searching for the documents in the collection most similar to `d`
    -   Such a search is useful in a system where a user may identify a document and seek others like it – a feature available in the results lists of search engines as a more like this feature
    -   We reduce the problem of finding the document(s) most similar to `d` to that of finding the `di` with the highest dot products (sim values) `v(d)·v(di)`.
    -   We could do this by computing the dot products between `v(d)` and each of `v(d1), . . . ,v(dN)`, then picking off the highest resulting `sim` values
-   Term-document matrix: this is an `M × N` matrix whose rows represent the `M` terms (dimensions) of the `N` columns, each of which corresponds to a document

## Example 6.2

-   ![](https://i.imgur.com/VbedOlv.png)
    -   ![](https://i.imgur.com/8lM3Hxt.png)
    -   ![](https://i.imgur.com/cn4MFtH.png)
-   For `Doc1`:
    -   sqrt(27^2 + 3^2 + 0^2 + 14^2) = 30.56
-   For `Doc2`:
    -   sqrt(4^2 + 33^2 + 33^2 + 0^2) = 46.84
-   For `Doc3`:
    -   sqrt(24^2 + 0^2 + 29^2 + 17^2) = 41.30
-   To calculate the values of the table of the Figure 6.11:
    -   For `Doc1`:
        -   For `car`:
            -   27 / 30.56 = 0.88
        -   ...
    -   ...

## Example 6.3

-   Figure 6.12 shows the number of occurrences of three terms (affection, jealous and gossip) in each of the following three novels: Jane Austen’s Sense and Sensibility (SaS) and Pride and Prejudice (PaP) and Emily Brontë’s Wuthering Heights (WH).
-   Of course, there are many other terms occurring in each of these novels. In this example we represent each of these novels as a unit vector in three dimensions, corresponding to these three terms (only); we use raw term frequencies here, with no `idf` multiplier. The resulting weights are as shown in Figure 6.13
    -   ![](https://i.imgur.com/U4TrS2e.png)
    -   ![](https://i.imgur.com/VUXva1h.png)
-   Now consider the cosine similarities between pairs of the resulting three-dimensional vectors. A simple computation shows that `sim(v(SAS), v(PAP))` is 0.999, whereas `sim(v(SAS), v(WH))` is 0.888; thus, the two books authored by Austen (SaS and PaP) are considerably closer to each other than to Brontë’s Wuthering Heights. In fact, the similarity between the first two is almost perfect (when restricted to the three terms we consider). Here we have considered `tf` weights, but we could of course use other term weight functions.

## Queries as vectors

-   The key idea now: to assign to each document `d` a score equal to the dot product
    -   ![](https://i.imgur.com/RnGyM8c.png)
-   The number of dimensions is equal to the vocabulary size `M`.
-   To summarize, by viewing a query as a "bag of words", we are able to treat it as a very short document. As a consequence, we can use the cosine similarity between the query vector and a document vector as a measure of the score of the document for that query. The resulting scores can then be used to select the top-scoring documents for a query
    -   ![](https://i.imgur.com/a9LJU8a.png)

## Example 6.4

-   ![](https://i.imgur.com/5TWHsJR.png)

## Questions in section 6.2

Consider the following `tf-idf` weights:

-   tf-idf(car) for `Doc1`, `Doc2`, `Doc3` => `44.55`, `6.6`, `39.6`
-   tf-idf(auto) for `Doc1`, `Doc2`, `Doc3` => `6.24`, `68.64`, `0`
-   tf-idf(insurance) for `Doc1`, `Doc2`, `Doc3` => `0`, `53.46`, `46.98`
-   tf-idf(best) for `Doc1`, `Doc2`, `Doc3` => `21`, `0`, `25.5`

Compute the Euclidean normalized document vectors for each of the documents, where each vector has four components, one for each of the four terms (car, auto, insurance, best).

-   For `Doc1`:
    -   `Euclidean normalization value = sqrt(44.55^2 + 6.24^2 + 0^2 + 21^2) = 49.65`
    -   `Euclidean normalized document vector = (44.55 / 49.65, 6.24 / 49.65, 0 / 49.65, 21 / 49.65) = (0.897, 0.126, 0, 0.422)`
-   For `Doc2`:
    -   `Euclidean normalization value = sqrt(6.6^2 + 68.64^2 + 53.46^2 + 0^2) = 87.25`
    -   `Euclidean normalized document vector = (6.6 / 87.25, 68.64 / 87.25, 53.46 / 87.25, 0 / 87.25) = (0.076, 0.7867, 0.613, 0)`
-   For `Doc3`:
    -   `Euclidean normalization value = sqrt(39.6^2 + 0^2 + 46.98^2 + 25.5^2) = 64.78`
    -   `Euclidean normalized document vector = (39.6 / 64.78, 0 / 64.78, 46.98 / 64.78, 25.5 / 64.78) = (0.611, 0, 0.725, 0.394)`

<hr>

Verify that the sum of the squares of the components of each of the document vectors in the previous exercise is 1 (to within rounding error). Why is this the case?

-   For `Doc1`:
    -   `0.897^2 + 0.126^2 + 0^2 + 0.422^2 = 1`
-   For `Doc2`:
    -   `0.076^2 + 0.7867^2 + 0.613^2 + 0^2 = 1`
-   For `Doc3`:
    -   `0.611^2 + 0^2 + 0.725^2 + 0.394^2 = 1`

The vectors were normalized, so the some of the squares of each component is 1.

<hr>

With term weights as computed in the first exercise of this section, rank the three documents by computed score for the query `car insurance`, for each of the following cases of term weighting in the query:

i) The weight of a term is 1 if present in the query, 0 otherwise
ii) Euclidean normalized idf

-   i)
    -   Term weights (`Doc1`, `Doc2`, `Doc3`):
        -   car => (0.897, 0.076, 0.611)
        -   auto => (0.126, 0.7667, 0)
        -   insurance => (0, 0.613, 0.725)
        -   best => (0.422, 0, 0.394)
    -   For `Doc1`:
        -   `score = v(q) . v(d) = (1, 0, 1, 0) . (0.897, 0.126, 0, 0.422) = 0.897`
    -   For `Doc2`:
        -   `score = v(q) . v(d) = (1, 0, 1, 0) . (0.076, 0.7867, 0.613, 0) = 0.076 + 0.613 = 0.689`
    -   For `Doc3`:
        -   `score = v(q) . v(d) = (1, 0, 1, 0) . (0.611, 0, 0.725, 0.394) = 0.611 + 0.725 = 1.336`
    -   Ranking = `Doc3`, `Doc1`, `Doc2`
