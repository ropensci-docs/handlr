# combine many handl objects

combine many handl objects

## Usage

``` r
# S3 method for class 'handl'
c(...)
```

## Arguments

- ...:

  one or more objects of class `handl`; see
  [handl](https://docs.ropensci.org/handlr/reference/handl.md) for more.
  all inputs must be of class `handl`. if the first input is not of
  class `handl`, you will not get back an object of class `handl`

## Value

an object of class `handl` of length equal to number of `handl` objects
passed in

## Examples

``` r
z <- system.file('extdata/crossref.ris', package = "handlr")
cr <- ris_reader(z)
z <- system.file('extdata/peerj.ris', package = "handlr")
prj <- ris_reader(z)
res <- c(cr, prj)
res
#> <handl> 
#>   from: ris,ris
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: https://doi.org/10.7554/elife.01567
#>     id/doi: https://doi.org/10.7717/peerj.5783
invisible(lapply(bibtex_writer(res), cat, sep = "\n\n"))
#> @misc{https://doi.org/10.7554/elife.01567,
#> 
#>   doi = {10.7554/elife.01567},
#> 
#>   url = {https://elifesciences.org/articles/01567},
#> 
#>   author = {{Sankar, Martial} and {Nieminen, Kaisa} and {Ragni, Laura} and {Xenarios, Ioannis} and {Hardtke, Christian S}},
#> 
#>   title = {Automated quantitative histology reveals vascular morphodynamics during Arabidopsis hypocotyl secondary growth},
#> 
#>   volume = {3},
#> 
#>   pages = {},
#> 
#>   year = {2014},
#> 
#> }
#> 
#> 
#> @misc{https://doi.org/10.7717/peerj.5783,
#> 
#>   doi = {10.7717/peerj.5783},
#> 
#>   url = {https://doi.org/10.7717/peerj.5783},
#> 
#>   author = {{Capa,María} and {Bakken,Torkild} and {Meißner,Karin} and {Nygren,Arne}},
#> 
#>   title = {Three, two, one! Revision of the long-bodied sphaerodorids (Sphaerodoridae, Annelida) and synonymization of Ephesiella, Ephesiopsis and Sphaerodorum},
#> 
#>   volume = {6},
#> 
#>   pages = {e5783--},
#> 
#>   year = {2018},
#> 
#> }
#> 
#> 
```
