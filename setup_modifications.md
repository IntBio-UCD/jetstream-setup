# modifications

Things to do differnetly next time.  These are updates I am making to my instance as I go

2025 has incorporated the previous updates, so this is blank for now.

# For 2025

# For 2024 (not needed for 2025 image)

## Freebayes

The apt install doesn't include scripts that  I need.  And it is picky about versions, so it gets its own Conda environment

```
conda create -n freebayes -c bioconda -c conda-forge freebayes=1.3.6 vcflib=1.0.1
```

## Jellyfish

```
conda create -n jellyfish -c bioconda kmer-jellyfish
```

## BBmap

```
conda activate sequencing
conda install bbmap -c bioconda
```
## Seqfu

```
conda activate sequencing
conda install -y -c conda-forge -c bioconda "seqfu>1.10"
```

## multiqc

```
conda activate sequencing
conda install multiqc
```

## trimmomatic

```
cd ~/Downloads
wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.39.zip
unzip Trimmomatic-0.39.zip
sudo mv Trimmomatic-0.39 /usr/local/bin
vi ~/.bashrc
# in vi, add the following line (without the #) to set up an alias:
alias trimmomatic="java -jar /usr/local/bin/Trimmomatic-0.39/trimmomatic-0.39.jar"

#exit vi, then
source ~/.bashrc
```
