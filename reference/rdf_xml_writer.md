# RDF XML writer

RDF XML writer

## Usage

``` r
rdf_xml_writer(z, ...)
```

## Arguments

- z:

  an object of class `handl`; see
  [handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

- ...:

  further params passed to
  [`jsonld::jsonld_to_rdf()`](https://docs.ropensci.org/jsonld/reference/jsonld.html)

## Value

RDF XML

## Details

package `jsonld` required for this writer

## See also

Other writers:
[`bibtex_writer()`](https://docs.ropensci.org/handlr/reference/bibtex_writer.md),
[`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md),
[`citeproc_writer()`](https://docs.ropensci.org/handlr/reference/citeproc_writer.md),
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md),
[`ris_writer()`](https://docs.ropensci.org/handlr/reference/ris_writer.md),
[`schema_org_writer()`](https://docs.ropensci.org/handlr/reference/schema_org_writer.md)

## Examples

``` r
if (require("jsonld") && interactive()) {
  library("jsonld")
  z <- system.file('extdata/citeproc.json', package = "handlr")
  (tmp <- citeproc_reader(z))
 
  if (requireNamespace("bibtex", quietly=TRUE)) {
  (z <- system.file('extdata/bibtex.bib', package = "handlr"))
  (tmp <- bibtex_reader(z))
  rdf_xml_writer(z = tmp)
  cat(rdf_xml_writer(z = tmp))
  }
}
#> Loading required package: jsonld
#> Warning: package ‘jsonld’ was built under R version 4.6.1
```
