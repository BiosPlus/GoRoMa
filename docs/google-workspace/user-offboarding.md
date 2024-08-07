---
layout: default
title: User Offboarding
parent: Google Workspace
---
# User Offboarding
{: .no_toc}

The common methodology in Microsoft 365 environments from my experience seems to be to convert a user account into a shared mailbox and deal out access to other users. Google doesn't offer that same functionality and their migration tool isn't great if someones position/data needs to be split among multiple successors.
{: .fs-6 .fw-300 }

---

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Requirements:

- Got Your Back ([Github](https://github.com/GAM-team/got-your-back)) - @GAM-team
    - Be sure to set this up with a service account, [follow their guide for more info](https://github.com/BiosPlus/GoRoMa/blob/main/README.md#offboarding-users).
- Google Applications Manager - GAMADV-XTD (Github)
    - [This guide](https://basuta.com/posts/installing-google-apps-manager-gam-on-google-cloud-shell/) is great for installing it on a [Google Cloud Shell](https://cloud.google.com/shell) (50 hour quota / 5GB storage / Unlimited Bandwidth - Free each week). You could probably do the same with Got Your Back.

{: .highlight}
This can all be done with the user account suspended.

## Mailbox Data handling

### 1. Create a group mailbox

With these properties you'll establish a good and scalable precedent.

| Property | Convention | Example |
|---|---|---|
| Name | `Offboarded User - [User Full Name] (email_prefix) - YYYY-MM-DD` | ***Offboarded User - John Smith (john.smith) - 2023-01-01***
| Address | `offboarded_[emailprefix]@domain.tld` | `offboarded_john.smith@domain.tld` |
| Group Owner | You | |
| Permissions | Set everything to "Owner" |  |


### 2. Take a copy of the users mail with `gyb` (ensuring only to take mail less than 25MB in size)

Open terminal and run the following command (substituting `john.smith` with the address of the offboarded user, and `you` with your address (provided you're a workspace administrator))
```sh
gyb --email john.smith@domain.tld --action backup --service-account --search smaller:25M
```

This will start a backup process which exports each email in the users inbox to .eml format in a nicely structured directory, as well as an SQLite database which keeps track of any relevant attributes.

### 3. Restore a copy to the group mailbox.

We’re going to take that backup and import it into the aforementioned group with:

```sh
gyb  --action restore-group --email offboarded_john.smith@domain.tld --use-admin you@domain.tld --service-account --local-folder /PATH/TO/BACKUP/DIR
```

This can be a very slow process, about 1 email per 1.5 seconds, can't be helped.

### 4. Take a full copy of the user mailbox with gyb (regardless of size)

Now we can take a full sized copy of the mailbox.

```sh
gyb --email john.smith@domain.tld --action backup --service-account
```

### 5. Zip a copy of that mailbox and throw it into a team/shared drive.

If you would like to speed this process up and save a lot of space, feel free to utilise the ZStandard compression format, just be sure to have `zstd` in your PATH.

```sh
tar -acvf john.smith.tar.zst GYB-GMail-Backup-john.smith\@domain.tld/
```

### 6. Remove yourself as the Owner from the Group Mailbox.

### 7. Add the relevant users inheriting this data as "Contributors" to the Mailbox.

## Drive Data Handling

{: .important}
If after this, the users account still shows drive storage quota being used, it's likely they have backed up their computer directories using the gogole drive dekstop app function. I don't have a good methodology for dealing with this at the moment.

### 1. Create a Google Shared Drive for the offboarded user.

With these properties you'll establish a good and scalable precedent.

| Property | Convention | Example |
|---|---|---|
| Name | `Offboarded User - [User Full Name] (email_prefix) - YYYY-MM-DD` | ***Offboarded User - John Smith (john.smith) - 2023-01-01***
| Access | You + Offboarded User added as `Managers` | |

This can be easily done with:

```sh
gam user you@domain.tld create teamdrive "Offboarded User - John Smith (john.smith) - 2023-01-01" adminmanagedrestrictions true asadmin
```
{: .important}
Be sure to grab the Teamdrive ID, it's a string of random characters output after the generation.

#### Add the offboarded user as a manager.

```sh
gam add drivefileacl TEAM_DRIVE_ID_HERE user john.smith@domain.tld role organizer
```

### 2. Move Data from the user ***"My Drive"*** to the ***"Share Drive"***.

{: .warning}
This will retain all the document level IDs and sharing settings, though you will lose directory based sharing (a la, if the user shared a whole folder, that access will be lost).

```sh
gam user john.smith@domain.tld move drivefile root teamdriveparentid TEAM_DRIVE_ID_HERE mergewithparent duplicatefolders merge createshortcutsfornonmovablefiles
```

### 3. Set access.
Remove yourself and the user from being drive managers. Add users who will need this data as `contributors` at most, *this sets a good precedent that they should be working in shared/team drives and not hoarding critical docs in their private storage.*

---

## Optional reading:

See [troubleshooting (transferring ownership of orphaned files)](troubleshooting.md#scenario-transferring-ownership-of-orphaned-files) for a fix to a rare scenario where you're still seeing drive storage quota in use even though the offboardee drive is empty.