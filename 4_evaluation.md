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

## What is… precision at k, R-precision?

## Name the components of a test collection.

-   A document collection
-   A test suite of information needs, expressible as queries
-   A set of relevance judgments, standardly a binary assessment of either relevant or nonrelevant for each query-document pair

## Why is a set of relevance judgment considered a "ground truth" for IR?

-   With respect to a user information need, a document in the test collection is given a binary classification as either relevant or nonrelevant. This decision is referred to as the gold standard or ground truth judgment of relevance
-   When a person judges a document to be relevant to a particular query, or information need, such a judgment is called a relevance judgment.
-   Relevance judgments are used to construct ground truth test collections, so that the retrieval accuracy of retrieval methods can be evaluated. Ground truth test collections for the evaluation of document retrieval systems have sets of queries and documents for which human experts have judged the relevance of document query pairs.

## Draw a precision-recall curve for capturing the evolution of precision in the ranked list of results for a query.

## What is an average 11-point precision-recall graph for a set of queries?

## What is MAP, and do you calculate it for a set of queries in a test collection?

## Exercise 8.1

An IR system returns 8 relevant documents, and 10 nonrelevant documents. There are a total of 20 relevant documents in the collection. What is the precision of the system on this search, and what is its recall?

-   `P = 8 / (10+8) = 0.44`
-   `R = 8 / 20 = 0.4`
