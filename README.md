# Ricopili Bioinformatics

This is a set of workflows meant to be used after running a GWAS with Ricopili.


## Installation

The bioinformatics tool can be installed with the following command: 

    pip install git+https://github.com/vtrubets/ricopili_bioinformatics.git

I would recommend installing into a python virtual environment manager such as `virtualev` or `conda`.

# RegionAnnotator

Running the RegionAnnotator on a DANER file on a local node.

    bioinformatics --mode drmaa \
                   --cluster-env local \
                   --output-dir "/path/to/output/directory/" \
                       region_annotator \
                           --daner "/path/to/input.daner" \

## MAGMA

Running is simple. On the LISA cluster, you should start a long-running interactive session and execute the following command:

    bioinformatics --mode drmaa \
                   --cluster-env lisa \
                   --output-dir "/path/to/output/directory/" \
                       magma \
                           --daner "/path/to/input.daner" \
                           --ref-1000g "/path/to/1000G_reference_file_prefix" \
                           --sample-size 20000
                   
Each option is fairly straightforward. Options are split into generic `bioinformatics` options, followed by `magma` specific options:
  * The `--mode` option specifies the execution mode. You can run MAGMA in a few contexts: a DRMAA compatible cluster, a less   capable "qsub" compatible cluster or a local machine.
  * The `--cluster-env` option specifies whether you are running on LISA or the Broad's UGER. This sets some environment variables and cluster options.
  * The `--output-dir` option specifies an output directory in which intermediate and final files are stored.
  * The `magma` action tells the `bioninformatics` tool that you wish to run the MAGMA subpipeline. MAGMGA specific options follow. 
  * The `--daner` option points to the daner-formated GWAS results file.
  * The `--ref-1000g` option specifies the path+prefix of the 1000 Genomes reference data that MAGMA provides for download on their site. See the Reference Data section on the [MAGMA website](http://ctg.cncr.nl/software/magma).
  * The `--sample-size` option specifies the sample size of the GWAS study from which the daner-formatted input file was produced.
  
The output directory currently contains many intermediate files in addition to the file output. The final output file can be found at `/path/to/output/directory/merged_results.*`.

If you are running on the Broad's UGER, the `--cluster-env` option should be set to `broad`.


