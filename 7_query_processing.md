# Query Processing

## Describe and distinguish between the two query processing techniques — document-at-a-time and term-at-a-time.

-   Document-at-a-time, calculates complete scores for documents by processing all term lists, one document at a time. At the end all documents are sorted according to their score.
-   Term-at-a-time, accumulates scores for documents by processing term lists one at a time. When all terms are processed, the accumulators contain the final scores of all matching documents
-   In both approaches, optimization techniques can significantly reduce the time required.

## In what contexts is query transformation / expansion advantageous?

-   In query expansion, users give additional input on query words or phrases, possibly suggesting additional query terms. Some search engines (especially on the web) suggest related queries in response to a query; the users then opt to use one of these alternative query suggestions

## What techniques can be used to apply transformations / expansions to user queries?

-   How to generate alternative question expansions for the user
    -   Use synonyms and related words from a global thesaurus
        -   Use a controlled vocabulary to build a thesaurus;
        -   Use a manual thesaurus built by editors;
        -   Automatically derive thesaurus, e.g. use text statistics;
        -   Use query log mining to find related expansions (global, contextual, user-based);

## Identify and describe query expansions techniques, such as relevance feedback or pseudo-relevance feedback.

-   The idea of **relevance feedback** (RF) is to involve the user in the retrieval process so as to improve the final result set. In particular, the user gives feedback on the relevance of documents in an initial set of results.
-   **Pseudo relevance feedback**, also known as blind relevance feedback, provides a method for automatic local analysis. It automates the manual part of relevance feedback, so that the user gets improved retrieval performance without an extended interaction. The method is to do normal retrieval to find an initial set of most relevant documents, to then assume that the top k ranked documents are relevant, and finally to do relevance feedback as before under this assumption.
-   We can also use indirect sources of evidence rather than explicit feedback on relevance as the basis for relevance feedback. This is often called **implicit (relevance) feedback**. Implicit feedback is less reliable than explicit feedback, but is more useful than pseudo relevance feedback, which contains no evidence of user judgments. Moreover, while users are often reluctant to provide explicit feedback, it is easy to collect implicit feedback in large quantities for a high volume system, such as a web search engine.
