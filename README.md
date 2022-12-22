# Working with remote servers

## Theory

**Q**: ***What are computer ports on a high level? How many ports are there on a typical computer?***

A: *Port is a virtual interface for network connections. There are 65,535 ports on typical computer*

**Q**: ***What is the difference between http, https, ssh, and other protocols? In what sense are they similar? Name default ports for several data transfer protocols.***

A: *HTTP means HyperText Transfer Protocol. HTTP is the underlying protocol used by the World Wide Web and this protocol defines how messages are formatted and transmitted, and what actions Web servers and browsers should take in response to various commands. It uses port 80 by default.*

*HTTPS uses TLS -Transport Level Security (SSL - Secure Sockets Layer) to encrypt normal HTTP requests and responses, and to digitally sign those requests and responses. As a result, HTTPS is far more secure than HTTP. HTTPS uses port 443 by default.*

*SSH means “Secure Shell”. It has a built-in username/password authentication system to establish a connection. It uses Port 22 to perform the negotiation or authentication process for connection. Authentication of the remote system is done by the use of public-key cryptography and if necessary, it allows the remote computer to authenticate users.*

**Q**: ***Explain briefly: (1) what is IP, (2) what IPs are called 'white'/public, (3) and what happens when you enter 'google.com' into the web browser.***

A: *IP address - an Internet Protocol address is a numerical label such as 109.120.189.181 that is connected to a computer network that uses the Internet Protocol for communication*

*A public IP address is an IP address that can be accessed directly over the internet and is assigned to your network router by your internet service provider*

*When you enter 'google.com' into the web browser [many things happen](https://github.com/alex/what-happens-when). 
*To put it briefly:*

-Browser looks up IP address for the domain.
-Browser initiates TCP connection with the server
-Browser sends the HTTP request to the server.
-Server processes request and sends back a response.
-Browser renders the content.

**Q**: ***What is Nginx? How does it work on the high level? List several alternative web servers.***

A: * *
**Q**: ***What is SSH, and for what is it typically used? Explain two ways to authenticate in an SSH server in detail.***

A: * *

## Remote Server

Generate SSH key pair:
```
ssh-keygen
```
Create virtual machine (disk space: 15 GB, RAM: 8 GB, OS: ubuntu 22.04). Use your favorite provider. Don't use vk cloud if you don't want to pay (charges 500 rub). Use public key (id_rsa.pub) when creating VM.

Connect to VM:
```
ssh -i <../id_rsa.pub> ubuntu@109.120.189.181
```
Dont't forget to update and upgrade:
```
sudo apt update && sudo apt upgrade -y
```
Download the latest human genome assembly (GRCh38) from the Ensemble FTP server:
```
wget https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
wget https://ftp.ensembl.org/pub/release-108/gff3/homo_sapiens/Homo_sapiens.GRCh38.108.gff3.gz
```
Unzip files:
```
gzip -dk Homo_sapiens.GRCh38.108.gff3.gz
gzip -dk Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz
```
Install samtools and tabix:
```
sudo apt install samtools
sudo apt install tabix
```
Index the fasta using samtools:
```
samtools faidx Homo_sapiens.GRCh38.dna.primary_assembly.fa
```
Install GenomeTools:
```
sudo apt install genometools
```
Sort gff3:
```
gt gff3 -sortlines -tidy -retainids Homo_sapiens.GRCh38.108.gff3 > Homo_sapiens.GRCh38.108.sorted.gff3
```
bgzip and tabix sorted gff3:
```
bgzip Homo_sapiens.GRCh38.108.sorted.gff3
tabix Homo_sapiens.GRCh38.108.sorted.gff3.gz
```
Dowload ATAC-seq and ChiP-seqs from ENCODE:
```
wget -O ATAC.bigBed "https://www.encodeproject.org/files/ENCFF274FAH/@@download/ENCFF274FAH.bigBed"
wget -O NR3C1.bigBed "https://www.encodeproject.org/files/ENCFF536FKB/@@download/ENCFF536FKB.bigBed"
wget -O CTCF.bigBed "https://www.encodeproject.org/files/ENCFF417LCP/@@download/ENCFF417LCP.bigBed"
wget -O EP300.bigBed "https://www.encodeproject.org/files/ENCFF642COK/@@download/ENCFF642COK.bigBed"
```
Dowload bigBed to BED converter:
```
wget http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/bigBedToBed
```
Give permisions:
```
chmod a+x bigBedToBed
```
Convert to BED:
```
./bigBedToBed ATAC.bigBed ATAC.bed
./bigBedToBed NR3C1.bigBed NR3C1.bed
./bigBedToBed CTCF.bigBed CTCF.bed
./bigBedToBed EP300.bigBed EP300.bed
```
Install Bebtools:
```
sudo apt install -y bedtools
```
Sort BED files:
```
bedtools sort -i ATAC.bed > ATAC.sorted.bed
bedtools sort -i NR3C1.bed > NR3C1.sorted.bed
bedtools sort -i CTCF.bed > CTCF.sorted.bed
bedtools sort -i EP300.bed > EP300.sorted.bed
```
bgzip and tabix sorted BED files:
```
bgzip ATAC.sorted.bed
tabix ATAC.sorted.bed.gz

bgzip NR3C1.sorted.bed
tabix NR3C1.sorted.bed.gz

bgzip CTCF.sorted.bed
tabix CTCF.sorted.bed.gz

bgzip EP300.sorted.bed
tabix EP300.sorted.bed.gz
```
Download JBrowse Web:
```
wget https://github.com/GMOD/jbrowse-components/releases/download/v2.3.2/jbrowse-web-v2.3.2.zip
```
Create repository  /mnt/JBrowse/ move jbrowse-web-v2.3.2.zip unzip / cleanup:
```
sudo mkdir /mnt/JBrowse/
sudo chmod a+rwx /mnt/JBrowse/
mv jbrowse-web-v2.3.2.zip /mnt/JBrowse/jbrowse-web-v2.3.2.zip
cd /mnt/JBrowse/
unzip jbrowse-web-v2.3.2.zip
rm jbrowse-web-v2.3.2.zip
```
Install JBrowse web prerequisites (node.js):
```
cd ~
curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh
sudo bash /tmp/nodesource_setup.sh
sudo apt install nodejs
```
Not figured better way to install jbrowse cli:
```
sudo apt install npm
npm install -g @jbrowse/cli
```

Install nginx:
```
sudo apt install nginx
```
Modify /etc/nginx/nginx.conf to contain the folowing:
```
sudo nano /etc/nginx/nginx.conf
```
> 
    http {
    # Don't touch other options!
    # ........
    # ........

    # Comment this line(!):
    # include /etc/nginx/sites-enabled/*;

    # Add this:
    server {
      listen 80 default_server;
      index index.html;
      server_name _;

      location /jbrowse/ {
        alias /mnt/JBrowse/;    
      }
    }
    }

Restart nginx:
```
sudo nginx -s reload
```

Add files (BED & FASTA & GFF3) to the genome browser
```
sudo jbrowse add-assembly Homo_sapiens.GRCh38.dna.primary_assembly.fa --load copy --out /mnt/JBrowse/
sudo jbrowse add-track Homo_sapiens.GRCh38.108.sorted.gff3.gz --load copy --out /mnt/JBrowse/
sudo jbrowse add-track ATAC.sorted.bed.gz --load copy --out /mnt/JBrowse/
sudo jbrowse add-track CTCF.sorted.bed.gz --load copy --out /mnt/JBrowse/
sudo jbrowse add-track EP300.sorted.bed.gz --load copy --out /mnt/JBrowse/
sudo jbrowse add-track NR3C1.sorted.bed.gz --load copy --out /mnt/JBrowse/
```


Spend over 8 hours still not working

http://109.120.189.181/jbrowse/
