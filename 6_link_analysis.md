# Link Analysis

## What are in-links and out-links for a web page?

-   In-links: links that redirect the user to our website
-   Out-links: links in our website that redirects the user to other websites

## How is anchor text used in web search?

-   The text used in HTML anchors, i.e. links, is called anchor text.
-   Represents a description from "others" about a given web page.
-   The collection of all anchor texts can be explored with standard IR techniques, and incorporated as an additional feature in an inverted index
-   Important feature for image search

## Calculate PageRank values for a set of linked documents.

`PR = sum (PageRank of the pages that are pointing to us / number of pages these pages are pointing)`

![](https://i.imgur.com/sz6fGRc.png)

For example:

`PR(N1) = PR(N4) / 1`

-   Pages that are pointing to N1 -> N4
-   Number of pages N4 is pointing to -> 1

Other example:

`PR(PR4) = PR(N2) / 2 + PR(N3) / 1`

-   Pages that are pointing to N4 -> N2, N3
-   Number of pages N2 is pointing to -> 2
-   Number of pages N3 is pointing to -> 1

## Calculate Hub and Authority values for a set of linked documents.

![](https://i.imgur.com/sz6fGRc.png)

#### Hub Values

`Hub(N) = sum (Auth values of the pages N is pointing to)`

For example:

`Hub(N2) = Auth(N3) + Auth(N4)`

-   Pages N2 is pointing to N3 and N4

#### Authority Values

`Auth(N) = sum (Hub values of the pages pointing to N)`

For example:

`Auth(N4) = Hub(N2) + Hub(N3)`

-   Pages N2 and N3 are pointing to N
