  

# GEO submission Tutorial

  

Modified based on Yeo Lab GEO submission Tutorial: https://yeolab.github.io/onboarding/geo.html

Download GEOarchive Templates and examples before starting data preparation:
https://www.ncbi.nlm.nih.gov/geo/info/spreadsheet.html#other
  

### Step 1. Login into GEO account and start new submission via FTP method
1. You will see GEO generated the personalized upload space, save the path name `uploads/username_storage_path`
2. Select data format you need to upload:

|**Option** | **Data** |
|---------- | -------- |
| HTS data | RNA-seq, single cell, etc |
| Microarray and other | Microarray, Methylation, Nanostring |

3. Save the FTP login information:
   
|**host address**| ftp.example.host.address |
|---------- | -------- |
|**username**|AAAA|
|**password**|ABCD12345|

After connecting, you **must navigate** to your personalized upload space: `uploads/username_storage_path`

### Step 2. Create submission folder on GreatLakes
1. Prepare all your raw files, processed matrix, and metadata under a seperate folder on GreatLakes server. Create single folder on your computer/Greatlakes that contains all raw and processed data files for your experiment. **If you have multiple data types, please use one folder per experiment.**
> **Example 1. Submission contains only Methylation**
> ```
> Data_to_geo/  
> ├── rawfile1.idat 
> ├── Metadata spreadsheet.xlsx  
> └── Processed data files 
> ```

> **Example 2. Submission contains multiple modalities**
> ```
> Data_to_geo/  
> ├── methyl/  
> │   ├── rawfile1.idat  
> │   ├── Metadata spreadsheet.xlsx  
> │   └── Processed data files 
> ├── rnaseq/  
> │   ├── rawfile1.fastq 
> │   ├── Metadata spreadsheet.xlsx  
> │   └── Processed data files 
>```

2. `cd /path/to/Data_to_geo` on server/locally before connecting FTP connection login

### Step 3. Log into GEO FTP
Use the username/password that GEO provides
>```
> (base) [AAA@gl-login4 Data_to_geo]$  ftp ftp.example.host.address 
> Trying ...Connected to
> 220 FTP Server ready. 
> Name (ftp ftp.example.host.address): AAAA 
> 331 Password required for geoftp 
> Password:  ABCD12345 
> 230 User geoftp logged in Remote system type is UNIX. 
> Using binary mode to transfer files.
>```
### Step 4. Turn off the interactive mode
Turn off interactive prompting for “are you sure you want to upload this file?” with `prompt  -n`, which requires you to respond within 60s or you lose your upload.
>```
> ftp> prompt n 
> Interactive mode off.
>```
### Step 5. Change the directory to you personalized upload space
>```
> ftp> cd  uploads/username_storage_path 
> 250 CWD command successful
>  ftp> ls
>  ftp> pwd
>```
>
### Step 6.  Upload all the files
You’ll next do a “multiple-file put” of all the files that are in your `/path/to/Data_to_geo` directory to put on GEO’s `uploads/username_storage_path` directory. The command is `mput  *`, and example output is below.
>```
> ftp> mput * 
> local: rawfile1.idat remote: rawfile1.idat 
> 227 Entering Passive Mode 
> 150 Opening BINARY mode data connection for rawfile1.idat
> 226 Transfer complete 
> 13676236 bytes sent in 0.149 secs (91878.70 Kbytes/sec) 
> 226 Transfer complete
>```
After the transfer is done, check the upload files using:
>```
> ftp> ls
> 227 Entering Passive Mode.
> 150 Opening ASCII mode data connection for file list
> -rw-rw-r--   1 ftp   geo  13676236 Jun 12 14:43 rawfile1.idat
>```
Exit FTP
>```
> ftp> bye
> Your connection to the remote server has been terminated.
>```
### Step 7. Contact GEO your upload
Fill out the submission form to notify GEO your submission: https://submit.ncbi.nlm.nih.gov/geo/submission/
Check the submission material
Confirm the release date
You will receive a confirmation after submit the form.
>```
> Transferred files are placed into the processing queue and will be
> reviewed within 5 business days; expect to receive an email from GEO
> curators with your GEO accession numbers, or questions about your
> submission. We can be contacted at
> [geo@ncbi.nlm.nih.gov](mailto:geo@ncbi.nlm.nih.gov) if you do not hear
> from us within the allotted time, or if you require additional
> assistance.
>```
