# handl object

handl object

## Details

A `handl` object is what's returned from the reader functions, and what
is passed to the writer functions. The `handl` object is a list, but
using the `print.handl` method makes it look something like:

    <handl>
      from: codemeta
      many: TRUE
      count: 2
      first 10
        id/doi: https://doi.org/10.5063%2ff1m61h5x
        id/doi: https://doi.org/10.5063%2ff1m61h5x

You can always [`unclass()`](https://rdrr.io/r/base/class.html) the
object to get the list itself.

The `handl` object follows <https://github.com/datacite/bolognese>,
which uses the Crosscite format as its internal representation. Note
that we don't currently support writing to or reading from Crosscite.

Details on each entry are stored in the named attributes:

- from: the data type the citations come from

- many: is there more than 1 citation?

- count: number of citations

- finally, some details of the first 10 are printed

If you have a `handl` object with 1 citation, it is a named list that
you can access with normal key indexing. If the result is length \> 1,
the data is an unnamed list of named lists; the top level list is
unnamed, with each list within it being named.

Each named list should have the following components:

- key: (string) a key for the citation, e.g., in a bibtex file

- id: (string) an id for the work being referenced, often a DOI

- type: (string) type of work

- bibtex_type: (string) bibtex type

- citeproc_type: (string) citeproc type

- ris_type: (string) ris type

- resource_type_general

- additional_type: (string) additional type

- doi: (string) DOI

- b_url: (string) additional URL

- title: (string) the title of the work

- author: (list) authors, with each author a named list of

  - type: type, typically "Person"

  - name: full name

  - givenName: given (first) name

  - familyName: family (last) name

- publisher: (string) the publisher name

- is_part_of: (list) what the work is published in, or part of, a named
  list with:

  - type: (string) the type of work

  - title: (string) title of the work, often a journal or edited book

  - issn: (string) the ISSN

- date_published: (string)

- volume: (string) the volume, if applicable

- first_page: (string) the first page

- last_page: (string) the last page

- description: (string) description of the work, often an abstract

- license: (string) license of the work, a named list

- state: (string) the state of the list

- software_version: (string) software version

Citeproc formats may have extra fields that begin with `csl_`
