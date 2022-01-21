# IR Concepts

### Information Retrieval

-   Information retrieval (IR) is finding material (usually documents) of an unstructured nature (usually text) that satisfies an information need from within large collections (usually stored on computers).

### Boolean Retrieval Model

-   The Boolean retrieval model is a model for information retrieval in which we can pose any query which is in the form of a Boolean expression of terms, that is, in which terms are combined with the operators AND, OR, and NOT.
-   The model views each document as just a set of words.

### Document

-   Whatever units we have decided to build a retrieval system over.

### Collection

-   Group of documents over which we perform retrieval.

### Term

-   Terms are the indexed units
-   They are usually words, but the information retrieval literature normally speaks of terms because some of them, such as perhaps I-9 or Hong Kong are not usually thought of as words.

### Other Concepts

-   An information need is the topic about which the user desires to know more
-   A query is what the user conveys to the computer in an attempt to communicate the information need.
-   Results list: list of results retrieved.
-   A document is relevant if it is one that the user perceives as containing information of value with respect to their personal information need.
-   Precision: What fraction of the returned results are relevant to the information need?
-   Recall: What fraction of the relevant documents in the collection were returned by the system?
-   A bag of words is a representation of text that describes the occurrence of words within a document. We just keep track of word counts and disregard the grammatical details and the word order. It is called a "bag" of words because any information about the order or structure of words in the document is discarded.
-   In information retrieval, stemming is the process of reducing inflected (or sometimes derived) words to their word stem, base or root form—generally a written word form.

### Inverted index

-   The name is actually redundant: an index always maps back from terms to the parts of a document where they occur.
-   The basic idea of an inverted index is shown in following figure:
    -   ![](https://i.imgur.com/oGALw0t.png)
-   We keep a dictionary of terms (sometimes also referred to as a vocabulary or lexicon; in this book, we use dictionary for the data structure and vocabulary for the set of terms)
-   Then for each term, we have a list that records which documents the term occurs in.
-   Each item in the list – which records that a term appeared in a document is conventionally called a posting
-   The list is then called a postings list (or inverted list), and all the postings lists taken together are referred to as the postings
-   Steps for building an inverted index:
    -   Collect the documents to be indexed
    -   Tokenize the text, turning each document into a list of tokens
    -   Do linguistic preprocessing, producing a list of normalized tokens, which are the indexing terms
    -   Index the documents that each term occurs in by creating an inverted index, consisting of a dictionary and postings
