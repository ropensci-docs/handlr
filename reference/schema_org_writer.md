# Schema org writer

Schema org writer

## Usage

``` r
schema_org_writer(z, auto_unbox = TRUE, pretty = TRUE, ...)
```

## Arguments

- z:

  an object of class `handl`; see
  [handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

- auto_unbox:

  (logical) automatically "unbox" all atomic vectors of length 1
  (default: `TRUE`). passed to
  [`jsonlite::toJSON()`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html)

- pretty:

  (logical) adds indentation whitespace to JSON output (default:
  `TRUE`), passed to
  [`jsonlite::toJSON()`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html)

- ...:

  further params passed to
  [`jsonlite::toJSON()`](https://jeroen.r-universe.dev/jsonlite/reference/fromJSON.html)

## Value

an object of class `json`

## See also

Other writers:
[`bibtex_writer()`](https://docs.ropensci.org/handlr/reference/bibtex_writer.md),
[`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md),
[`citeproc_writer()`](https://docs.ropensci.org/handlr/reference/citeproc_writer.md),
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md),
[`rdf_xml_writer()`](https://docs.ropensci.org/handlr/reference/rdf_xml_writer.md),
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md)

## Examples

``` r
if (requireNamespace("bibtex", quietly=TRUE)) {
(z <- system.file('extdata/bibtex.bib', package = "handlr"))
(tmp <- bibtex_reader(z))
schema_org_writer(tmp)
schema_org_writer(tmp, pretty = FALSE)
}
#> {"@context":"https://schema.org","@type":"article","@id":"https://doi.org/10.1142/s1363919602000495","identifier":{"@type":"PropertyValue","propertyID":"doi","value":"https://doi.org/10.1142/s1363919602000495"},"url":"https://doi.org/10.1142%2Fs1363919602000495","additionalType":"JournalArticle","name":"{THE} {INTENSIFICATION} {OF} {INNOVATION}","author":[{"@type":"Person","name":"MARK DODGSON","givenName":"MARK","familyName":"DODGSON"},{"@type":"Person","name":"DAVID M. GANN","givenName":"DAVID M.","familyName":"GANN"},{"@type":"Person","name":"AMMON. J SALTER","givenName":"AMMON. J","familyName":"SALTER"}],"editor":[],"pageStart":"53","pageEnd":"83","sameAs":[],"isPartOf":[{"@type":"Periodical","name":"International Journal of Innovation Management"}],"hasPart":[],"predecessor_of":[],"successor_of":[],"citation":[],"publisher":{"@type":"Organization","name":"World Scientific Pub Co Pte Lt"},"funding":[]} 

# many citeproc to schema
z <- system.file('extdata/citeproc-many.json', package = "handlr")
w <- citeproc_reader(x = z)
schema_org_writer(w)
#> [
#>   {
#>     "@context": "https://schema.org",
#>     "@type": "BlogPosting",
#>     "@id": "https://doi.org/10.5438/4k3m-nyvg",
#>     "identifier": {
#>       "@type": "PropertyValue",
#>       "propertyID": "doi",
#>       "value": "https://doi.org/10.5438/4k3m-nyvg"
#>     },
#>     "name": "Eating your own Dog Food",
#>     "author": [
#>       {
#>         "@type": "Person",
#>         "name": "Martin Fenner",
#>         "givenName": "Martin",
#>         "familyName": "Fenner"
#>       }
#>     ],
#>     "editor": [],
#>     "description": "Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...",
#>     "keywords": "Phylogeny, Malaria, Parasites, Taxonomy, Mitochondrial genome, Africa, Plasmodium",
#>     "datePublished": "2016-12-20",
#>     "sameAs": [],
#>     "isPartOf": [
#>       {
#>         "@type": "Periodical",
#>         "name": "DataCite Blog"
#>       }
#>     ],
#>     "hasPart": [],
#>     "predecessor_of": [],
#>     "successor_of": [],
#>     "citation": [],
#>     "publisher": {
#>       "@type": "Organization",
#>       "name": "DataCite"
#>     },
#>     "funding": []
#>   },
#>   {
#>     "@type": "ScholarlyArticle",
#>     "identifier": {
#>       "@type": "PropertyValue",
#>       "propertyID": "url",
#>       "value": {}
#>     },
#>     "name": "Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)",
#>     "author": [
#>       {
#>         "sequence": "first",
#>         "affiliation": [],
#>         "@type": "Person",
#>         "name": "Karen L Juillerat",
#>         "givenName": "Karen L",
#>         "familyName": "Juillerat"
#>       },
#>       {
#>         "sequence": "additional",
#>         "affiliation": [],
#>         "@type": "Person",
#>         "name": "Felipe A Cornejo",
#>         "givenName": "Felipe A",
#>         "familyName": "Cornejo"
#>       },
#>       {
#>         "sequence": "additional",
#>         "affiliation": [],
#>         "@type": "Person",
#>         "name": "Ramón D Castillo",
#>         "givenName": "Ramón D",
#>         "familyName": "Castillo"
#>       },
#>       {
#>         "sequence": "additional",
#>         "affiliation": [],
#>         "@type": "Person",
#>         "name": "Sergio E Chaigneau",
#>         "givenName": "Sergio E",
#>         "familyName": "Chaigneau"
#>       }
#>     ],
#>     "editor": [],
#>     "datePublished": "2015-12",
#>     "pageStart": "221",
#>     "pageEnd": "238",
#>     "sameAs": [],
#>     "isPartOf": [
#>       {
#>         "@type": "Periodical",
#>         "name": "Terapia psicológica",
#>         "issn": [
#>           "0718-4808"
#>         ]
#>       }
#>     ],
#>     "hasPart": [],
#>     "predecessor_of": [],
#>     "successor_of": [],
#>     "citation": [],
#>     "publisher": {
#>       "@type": "Organization",
#>       "name": "SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)"
#>     },
#>     "funding": []
#>   }
#> ] 
schema_org_writer(w, pretty = FALSE)
#> [{"@context":"https://schema.org","@type":"BlogPosting","@id":"https://doi.org/10.5438/4k3m-nyvg","identifier":{"@type":"PropertyValue","propertyID":"doi","value":"https://doi.org/10.5438/4k3m-nyvg"},"name":"Eating your own Dog Food","author":[{"@type":"Person","name":"Martin Fenner","givenName":"Martin","familyName":"Fenner"}],"editor":[],"description":"Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...","keywords":"Phylogeny, Malaria, Parasites, Taxonomy, Mitochondrial genome, Africa, Plasmodium","datePublished":"2016-12-20","sameAs":[],"isPartOf":[{"@type":"Periodical","name":"DataCite Blog"}],"hasPart":[],"predecessor_of":[],"successor_of":[],"citation":[],"publisher":{"@type":"Organization","name":"DataCite"},"funding":[]},{"@type":"ScholarlyArticle","identifier":{"@type":"PropertyValue","propertyID":"url","value":{}},"name":"Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)","author":[{"sequence":"first","affiliation":[],"@type":"Person","name":"Karen L Juillerat","givenName":"Karen L","familyName":"Juillerat"},{"sequence":"additional","affiliation":[],"@type":"Person","name":"Felipe A Cornejo","givenName":"Felipe A","familyName":"Cornejo"},{"sequence":"additional","affiliation":[],"@type":"Person","name":"Ramón D Castillo","givenName":"Ramón D","familyName":"Castillo"},{"sequence":"additional","affiliation":[],"@type":"Person","name":"Sergio E Chaigneau","givenName":"Sergio E","familyName":"Chaigneau"}],"editor":[],"datePublished":"2015-12","pageStart":"221","pageEnd":"238","sameAs":[],"isPartOf":[{"@type":"Periodical","name":"Terapia psicológica","issn":["0718-4808"]}],"hasPart":[],"predecessor_of":[],"successor_of":[],"citation":[],"publisher":{"@type":"Organization","name":"SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)"},"funding":[]}] 
```
