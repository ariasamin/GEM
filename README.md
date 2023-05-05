## Lab Overview: 
This is a workflow to analyze the human RNA sequencing data. There are several platforms available for RNA sequencing. However, new software and workflows develop and introduce every day. Here we introduce a workfow for analyzing the human RNA sequencing data Using GEMprep and Nextflow. By running this workflow, you will learn how to find out the RNAseq data from NCBI database and make GEM. Then, you will analyze the RNA sequencing data from homo sapiens.

## Learning Objectives:

1. Make a GEM
2. RNAseq Analysis

## Lab Tasks:

### install Nextflow

curl -s https://get.nextflow.io/ | bash
cp nextflow ~/bin
sudo apt update #Updates software repositories.
sudo apt install default-jre #Install Java
wget -qO- https://get.nextflow.io/ | bash #Compile nextflow
sudo cp nextflow /usr/local/bin #Adds nextflow to your PATH
Type this to see if nextflow software installed
nextflow

### Install Singularity

Update the Linux software repositories
sudo apt-get update
### Install dependencies
sudo apt install -y build-essential libseccomp-dev pkg-config squashfs-tools cryptsetup libglib2.0-dev

### Install GO software

wget https://go.dev/dl/go1.20.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.20.3.linux-amd64.tar.gz
echo $PATH | grep "/usr/local/go/bin"
source ~/.bashrc

### Install singularity software

### Download source code
export VERSION=3.10.0 && # adjust this as necessary 
wget https://github.com/sylabs/singularity/releases/download/v$%7BVERSION%7D/singularity-ce-$%7BVERSION%7D.tar.gz && 
tar -xzf singularity-ce-${VERSION}.tar.gz && cd singularity-ce-${VERSION}
### Compile source code
./mconfig && make -C ./builddir && sudo make -C ./builddir install
### Install dependencies
sudo apt-get install -y build-essential libseccomp-dev pkg-config squashfs-tools cryptsetup
Type this to see if nextflow singularity installed
Singularity

### Run GEMMaker

nextflow run systemsgenetics/gemmaker -profile test,singularity

### Install GEMprep

conda create -n gemprep python=3.6 matplotlib mpi4py numpy pandas r scikit-learn seaborn
source activate gemprep
git clone https://github.com/SystemsGenetics/GEMprep
cd GEMprep 
