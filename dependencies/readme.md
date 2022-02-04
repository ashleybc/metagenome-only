# Clean up and taxonomic classification

## Krona

[Krona can be conda installed](https://anaconda.org/bioconda/krona ).

Prior to installation create a conda env for krona if you don't have a designated environment for metagenome tools in command line by `conda create --name myenv`, then source activate by `source activate myenv` prior to conda installation.

tip- if you want to rename your conda env., you can't. You need to create a new environment and clone the old environment to it, then delete the old one: `conda create --name new_name --clone old_name` `conda remove --name old_name --all`

Once Krona is conda installed, manually update the taxonomy databases before Krona can generate taxonomic reports by `ktUpdateTaxonomy.sh`

The default location for storing the taxonomic databases is `../myenv/opt/krona/taxonomy`

## bbduk

bbduk is part of the [bbtools](https://jgi.doe.gov/data-and-tools/bbtools/) package created and maintained by the Joint Genome Institute that consistents of tools for trimming, MinHash, and much more!

bbtools can be [conda installed](https://anaconda.org/agbiome/bbtools) on Linux or [Homebrew installed](https://formulae.brew.sh/formula/bbtools)
on Mac OS X

An important note on memory usage with bbtools! Typically, bbtools will only be able to use a maximum to use 85% of your machine's memory. Memory usage can be specified in bbtools commands with the -`Xmx` flag. For example, `-Xmx800m` specifies 800 megbytes of memory.
## Kraken2

[Kraken2](github.com/DerrickWood/kraken2/archive/v2.0.9-beta.tar.gz) can be installed from tarball

Once source code is extracted, move to the Kraken2 directory and run `./install_kraken2.sh ./`

After running installation code, be sure to set PATH- ``export PATH=$PATH:`pwd` ``

Once installation is complete and export PATH is set, the database the user intends to use needs to be built using the command `kraken2-build` . The default/standard gene and protein database is built by `kraken2-build --standard --threads 4 --db standard` . Special databases require `kraken2-build --db mydatabase --special mydatabase` . Once the database is built, add the database to a kraken2 database path: `` export KRAKEN2_DB_PATH=`pwd` ``

### Specific to Mac OS X

Before running `./install_kraken2.sh ./` , you will need to install a different compiler, or running the installation script will result in a clang error, as  Apple Clang does not support OpenMP by default. This can be done by first running `brew install gcc` to install a GNU compiler. Then, move into the `src` folder of the kraken directory, and enter `vim Makefile` to edit the Makefile.  Modify `g++` to `g++-11`

## Phyloflash

The Phyloflash tool is a convenient and quick way to estimate the 16S rRNA composition of metagenomes and predict the relative abundances of taxa. 
Phyloflash can be [conda installed](https://anaconda.org/bioconda/phyloflash)

## trimmomatic

[trimmomatic](https://anaconda.org/bioconda/trimmomatic) can be conda installed on all OS. For usage instructions, see the [online manual](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf). This tool is more suitable than bbduk if, for example, you want to trim to an exact length or using a sliding window based on Fast or Multi QC data and therefore require more control over the trimming. This can be used instead of bbduk in the example workflow, followed by Kraken2 classification and Krona visualization.

## sourmash (MinHash)
Implements bloom filter and scalable-s. More info about the tool can be found [here](https://sourmash.readthedocs.io). Sourmash can be [conda installed](https://anaconda.org/bioconda/sourmash). Note that if you already have bbtools, there are similar tools (sketchmaker, comparesketch, sendsketch). The most recent release of sourmash is only compatible with python up through version 3.7, so be sure to set your conda environment python to no higher than 3.7. If your existing environment has a higher version of python, this can be changed by
`conda activate my_env`
`conda install python=3.7`

Note that `bbtools` has a similar tool, `bbsketch` 

# Mapping

## bbmap

part of the bbtools package (See information above in the **clean-up and taxnonomic classification** section). Note that if you are working with eukaryotic genomes to appropriately increase the `maxindel` from the default (16000). Also be aware that SAM output files assume SAM 1.4 format ("X"=substitutions, “=”= match, "M" for degenerate bases) unless specified otherwise. By default, SAM files are converted to BAM (binary) files before being output to save space.

## bowtie2

## samtools

Samtools can be [conda installed](https://anaconda.org/bioconda/samtools). Sam tools has a variety of useful functions for viewing, indexing, sorting, and compressing sam and bam mapping files. Be aware that there are a few bugs, which are well-documented ([here is a pretty thorough summary](https://programmerah.com/samtools-run-error-error-while-loading-shared-libraries-libcrypto-so-1-0-0-or-libncurses-so-5-or-libtinfow-so-5-28066/)). I have determined a work-around specific to **Mac OS X** (described below).

### Mac OS X work-around

In the terminal, first navigate to the `lib` subfolder of the conda environment. First determine the version of libcrpyto that you have by ` ./ -name "libcrypto*"` . Once you determine this, change to the version that is used by samtools by `ln -s libcrypto.yourversion.dylib libcrypto.1.0.0.dylib` . Note that `dylib` is specific to Mac OS X. If using Linux, see the linked page for that version.

# Assembly

## SPAdes (St. Petersburg genome assembler)

SPAdes can be [conda installed](https://anaconda.org/bioconda/spades). Note that on Mac OS X, conda installed SPAdes may be slower than the tarball installation due to unavailability of parallel libstdc++ for the Clang compiler used by bioconda on MacOS
