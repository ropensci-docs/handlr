# codemeta writer

codemeta writer

## Usage

``` r
codemeta_writer(z, auto_unbox = TRUE, pretty = TRUE, ...)
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
[`rdf_xml_writer()`](https://docs.ropensci.org/handlr/reference/rdf_xml_writer.md),
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md),
[`schema_org_writer()`](https://docs.ropensci.org/handlr/reference/schema_org_writer.md)

Other codemeta:
[`codemeta_reader()`](https://docs.ropensci.org/handlr/reference/codemeta_reader.md)

## Examples

``` r
if (requireNamespace("bibtex", quietly=TRUE)) {
(x <- system.file('extdata/crossref.bib', package = "handlr"))
(z <- bibtex_reader(x))
codemeta_writer(z)
}
#> {
#>   "@context": ["https://purl.org/codemeta/2.0", "https://schema.org"],
#>   "@type": "article",
#>   "@id": "https://doi.org/10.7554/elife.01567",
#>   "identifier": "https://doi.org/10.7554/elife.01567",
#>   "codeRepository": "https://elifesciences.org/articles/01567",
#>   "title": "Automated quantitative histology reveals vascular morphodynamics during Arabidopsis hypocotyl secondary growth",
#>   "agents": [
#>     {
#>       "type": "Person",
#>       "name": "Martial Sankar",
#>       "givenName": "Martial",
#>       "familyName": "Sankar"
#>     },
#>     {
#>       "type": "Person",
#>       "name": "Kaisa Nieminen",
#>       "givenName": "Kaisa",
#>       "familyName": "Nieminen"
#>     },
#>     {
#>       "type": "Person",
#>       "name": "Laura Ragni",
#>       "givenName": "Laura",
#>       "familyName": "Ragni"
#>     },
#>     {
#>       "type": "Person",
#>       "name": "Ioannis Xenarios",
#>       "givenName": "Ioannis",
#>       "familyName": "Xenarios"
#>     },
#>     {
#>       "type": "Person",
#>       "name": "Christian S Hardtke",
#>       "givenName": "Christian S",
#>       "familyName": "Hardtke"
#>     }
#>   ],
#>   "description": "Among various advantages, their small size makes model organisms preferred subjects of investigation. Yet, even in model systems detailed analysis of numerous developmental processes at cellular level is severely hampered by their scale.",
#>   "publisher": "{eLife} Sciences Organisation, Ltd."
#> } 

# many citeproc to schema
z <- system.file('extdata/citeproc-many.json', package = "handlr")
w <- citeproc_reader(x = z)
codemeta_writer(w)
#> [
#>   {
#>     "@context": ["https://purl.org/codemeta/2.0", "https://schema.org"],
#>     "@type": "BlogPosting",
#>     "@id": "https://doi.org/10.5438/4k3m-nyvg",
#>     "identifier": "https://doi.org/10.5438/4k3m-nyvg",
#>     "title": "Eating your own Dog Food",
#>     "agents": [
#>       {
#>         "@type": "Person",
#>         "name": "Martin Fenner",
#>         "givenName": "Martin",
#>         "familyName": "Fenner"
#>       }
#>     ],
#>     "description": "Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...",
#>     "tags": ["Phylogeny", "Malaria", "Parasites", "Taxonomy", "Mitochondrial genome", "Africa", "Plasmodium"],
#>     "datePublished": "2016-12-20",
#>     "publisher": "DataCite"
#>   },
#>   {
#>     "@type": "ScholarlyArticle",
#>     "title": "Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)",
#>     "agents": [
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
#>     "datePublished": "2015-12",
#>     "publisher": "SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)"
#>   }
#> ] 
codemeta_writer(w, pretty = FALSE)
#> [{"@context":["https://purl.org/codemeta/2.0","https://schema.org"],"@type":"BlogPosting","@id":"https://doi.org/10.5438/4k3m-nyvg","identifier":"https://doi.org/10.5438/4k3m-nyvg","title":"Eating your own Dog Food","agents":[{"@type":"Person","name":"Martin Fenner","givenName":"Martin","familyName":"Fenner"}],"description":"Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...","tags":["Phylogeny","Malaria","Parasites","Taxonomy","Mitochondrial genome","Africa","Plasmodium"],"datePublished":"2016-12-20","publisher":"DataCite"},{"@type":"ScholarlyArticle","title":"Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)","agents":[{"sequence":"first","affiliation":[],"@type":"Person","name":"Karen L Juillerat","givenName":"Karen L","familyName":"Juillerat"},{"sequence":"additional","affiliation":[],"@type":"Person","name":"Felipe A Cornejo","givenName":"Felipe A","familyName":"Cornejo"},{"sequence":"additional","affiliation":[],"@type":"Person","name":"Ramón D Castillo","givenName":"Ramón D","familyName":"Castillo"},{"sequence":"additional","affiliation":[],"@type":"Person","name":"Sergio E Chaigneau","givenName":"Sergio E","familyName":"Chaigneau"}],"datePublished":"2015-12","publisher":"SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)"}] 
```
