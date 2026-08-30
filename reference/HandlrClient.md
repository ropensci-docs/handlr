# HandlrClient

handlr client, read and write to and from all citation formats

## Details

The various inputs to the `x` parameter are handled in different ways:

- file: contents read from file, we grab file extension, and we guess
  format based on combination of contents and file extension because
  file extensions may belie what's in the file

- string: string read in, and we guess format based on contents of the
  string

- DOI: we request citeproc-json format from the Crossref API

- DOI url: we request citeproc-json format from the Crossref API

## Note

If `$parsed` is `NULL` then it's likely `$read()` has not been run - in
which case we attempt to run `$read()` to populate `$parsed`

## Public fields

- `path`:

  (character) non-empty if file path passed to initialize

- `string`:

  (character) non-empty if string (non-file) passed to initialize

- `parsed`:

  after `read()` is run, the parsed content

- `file`:

  (logical) `TRUE` if a file passed to initialize, else `FALSE`

- `ext`:

  (character) the file extension

- `format_guessed`:

  (character) the guessed file format

- `doi`:

  (character) the DOI, if any found

## Methods

### Public methods

- [`HandlrClient$print()`](#method-HandlrClient-print)

- [`HandlrClient$new()`](#method-HandlrClient-new)

- [`HandlrClient$read()`](#method-HandlrClient-read)

- [`HandlrClient$write()`](#method-HandlrClient-write)

- [`HandlrClient$as_df()`](#method-HandlrClient-as_df)

- [`HandlrClient$clone()`](#method-HandlrClient-clone)

------------------------------------------------------------------------

### Method [`print()`](https://rdrr.io/r/base/print.html)

print method for `HandlrClient` objects

#### Usage

    HandlrClient$print(x, ...)

#### Arguments

- `x`:

  self

- `...`:

  ignored

------------------------------------------------------------------------

### Method `new()`

Create a new `HandlrClient` object

#### Usage

    HandlrClient$new(x, format = NULL, ...)

#### Arguments

- `x`:

  (character) a file path (the file must exist), a string containing
  contents of the citation, a DOI, or a DOI as a URL. See Details.

- `format`:

  (character) one of citeproc, ris, bibtex, codemeta, cff, or `NULL`. If
  `NULL`, we attempt to guess the format, and error if we can not guess

- `...`:

  curl options passed on to
  [crul::verb-GET](https://docs.ropensci.org/crul/reference/verb-GET.html)

#### Returns

A new `HandlrClient` object

------------------------------------------------------------------------

### Method `read()`

read input

#### Usage

    HandlrClient$read(format = NULL, ...)

#### Arguments

- `format`:

  (character) one of citeproc, ris, bibtex, codemeta, cff, or `NULL`. If
  `NULL`, we attempt to guess the format, and error if we can not guess

- `...`:

  further args to the writer fxn, if any

------------------------------------------------------------------------

### Method [`write()`](https://rdrr.io/r/base/write.html)

write to std out or file

#### Usage

    HandlrClient$write(format, file = NULL, ...)

#### Arguments

- `format`:

  (character) one of citeproc, ris, bibtex, schema_org, rdfxml,
  codemeta, or cff

- `file`:

  a file path, if NULL to stdout. for `format=ris`, number of files must
  equal number of ris citations

- `...`:

  further args to the writer fxn, if any

------------------------------------------------------------------------

### Method `as_df()`

convert data to a data.frame using
[`handl_to_df()`](https://docs.ropensci.org/handlr/reference/handl_to_df.md)

#### Usage

    HandlrClient$as_df()

#### Returns

a data.frame

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    HandlrClient$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.

## Examples

``` r
# read() can be run with format specified or not
# if format not given, we attempt to guess the format and then read
z <- system.file('extdata/citeproc.json', package = "handlr")
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: json
#>   format (guessed): citeproc
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citeproc.json
#>   string (abbrev.): none
x$read()
x$read("citeproc")
x$parsed
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg

# you can run read() then write()
# or just run write(), and read() will be run for you if possible
z <- system.file('extdata/citeproc.json', package = "handlr")
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: json
#>   format (guessed): citeproc
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citeproc.json
#>   string (abbrev.): none
cat(x$write("ris"))
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

# read from a DOI as a url
if (interactive()) {
  (x <- HandlrClient$new('https://doi.org/10.7554/elife.01567'))
  x$parsed
  x$read()
  x$parsed
  x$write('bibtex')
}

# read from a DOI
if (interactive()) {
  (x <- HandlrClient$new('10.7554/elife.01567'))
  x$parsed
  x$read()
  x$write('bibtex')
}

# read in citeproc, write out bibtex
z <- system.file('extdata/citeproc.json', package = "handlr")
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: json
#>   format (guessed): citeproc
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citeproc.json
#>   string (abbrev.): none
x$path
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citeproc.json"
x$ext
#> [1] "json"
x$read("citeproc")
x$parsed
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
x$write("bibtex")
#>  [1] "@article{https://doi.org/10.5438/4k3m-nyvg,"
#>  [2] "  doi = {10.5438/4k3m-nyvg},"               
#>  [3] "  author = {Martin Fenner},"                
#>  [4] "  title = {Eating your own Dog Food},"      
#>  [5] "  journal = {DataCite Blog},"               
#>  [6] "  pages = {},"                              
#>  [7] "  publisher = {DataCite},"                  
#>  [8] "  year = {2016},"                           
#>  [9] "}"                                          
#> [10] ""                                           
f <- tempfile(fileext = ".bib")
x$write("bibtex", file = f)
readLines(f)
#>  [1] "@article{https://doi.org/10.5438/4k3m-nyvg,"
#>  [2] "  doi = {10.5438/4k3m-nyvg},"               
#>  [3] "  author = {Martin Fenner},"                
#>  [4] "  title = {Eating your own Dog Food},"      
#>  [5] "  journal = {DataCite Blog},"               
#>  [6] "  pages = {},"                              
#>  [7] "  publisher = {DataCite},"                  
#>  [8] "  year = {2016},"                           
#>  [9] "}"                                          
#> [10] ""                                           
unlink(f)

# read in ris, write out ris
z <- system.file('extdata/peerj.ris', package = "handlr")
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: ris
#>   format (guessed): ris
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/peerj.ris
#>   string (abbrev.): none
x$path
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/peerj.ris"
x$format_guessed
#> [1] "ris"
x$read("ris")
x$parsed
#> <handl> 
#>   from: ris
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.7717/peerj.5783
x$write("ris")
#> [1] "TY  - JOUR\r\nT1  - Three, two, one! Revision of the long-bodied sphaerodorids (Sphaerodoridae, Annelida) and synonymization of Ephesiella, Ephesiopsis and Sphaerodorum\r\nAU  - Capa,María\r\nAU  - Bakken,Torkild\r\nAU  - Meißner,Karin\r\nAU  - Nygren,Arne\r\nDO  - 10.7717/peerj.5783\r\nUR  - https://doi.org/10.7717/peerj.5783\r\nAB  - Background                Long-bodied sphaerodorids (Annelida, Sphaerodoridae) is the common name for members of the three closely and morphologically homogenous currently accepted genera of benthic marine bristle worms: Ephesiella, Ephesiopsis and Sphaerodorum. Members of this group share the presence of two dorsal and longitudinal rows of macrotubercles with terminal papillae, and two longitudinal rows of microtubercles, features that are unique among sphaerodorids. Genera are distinguished by the chaetae morphology. Members of Ephesiella are characterised by having compound chaetae (except, sometimes, simple chaetae in the first chaetigers), Sphaerodorum bear only simple chaetae, and Ephesiopsis have both compound and simple chaetae in all parapodia.                                          Methods                Mitochondrial (partial COI and 16S rDNA) and nuclear (partial 18S rDNA and 28S rDNA) sequence data of long-bodied sphaerodorids with compound and simple chaetae, and an outgroup of additional seven sphaerodorid species were analysed separately and in combination using Bayesian inference (BA), and Maximum Likelihood (ML) methods. Long-bodied sphaerodorids from around the world (including type specimens) were examined under a range of optical equipment in order to evaluate putative generic and specific diagnostic features, in addition to intraspecific variability.                                          Results                Phylogenetic analyses of mitochondrial and nuclear DNA sequences of specimens identified as Ephesiella and Sphaerodorum, based on chaeta morphology, were performed. Sphaerodorum and Ephesiella were recovered as paraphyletic and nested within each other. Revision of current nominal species diagnostic features are performed and discussed.                                          Discussion                Results contradict current generic definitions. Recovery of paraphyletic compound and simple chaetae clades urge the synonymization of these two genera of long-bodied sphaerodorids. Morphological data also suggest the synonymization of Ephesiopsis.\r\nKW  - Diagnostic features\r\nKW  - Polychaetes\r\nKW  - Morphology\r\nKW  - Molecular phylogeny\r\nKW  - Reciprocal monophyly\r\nKW  - Systematics\r\nKW  - Classification\r\nKW  - Genera synonimization\r\nJO  - PeerJ\r\nVL  - 6\r\nSP  - e5783\r\nSN  - 2167-8359\r\nER  - "
cat(x$write("ris"))
#> TY  - JOUR
#> T1  - Three, two, one! Revision of the long-bodied sphaerodorids (Sphaerodoridae, Annelida) and synonymization of Ephesiella, Ephesiopsis and Sphaerodorum
#> AU  - Capa,María
#> AU  - Bakken,Torkild
#> AU  - Meißner,Karin
#> AU  - Nygren,Arne
#> DO  - 10.7717/peerj.5783
#> UR  - https://doi.org/10.7717/peerj.5783
#> AB  - Background                Long-bodied sphaerodorids (Annelida, Sphaerodoridae) is the common name for members of the three closely and morphologically homogenous currently accepted genera of benthic marine bristle worms: Ephesiella, Ephesiopsis and Sphaerodorum. Members of this group share the presence of two dorsal and longitudinal rows of macrotubercles with terminal papillae, and two longitudinal rows of microtubercles, features that are unique among sphaerodorids. Genera are distinguished by the chaetae morphology. Members of Ephesiella are characterised by having compound chaetae (except, sometimes, simple chaetae in the first chaetigers), Sphaerodorum bear only simple chaetae, and Ephesiopsis have both compound and simple chaetae in all parapodia.                                          Methods                Mitochondrial (partial COI and 16S rDNA) and nuclear (partial 18S rDNA and 28S rDNA) sequence data of long-bodied sphaerodorids with compound and simple chaetae, and an outgroup of additional seven sphaerodorid species were analysed separately and in combination using Bayesian inference (BA), and Maximum Likelihood (ML) methods. Long-bodied sphaerodorids from around the world (including type specimens) were examined under a range of optical equipment in order to evaluate putative generic and specific diagnostic features, in addition to intraspecific variability.                                          Results                Phylogenetic analyses of mitochondrial and nuclear DNA sequences of specimens identified as Ephesiella and Sphaerodorum, based on chaeta morphology, were performed. Sphaerodorum and Ephesiella were recovered as paraphyletic and nested within each other. Revision of current nominal species diagnostic features are performed and discussed.                                          Discussion                Results contradict current generic definitions. Recovery of paraphyletic compound and simple chaetae clades urge the synonymization of these two genera of long-bodied sphaerodorids. Morphological data also suggest the synonymization of Ephesiopsis.
#> KW  - Diagnostic features
#> KW  - Polychaetes
#> KW  - Morphology
#> KW  - Molecular phylogeny
#> KW  - Reciprocal monophyly
#> KW  - Systematics
#> KW  - Classification
#> KW  - Genera synonimization
#> JO  - PeerJ
#> VL  - 6
#> SP  - e5783
#> SN  - 2167-8359
#> ER  - 

# read in bibtex, write out ris
(z <- system.file('extdata/bibtex.bib', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/bibtex.bib"
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: bib
#>   format (guessed): bibtex
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/bibtex.bib
#>   string (abbrev.): none
x$path
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/bibtex.bib"
x$format_guessed
#> [1] "bibtex"
if (requireNamespace("bibtex", quietly = TRUE)) {
x$read("bibtex")
x$parsed
x$write("ris")
cat(x$write("ris"))
}
#> TY  - JOUR
#> T1  - {THE} {INTENSIFICATION} {OF} {INNOVATION}
#> AU  - DODGSONMARK
#> AU  - GANNDAVID M.
#> AU  - SALTERAMMON. J
#> DO  - 10.1142/s1363919602000495
#> UR  - https://doi.org/10.1142%2Fs1363919602000495
#> PB  - World Scientific Pub Co Pte Lt
#> VL  - 06
#> SP  - 53
#> EP  - 83
#> ER  - 

# read in bibtex, write out RDF XML
if (requireNamespace("bibtex", quietly = TRUE) && interactive()) {
  (z <- system.file('extdata/bibtex.bib', package = "handlr"))
  (x <- HandlrClient$new(x = z))
  x$path
  x$format_guessed
  x$read("bibtex")
  x$parsed
  x$write("rdfxml")
  cat(x$write("rdfxml"))
}

# codemeta
(z <- system.file('extdata/codemeta.json', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/codemeta.json"
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: json
#>   format (guessed): codemeta
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/codemeta.json
#>   string (abbrev.): none
x$path
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/codemeta.json"
x$format_guessed
#> [1] "codemeta"
x$read("codemeta")
x$parsed
#> <handl> 
#>   from: codemeta
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5063/f1m61h5x
x$write("codemeta")
#> {
#>   "@context": ["https://purl.org/codemeta/2.0", "https://schema.org"],
#>   "@type": "SoftwareSourceCode",
#>   "@id": "https://doi.org/10.5063/f1m61h5x",
#>   "identifier": "https://doi.org/10.5063/f1m61h5x",
#>   "codeRepository": "https://github.com/DataONEorg/rdataone",
#>   "title": "R Interface to the DataONE REST API",
#>   "agents": [],
#>   "description": "Provides read and write access to data and metadata from the DataONE network of data repositories.Each DataONE repository implements a consistent repository application programming interface. Users call methods in R to access these remote repository functions, such as methods to query the metadata catalog, get access to metadata for particular data packages, and read the data objects from the data repository.Users can also insert and update data objects on repositories that support these methods.",
#>   "version": "2.0.0",
#>   "tags": ["data sharing", "data repository", "DataONE"],
#>   "dateCreated": "2016-05-27",
#>   "datePublished": "2016-05-27",
#>   "dateModified": "2016-05-27",
#>   "publisher": "https://cran.r-project.org"
#> } 

# cff: Citation File Format
(z <- system.file('extdata/citation.cff', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation.cff"
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: cff
#>   format (guessed): cff
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation.cff
#>   string (abbrev.): none
x$path
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation.cff"
x$format_guessed
#> [1] "cff"
x$read("cff")
x$parsed
#> <handl> 
#>   from: cff
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5281/zenodo.1234
x$write("codemeta")
#> {
#>   "@context": ["https://purl.org/codemeta/2.0", "https://schema.org"],
#>   "@type": "SoftwareSourceCode",
#>   "@id": "https://doi.org/10.5281/zenodo.1234",
#>   "identifier": "https://doi.org/10.5281/zenodo.1234",
#>   "title": "My Research Software",
#>   "agents": [
#>     {
#>       "type": "Person",
#>       "name": "Stephan Druskat",
#>       "givenName": "Stephan",
#>       "familyName": "Druskat",
#>       "orcid": "https://orcid.org/0000-0003-4925-7248"
#>     }
#>   ],
#>   "version": "2.0.4",
#>   "tags": ["McAuthor's algorithm", "linguistics", "nlp", "parser"],
#>   "datePublished": "2017-12-18"
#> } 

# > 1 citation
z <- system.file('extdata/citeproc-many.json', package = "handlr")
(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: json
#>   format (guessed): citeproc
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citeproc-many.json
#>   string (abbrev.): none
x$parsed
#> NULL
x$read()
x$parsed
#> <handl> 
#>   from: citeproc
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
#>     id/doi: 10.4067/s0718-48082015000300006
## schmea org
x$write("schema_org")
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
## bibtex
x$write("bibtex")
#> [[1]]
#>  [1] "@article{https://doi.org/10.5438/4k3m-nyvg,"
#>  [2] "  doi = {10.5438/4k3m-nyvg},"               
#>  [3] "  author = {Martin Fenner},"                
#>  [4] "  title = {Eating your own Dog Food},"      
#>  [5] "  journal = {DataCite Blog},"               
#>  [6] "  pages = {},"                              
#>  [7] "  publisher = {DataCite},"                  
#>  [8] "  year = {2016},"                           
#>  [9] "}"                                          
#> [10] ""                                           
#> 
#> [[2]]
#>  [1] "@article{10.4067/s0718-48082015000300006,"                                                                                                                              
#>  [2] "  doi = {10.4067/s0718-48082015000300006},"                                                                                                                             
#>  [3] "  author = {Karen L Juillerat and Felipe A Cornejo and Ramón D Castillo and Sergio E Chaigneau},"                                                                       
#>  [4] "  title = {Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)},"
#>  [5] "  journal = {Terapia psicológica},"                                                                                                                                     
#>  [6] "  volume = {33},"                                                                                                                                                       
#>  [7] "  pages = {221--238},"                                                                                                                                                  
#>  [8] "  publisher = {SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)},"                                                                          
#>  [9] "  year = {2015},"                                                                                                                                                       
#> [10] "}"                                                                                                                                                                      
#> [11] ""                                                                                                                                                                       
#> 
## bibtex to file
f <- tempfile(fileext=".bib")
x$write("bibtex", f)
readLines(f)
#>  [1] "@article{https://doi.org/10.5438/4k3m-nyvg,"                                                                                                                            
#>  [2] "  doi = {10.5438/4k3m-nyvg},"                                                                                                                                           
#>  [3] "  author = {Martin Fenner},"                                                                                                                                            
#>  [4] "  title = {Eating your own Dog Food},"                                                                                                                                  
#>  [5] "  journal = {DataCite Blog},"                                                                                                                                           
#>  [6] "  pages = {},"                                                                                                                                                          
#>  [7] "  publisher = {DataCite},"                                                                                                                                              
#>  [8] "  year = {2016},"                                                                                                                                                       
#>  [9] "}"                                                                                                                                                                      
#> [10] ""                                                                                                                                                                       
#> [11] "@article{10.4067/s0718-48082015000300006,"                                                                                                                              
#> [12] "  doi = {10.4067/s0718-48082015000300006},"                                                                                                                             
#> [13] "  author = {Karen L Juillerat and Felipe A Cornejo and Ramón D Castillo and Sergio E Chaigneau},"                                                                       
#> [14] "  title = {Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)},"
#> [15] "  journal = {Terapia psicológica},"                                                                                                                                     
#> [16] "  volume = {33},"                                                                                                                                                       
#> [17] "  pages = {221--238},"                                                                                                                                                  
#> [18] "  publisher = {SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)},"                                                                          
#> [19] "  year = {2015},"                                                                                                                                                       
#> [20] "}"                                                                                                                                                                      
#> [21] ""                                                                                                                                                                       
unlink(f)
## to RIS
x$write("ris")
#> [1] "TY  - GEN\r\nT1  - Eating your own Dog Food\r\nT2  - DataCite Blog\r\nAU  - FennerMartin\r\nDO  - 10.5438/4k3m-nyvg\r\nAB  - Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...\r\nKW  - Phylogeny\r\nKW  - Malaria\r\nKW  - Parasites\r\nKW  - Taxonomy\r\nKW  - Mitochondrial genome\r\nKW  - Africa\r\nKW  - Plasmodium\r\nPB  - DataCite\r\nIS  - list(list(2016, 12, 20))\r\nER  - "
#> [2] "TY  - GEN\r\nT1  - Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)\r\nT2  - Terapia psicológica\r\nAU  - JuilleratKaren L\r\nAU  - CornejoFelipe A\r\nAU  - CastilloRamón D\r\nAU  - ChaigneauSergio E\r\nDO  - 10.4067/s0718-48082015000300006\r\nPB  - SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)\r\nVL  - 33\r\nIS  - 3\r\nSP  - 221\r\nEP  - 238\r\nSN  - 0718-4808\r\nER  - "                                                                     
### only one per file, so not combined
files <- replicate(2, tempfile(fileext=".ris"))
x$write("ris", files)
lapply(files, readLines)
#> [[1]]
#>  [1] "TY  - GEN"                                                                                                                                                                                                                                                          
#>  [2] "T1  - Eating your own Dog Food"                                                                                                                                                                                                                                     
#>  [3] "T2  - DataCite Blog"                                                                                                                                                                                                                                                
#>  [4] "AU  - FennerMartin"                                                                                                                                                                                                                                                 
#>  [5] "DO  - 10.5438/4k3m-nyvg"                                                                                                                                                                                                                                            
#>  [6] "AB  - Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for..."
#>  [7] "KW  - Phylogeny"                                                                                                                                                                                                                                                    
#>  [8] "KW  - Malaria"                                                                                                                                                                                                                                                      
#>  [9] "KW  - Parasites"                                                                                                                                                                                                                                                    
#> [10] "KW  - Taxonomy"                                                                                                                                                                                                                                                     
#> [11] "KW  - Mitochondrial genome"                                                                                                                                                                                                                                         
#> [12] "KW  - Africa"                                                                                                                                                                                                                                                       
#> [13] "KW  - Plasmodium"                                                                                                                                                                                                                                                   
#> [14] "PB  - DataCite"                                                                                                                                                                                                                                                     
#> [15] "IS  - list(list(2016, 12, 20))"                                                                                                                                                                                                                                     
#> [16] "ER  - "                                                                                                                                                                                                                                                             
#> 
#> [[2]]
#>  [1] "TY  - GEN"                                                                                                                                                       
#>  [2] "T1  - Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)"
#>  [3] "T2  - Terapia psicológica"                                                                                                                                       
#>  [4] "AU  - JuilleratKaren L"                                                                                                                                          
#>  [5] "AU  - CornejoFelipe A"                                                                                                                                           
#>  [6] "AU  - CastilloRamón D"                                                                                                                                           
#>  [7] "AU  - ChaigneauSergio E"                                                                                                                                         
#>  [8] "DO  - 10.4067/s0718-48082015000300006"                                                                                                                           
#>  [9] "PB  - SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)"                                                                              
#> [10] "VL  - 33"                                                                                                                                                        
#> [11] "IS  - 3"                                                                                                                                                         
#> [12] "SP  - 221"                                                                                                                                                       
#> [13] "EP  - 238"                                                                                                                                                       
#> [14] "SN  - 0718-4808"                                                                                                                                                 
#> [15] "ER  - "                                                                                                                                                          
#> 

# handle strings instead of files
z <- system.file('extdata/citeproc-crossref.json', package = "handlr")
(x <- HandlrClient$new(x = readLines(z)))
#> <handlr> 
#>   doi: 
#>   ext: 
#>   format (guessed): citeproc
#>   path: none
#>   string (abbrev.): {"indexed":{"date-parts":[[2018,5,8]],"date-time":"2018-05-08T02:36:58Z","timest
x$read("citeproc")
x$parsed
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: 10.4067/s0718-48082015000300006
cat(x$write("bibtex"), sep = "\n")
#> @article{10.4067/s0718-48082015000300006,
#>   doi = {10.4067/s0718-48082015000300006},
#>   author = {Karen L Juillerat and Felipe A Cornejo and Ramón D Castillo and Sergio E Chaigneau},
#>   title = {Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)},
#>   journal = {Terapia psicológica},
#>   volume = {33},
#>   pages = {221--238},
#>   publisher = {SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)},
#>   year = {2015},
#> }
#> 
```
