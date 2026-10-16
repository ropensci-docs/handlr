# Changelog

## handlr 0.3.1

CRAN release: 2025-03-03

#### MINOR IMPROVEMENTS

- Update maintainer to Brenton M. Wiernik.
- Improved support for Citation File Format (CFF) and codemeta.json

## handlr 0.3.0

CRAN release: 2020-10-15

#### DEPENDENCIES

- drop `RefManageR` from package Imports as it will likely be archived
  soon - add package `bibtex` to Suggests for reading/writing bibtex
  (can’t be in Imports because it’s Orphaned on CRAN)
  ([\#22](https://github.com/ropensci/handlr/issues/22))

#### NEW FEATURES

- handlr gains support for Citation File Format (CFF), “plain text files
  with human- and machine-readable citation information for software”.
  See <https://citation-file-format.github.io/> for more info - new
  functions:
  [`cff_reader()`](https://docs.ropensci.org/handlr/reference/cff_reader.md)
  and
  [`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md)
  and associated changes in `HandlrClient`. Associated with CFF support,
  handlr gains new Import package `yaml`
  ([\#16](https://github.com/ropensci/handlr/issues/16))

#### MINOR IMPROVEMENTS

- improvements to Citeproc parsing: previously dropped many fields that
  we didn’t support; now including all Citeproc fields that we don’t
  specifically parse into extra fields prefixed with `csl_`
  ([\#20](https://github.com/ropensci/handlr/issues/20))
- nothing changed, but see discussion of bibtex errors in case you run
  into them ([\#9](https://github.com/ropensci/handlr/issues/9))

## handlr 0.2.0

CRAN release: 2019-08-19

#### NEW FEATURES

- gains function
  [`handl_to_df()`](https://docs.ropensci.org/handlr/reference/handl_to_df.md);
  converts any `handl` object (output from `HandlClient` or any
  `*_reader()` functions) to a data.frame for easier downstream data
  munging; `HandlClient` gains `$as_df()` method which runs
  [`handl_to_df()`](https://docs.ropensci.org/handlr/reference/handl_to_df.md);
  to support this, now importing data.table package
  ([\#15](https://github.com/ropensci/handlr/issues/15))
  ([\#19](https://github.com/ropensci/handlr/issues/19)) feature request
  by [@GeraldCNelson](https://github.com/GeraldCNelson)

#### MINOR IMPROVEMENTS

- now exporting the `print.handl` method. it only affects how a `handl`
  class object prints in the console, but is useful for making output
  more brief/concise
  ([\#14](https://github.com/ropensci/handlr/issues/14))
- filled out a lot more details of what a `handl` object contains. see
  [`?handl`](https://docs.ropensci.org/handlr/reference/handl.md) for
  the documentation
  ([\#17](https://github.com/ropensci/handlr/issues/17))

## handlr 0.1.0

CRAN release: 2019-02-27

#### NEW FEATURES

- Released to CRAN
