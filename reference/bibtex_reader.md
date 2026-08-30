# bibtex reader

bibtex reader

## Usage

``` r
bibtex_reader(x)
```

## Arguments

- x:

  (character) a file path or a bibtex string

## Value

an object of class `handl`; see
[handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

## Note

requires package `bibtex`, an optional package for handlr

## See also

Other readers:
[`cff_reader()`](https://docs.ropensci.org/handlr/reference/cff_reader.md),
[`citeproc_reader()`](https://docs.ropensci.org/handlr/reference/citeproc_reader.md),
[`codemeta_reader()`](https://docs.ropensci.org/handlr/reference/codemeta_reader.md),
[`ris_reader()`](https://docs.ropensci.org/handlr/reference/ris_reader.md)

Other bibtex:
[`bibtex_writer()`](https://docs.ropensci.org/handlr/reference/bibtex_writer.md)

## Examples

``` r
if (requireNamespace("bibtex", quietly=TRUE)) {
(z <- system.file('extdata/crossref.bib', package = "handlr"))
bibtex_reader(x = z)
(z <- system.file('extdata/bibtex.bib', package = "handlr"))
bibtex_reader(x = z)

# many at once 
(z <- system.file('extdata/bib-many.bib', package = "handlr"))
bibtex_reader(x = z)
}
#> <handl> 
#>   from: bibtex
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: 
```
