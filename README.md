# EXP 2 : ANALYSIS THE DISK STRUCTURE USING SLEUTH KIT

## AIM:
To analyze the internal disk structure of a disk image using Sleuth Kit tools and identify file system metadata, directory structure, and other forensic details for digital investigation purposes.

## EQUIPMENT REQUIRED:
  ●	Hardware: Personal Computer (PC)

```
Register Number: 212222040128
Name: RAGHUL S
```

## DESIGN STEPS:
### Step 1:

Obtain or create a disk image file (e.g., praveendisk.iso) to analyze. 

### Step 2:
Use Sleuth Kit tools like istat, fsstat, and fls to examine the partition layout, file system details, and file listing.

### Step 3:
Interpret the output of the tools to understand the disk structure, including partitions, sectors, and files.

## PROGRAM:
Sleuth Kit Disk Analysis Commands
## PRELIMINARY STEP:
### Step1:

  ●	Run command prompt as administrator
 ![1](https://github.com/user-attachments/assets/756c20ae-9906-429e-a956-a89afbc3e3c1)


### Step2:

  ●	Verify Sleuthkit is installed.
  ![2](https://github.com/user-attachments/assets/27f5730b-eed5-49dd-baed-d2546e011883)


### Step3:

  ●	Navigate to the binary file of Sleuthkit in command prompt: 
 ![3](https://github.com/user-attachments/assets/622235b7-44cd-42b5-9888-12f4a29f1e3f)


## PROCEDURE:
## ANALYSE THE FILE USING SLEUTHKIT TOOL:

### 1. View File Metadata
  ●	Use istat to view metadata of a file/directory using its inode number 0:
  
  ●	Command:  istat.exe -f filetype “file path” <inode number>
  
 ![1_f](https://github.com/user-attachments/assets/d47b1e9e-7669-4595-96df-31e2cbd887e4)

  #### OUTPUT SUMMARY:
  ●	Type: Directory
  
  ●	Permissions: dr-xr-xr-x (read + execute for all)
  
  ●	Created On: 2025-04-14 12:43:12 IST
  
  ●	Size: 2048 bytes, Sectors Used: 31

  
### 2. View Metadata of Inode 1

  ●	Use istat to view metadata of a file/directory using its inode number 1:
  
  ●	Command:  istat.exe -f filetype “file path” <inode number>
  
  ![2_f](https://github.com/user-attachments/assets/fcfe84d8-aff6-40dc-971b-ba2db90c34d1)


  #### OUTPUT SUMMARY:
  
  ●	Type: Directory (metasploitable-linux-2.0.0)
  
  ●	Permissions: dr-xr-xr-x (read + execute for all)
  
  ●	Created On: 2 2025-03-11 19:34:00 IST
  
  ●	Size: 2048 bytes, Sectors Used: 32
  
### 3. View Metadata of Inode 6

  ●	Use istat to view metadata of a file/directory using its inode number 6:
  
  ●	Command:  istat.exe -f filetype “file path” <inode number>
  
  ![3_f](https://github.com/user-attachments/assets/4c4fb2b9-5b37-4828-9469-7fc211d32bd1)


  #### OUTPUT SUMMARY:
  
  ●	File Name: Metasploitable.vmx — This is a VMware configuration.
  
  ●	Type: File — It's a regular file, not a folder.
  
  ●	Permissions: -r-xr-xr-x — Read & execute allowed for everyone, no write access.
  
  ●	Created Time: 2025-03-11 19:34:16 IST — This is when the file was added to the ISO.
  
  ●	Size: 2804 bytes — Small file (just a few KB).
  
  ●	Sectors: 940391, 940392 — The disk sectors storing this file's content.

### 4. Analysis of Inode 6 Metadata via icat Utility

  ●	Use icat to extract file content using its inode number 6:
  
  ●	Command:  icat.exe -f filetype “file path” <inode number>
  
  ![4_f](https://github.com/user-attachments/assets/12bb0bbe-4ab4-4751-8b12-6ce69b19dc62)


  #### OUTPUT SUMMARY:
  The command retrieves the contents of a VMware virtual machine configuration file (Metasploitable.vmx). This file defines how the virtual machine is set up, including:
  
  ●	Hardware settings like CPU (numvcpus = "1"), RAM (memsize = "512"), and SCSI controller.
  
  ●	Networking options, with both NAT (ethernet0) and Host-only (ethernet1) adapters configured.
  
  ●	Storage devices, such as virtual hard disk (Metasploitable.vmdk) and CD-ROM (auto detect).
  
  ●	Additional devices like USB, EHCI, and multiple PCI bridges.
  
  ●	VM metadata, including UUID, display name (Metasploitable2-Linux), OS type (ubuntu), and annotations.
  
  ●	Security note: The annotation warns that this VM is intentionally vulnerable and should not be exposed to untrusted networks.

### 5. View File System Details Using fsstat
  ●	Use fsstat to view file system metadata of the ISO image.
  
  ●	Command:  fsstat -f filetype “file path”
  ![5_f](https://github.com/user-attachments/assets/464b4c13-ca52-4361-b50c-64755d6098ed)
  ![6_f](https://github.com/user-attachments/assets/b94b99b0-f84c-466f-8c99-a44ec405d563)

  
  #### OUTPUT SUMMARY:
  PRIMARY VOLUME DESCRIPTOR 1 File System Information:
  
  •	File System Type: ISO9660
  
  •	Volume Name: 14_04_2025
  
  •	Volume Set Size: 1
  
  •	Volume Set Sequence: 1
  
  •	Recording Application: AnyBurn
  
  Metadata Information:
  
  •	Path Table Location: 22–22
  
  •	Inode Range: 0 – 9
  
  •	Root Directory Block: 36827386058113052
  
  Content Information:
  
  •	Sector Size: 2048 bytes
  
  •	Block Size: 2048 bytes
  
  •	Total Sector Range: 0 – 940393
  
  •	Total Block Range: 0 – 940393

### 6.List Directory Structure

  ●	Use fls to view directory structure.
  
  ●	Command:  fls -f filetype -r  “file path”
 ![7_f](https://github.com/user-attachments/assets/77b201a0-c21b-49f1-b80b-f1669697214f)



  #### OUTPUT SUMMARY:
  
  •	Root Directory: metasploitable-linux-2.0.0 (Inode 1)
  
  •	Contained Files and Subdirectories:
  
  o	Metasploitable2-Linux/ — A directory (Inode 2)
  
  o	Metasploitable.nvram — NVRAM file storing BIOS settings (Inode 3)
  
  o	Metasploitable.vmdk — Virtual hard disk file (Inode 4)
  
  o	Metasploitable.vmsd — Snapshot metadata file (Inode 5)
  
  o	Metasploitable.vmx — Main configuration file (Inode 6)
  
  o	Metasploitable.vmxf — Extended configuration file (Inode 7)

### 7. Image File Information

  ●	Use img_stat – Sleuth Kit utility for viewing image file metadata.
  
  ●	Command:  img_stat  “file path”
  ![8_f](https://github.com/user-attachments/assets/c6535668-5171-4c02-94ec-9d908782af85)


  #### OUTPUT SUMMARY:
  •	Image Type: raw
  
  •	Size in Bytes: 1925926912 (approx. 1.79 GB)
  
  •	Sector Size: 512 bytes
  
  •	Confirms that the input image is a raw format disk image with standard sector configuration.


## RESULT:
Using The Sleuth Kit, the disk structure was successfully analyzed. 

