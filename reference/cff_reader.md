# Citation File Format (cff) reader

Citation File Format (cff) reader

## Usage

``` r
cff_reader(x)
```

## Arguments

- x:

  (character) a file path or a yaml string

## Value

an object of class `handl`; see
[handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

## Details

CFF only supports one citation, so `many` will always be `FALSE`.

Required fields:

- CFF **v1.1.0**: `cff-version`, `version`, `message`, `date-released`,
  `title`, `authors`.

- CFF **v1.2.0**: `cff-version`, `message`, `title`, `authors`.

We'll stop with error if any of these are missing.

You can though have many references in your CFF file associated with the
citation. `references` is an optional component in cff files. If
included, we check the following:

- each reference must have the 3 required fields: type, authors, title

- type must be in the allowed set, see
  [cff_reference_types](https://docs.ropensci.org/handlr/reference/cff_reference_types.md)

- the elements within authors must each be an entity or person object
  https://github.com/citation-file-format/citation-file-format#entity-objects
  https://github.com/citation-file-format/citation-file-format#person-objects

- title must be a string

## References

CFF format: https://github.com/citation-file-format/citation-file-format

## See also

Other readers:
[`bibtex_reader()`](https://docs.ropensci.org/handlr/reference/bibtex_reader.md),
[`citeproc_reader()`](https://docs.ropensci.org/handlr/reference/citeproc_reader.md),
[`codemeta_reader()`](https://docs.ropensci.org/handlr/reference/codemeta_reader.md),
[`ris_reader()`](https://docs.ropensci.org/handlr/reference/ris_reader.md)

Other cff:
[`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md)

## Examples

``` r
(z <- system.file("extdata/citation.cff", package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation.cff"
res <- cff_reader(x = z)
res
#> <handl> 
#>   from: cff
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5281/zenodo.1234
res$cff_version
#> [1] "1.1.0"
res$software_version
#> [1] "2.0.4"
res$message
#> [1] "If you use this software, please cite it as below."
res$id
#> [1] "https://doi.org/10.5281/zenodo.1234"
res$doi
#> [1] "10.5281/zenodo.1234"
res$title
#> [1] "My Research Software"
res$author
#> [[1]]
#> [[1]]$type
#> [1] "Person"
#> 
#> [[1]]$name
#> [1] "Stephan Druskat"
#> 
#> [[1]]$givenName
#> [1] "Stephan"
#> 
#> [[1]]$familyName
#> [1] "Druskat"
#> 
#> [[1]]$orcid
#> [1] "https://orcid.org/0000-0003-4925-7248"
#> 
#> 
res$references
#> [[1]]
#> [[1]]$type
#> [1] "book"
#> 
#> [[1]]$authors
#> [[1]]$authors[[1]]
#> [[1]]$authors[[1]]$`family-names`
#> [1] "Doe"
#> 
#> [[1]]$authors[[1]]$`given-names`
#> [1] "Jane"
#> 
#> 
#> [[1]]$authors[[2]]
#> [[1]]$authors[[2]]$name
#> [1] "Foo Bar Working Group"
#> 
#> [[1]]$authors[[2]]$website
#> [1] "https://foo-bar.com"
#> 
#> 
#> 
#> [[1]]$title
#> [1] "The science of citation"
#> 
#> 
#> [[2]]
#> [[2]]$type
#> [1] "software"
#> 
#> [[2]]$authors
#> [[2]]$authors[[1]]
#> [[2]]$authors[[1]]$`family-names`
#> [1] "Doe"
#> 
#> [[2]]$authors[[1]]$`given-names`
#> [1] "John"
#> 
#> 
#> 
#> [[2]]$title
#> [1] "Software Citation Tool"
#> 
#> 

# no references
(z <- system.file("extdata/citation-norefs.cff", package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citation-norefs.cff"
out <- cff_reader(x = z)
out
#> <handl> 
#>   from: cff
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5281/zenodo.1234
out$references
#> NULL
```
