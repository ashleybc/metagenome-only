# Clean up and taxonomic classification

## Krona

[Krona can be conda installed](https://anaconda.org/bioconda/krona ).

Prior to installation create a conda env for krona if you don't have a designated environment for metagenome tools in command line by `conda create --name myenv`, then source activate by `source activate myenv` prior to conda installation.

tip- if you want to rename your conda env., you can't. You need to create a new environment and clone the old environment to it, then delete the old one: `conda create --name new_name --clone old_name` `conda remove --name old_name --all`

Once Krona is conda installed, manually update the taxonomy databases before Krona can generate taxonomic reports by `ktUpdateTaxonomy.sh`

The default location for storing the taxonomic databases is `../myenv/opt/krona/taxonomy`

## bbtools

[bbtools](https://jgi.doe.gov/data-and-tools/bbtools/) is a package created and maintained by the Joint Genome Institute

bbtools can be [conda installed](https://anaconda.org/agbiome/bbtools) on Linux or [Homebrew installed](https://formulae.brew.sh/formula/bbtools)
on Mac OS X

## Kraken2

[Kraken2](github.com/DerrickWood/kraken2/archive/v2.0.9-beta.tar.gz) can be installed from tarball

Once source code is extracted, move to the Kraken2 directory and run `./install_kraken2.sh ./`

After running installation code, be sure to set PATH- `export PATH=$PATH:pwd`
