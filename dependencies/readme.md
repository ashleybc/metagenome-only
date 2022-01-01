Krona can be conda installed. Visit https://anaconda.org/bioconda/krona 
Prior to installation create a conda env for krona in command line by conda create --name myenv, then source activate prior to conda installation.

The update\nscript is ktUpdateTaxonomy.sh.  
The default location for storing\ntaxonomic databases is /Users/ashley/miniconda3/envs/krona-2.8.1/opt/krona/taxonomy\n\n
If you would like the taxonomic data stored elsewhere, simply replace\nthis directory with a symlink.  
For example:\n\nrm -rf /Users/ashley/miniconda3/envs/krona-2.8.1/opt/krona/taxonomy\nmkdir /path/on/big/disk/taxonomy\nln -s /path/on/big/disk/taxonomy /Users/ashley/miniconda3/envs/krona-2.8.1/opt/krona/taxonomy\nktUpdateTaxonomy.sh\n\n'

