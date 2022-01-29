# Evaluation

## What is… precision, recall, interpolated precision?

-   Precision (P): the fraction of retrieved documents that are relevant. `P = #(relevant items retrieved) / #(retrieved items)`
-   Recall (R): the fraction of relevant documents that are retrieved. `R = #(relevant items retrieved) / #(relevant items)`
-   Why accuracy is not a good measure:
    -   There is a good reason why accuracy is not an appropriate measure for information retrieval problems. In almost all circumstances, the data is extremely skewed: normally over 99.9% of the documents are in the nonrelevant category. A system tuned to maximize accuracy can appear to perform well by simply deeming all documents nonrelevant to all queries. Even if the system is quite good, trying to label some documents as relevant will almost always lead to a high rate of false positives. However, labeling all documents as nonrelevant is completely unsatisfying to an information retrieval system user.
-   you can always get a recall of 1 (but very low precision) by retrieving all documents for all queries!
-   in a good system, precision usually decreases as the number of documents retrieved is increased.
-   A single measure that trades off precision versus recall is the F measure, which is the weighted harmonic mean of precision and recall. F1-measure:
    -   ![](https://i.imgur.com/LUPlDT4.png)
    -   Values of β < 1 emphasize precision, while values of β > 1 emphasize recall.
-   Interpolated precision: the interpolated precision at a certain recall level r is defined as the highest precision found for any recall level r′ ≥ r:
    -   ![](https://i.imgur.com/7MNVLLe.png)

## What is… precision at k, R-precision?

-   Precision at k:
    -   This leads to measuring precision at fixed low levels of retrieved results, such as 10 or 30 documents. This is referred to as “Precision at k”, for example “Precision at 10”. It has the advantage of not requiring any estimate of the size of the set of relevant documents but the disadvantages that it is the least stable of the commonly used evaluation measures and that it does not average well, since the total number of relevant documents for a query has a strong influence on precision at k.
-   R-precision:
    -   R-precision requires knowing all documents that are relevant to a query. The number of relevant documents, R, is used as the cutoff for calculation, and this varies from query to query. For example, if there are 15 documents relevant to "red" in a corpus (R=15), R-precision for "red" looks at the top 15 documents returned, counts the number that are relevant r turns that into a relevancy fraction: `r/R = r/15`
    -   R-Precision is equal to recall at the R-th position
    -   Empirically, this measure is often highly correlated to mean average precision

## Name the components of a test collection.

-   A document collection
-   A test suite of information needs, expressible as queries
-   A set of relevance judgments, standardly a binary assessment of either relevant or nonrelevant for each query-document pair

## Why is a set of relevance judgment considered a "ground truth" for IR?

-   With respect to a user information need, a document in the test collection is given a binary classification as either relevant or nonrelevant. This decision is referred to as the gold standard or ground truth judgment of relevance
-   When a person judges a document to be relevant to a particular query, or information need, such a judgment is called a relevance judgment.
-   Relevance judgments are used to construct ground truth test collections, so that the retrieval accuracy of retrieval methods can be evaluated. Ground truth test collections for the evaluation of document retrieval systems have sets of queries and documents for which human experts have judged the relevance of document query pairs.

## What is an average 11-point precision-recall graph for a set of queries?

-   Examining the entire precision-recall curve is very informative, but there is often a desire to boil this information down to a few numbers, or perhaps even a single number. The traditional way of doing this (used for instance in the first 8 TREC Ad Hoc evaluations) is the 11-point interpolated average precision. For each information need, the interpolated precision is measured at the 11 recall levels of 0.0, 0.1, 0.2, . . . , 1.0.

## What is MAP, and do you calculate it for a set of queries in a test collection?

-   Mean Average Precision (MAP) provides a single-figure measure of quality across recall levels. Among evaluation measures, MAP has been shown to have especially good discrimination and stability.
-   For a single information need, Average Precision is the average of the precision value obtained for the set of top k documents existing after each relevant document is retrieved, and this value is then averaged over information needs
-   ![](https://i.imgur.com/BDZ1Jco.png)
-   For a single information need, the average precision approximates the area under the uninterpolated precision-recall curve, and so the MAP is roughly the average area under the precision-recall curve for a set of queries.
-   The MAP value for a test collection is the arithmetic mean of average precision values for individual information needs

## Exercise 8.1

An IR system returns 8 relevant documents, and 10 nonrelevant documents. There are a total of 20 relevant documents in the collection. What is the precision of the system on this search, and what is its recall?

-   `P = 8 / (10+8) = 0.44`
-   `R = 8 / 20 = 0.4`

## Exercise 8.4

What are the possible values for interpolated precision at a recall level of 0?

-   the interpolated precision at a certain recall level r is defined as the highest precision found for any recall level r′ ≥ r
-   the interpolated precision at a recall level of 0: `0 <= p <= 1`
-   then, `0 <= interpolated precision at a recall level of 0 <= 1`

## Exercise 8.8

Consider an information need for which there are 4 relevant documents in the collection. Contrast two systems run on this collection. Their top 10 results are judged for relevance as follows (the leftmost item is the top ranked search result):

System 1 => R N R N N N N N R R

System 2 => N R N N R R R N N N

Precisions:

System 1 => 1 0.5 0.67 0.5 0.4 0.33 0.29 0.25 0.33 0.4

System 2 => 0 0.5 0.3 0.25 0.4 0.5 0.57 0.5 0.44 0.4

a. What is the MAP of each system? Which has a higher MAP?

-   For the System 1:
    -   `MAP = (1 + 0.67 + 0.33 + 0.4) / 4 = 0.6`
-   For the System 2:
    -   `MAP = (0.5 + 0.4 + 0.5 + 0.57) / 4 = 0.4925`
-   System 1 has a higher MAP

b. Does this result intuitively make sense? What does it say about what is important in getting a good MAP score?

-   For a good MAP score, it is essential to more relevant documents in the first few (3-5) retrieved ones

c. What is the R-precision of each system? (Does it rank the systems the same as MAP?)

-   R-precision(System 1) = 2 / 4 = 0.5
-   R-precision(System 2) = 1 / 4 = 0.25
-   It ranks the systems the same as MAP (System 1 is better in both)

## Exercise 8.9

The following list of Rs and Ns represents relevant (R) and nonrelevant (N) returned documents in a ranked list of 20 documents retrieved in response to a query from a collection of 10,000 documents. The top of the ranked list (the document the system thinks is most likely to be relevant) is on the left of the list. This list shows 6 relevant documents. Assume that there are 8 relevant documents in total in the collection.

R R N N N N N N R N R N N N R N N N N R

a. What is the precision of the system on the top 20?

-   `P = 6 / 20 = 0.3`

b. What is the F1 on the top 20?

-   `F1 = (2*P*R)/(P+R)`
-   `R = 6 / 8 = 0.75`
-   `F1 = (2*0.3*0.75)/(0.3+0.75) = 0.43`

c. What is the interpolated precision of the system at 25% recall?

-   Recall values:
    -   0.125 0.25
-   Precision values:
    -   1 1
-   The precision is 1

e. Assume that these 20 documents are the complete result set of the system. What is the MAP for the query?

-   `MAP = (1/1 + 2/2 + 3/9 + 4/11 + 5/15 + 6/20) / 6 = 0.555`
