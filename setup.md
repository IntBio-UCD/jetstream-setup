From Image: Ubuntu22
Flavor: m3.quad  

 * 4 CPU cores  
 * 15 GB RAM  
 * 100 GB Root Disk (Custom size, increase from 20 to 100 GB)

Add SSH Key  
Add Web Desktop
3 minutes to build

Open Web Desktop  
Click through initial setup  
Accept software update  

ctrl-alt-t

### Install packages and libraries
```
sudo -i
apt update

export NEEDRESTART_MODE=a # prevents interactice restart services screen from popping up

apt install libboost-iostreams-dev -y
apt install libgsl0-dev -y
apt install libmysql++-dev -y
apt install libboost-graph-dev -y
apt install libgl1-mesa-dev -y #for rgl
apt install libglu1-mesa-dev -y #for rgl
apt install libmysqlclient-dev -y #for R mysql
apt install libfontconfig1-dev -y
apt install libmpfr-dev -y 
apt install libgmp-dev -y
apt install openmpi-bin -y
apt install libopenmpi-dev -y
apt install mysql-client -y
apt install mysql-server -y
apt install libssl-dev -y
apt install libudunits2-dev -y
apt install libxml2-dev -y
apt install cargo -y 
apt install libcairo2-dev -y
apt install libmagick++-dev -y
apt install libxslt1-dev -y
apt install libgeos-dev -y 
apt install libgdal-dev -y
apt install libpq-dev -y
apt install libfftw3-3 libfftw3-dev -y 
apt install libgconf-2-4 -y
apt install texlive-latex-extra -y
apt install texlive-fonts-recommended -y
apt install dkms -y
apt install liblist-moreutils-perl -y
apt install libstatistics-descriptive-perl -y 
apt install libstatistics-r-perl -y
apt install perl-doc -y
apt install libtext-table-perl -y
apt install gdebi-core -y
apt install cmake -y
apt install cython -y
apt install gedit gir1.2-gtksource-3.0 -y
apt install default-jdk -y 
apt install openjdk-8-jdk -y
apt install ruby-dev nodejs -y
apt install python3-pip python3-numpy python3-scipy -y
apt install libharfbuzz-dev libfribidi-dev -y
apt install bwa -y # probably not needed use hisat
apt install bowtie2 -y # probably not needed use hisat
apt install hisat2 python3-hisat2 -y 
apt install bedtools -y
apt install mafft -y
apt install probalign -y
apt install t-coffee -y
apt install fasttree -y


exit
```

# Make minimize and maximize buttons appear
```
gsettings set org.gnome.desktop.wm.preferences button-layout ":minimize,maximize,close"
```

# Fix date and time
```
sudo dpkg-reconfigure tzdata
```

# Make the toolbar more windows like  

## unfortunately this is not working (June 2024)
```
sudo apt-get install chrome-gnome-shell
```

Add native installer extension from https://extensions.gnome.org/  (on that website click on the link in the purple box near the top to add the installer.  This allows gnome extensions to be installed from the web browser)

Turn on and install "Dash to Panel" (search for it with search bar and then click the switch)

### Installing latest R 

Although the base Ubuntu 22 image has R and RStudio they are out of date.

Go to [https://cran.r-project.org/](cran) to get latest script
```
# update indices
sudo apt update -qq
# install two helper packages we need
sudo apt install --no-install-recommends software-properties-common dirmngr
# add the signing key (by Michael Rutter) for these repos
# To verify key, run gpg --show-keys /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc 
# Fingerprint: E298A3A825C0D65DFD57CBB651716619E084DAB9
wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
# add the R 4.0 repo from CRAN -- adjust 'focal' to 'groovy' or 'bionic' as needed
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
sudo apt install --no-install-recommends r-base # Y
```

### Installing Rstudio

Check Posit website for latest
```
wget https://download1.rstudio.org/electron/jammy/amd64/rstudio-2024.04.2-764-amd64.deb
sudo gdebi rstudio-2024.04.2-764-amd64.deb  # y
rm rstudio-2024.04.2-764-amd64.deb
## Edit the exec command of ~/.local/share/applications/rstudio.desktop to just run rstudio and not that module crap
```

### Installing R packages 

Install what we can from the apt system. It is faster because packages do not need to be compiled    
```

# add another repository

sudo add-apt-repository ppa:c2d4u.team/c2d4u4.0+

sudo apt update

sudo apt install --no-install-recommends r-cran-swirl r-cran-tidyverse r-cran-seqinr r-cran-qtl r-cran-evaluate  r-cran-highr r-cran-markdown r-cran-yaml r-cran-htmltools  r-cran-bitops r-cran-knitr r-cran-rmarkdown r-cran-devtools r-cran-shiny r-cran-pvclust r-cran-gplots r-cran-cluster r-cran-igraph r-cran-scatterplot3d r-cran-poisbinom r-cran-biocmanager  r-cran-igraph r-cran-ggdendro r-cran-upsetr r-cran-statgengwas

# rstan
# Add Michael Rutter's c2d4u4.0 PPA
sudo add-apt-repository ppa:marutter/rrutter4.0
sudo apt update
sudo apt-get install -y libv8-dev
sudo apt install -y r-cran-rstan

# more bayes
sudo apt install r-cran-mvtnorm r-cran-loo r-cran-coda r-cran-brms

# statistical learning
sudo apt install r-cran-glmnet r-cran-gam r-cran-pls r-cran-tree r-cran-gbm r-cran-xgboost

# phylogenetics
sudo apt install r-cran-ape r-cran-ouch r-cran-phytools r-cran-phylolm

# tidy models
sudo apt install r-cran-tidymodels r-cran-corrplot r-cran-mda  r-cran-rules
```

```
sudo -i

R 

# within R: #installs into /usr/local/lib/R/site-library since we are sudo
# Cran packages
install.packages(c('hwde', 'caTools', 'formatR'), dependencies=T)

# Install Bioconductor packages    
BiocManager::install(c("BiocStyle","snpStats","rtracklayer","goseq","impute","multtest","VariantAnnotation","chopsticks","edgeR", "GenomicRanges", "genomation", "plyranges", "Rsamtools"))

# Set up C++ toolchain for Rstan
dotR <- file.path(Sys.getenv("HOME"), ".R")
if (!file.exists(dotR)) dir.create(dotR)
M <- file.path(dotR, "Makevars")
if (!file.exists(M)) file.create(M)
cat("\nCXX17FLAGS=-O3 -march=native -mtune=native -fPIC",
    "CXX17=g++", # or clang++ but you may need a version postfix
    file = M, sep = "\n", append = TRUE)



# More statistical Learning
install.packages("LEAP")
install.packages("randomForest")

# phylogenetic
install.packages("ouch")
install.packages("phytools")
install.packages("phylolm")

# more tidymodels
install.packages("usemodels")
install.packages("baguette")
install.packages("discrim")
BiocManager::install("mixOmics")
devtools::install_github("tidymodels/learntidymodels")
install.packages("bestNormalize")
install.packages("textrecipes")
install.packages("DALEXtra")
install.packages("stacks")
install.packages("poissonreg")
```

### Install github desktop

See https://github.com/shiftkey/desktop

```
wget -qO - https://apt.packages.shiftkey.dev/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/shiftkey-packages.gpg > /dev/null
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/shiftkey-packages.gpg] https://apt.packages.shiftkey.dev/ubuntu/ any main" > /etc/apt/sources.list.d/shiftkey-packages.list'
sudo apt update && sudo apt install github-desktop
```

### Installing BLAST 2.15.0+ from NCBI (version 2.12 installed by default, replace it with code below)

```
cd /usr/local/src
sudo wget https://ftp.ncbi.nlm.nih.gov/blast/executables/LATEST/ncbi-blast-2.15.0+-x64-linux.tar.gz
sudo tar zxvpf ncbi-blast-2.15.0+-x64-linux.tar.gz
sudo rm ncbi-blast-2.15.0+-x64-linux.tar.gz
cd /usr/local/bin
sudo ln -sf /usr/local/src/ncbi-blast-2.15.0+/bin/* .
cd
```

### Installing Samtools, bctools, htslib
(apt versions are way behind)
```
cd /usr/local/src
sudo wget https://github.com/samtools/samtools/releases/download/1.19.2/samtools-1.19.2.tar.bz2
sudo tar xvfj samtools-1.19.2.tar.bz2
sudo rm samtools-1.19.2.tar.bz2
cd samtools-1.19.2
sudo ./configure --prefix=/usr/local/bin
sudo make
sudo make install

cd /usr/local/src
sudo wget https://github.com/samtools/bcftools/releases/download/1.19/bcftools-1.19.tar.bz2
sudo tar xvfj bcftools-1.19.tar.bz2
sudo rm bcftools-1.19.tar.bz2
cd bcftools-1.19
sudo ./configure --prefix=/usr/local/bin
sudo make
sudo make install

cd /usr/local/src
sudo wget https://github.com/samtools/htslib/releases/download/1.19.1/htslib-1.19.1.tar.bz2
sudo tar xvfj htslib-1.19.1.tar.bz2
sudo rm htslib-1.19.1.tar.bz2
cd htslib-1.19.1
sudo ./configure --prefix=/usr/local/bin
sudo make
sudo make install
```

### Installing Fastqc

```
cd /usr/local/src
sudo wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.12.1.zip
sudo unzip fastqc_v0.12.1.zip
sudo rm fastqc_v0.12.1.zip
cd FastQC/
sudo chmod 0755 fastqc
cd /usr/local/bin
sudo cp -s ../src/FastQC/fastqc .
cd
```


### Installing GATK 4.5.0.0

```
cd /usr/local/src
sudo wget https://github.com/broadinstitute/gatk/releases/download/4.5.0.0/gatk-4.5.0.0.zip
sudo unzip gatk-4.5.0.0.zip
sudo rm gatk-4.5.0.0.zip
cd /usr/local/bin
sudo ln -s /usr/local/src/gatk-4.5.0.0/gatk .
cd
```


### ADMIXTURE
https://dalexander.github.io/admixture/download.html
```
cd /usr/local/src
sudo wget https://dalexander.github.io/admixture/binaries/admixture_linux-1.3.0.tar.gz
sudo tar -xvzf admixture_linux-1.3.0.tar.gz
cd ../bin
sudo ln -s /usr/local/src/dist/admixture_linux-1.3.0/admixture .
cd
```

### htseq

```
pip install HTseq
```



### [hifiasm](https://github.com/chhylp123/hifiasm)
```
sudo -i

cd /usr/local/src
git clone https://github.com/chhylp123/hifiasm
cd hifiasm
make
cd /usr/local/bin
ln -s /usr/local/src/hifiasm/hifiasm ./
exit
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

### Miniconda (needed for seqkit, busco, minimap2)

See https://docs.anaconda.com/free/miniconda/miniconda-install/

Do as exouser, not root
```
cd
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh

~/miniconda3/bin/conda init bash
source .bashrc

```


### a bunch of sequencing relateed tools via miniconda [seqkit](https://github.com/shenwei356/seqkit), [busco](), minimap2, STAR, igv
```
conda create --name sequencing
conda activate sequencing
conda install -c bioconda star
conda install -c bioconda minimap2
conda install -c bioconda seqkit
conda install -c bioconda igv
conda install -c bioconda igvtools
conda install -c conda-forge -c bioconda busco
conda install bbmap -c bioconda
conda install -y -c conda-forge -c bioconda "seqfu>1.10"
conda install multiqc
conda deactivate
```

## Freebayes
```
conda create -n freebayes -c bioconda -c conda-forge freebayes=1.3.6 vcflib=1.0.1
```

## Jellyfish
```
conda create -n jellyfish -c bioconda kmer-jellyfish
```

## Installing [fail2ban](https://github.com/fail2ban/fail2ban)
This software blocks ssh access after X failed attempts (default 10)
```
sudo apt -u install fail2ban
```

## mosh and fish

```
sudo apt -y install mosh
sudo apt -y install fish
```

## update Rstudio prefs

Do not restore workspace with .Rdata
Never save workspace to .Rdata
Softwrap R source files

## Create and add access to shares

See [manila shares](https://docs.jetstream-cloud.org/general/manilaVM/)

# Create image snapshot
On Jetstream gui click create snapshot image of instance under actions while server is running

# Create new instances
Image: Intbio-2024_image
Flavor: m3.quad  

 * 4 CPU cores  
 * 15 GB RAM  
 * 80 GB Root Disk (Custom size, increase from 20 to 80 GB)
