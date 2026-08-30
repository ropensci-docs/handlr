# bibtex writer

bibtex writer

## Usage

``` r
bibtex_writer(z, key = NULL)
```

## Arguments

- z:

  an object of class `handl`; see
  [handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

- key:

  (character) optional bibtex key to use. if `NULL` we attempt try the
  following fields in order: `key`, `identifier`, `id`, `doi`. if you
  pass in ouput from
  [`bibtex_reader()`](https://docs.ropensci.org/handlr/reference/bibtex_reader.md)
  you're likely to have a `key` field, but otherwise probably not

## Value

an object of class `BibEntry`

## See also

Other writers:
[`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md),
[`citeproc_writer()`](https://docs.ropensci.org/handlr/reference/citeproc_writer.md),
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md),
[`rdf_xml_writer()`](https://docs.ropensci.org/handlr/reference/rdf_xml_writer.md),
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md),
[`schema_org_writer()`](https://docs.ropensci.org/handlr/reference/schema_org_writer.md)

Other bibtex:
[`bibtex_reader()`](https://docs.ropensci.org/handlr/reference/bibtex_reader.md)

## Examples

``` r
(z <- system.file('extdata/citeproc.json', package = "handlr"))
#> [1] "/github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/citeproc.json"
(tmp <- citeproc_reader(z))
#> <handl> 
#>   from: citeproc
#>   many: FALSE
#>   count: 1
#>   first 10 
#>     id/doi: https://doi.org/10.5438/4k3m-nyvg
bibtex_writer(z = tmp)
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
cat(bibtex_writer(z = tmp), sep = "\n")
#> @article{https://doi.org/10.5438/4k3m-nyvg,
#>   doi = {10.5438/4k3m-nyvg},
#>   author = {Martin Fenner},
#>   title = {Eating your own Dog Food},
#>   journal = {DataCite Blog},
#>   pages = {},
#>   publisher = {DataCite},
#>   year = {2016},
#> }
#> 

# give a bibtex key
cat(bibtex_writer(tmp, "foobar89"), sep = "\n")
#> @article{foobar89,
#>   doi = {10.5438/4k3m-nyvg},
#>   author = {Martin Fenner},
#>   title = {Eating your own Dog Food},
#>   journal = {DataCite Blog},
#>   pages = {},
#>   publisher = {DataCite},
#>   year = {2016},
#> }
#> 

# many at once
if (requireNamespace("bibtex", quietly=TRUE)) {
(z <- system.file('extdata/bib-many.bib', package = "handlr"))
out <- bibtex_reader(x = z)
bibtex_writer(out)
}
#> $Amano_2016
#>  [1] "@article{Amano_2016,"                                                                        
#>  [2] "  doi = {10.1093/biosci/biw022},"                                                            
#>  [3] "  url = {https://doi.org/10.1093/biosci/biw022},"                                            
#>  [4] "  author = {Tatsuya Amano and James D. L. Lamming and William J. Sutherland},"               
#>  [5] "  title = {Spatial Gaps in Global Biodiversity Information and the Role of Citizen Science},"
#>  [6] "  volume = {66},"                                                                            
#>  [7] "  pages = {393--400},"                                                                       
#>  [8] "  publisher = {Oxford University Press ({OUP})},"                                            
#>  [9] "}"                                                                                           
#> [10] ""                                                                                            
#> 
#> $Bachelot_2016
#> [1] "@article{Bachelot_2016,"                                                                                                                                                 
#> [2] "  doi = {10.1890/15-1397.1},"                                                                                                                                            
#> [3] "  url = {https://doi.org/10.1890/15-1397.1},"                                                                                                                            
#> [4] "  author = {Benedicte Bachelot and Mar\\'\\ia Uriarte and Jess K. Zimmerman and Jill Thompson and Jonathan W. Leff and Ava Asiaii and Jenny Koshner and Krista McGuire},"
#> [5] "  title = {Long-lasting effects of land use history on soil fungal communities in second-growth tropical rain forests},"                                                 
#> [6] "  pages = {},"                                                                                                                                                           
#> [7] "  publisher = {Wiley-Blackwell},"                                                                                                                                        
#> [8] "}"                                                                                                                                                                       
#> [9] ""                                                                                                                                                                        
#> 
```
