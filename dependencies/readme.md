# Clean up and taxonomic classification

## Krona

[Krona can be conda installed](https://anaconda.org/bioconda/krona ).

Prior to installation create a conda env for krona if you don't have a designated environment for metagenome tools in command line by `conda create --name myenv`, then source activate by `source activate myenv` prior to conda installation.

tip- if you want to rename your conda env., you can't. You need to create a new environment and clone the old environment to it, then delete the old one: `conda create --name new_name --clone old_name` `conda remove --name old_name --all`

Once Krona is conda installed, manually update the taxonomy databases before Krona can generate taxonomic reports by `ktUpdateTaxonomy.sh`

The default location for storing the taxonomic databases is `../myenv/opt/krona/taxonomy`

## bbtools

[bbtools](https://jgi.doe.gov/data-and-tools/bbtools/) is a package created and maintained by the Joint Genome Institute that consistents of tools for trimming, MinHash, and much more!

bbtools can be [conda installed](https://anaconda.org/agbiome/bbtools) on Linux or [Homebrew installed](https://formulae.brew.sh/formula/bbtools)
on Mac OS X

## Kraken2

[Kraken2](github.com/DerrickWood/kraken2/archive/v2.0.9-beta.tar.gz) can be installed from tarball

Once source code is extracted, move to the Kraken2 directory and run `./install_kraken2.sh ./`

After running installation code, be sure to set PATH- ``export PATH=$PATH:`pwd` ``

Once installation is complete and export PATH is set, the database the user intends to use needs to be built using the command `kraken2-build` . The default/standard gene and protein database is built by `kraken2-build --standard --threads 4 --db standard` . Special databases require `kraken2-build --db mydatabase --special mydatabase` . Once the database is built, add the database to a kraken2 database path: `` export KRAKEN2_DB_PATH=`pwd` ``

### Specific to Mac OS X

Before running `./install_kraken2.sh ./` , you will need to install a different compiler, or running the installation script will result in a clang error, as  Apple Clang does not support OpenMP by default. This can be done by first running `brew install gcc` to install a GNU compiler. Then, move into the `src` folder of the kraken directory, and enter `vim Makefile` to edit the Makefile.  Modify `g++` to `g++-11`

## trimmomatic

[trimmomatic](https://anaconda.org/bioconda/trimmomatic) can be conda installed on all OS. For usage instructions, see the [online manual](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf). This tool is more suitable than bbduk if, for example, you want to trim to an exact length or using a sliding window based on Fast or Multi QC data and therefore require more control over the trimming. This can be used instead of bbduk in the example workflow, followed by Kraken2 classification and Krona visualization.

## sourmash (MinHash)
Implements bloom filter and scalable-s. More info about the tool can be found [here](https://sourmash.readthedocs.io). Sourmash can be [conda installed](https://anaconda.org/bioconda/sourmash). Note that if you already have bbtools, there are similar tools (sketchmaker, comparesketch, sendsketch). The most recent release of sourmash is only compatible with python up through version 3.7, so be sure to set your conda environment python to no higher than 3.7. If your existing environment has a higher version of python, this can be changed by
`conda activate my_env\n
conda install python=3.7`
