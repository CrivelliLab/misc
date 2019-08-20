# Connect to the Enclave

1. Connect to LBL VPN

2. either [https://vavdi.ornl.gov](https://vavdi.ornl.gov) in browser and use the HTML client, or use the VMWare Horizon Client to connect to the same address.

3. Type in your passcode (six-digit personal PIN + RSA token) to log in the enclave
4. Connect to the Windows VM (mvp011-01) or either of the two Linux VMs (mvp011-02 and mvp011-03)
5. Login a VM with your KDI user name (liux.mvp011w@kdi.local) and password, which will be set after you log in with the temporary password for the first time.



# Connect to VASQL

* From Windows using Microsoft SQL Server Management Studio (SSMS):
  1. Launch Windows PowerShell
  2. Type SSMS.exe

* From Linux through sqlcmd:

  Example: 

  ```console
  $ /opt/mssql-tools/bin/sqlcmd -D -SMVPSQL -Q "SELECT TOP 10 * FROM CDWWork.Patient.Patient"
  ```

* From Linux through Azure Data Studio:

  Example:

  ```console
  $ azuredatastudio
  ```

  Use *VASQL* as database name and choose *Windows Authentication*.

# Data Processing

## Read RDS files prepared by Ben McMahon:

```python
>> import pyreadr
>> results = pyreadr.read_r('demo42.RDS')
```

Not all RDS files can be parsed correctly.

# The HPC Environment

## Computer resources

### VM

* Linux VM: Xeon Gold 6142, 8 threads, 64GB RAM, 100GB storage
* Windows limts maximum concurrent users to 2



### The Computer cluster:

- 30 CPU nodes, 36 CPU cores, 128 GB RAM, 2TB HDD
- 15 GPU nodes, dual K80 GPUs, 36 CPU cores, 128 GB RAM, 2 TB HDD

* 3.2 PB Lustre file system

* 5 PB NFS and tape file system

  

### The Relational Database

  * 2 nodes, 40 cores, 3TB RAM, 11TB SSD storage, 167 TB HHD storage



### System Repositories: 

* CentOS 7 Base, CentOS 7 Updates, CentOS 7 Extras, EPEL

### User Repositories:

* Anaconda, install by /usr/local/bin/condaenv
* CRAN
* PyPI



### VM Project Shared folder 1.5 TB:

* Windows: file:\\\vafs01\data\VA_MVP011_CDW

* Linux: /mnt/vafs01/data/



### Murphy: 

* project shared folder: /mnt/vafs01/data, available on login node only
* HPC shared folder: /lustre/valustre/VA_MVP011_CDW
* Local scratch: /localscratch



## Connect to HPC

```
$ ssh va-murphy-login.kdi.local
```

### Install Jupyter Notebook on Linux VM

```
$ python -m pip install jupyter
```

### Install Anaconda on Linux VM

```
$ condaenv
```

Setting anaconda path will conflict with Linux VM remote desktop.  Do not let the installer change the .bashrc file.

### Using Jupyter Notebook on Murphy

From the Murphy Login node:

```
$ module load apps/python/anaconda/3/4.3.1
$ jupyter notebook --no-browser --ip=0.0.0.0
```

From VM: 

```
$ ssh -N -f -L locahost:8889:localhost:8888 va-murphy-login.kdi.local
```

Type in a browser search bar: locahost:8889



# Request new software

EMail <KDIsupport@ornl.gov>, with

*Subject:* VA Tenant Software Change Request

*Research Project Title*: 

*Project Technical Contact:*

*Requestor Contact Information*

*Software Name:*

*Software Version(s), or Git revision/ SVN revision/Release updates:*

*Release Date:*

*License Agreement:*

*Software Homepage URL:*

*Installation Target OS:*

*Installation target(s) in KDI: specific VM, or cluster names*

*Prerequisites/dependencies:*

*Purpose/Justification:*

# Documentation

## GitLab

https://code-va.kdi.local

Use Ad Login and your userid liux.mvp011w without the kdi.local part



- Getting Started [http://operations.va.kdi.local/va-docs/user-guide/getting-started](http://operations.va.kdi.local/va-docs/user-guide/getting-started)