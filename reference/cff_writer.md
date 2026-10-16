# Citation File Format (cff) writer

Citation File Format (cff) writer

## Usage

``` r
cff_writer(
  z,
  path = NULL,
  message = "Please cite the following works when using this software."
)
```

## Arguments

- z:

  an object of class `handl`; see
  [handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

- path:

  a file path or connection; default:
  [`stdout()`](https://rdrr.io/r/base/showConnections.html)

- message:

  a message to display. Defaults to
  `"Please cite the following works when using this software."`

## Value

text if one cff citation or list of many

## Details

uses
[`yaml::write_yaml`](https://yaml.r-lib.org/reference/write_yaml.html)
to write to yaml format that CFF uses

## Converting to CFF from other formats

CFF has required fields that can't be missing. This means that
converting from other citation types to CFF will likely require adding
the required CFF fields manually. Adding fields to a `handl` object is
easy: it's really just an R list so add named elements to it. The
required CFF fields are:

- CFF **v1.1.0**:

  - cff-version: add `cff_version`

  - message: add `message`

  - version: add `software_version`

  - title: add `title`

  - authors: add `author`

  - date-released: add `date_published`

- CFF **v1.2.0**:

  - Only fields `cff-version`, `message`, `title` and `authors` are
    required.

If `cff_version` is not provided, the value by default is "1.2.0".

## References

CFF format: https://github.com/citation-file-format/citation-file-format

## See also

Other writers:
[`bibtex_writer()`](https://docs.ropensci.org/handlr/reference/bibtex_writer.md),
[`citeproc_writer()`](https://docs.ropensci.org/handlr/reference/citeproc_writer.md),
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md),
[`rdf_xml_writer()`](https://docs.ropensci.org/handlr/reference/rdf_xml_writer.md),
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md),
[`schema_org_writer()`](https://docs.ropensci.org/handlr/reference/schema_org_writer.md)

Other cff:
[`cff_reader()`](https://docs.ropensci.org/handlr/reference/cff_reader.md)

## Examples

``` r
(z <- system.file('extdata/citation.cff', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation.cff"
res <- cff_reader(x = z)
res
#> <handl> 
#>   from: cff
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5281/zenodo.1234
unclass(res)
#> $cff_version
#> [1] "1.1.0"
#> 
#> $message
#> [1] "If you use this software, please cite it as below."
#> 
#> $id
#> [1] "https://doi.org/10.5281/zenodo.1234"
#> 
#> $type
#> [1] "SoftwareSourceCode"
#> 
#> $citeproc_type
#> [1] "article-journal"
#> 
#> $bibtex_type
#> [1] "misc"
#> 
#> $ris_type
#> [1] "COMP"
#> 
#> $resource_type_general
#> [1] "Software"
#> 
#> $identifier
#> [1] "10.5281/zenodo.1234"
#> 
#> $doi
#> [1] "10.5281/zenodo.1234"
#> 
#> $b_url
#> NULL
#> 
#> $title
#> [1] "My Research Software"
#> 
#> $author
#> $author[[1]]
#> $author[[1]]$type
#> [1] "Person"
#> 
#> $author[[1]]$name
#> [1] "Stephan Druskat"
#> 
#> $author[[1]]$givenName
#> [1] "Stephan"
#> 
#> $author[[1]]$familyName
#> [1] "Druskat"
#> 
#> $author[[1]]$orcid
#> [1] "https://orcid.org/0000-0003-4925-7248"
#> 
#> 
#> 
#> $date_published
#> [1] "2017-12-18"
#> 
#> $software_version
#> [1] "2.0.4"
#> 
#> $description
#> $description$text
#> NULL
#> 
#> 
#> $license
#> $license$id
#> NULL
#> 
#> 
#> $keywords
#> [1] "McAuthor's algorithm" "linguistics"          "nlp"                 
#> [4] "parser"              
#> 
#> $state
#> [1] "findable"
#> 
#> $references
#> $references[[1]]
#> $references[[1]]$type
#> [1] "book"
#> 
#> $references[[1]]$authors
#> $references[[1]]$authors[[1]]
#> $references[[1]]$authors[[1]]$`family-names`
#> [1] "Doe"
#> 
#> $references[[1]]$authors[[1]]$`given-names`
#> [1] "Jane"
#> 
#> 
#> $references[[1]]$authors[[2]]
#> $references[[1]]$authors[[2]]$name
#> [1] "Foo Bar Working Group"
#> 
#> $references[[1]]$authors[[2]]$website
#> [1] "https://foo-bar.com"
#> 
#> 
#> 
#> $references[[1]]$title
#> [1] "The science of citation"
#> 
#> 
#> $references[[2]]
#> $references[[2]]$type
#> [1] "software"
#> 
#> $references[[2]]$authors
#> $references[[2]]$authors[[1]]
#> $references[[2]]$authors[[1]]$`family-names`
#> [1] "Doe"
#> 
#> $references[[2]]$authors[[1]]$`given-names`
#> [1] "John"
#> 
#> 
#> 
#> $references[[2]]$title
#> [1] "Software Citation Tool"
#> 
#> 
#> 
#> attr(,"from")
#> [1] "cff"
#> attr(,"source_type")
#> [1] "file"
#> attr(,"file")
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation.cff"
#> attr(,"many")
#> [1] FALSE
cff_writer(res)
#> [1] "cff-version: 1.1.0\nmessage: If you use this software, please cite it as below.\nversion: 2.0.4\ntitle: My Research Software\nauthors:\n- family-names: Druskat\n  given-names: Stephan\n  orcid: https://orcid.org/0000-0003-4925-7248\ndoi: 10.5281/zenodo.1234\ndate-released: '2017-12-18'\nkeywords:\n- McAuthor's algorithm\n- linguistics\n- nlp\n- parser\nreferences:\n- type: book\n  authors:\n  - family-names: Doe\n    given-names: Jane\n  - name: Foo Bar Working Group\n    website: https://foo-bar.com\n  title: The science of citation\n- type: software\n  authors:\n  - family-names: Doe\n    given-names: John\n  title: Software Citation Tool"
cat(cff_writer(res))
#> cff-version: 1.1.0
#> message: If you use this software, please cite it as below.
#> version: 2.0.4
#> title: My Research Software
#> authors:
#> - family-names: Druskat
#>   given-names: Stephan
#>   orcid: https://orcid.org/0000-0003-4925-7248
#> doi: 10.5281/zenodo.1234
#> date-released: '2017-12-18'
#> keywords:
#> - McAuthor's algorithm
#> - linguistics
#> - nlp
#> - parser
#> references:
#> - type: book
#>   authors:
#>   - family-names: Doe
#>     given-names: Jane
#>   - name: Foo Bar Working Group
#>     website: https://foo-bar.com
#>   title: The science of citation
#> - type: software
#>   authors:
#>   - family-names: Doe
#>     given-names: John
#>   title: Software Citation Tool
f <- tempfile()
cff_writer(res, f)
readLines(f)
#>  [1] "cff-version: 1.1.0"                                         
#>  [2] "message: If you use this software, please cite it as below."
#>  [3] "version: 2.0.4"                                             
#>  [4] "title: My Research Software"                                
#>  [5] "authors:"                                                   
#>  [6] "- family-names: Druskat"                                    
#>  [7] "  given-names: Stephan"                                     
#>  [8] "  orcid: https://orcid.org/0000-0003-4925-7248"             
#>  [9] "doi: 10.5281/zenodo.1234"                                   
#> [10] "date-released: '2017-12-18'"                                
#> [11] "keywords:"                                                  
#> [12] "- McAuthor's algorithm"                                     
#> [13] "- linguistics"                                              
#> [14] "- nlp"                                                      
#> [15] "- parser"                                                   
#> [16] "references:"                                                
#> [17] "- type: book"                                               
#> [18] "  authors:"                                                 
#> [19] "  - family-names: Doe"                                      
#> [20] "    given-names: Jane"                                      
#> [21] "  - name: Foo Bar Working Group"                            
#> [22] "    website: https://foo-bar.com"                           
#> [23] "  title: The science of citation"                           
#> [24] "- type: software"                                           
#> [25] "  authors:"                                                 
#> [26] "  - family-names: Doe"                                      
#> [27] "    given-names: John"                                      
#> [28] "  title: Software Citation Tool"                            
unlink(f)

# convert from a different citation format
## see "Converting to CFF from other formats" above
z <- system.file('extdata/citeproc.json', package = "handlr")
w <- citeproc_reader(x = z)
# cff_writer(w) # fails unless we add required fields
w$cff_version <- "1.1.0"
w$software_version <- "2.5"
w$title <- "A cool library"
w$date_published <- "2017-12-18"
cff_writer(w)
#> [1] "cff-version: 1.1.0\nmessage: Please cite the following works when using this software.\nversion: '2.5'\ntitle: A cool library\nauthors:\n- family-names: Fenner\n  given-names: Martin\ndoi: 10.5438/4k3m-nyvg\ndate-released: '2017-12-18'\nkeywords:\n- Phylogeny\n- Malaria\n- Parasites\n- Taxonomy\n- Mitochondrial genome\n- Africa\n- Plasmodium"
cat(cff_writer(w))
#> cff-version: 1.1.0
#> message: Please cite the following works when using this software.
#> version: '2.5'
#> title: A cool library
#> authors:
#> - family-names: Fenner
#>   given-names: Martin
#> doi: 10.5438/4k3m-nyvg
#> date-released: '2017-12-18'
#> keywords:
#> - Phylogeny
#> - Malaria
#> - Parasites
#> - Taxonomy
#> - Mitochondrial genome
#> - Africa
#> - Plasmodium
```
