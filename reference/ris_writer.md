# ris writer (Research Information Systems)

ris writer (Research Information Systems)

## Usage

``` r
ris_writer(z)
```

## Arguments

- z:

  an object of class `handl`; see
  [handl](https://docs.ropensci.org/handlr/reference/handl.md) for more

## Value

text if one RIS citation or list of many

## References

RIS tags https://en.wikipedia.org/wiki/RIS\_(file_format)

## See also

Other writers:
[`bibtex_writer()`](https://docs.ropensci.org/handlr/reference/bibtex_writer.md),
[`cff_writer()`](https://docs.ropensci.org/handlr/reference/cff_writer.md),
[`citeproc_writer()`](https://docs.ropensci.org/handlr/reference/citeproc_writer.md),
[`codemeta_writer()`](https://docs.ropensci.org/handlr/reference/codemeta_writer.md),
[`rdf_xml_writer()`](https://docs.ropensci.org/handlr/reference/rdf_xml_writer.md),
[`schema_org_writer()`](https://docs.ropensci.org/handlr/reference/schema_org_writer.md)

Other ris:
[`ris_reader()`](https://docs.ropensci.org/handlr/reference/ris_reader.md)

## Examples

``` r
# from a RIS file
z <- system.file('extdata/crossref.ris', package = "handlr")
tmp <- ris_reader(z)
cat(ris_writer(z = tmp))
#> TY  - JOUR
#> T1  - Automated quantitative histology reveals vascular morphodynamics during Arabidopsis hypocotyl secondary growth
#> AU  - Sankar, Martial
#> AU  - Nieminen, Kaisa
#> AU  - Ragni, Laura
#> AU  - Xenarios, Ioannis
#> AU  - Hardtke, Christian S
#> DO  - 10.7554/elife.01567
#> UR  - https://elifesciences.org/articles/01567
#> AB  - Among various advantages, their small size makes model organisms preferred subjects of investigation. Yet, even in model systems detailed analysis of numerous developmental processes at cellular level is severely hampered by their scale.
#> JO  - eLife
#> VL  - 3
#> ER  - 

# peerj
z <- system.file('extdata/peerj.ris', package = "handlr")
tmp <- ris_reader(z)
cat(ris_writer(z = tmp))
#> TY  - JOUR
#> T1  - Three, two, one! Revision of the long-bodied sphaerodorids (Sphaerodoridae, Annelida) and synonymization of Ephesiella, Ephesiopsis and Sphaerodorum
#> AU  - Capa,María
#> AU  - Bakken,Torkild
#> AU  - Meißner,Karin
#> AU  - Nygren,Arne
#> DO  - 10.7717/peerj.5783
#> UR  - https://doi.org/10.7717/peerj.5783
#> AB  - Background                Long-bodied sphaerodorids (Annelida, Sphaerodoridae) is the common name for members of the three closely and morphologically homogenous currently accepted genera of benthic marine bristle worms: Ephesiella, Ephesiopsis and Sphaerodorum. Members of this group share the presence of two dorsal and longitudinal rows of macrotubercles with terminal papillae, and two longitudinal rows of microtubercles, features that are unique among sphaerodorids. Genera are distinguished by the chaetae morphology. Members of Ephesiella are characterised by having compound chaetae (except, sometimes, simple chaetae in the first chaetigers), Sphaerodorum bear only simple chaetae, and Ephesiopsis have both compound and simple chaetae in all parapodia.                                          Methods                Mitochondrial (partial COI and 16S rDNA) and nuclear (partial 18S rDNA and 28S rDNA) sequence data of long-bodied sphaerodorids with compound and simple chaetae, and an outgroup of additional seven sphaerodorid species were analysed separately and in combination using Bayesian inference (BA), and Maximum Likelihood (ML) methods. Long-bodied sphaerodorids from around the world (including type specimens) were examined under a range of optical equipment in order to evaluate putative generic and specific diagnostic features, in addition to intraspecific variability.                                          Results                Phylogenetic analyses of mitochondrial and nuclear DNA sequences of specimens identified as Ephesiella and Sphaerodorum, based on chaeta morphology, were performed. Sphaerodorum and Ephesiella were recovered as paraphyletic and nested within each other. Revision of current nominal species diagnostic features are performed and discussed.                                          Discussion                Results contradict current generic definitions. Recovery of paraphyletic compound and simple chaetae clades urge the synonymization of these two genera of long-bodied sphaerodorids. Morphological data also suggest the synonymization of Ephesiopsis.
#> KW  - Diagnostic features
#> KW  - Polychaetes
#> KW  - Morphology
#> KW  - Molecular phylogeny
#> KW  - Reciprocal monophyly
#> KW  - Systematics
#> KW  - Classification
#> KW  - Genera synonimization
#> JO  - PeerJ
#> VL  - 6
#> SP  - e5783
#> SN  - 2167-8359
#> ER  - 

# plos
z <- system.file('extdata/plos.ris', package = "handlr")
tmp <- ris_reader(z)
cat(ris_writer(z = tmp))
#> TY  - JOUR
#> T1  - Thy1 transgenic mice expressing the red fluorescent calcium indicator jRGECO1a for neuronal population imaging in vivo
#> AU  - Dana, Hod
#> AU  - Novak, Ondrej
#> AU  - Guardado-Montesino, Michael
#> AU  - Fransen, James W.
#> AU  - Hu, Amy
#> AU  - Borghuis, Bart G.
#> AU  - Guo, Caiying
#> AU  - Kim, Douglas S.
#> AU  - Svoboda, Karel
#> DO  - 10.1371/journal.pone.0205444
#> UR  - https://doi.org/10.1371/journal.pone.0205444
#> AB  - Calcium imaging is commonly used to measure the neural activity of large groups of neurons in mice. Genetically encoded calcium indicators (GECIs) can be delivered for this purpose using non-invasive genetic methods. Compared to viral gene transfer, transgenic targeting of GECIs provides stable long-term expression and obviates the need for invasive viral injections. Transgenic mice expressing the green GECI GCaMP6 are already widely used. Here we present the generation and characterization of transgenic mice expressing the sensitive red GECI jRGECO1a, driven by the Thy1 promoter. Four transgenic lines with different expression patterns showed sufficiently high expression for cellular in vivo imaging. We used two-photon microscopy to characterize visual responses of individual neurons in the visual cortex in vivo. The signal-to-noise ratio in transgenic mice was comparable to, or better than, mice transduced with adeno-associated virus. In addition, we show that Thy1-jRGECO1a transgenic mice are useful for transcranial population imaging and functional mapping using widefield fluorescence microscopy. We also demonstrate imaging of visual responses in retinal ganglion cells in vitro. Thy1-jRGECO1a transgenic mice are therefore a useful addition to the toolbox for imaging activity in intact neural networks.
#> Y1  - 2018/10/11
#> PB  - Public Library of Science
#> JO  - PLOS ONE
#> VL  - 13
#> IS  - 10
#> SP  - e0205444
#> ER  - 

# elsevier
z <- system.file('extdata/elsevier.ris', package = "handlr")
tmp <- ris_reader(z)
cat(ris_writer(z = tmp))
#> TY  - JOUR
#> T1  - Does conservation on farmland contribute to halting the biodiversity decline?
#> AU  - Kleijn, David
#> AU  - Rundlöf, Maj
#> AU  - Scheper, Jeroen
#> AU  - Smith, Henrik G.
#> AU  - Tscharntke, Teja
#> DO  - 10.1016/j.tree.2011.05.009
#> UR  - https://doi.org/10.1016/j.tree.2011.05.009
#> PB  - Elsevier BV
#> JO  - Trends in Ecology & Evolution
#> VL  - 26
#> IS  - 9
#> SP  - 474-481
#> SN  - 0169-5347
#> ER  - 

z <- system.file('extdata/citeproc.json', package = "handlr")
res <- citeproc_reader(z)
cat(ris_writer(z = res))
#> TY  - GEN
#> T1  - Eating your own Dog Food
#> T2  - DataCite Blog
#> AU  - FennerMartin
#> DO  - 10.5438/4k3m-nyvg
#> AB  - Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...
#> KW  - Phylogeny
#> KW  - Malaria
#> KW  - Parasites
#> KW  - Taxonomy
#> KW  - Mitochondrial genome
#> KW  - Africa
#> KW  - Plasmodium
#> PB  - DataCite
#> IS  - list(list(2016, 12, 20))
#> ER  - 

# many
## combine many RIS in a handl object
z <- system.file('extdata/crossref.ris', package = "handlr")
cr <- ris_reader(z)
z <- system.file('extdata/peerj.ris', package = "handlr")
prj <- ris_reader(z)
c(cr, prj)
#> <handl> 
#>   from: ris,ris
#>   many: TRUE
#>   count: 2
#>   first 10 
#>     id/doi: https://doi.org/10.7554/elife.01567
#>     id/doi: https://doi.org/10.7717/peerj.5783

# many bibtex to ris via c method
if (requireNamespace("bibtex", quietly=TRUE)) {
a <- system.file('extdata/bibtex.bib', package = "handlr")
b <- system.file('extdata/crossref.bib', package = "handlr")
aa <- bibtex_reader(a)
bb <- bibtex_reader(a)
(res <- c(aa, bb))
cat(ris_writer(res), sep = "\n\n")
}
#> TY  - JOUR
#> T1  - {THE} {INTENSIFICATION} {OF} {INNOVATION}
#> AU  - DODGSONMARK
#> AU  - GANNDAVID M.
#> AU  - SALTERAMMON. J
#> DO  - 10.1142/s1363919602000495
#> UR  - https://doi.org/10.1142%2Fs1363919602000495
#> PB  - World Scientific Pub Co Pte Lt
#> VL  - 06
#> SP  - 53
#> EP  - 83
#> ER  - 
#> 
#> TY  - JOUR
#> T1  - {THE} {INTENSIFICATION} {OF} {INNOVATION}
#> AU  - DODGSONMARK
#> AU  - GANNDAVID M.
#> AU  - SALTERAMMON. J
#> DO  - 10.1142/s1363919602000495
#> UR  - https://doi.org/10.1142%2Fs1363919602000495
#> PB  - World Scientific Pub Co Pte Lt
#> VL  - 06
#> SP  - 53
#> EP  - 83
#> ER  - 

## manhy Citeproc to RIS
z <- system.file('extdata/citeproc-many.json', package = "handlr")
w <- citeproc_reader(x = z)
ris_writer(w)
#> [1] "TY  - GEN\r\nT1  - Eating your own Dog Food\r\nT2  - DataCite Blog\r\nAU  - FennerMartin\r\nDO  - 10.5438/4k3m-nyvg\r\nAB  - Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...\r\nKW  - Phylogeny\r\nKW  - Malaria\r\nKW  - Parasites\r\nKW  - Taxonomy\r\nKW  - Mitochondrial genome\r\nKW  - Africa\r\nKW  - Plasmodium\r\nPB  - DataCite\r\nIS  - list(list(2016, 12, 20))\r\nER  - "
#> [2] "TY  - GEN\r\nT1  - Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)\r\nT2  - Terapia psicológica\r\nAU  - JuilleratKaren L\r\nAU  - CornejoFelipe A\r\nAU  - CastilloRamón D\r\nAU  - ChaigneauSergio E\r\nDO  - 10.4067/s0718-48082015000300006\r\nPB  - SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)\r\nVL  - 33\r\nIS  - 3\r\nSP  - 221\r\nEP  - 238\r\nSN  - 0718-4808\r\nER  - "                                                                     
cat(ris_writer(w), sep = "\n")
#> TY  - GEN
#> T1  - Eating your own Dog Food
#> T2  - DataCite Blog
#> AU  - FennerMartin
#> DO  - 10.5438/4k3m-nyvg
#> AB  - Eating your own dog food is a slang term to describe that an organization should itself use the products and services it provides. For DataCite this means that we should use DOIs with appropriate metadata and strategies for long-term preservation for...
#> KW  - Phylogeny
#> KW  - Malaria
#> KW  - Parasites
#> KW  - Taxonomy
#> KW  - Mitochondrial genome
#> KW  - Africa
#> KW  - Plasmodium
#> PB  - DataCite
#> IS  - list(list(2016, 12, 20))
#> ER  - 
#> TY  - GEN
#> T1  - Procesamiento semántico de palabras epistémicas y metafísicas en niños y adolescentes con Trastorno de Espectro Autista (TEA) y con Desarrollo Típico (DT)
#> T2  - Terapia psicológica
#> AU  - JuilleratKaren L
#> AU  - CornejoFelipe A
#> AU  - CastilloRamón D
#> AU  - ChaigneauSergio E
#> DO  - 10.4067/s0718-48082015000300006
#> PB  - SciELO Comision Nacional de Investigacion Cientifica Y Tecnologica (CONICYT)
#> VL  - 33
#> IS  - 3
#> SP  - 221
#> EP  - 238
#> SN  - 0718-4808
#> ER  - 
```
