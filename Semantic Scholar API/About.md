# Summary of this section


## Documentation on the API
For this analysis, the Semantic Scholar Documentation on [Paper Data](https://api.semanticscholar.org/api-docs/graph#tag/Paper-Data) is referred for using their API to address the research question. <br>
Since the research paper explorer is aimed to analyze the search results which come up as a result of setting the <b>query keywords</b>, so the API's [Search for papers by keyword](https://api.semanticscholar.org/api-docs/graph#tag/Paper-Data/operation/get_graph_get_paper_search) documentation is especially focused upon.

#### Examples:
(as shown in their documentation)

- ```https://api.semanticscholar.org/graph/v1/paper/search?query=covid+vaccination&offset=100&limit=3```
    - Returns with total=576278, offset=100, next=103, and data is a list of 3 papers.
    - Each paper has its paperId and title.
- ```https://api.semanticscholar.org/graph/v1/paper/search?query=covid&fields=url,abstract,authors```
    - Returns with total=639637, offset=0, next=100, and data is a list of 100 papers.
    - Each paper has paperId, url, abstract, and a list of authors.
    - Each author under that list has authorId and name.
- ```https://api.semanticscholar.org/graph/v1/paper/search?query=totalGarbageNonsense```
    - Returns with total=0, offset=0, and data is a list of 0 papers.
- ```https://api.semanticscholar.org/graph/v1/paper/search?query=covid&year=2020-2023&fieldsOfStudy=Physics,Philosophy&fields=title,year,author```
    - Returns with total=1543075, offset=0, next=10, and data is a list of 10 papers.
    - Filters to include only papers published between 2020-2023.
    - Filters to include only papers that have a field of study either matching Physics or Philosophy.
    - Each paper has the fields paperId, title, year, and author.

### Query parameters
- query ${\color{red}[Required]}$ _Type:string_ <br>A plain-text search query string. No special query syntax is supported.
- fields _Type:string_ <br> A comma-separated list of the fields to be returned.
- year _Type:string_ <br> Restrict results to the given range of publication year (inclusive).
- fieldsOfStudy _Type:string_ <br> Restrict results to given field-of-study, using the s2FieldsOfStudy paper field.
- offset _Type:integer_ <br> Default: 0 <br>When returning a list of results, start with the element at this.position in the list. <br> The sum of offset and limit must be < 10000
- limit _Type:integer_ <br> Default: 100 <br>The maximum number of results to return. <br>Must be <= 100

### Understanding Responses

200 Batch of papers with default or requested fields <br>
RESPONSE SCHEMA: ```application/json``` <br>
- total ${\color{red}[Required]}$ _Type:string_ <br> Number of matching search results
- offset ${\color{red}[Required]}$ _Type:integer_ <br> Default: 0 <br> starting position for this batch
- next ${\color{red}[Required]}$ _Type:integer_ <br>(absent if no more data exists) <br>Default: 1 <br> starting position of the next batch
- data	
Array of objects (contents of this batch)
Array 
paperId
required
string
externalIds	
object
Other catalog IDs for this paper, if known. Supports ArXiv, MAG, ACL, PubMed, Medline, PubMedCentral, DBLP, DOI.

url	
string
URL on the Semantic Scholar website

title	
string (This field will be provided if no fields are specified)
abstract	
string
venue	
string
normalized venue name

publicationVenue	
string
Details about the journal or conference in which this paper was published

year	
integer
referenceCount	
integer
citationCount	
integer
influentialCitationCount	
integer
https://www.semanticscholar.org/faq#influential-citations

isOpenAccess	
boolean
https://www.openaccess.nl/en/what-is-open-access

openAccessPdf	
string
A link to the paper if it is open access, and we have a direct link to the pdf. As well as the paper's status. More info on status here: https://en.wikipedia.org/wiki/Open_access#Colour_naming_system

fieldsOfStudy	
object
A list of high-level academic categories from external sources.

s2FieldsOfStudy	
object
A list of high-level academic categories, inc their sources

publicationTypes	
Array of strings
The type of this publication

publicationDate	
string
Year-month-day when this paper was published

journal	
object
Journal name, volume, and pages

citationStyles	
object
Bibliographic citations for paper, currently supported styles: BibTeX

authors	
Array of objects (Author Info) 
 Up to 500 will be returned
- authorId - Always included <br> <i>On the author page, for every author, Semantic Scholar ID is the numerical string at the end of the URL.</i>
- name - Always included


### Using the variables
- 'query': 'online sexism misogyny'
- 'year': 2012-2022 (The period of study for this research)

