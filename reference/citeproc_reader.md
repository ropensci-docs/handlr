# citeproc reader

citeproc reader

## Usage

``` r
citeproc_reader(x)
```

## Arguments

- x:

  (character) a file path or string

## Value

an object of class `handl`; see
[handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

## See also

Other readers:
[`bibtex_reader()`](https://docs.ropensci.org/handlr/reference/bibtex_reader.md),
[`cff_reader()`](https://docs.ropensci.org/handlr/reference/cff_reader.md),
[`codemeta_reader()`](https://docs.ropensci.org/handlr/reference/codemeta_reader.md),
[`ris_reader()`](https://docs.ropensci.org/handlr/reference/ris_reader.md)

Other citeproc:
[`citeproc_writer()`](https://docs.ropensci.org/handlr/reference/citeproc_writer.md)

## Examples

``` r
# single
z <- system.file('extdata/citeproc.json', package = "handlr")
citeproc_reader(x = z)
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
w <- system.file('extdata/citeproc2.json', package = "handlr")
citeproc_reader(x = w)
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: JolySilencetablemanners2008

# many
z <- system.file('extdata/citeproc-many.json', package = "handlr")
citeproc_reader(x = z)
#> <handl> 
#>   from: citeproc
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
#>     id/doi: 10.4067/s0718-48082015000300006
```
