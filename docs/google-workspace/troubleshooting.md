---
layout: default
title: Troubleshooting
parent: Google Workspace
nav_oder: 1
---

# Troubleshooting Google Workspace
{: .no_toc }

Just some really good methodologies and GAM commands I use whenever a situation arises.
{: .fs-6 .fw-300 }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Transferring ownership of orphaned files.

### Example
{: .no_toc }

John Smith gives Jane Parker access to a folder on his My Drive. Jane transfers a 20GB video file to that folder. Jane technically still retains ownership of the file, and as the file is in the "My Drive" realm, it counts against her storage quota.

You have been tasked with offboarding Jane, and have moved 80GB worth of files to a share drive from Janes 'My Drive', but as the comamnds above only address files in her My Drive, you're still seeing 20GB of her quota in use. When deleting an account you are presented with the option to `Transfer` data to a new user, or `Do Not Transfer`. 

- Selecting `Do Not Transfer` will delete the 20GB video file that Jane currently owns which resides in Johns drive.
- Selecting `Transfer` will instead burden the new target user with ownership of the video file, and spend 20GB of their storage quota. Quite unfair, and a bad practice.

This is also a problem as sharing/management permissions for a file are the responsibility of the file owner, and not the directory owner. Behaviour wise, we can expect that files transferred in this manner from user to user are intended as a granting of ownership (though technically not in function).

### How to solve it
{: .no_toc }

You can run the following commands across your tenancy, which will search for files owned by Jane and reassign ownership to the user whose share drive the file resides in.

#### Command 1: Generate a CSV file which lists files owned by Jane in other users My Drives.
{: .no_toc }

```sh
gam all users show filelist corpora user showownedby others fullquery "'jane.parker@domain.tld' in owners" name id owners > ownedbyoffboarded.csv
```

#### Command 2: Itterate through the CSV, reassigning ownership of the corresponding file to the parent owner of the My Drive. 
{: .no_toc }

This will relegate Jane to Editor permission of the affected files, and still show the files in the "Shared to me" section on the drive website. Quota usage for each file will be reassigned to the owner of the My Drive.

```sh
gam csv ownedbyoffboarded.csv gam user jane.parker@domain.tld transfer ownership "~id" "~Owner"
```

#### Command 3 (Optional): Remove Jane from the access control of the files.
{: .no_toc }

This may be a good practice if you don't want to overburden the new user you're transferring file ownership to.

```sh
gam csv ownedbyoffboarded.csv gam user "~Owner" delete drivefileacl "~id" jane.parker@domain.tld
```

### Notes
- This process will not affect the permisions of files still present in Janes 'My Drive'.
- If a folder ID is generated/supplied to the CSV in the first command, the folder will be recusrively scanned through in the second command to find any files that fit this ownership scenario/criteria. Again, this will not affect files where Jane is not already the owner coming into the scenario..
{: .highlight }

---

