# codemeta reader

codemeta reader

## Usage

``` r
codemeta_reader(x)
```

## Arguments

- x:

  (character) a file path or string (character or json)

## Value

an object of class `handl`; see
[handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

## See also

Other readers:
[`bibtex_reader()`](https://docs.ropensci.org/handlr/reference/bibtex_reader.md),
[`cff_reader()`](https://docs.ropensci.org/handlr/reference/cff_reader.md),
[`citeproc_reader()`](https://docs.ropensci.org/handlr/reference/citeproc_reader.md),
[`ris_reader()`](https://docs.ropensci.org/handlr/reference/ris_reader.md)

Other codemeta:
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md)

## Examples

``` r
# single
(z <- system.file('extdata/codemeta.json', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/codemeta.json"
codemeta_reader(x = z)
#> <handl> 
#>   from: codemeta
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5063/f1m61h5x

# many
(z <- system.file('extdata/codemeta-many.json', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/codemeta-many.json"
codemeta_reader(x = z)
#> <handl> 
#>   from: codemeta
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: https://doi.org/10.5063/f1m61h5x
#>     id/doi: https://doi.org/10.5063/f1m61h5x
```
