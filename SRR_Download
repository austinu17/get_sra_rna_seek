import subprocess
import pandas as pd
import sys
import os.path
from shutil import copyfile

df= pd.read_csv(sys.argv[1],header=None)
sras = df[0].tolist()

for sra in sras:
#skipping sra download for already downloaded .fastq file
    if os.path.isfile(sra +".fastq") == True and os.path.isfile(sra +".sra")== False:
        continue
#skipping if SRA file is already downloaded
    if os.path.isfile(sra+".sra") == True and os.path.isfile(sra+"_tmp.sra") == False:
        print(sra+".sra" " FILE ALREADY DOWNLOADED")
        continue
    ftp_root = "ftp://ftp-trace.ncbi.nih.gov"
    #sra_path = "/sra/sra-instant/reads/ByRun/sra/{SRR|ERR|DRR}/<first 6 characters of accession>/<accession>/<accession>.sra"  
    sra_path = "/sra/sra-instant/reads/ByRun/sra/{}/{}/{}/{}.sra".format(sra[0:3],sra[0:6],sra,sra)
    #print(ftp_root + sra_path)
    exit_status = subprocess.call(['wget','-c' ,'-O',sra+"_tmp.sra",ftp_root + sra_path])
    print(exit_status)
    if exit_status == 0:
        os.rename(sra+"_tmp.sra", sra+".sra")
    else:
        print("DID NOT COPY")
     
