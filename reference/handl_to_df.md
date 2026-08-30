# handl to data.frame conversion

handl to data.frame conversion

## Usage

``` r
handl_to_df(x)
```

## Arguments

- x:

  an object of class handl

## Value

data.frame with column following
[handl](https://docs.ropensci.org/handlr/reference/handl.md), with as
many rows as there are citations

## Note

requires the Suggested package `data.table`

## Examples

``` r
z <- system.file('extdata/crossref.ris', package = "handlr")
res <- ris_reader(z)
handl_to_df(res)
#>                                    id             type citeproc_type ris_type
#> 1 https://doi.org/10.7554/elife.01567 ScholarlyArticle          misc     JOUR
#>   resource_type_general                 doi
#> 1                  Text 10.7554/elife.01567
#>                                      b_url
#> 1 https://elifesciences.org/articles/01567
#>                                                                                                            title
#> 1 Automated quantitative histology reveals vascular morphodynamics during Arabidopsis hypocotyl secondary growth
#>               author publisher journal       is_part_of date_created
#> 1  .,  .,  .,  .,  .      <NA>   eLife Periodical;eLife         <NA>
#>   date_published date_accessed
#> 1           2014          <NA>
#>                                                                                                                                                                                                                                     description
#> 1 Among various advantages, their small size makes model organisms preferred subjects of investigation. Yet, even in model systems detailed analysis of numerous developmental processes at cellular level is severely hampered by their scale.
#>   volume issue first_page last_page keywords language    state
#> 1      3  <NA>       <NA>      <NA>     <NA>     <NA> findable

(x <- HandlrClient$new(x = z))
#> <handlr> 
#>   doi: 
#>   ext: ris
#>   format (guessed): ris
#>   path: /github/home/R/x86_64-pc-linux-gnu-library/4.6/handlr/extdata/crossref.ris
#>   string (abbrev.): none
x$as_df() # empty data.frame
#>   id type citeproc_type ris_type resource_type_general doi b_url title author
#> 1                                                                            
#>   publisher journal is_part_of date_created date_published date_accessed
#> 1                                                                       
#>   description volume issue first_page last_page keywords language state
#> 1                                                                      
x$read()
x$as_df() # data.frame with citation data
#>                                    id             type citeproc_type ris_type
#> 1 https://doi.org/10.7554/elife.01567 ScholarlyArticle          misc     JOUR
#>   resource_type_general                 doi
#> 1                  Text 10.7554/elife.01567
#>                                      b_url
#> 1 https://elifesciences.org/articles/01567
#>                                                                                                            title
#> 1 Automated quantitative histology reveals vascular morphodynamics during Arabidopsis hypocotyl secondary growth
#>               author publisher journal       is_part_of date_created
#> 1  .,  .,  .,  .,  .      <NA>   eLife Periodical;eLife         <NA>
#>   date_published date_accessed
#> 1           2014          <NA>
#>                                                                                                                                                                                                                                     description
#> 1 Among various advantages, their small size makes model organisms preferred subjects of investigation. Yet, even in model systems detailed analysis of numerous developmental processes at cellular level is severely hampered by their scale.
#>   volume issue first_page last_page keywords language    state
#> 1      3  <NA>       <NA>      <NA>     <NA>     <NA> findable

if (requireNamespace("bibtex", quietly=TRUE)) {
(z <- system.file('extdata/bib-many.bib', package = "handlr"))
res2 <- bibtex_reader(x = z)
handl_to_df(res2)
}
#>             key                                    id    type bibtex_type
#> 1    Amano_2016 https://doi.org/10.1093/biosci/biw022 article     article
#> 2 Bachelot_2016     https://doi.org/10.1890/15-1397.1 article     article
#>     citeproc_type ris_type resource_type_general additional_type
#> 1 article-journal     JOUR                  <NA>  JournalArticle
#> 2 article-journal     JOUR                  <NA>  JournalArticle
#>                     doi                                 b_url
#> 1 10.1093/biosci/biw022 https://doi.org/10.1093/biosci/biw022
#> 2     10.1890/15-1397.1     https://doi.org/10.1890/15-1397.1
#>                                                                                                        title
#> 1                            Spatial Gaps in Global Biodiversity Information and the Role of Citizen Science
#> 2 Long-lasting effects of land use history on soil fungal communities in second-growth tropical rain forests
#>                                                                                           author
#> 1                                                            Amano T., Lamming J., Sutherland W.
#> 2 Bachelot B., Uriarte M., Zimmerman J., Thompson J., Leff J., Asiaii A., Koshner J., McGuire K.
#>                         publisher                         is_part_of
#> 1 Oxford University Press ({OUP})            Periodical;{BioScience}
#> 2                 Wiley-Blackwell Periodical;Ecological Applications
#>   date_published volume first_page last_page    state
#> 1           <NA>     66        393       400 findable
#> 2           <NA>   <NA>       <NA>      <NA> findable
```
