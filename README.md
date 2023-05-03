# GEM
GEMmaker

#install nextflow and copy to PATH
curl -s https://get.nextflow.io | bas 
cp nextflow ~/bin

#Update the Linux software repositories
sudo apt-get update

#Install dependencies
sudo apt install -y build-essential libseccomp-dev pkg-config squashfs-tools cryptsetup libglib2.0-dev

#Install GO software		#updated version:https://gist.github.com/nikhita/432436d570b89cab172dcf2894465753
sudo rm -r /usr/local/go -rf
export VERSION=1.18.3 OS=linux ARCH=amd64 				# change this if you need
wget -O /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz \
https://dl.google.com/go/go${VERSION}.${OS}-${ARCH}.tar.gz
sudo tar -C /usr/local -xzf /tmp/go${VERSION}.${OS}-${ARCH}.tar.gz
echo 'export GOPATH=${HOME}/go' >> ~/.bashrc
echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc
source ~/.bashrc
go						#test go

#Install singularity software using source code
export VERSION=3.10.0 && # adjust this as necessary \
wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-ce-${VERSION}.tar.gz && tar -xzf singularity-ce-${VERSION}.tar.gz && cd 
singularity-ce-${VERSION}
#Compile source code
./mconfig  &&  make -C ./builddir  &&  sudo make -C ./builddir install

#test sigularity
nextflow run systemsgenetics/gemmaker -profile test,singularity

#Nextflow intallation
sudo apt update #Updates software repositories.
sudo apt install default-jre 			#Install Java
wget -qO- https://get.nextflow.io | bash 	#Compile nextflow
sudo cp nextflow /usr/local/bin 		#Adds nextflow to your PATH								#test nextflow 
nextflow


#Input data: from ncbi db (https://trace.ncbi.nlm.nih.gov/Traces/index.html?view=run_browser&display=metadata)
#example: 
wget https://trace.ncbi.nlm.nih.gov/Traces?run=SRR24121374

#build GEMmaker to pull the database from NCBI and run the steps using nexflow
nextflow run systemsgenetics/gemmaker -profile singularity \
--pipeline kallisto \
--kallisto_index_path TAIR10_cdna_20101214.indexed \
--sras SRAs.txt


nextflow run systemsgenetics/gemmaker -profile singularity \  
--pipeline kallisto		\
--kallisto_index_path  Homo_sapiens.GRCh38.cdna.all.kallisto.indexed	\
--sras SRAs.txt



