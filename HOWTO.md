
# How I created these files!

---

***This is a brief write up on how I created these files.***
 

[Per this post] [1] Jeremey pointed me to [TKLBAM Profiles page] [2].
I gave it a good look and then followed his other option was to use a
[build task script] [3] they use to build the TKL apps.  

---

With this knowledge I used a clean version of TKLDev v15 and did the following

I downloaded the ISO and uploaded to my TKLDev server then ran the following commands:


```

# Create the MD5 hash of the ISO
root@TKLDev15 ~# md5sum mineos-node_stretch-x64.iso > mineos-node_stretch-x64.iso.md5

# Change to buildtask and execute script
root@TKLDev15 ~/projects/mineos-tklbm-profile# cd buildtasks/
/turnkey/buildtasks
root@TKLDev15 /turnkey/buildtasks# ./bin/generate-tklbam-profile ~/mineos-node_stretch-x64.iso ~/ --profiles-conf=/turnkey/tklbam-profiles
mount: /dev/loop0 is write-protected, mounting read-only
root@TKLDev15 /turnkey/buildtasks#

```
This will create a tar.gz file that I uncompressed into the three files you need. I then 
add some documentation and directoies that will need to backed up.




[1]: https://www.turnkeylinux.org/comment/47730#comment-47730 "Click here to view the post"
[2]: https://github.com/turnkeylinux/tklbam-profiles/blob/master/README.rst "Click here to see it"
[3]: https://github.com/turnkeylinux/buildtasks/blob/master/bin/generate-tklbam-profile "Click to view the code"

