# citeproc writer

citeproc writer

## Usage

``` r
citeproc_writer(z, auto_unbox = TRUE, pretty = TRUE, ...)
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

citeproc as JSON

## See also

Other writers:
[`bibtex_writer()`](https://docs.ropensci.org/handlr/reference/bibtex_writer.md),
[`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md),
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md),
[`rdf_xml_writer()`](https://docs.ropensci.org/handlr/reference/rdf_xml_writer.md),
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md),
[`schema_org_writer()`](https://docs.ropensci.org/handlr/reference/schema_org_writer.md)

Other citeproc:
[`citeproc_reader()`](https://docs.ropensci.org/handlr/reference/citeproc_reader.md)

## Examples

``` r
z <- system.file('extdata/citeproc.json', package = "handlr")
(tmp <- citeproc_reader(z))
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
citeproc_writer(z = tmp)
#> {
#>   "type": "post-weblog",
#>   "id": "https://doi.org/10.5438/4k3m-nyvg",
#>   "categories": [
#>     "Phylogeny",
#>     "Malaria",
#>     "Parasites",
#>     "Taxonomy",
#>     "Mitochondrial genome",
#>     "Africa",
#>     "Plasmodium"
#>   ],
#>   "language": {},
#>   "author": [
#>     {
#>       "name": "Martin Fenner",
#>       "family": "Fenner",
#>       "given": "Martin",
#>       "literal": "Fenner"
#>     }
#>   ],
#>   "editor": [],
#>   "issued": {
#>     "date-parts": ["2016", "12", "20"]
#>   },
#>   "submitted": {
#>     "date-parts": {}
#>   },
#>   "abstract": "Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...",
#>   "container-title": "DataCite Blog",
#>   "DOI": "10.5438/4k3m-nyvg",
#>   "issue": {
#>     "date-parts": [
#>       [
#>         2016,
#>         12,
#>         20
#>       ]
#>     ]
#>   },
#>   "page": [],
#>   "publisher": "DataCite",
#>   "title": "Eating your own Dog Food",
#>   "URL": "https://blog.datacite.org/eating-your-own-dog-food",
#>   "version": {},
#>   "volume": {}
#> } 
citeproc_writer(z = tmp, pretty = FALSE)
#> {"type":"post-weblog","id":"https://doi.org/10.5438/4k3m-nyvg","categories":["Phylogeny","Malaria","Parasites","Taxonomy","Mitochondrial genome","Africa","Plasmodium"],"language":{},"author":[{"name":"Martin Fenner","family":"Fenner","given":"Martin","literal":"Fenner"}],"editor":[],"issued":{"date-parts":["2016","12","20"]},"submitted":{"date-parts":{}},"abstract":"Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...","container-title":"DataCite Blog","DOI":"10.5438/4k3m-nyvg","issue":{"date-parts":[[2016,12,20]]},"page":[],"publisher":"DataCite","title":"Eating your own Dog Food","URL":"https://blog.datacite.org/eating-your-own-dog-food","version":{},"volume":{}} 
cat(ris_writer(z = tmp))
#> TY  - GEN
#> T1  - Eating your own Dog Food
#> T2  - DataCite Blog
#> AU  - FennerMartin
#> DO  - 10.5438/4k3m-nyvg
#> AB  - Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...
#> KW  - Phylogeny
#> KW  - Malaria
#> KW  - Parasites
#> KW  - Taxonomy
#> KW  - Mitochondrial genome
#> KW  - Africa
#> KW  - Plasmodium
#> PB  - DataCite
#> IS  - list(list(2016, 12, 20))
#> ER  - 

# many
z <- system.file('extdata/citeproc-many.json', package = "handlr")
w <- citeproc_reader(x = z)
citeproc_writer(w)
#> [
#>   {
#>     "type": "post-weblog",
#>     "id": "https://doi.org/10.5438/4k3m-nyvg",
#>     "categories": [
#>       "Phylogeny",
#>       "Malaria",
#>       "Parasites",
#>       "Taxonomy",
#>       "Mitochondrial genome",
#>       "Africa",
#>       "Plasmodium"
#>     ],
#>     "language": {},
#>     "author": [
#>       {
#>         "name": "Martin Fenner",
#>         "family": "Fenner",
#>         "given": "Martin",
#>         "literal": "Fenner"
#>       }
#>     ],
#>     "editor": [],
#>     "issued": {
#>       "date-parts": ["2016", "12", "20"]
#>     },
#>     "submitted": {
#>       "date-parts": {}
#>     },
#>     "abstract": "Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...",
#>     "container-title": "DataCite Blog",
#>     "DOI": "10.5438/4k3m-nyvg",
#>     "issue": {
#>       "date-parts": [
#>         [
#>           2016,
#>           12,
#>           20
#>         ]
#>       ]
#>     },
#>     "page": [],
#>     "publisher": "DataCite",
#>     "title": "Eating your own Dog Food",
#>     "URL": "https://blog.datacite.org/eating-your-own-dog-food",
#>     "version": {},
#>     "volume": {}
#>   },
#>   {
#>     "type": "article-journal",
#>     "id": {},
#>     "categories": [],
#>     "language": {},
#>     "author": [
#>       {
#>         "affiliation": [],
#>         "givenName": "Karen L",
#>         "familyName": "Juillerat",
#>         "family": "Juillerat",
#>         "literal": "Juillerat"
#>       },
#>       {
#>         "affiliation": [],
#>         "givenName": "Felipe A",
#>         "familyName": "Cornejo",
#>         "family": "Cornejo",
#>         "literal": "Cornejo"
#>       },
#>       {
#>         "affiliation": [],
#>         "givenName": "Ramón D",
#>         "familyName": "Castillo",
#>         "family": "Castillo",
#>         "literal": "Castillo"
#>       },
#>       {
#>         "affiliation": [],
#>         "givenName": "Sergio E",
#>         "familyName": "Chaigneau",
#>         "family": "Chaigneau",
#>         "literal": "Chaigneau"
#>       }
#>     ],
#>     "editor": [],
#>     "issued": {
#>       "date-parts": ["2015", "12", ""]
#>     },
#>     "submitted": {
#>       "date-parts": {}
#>     },
#>     "abstract": {},
#>     "container-title": "Terapia psicológica",
#>     "DOI": "10.4067/s0718-48082015000300006",
#>     "issue": "3",
#>     "page": "221-238",
#>     "publisher": "SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)",
#>     "title": "Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)",
#>     "URL": "https://doi.org/10.4067/s0718-48082015000300006",
#>     "version": {},
#>     "volume": "33"
#>   }
#> ] 
```
