# ris reader (Research Information Systems)

ris reader (Research Information Systems)

## Usage

``` r
ris_reader(x)
```

## Arguments

- x:

  (character) a file path or string

## Value

an object of class `handl`; see
[handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

## References

RIS tags https://en.wikipedia.org/wiki/RIS\_(file_format)

## See also

Other readers:
[`bibtex_reader()`](https://docs.ropensci.org/handlr/reference/bibtex_reader.md),
[`cff_reader()`](https://docs.ropensci.org/handlr/reference/cff_reader.md),
[`citeproc_reader()`](https://docs.ropensci.org/handlr/reference/citeproc_reader.md),
[`codemeta_reader()`](https://docs.ropensci.org/handlr/reference/codemeta_reader.md)

Other ris:
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md)

## Examples

``` r
z <- system.file('extdata/crossref.ris', package = "handlr")
ris_reader(z)
#> <handl> 
#>   from: ris
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.7554/elife.01567

z <- system.file('extdata/peerj.ris', package = "handlr")
ris_reader(z)
#> <handl> 
#>   from: ris
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.7717/peerj.5783

z <- system.file('extdata/plos.ris', package = "handlr")
ris_reader(z)
#> <handl> 
#>   from: ris
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.1371/journal.pone.0205444

# from a string
z <- system.file('extdata/crossref.ris', package = "handlr")
my_string <- ris_writer(ris_reader(z))
class(my_string)
#> [1] "character"
ris_reader(my_string)
#> <handl> 
#>   from: ris
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.7554/elife.01567

# many
z <- system.file('extdata/multiple-eg.ris', package = "handlr")
ris_reader(z)
#> <handl> 
#>   from: ris
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
#>     id/doi: https://doi.org/10.4067/s0718-48082015000300006
```
