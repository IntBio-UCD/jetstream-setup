# modifications

Things to do differnetly next time.  These are updates I am making to my instance as I go

## Freebayes

The apt install doesn't include scripts that  I need.  And it is picky about versions, so it gets its own Conda environment

```
conda create -n freebayes -c bioconda -c conda-forge freebayes=1.3.6 vcflib=1.0.1
```

## Jellyfish

```
conda create -n jellyfish -c bioconda kmer-jellyfish
```
