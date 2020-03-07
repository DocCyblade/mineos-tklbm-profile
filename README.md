# MineOS TKLBAM Custom Profile
    Turnkey Linux Backup and Migration (TKLBAM) profile for MineOS

## History of this repo
I found [MineOS][1] when I wanted to run a Minecraft server for my kids. MineOS
is as your probably know is a great and easy way of hosting more than one
Minecraft server. What made it even better for me is it is built up on
[Turnkey Linux project][2]. As a part time app developer with TKL this 
made me happy!  

I quickly found out however since this ISO is NOT an official TKL
appliance, when I tried to use [Turnkey Linux Backup and Migration (TKLBAM)][3] 
service that is built into all TKL apps I was let down that TKLBAM 
did not have a profile for this!

I hopped on Turnkey Linux forums and [posted my problem][5]. Jeremey, like 
always pointed me in the right direction. (Thanks mate)


## What this does

Since you more than likely arrived here looking for a way to backup your
MineOS server this profile will allow you to use TKLBAM to backup your
server to the [Turnkey Linux Hub][4]. You need a Hub account setup to do this.
I already have a Hub account and other TLK apps being backed up. Check the
links above to see how to setup a Hub account. You don't have to backup
to the Hub, [see here for info on backing up else where][6].

These files will allow you to backup only what changes on your MineOS server
usually the server data!



# Support for these files

If you need help with these file [open an issue][8] on this repo in GitHub. If you have
issues with TKLBAM the hub or anything Turnkey Linux related [post in the forums][7]

--

# How to use


## 1. Get the files

Login as root and download or clone the git repo:

`git clone https://github.com/DocCyblade/mineos-tklbm-profile.git


## 2. Verify your ISO build

Next verify the md5 checksum of the ISO you used to install your server.
This is to make sure that the custom profile I have here will work with
the version of the ISO your server is running.

Assuming that your ISO file is in the same directory as the md5 files
and is on your MineOS server issue this command:

`md5sum -c mineos-node_stretch-x64.iso.md5 `

---

**Example successful output:**
```
root@mineos ~# md5sum -c mineos-node_stretch-x64.iso.md5 
mineos-node_stretch-x64.iso: OK
root@TKLDev15 ~#
```

---

**Example failed output:**
```
root@mineos ~# md5sum -c mineos-node_stretch-x64.iso.md5
mineos-node_stretch-x64.iso: FAILED
md5sum: WARNING: 1 computed checksum did NOT match
root@TKLDev15 ~#

```

## 3. Customize your backup

Edit the file `mineos-tklbm-profile/dirindex.conf` for your needs. The base config will 
backup everything under `/var/games/minecraft` and `/var/games/minecraft` except your
profiles `-/var/games/minecraft/profiles`


Also edit your TKLBAM config file to set how often you do a full backup etc
`nano /etc/tklbam/conf` The file is self documented and should be easy to understand.


## 4. Copy your customized profile

We will store our customized profile under `/etc/tklbam/mineos-profile`

Assuming you are working from `/root`:

```
# Make directory and copy files
mkdir /etc/tklbam/mineos-profile
cd ~/mineos-tklbm-profile/
cp dirindex dirindex.conf packages /etc/tklbam/mineos-profile/

```

## 5. Initialize TKLBAM and test your first backup

For this next step you will need to have your hub account setup and know your Hub API
key. Once you know your key, log in as root on your MineOS server and run the following
commands

```
# Setup the server to connect to the hub
tklbam-init YOUR_HUB_API_KEY_HERE --force-profile=/etc/tklbam/mineos-profile/


# Do a backup dry run
tklbam-backup --simulate


```

## 6. First backup and setting up daily backups

To do your first REAL backup issue the command `tklbam-backup`

To setup daily incremental backups run `chmod +x /etc/cron.daily/tklbam-backup`

Be sure to login to your [TKL Hub account][4] and find your new backup and rename it
as it will show up as `Turnkey Core`

Also think about how many full backups you want to keep and adjust that as well

---


[1]: https://minecraft.codeemo.com/mineoswiki/index.php?title=Main_Page#Previous_version_ISOs "Click here for more on MineOS"
[2]: https://www.turnkeylinux.org "Click to learn more about TKL"
[3]: https://www.turnkeylinux.org/docs/tklbam "Click to learn more about TKLBAM"
[4]: https://hub.turnkeylinux.org "Click to learn more about TKL Hub"
[5]: https://www.turnkeylinux.org/forum/support/tue-20200225-1243/mineos-backup "Click to see the post"
[6]: https://www.turnkeylinux.org/faq/backup-and-migration-tklbam#t599n2387 "Click to see other places to backup to"
[7]: https://www.turnkeylinux.org/forum/support "Click here for Turnkey Linux Forums"
[8]: https://github.com/DocCyblade/mineos-tklbm-profile/issues/new "Click here to open an issue on github"




