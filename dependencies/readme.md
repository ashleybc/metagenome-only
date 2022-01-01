[Krona can be conda installed](https://anaconda.org/bioconda/krona ).

Prior to installation create a conda env for krona in command line by `conda create --name myenv`, then source activate by `source activate myenv` prior to conda installation.

Once Krona is conda installed, manually update the taxonomy databases before Krona can generate taxonomic reports by `ktUpdateTaxonomy.sh`

The default location for storing the taxonomic databases is `../myenv/opt/krona/taxonomy`
