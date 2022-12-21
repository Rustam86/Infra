# Working with remote servers

## Theory

Q: *What are computer ports on a high level? How many ports are there on a typical computer?*

A: * *

Q: *What is the difference between http, https, ssh, and other protocols? In what sense are they similar? Name default ports for several data transfer protocols.*

A: * *

Q: *Explain briefly: (1) what is IP, (2) what IPs are called 'white'/public, (3) and what happens when you enter 'google.com' into the web browser.*

A: * *
Q: *What is Nginx? How does it work on the high level? List several alternative web servers.*

A: * *
Q: *What is SSH, and for what is it typically used? Explain two ways to authenticate in an SSH server in detail.*

A: * *

## Remote Server

Generate SSH key pair:
```
ssh-keygen
```
Create virtual machine (disk space: 15 GB, RAM: 8000 GB, OS: ubuntu 22.04). Use your favorite provider. Don't use vk cloud if you don't want to pay (charges 500 rub). Use public key (id_rsa.pub) when creating VM.

Connect to VM:
```
ssh -i <../id_rsa.pub> ubuntu@109.120.189.181
```

Download the latest human genome assembly (GRCh38) from the Ensemble FTP server:
```
wget https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
wget https://ftp.ensembl.org/pub/release-108/gff3/homo_sapiens/Homo_sapiens.GRCh38.108.gff3.gz
```
Download SAMtools and htslib:
```
wget https://github.com/samtools/samtools/releases/download/1.16.1/samtools-1.16.1.tar.bz2
wget https://github.com/samtools/htslib/releases/download/1.16/htslib-1.16.tar.bz2
```
Uzip samtools-1.16.1.tar.bz2 and htslib-1.16.tar.bz2
```
bzip2 -dk samtools-1.16.1.tar.bz2
bzip2 -dk htslib-1.16.tar.bz2
```

Build SAMtools:
```
cd samtools-1.x    # and similarly for bcftools and htslib
./configure --prefix=/where/to/install
make
make install
```
