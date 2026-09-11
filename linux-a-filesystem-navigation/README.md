# Linux-A - Filesystem and Navigation

First proper Linux fundamentals session, done on a fresh EC2 instance I launched myself (no help this time, including fixing my own security group).

## What I practiced

Started with the basics: whoami, pwd, ls, and ls -l to see permissions, ownership, size and timestamps on a file. Learned to read a permissions string like rw-r--r-- as three groups of three: owner, group, everyone else, each with read/write/execute.

Then moved on to actually navigating around: mkdir to create folders, cd to move into and out of them, and cd .. to go up a level. Also covered the difference between relative paths (directions from where you are) and absolute paths (the full address from root), plus the ~ shortcut which always jumps back to your home folder from anywhere.

## Mistakes along the way

Typed ls- l with no space and got command not found, since bash read it as one word. Also tried cd practice-folder right after creating a folder actually named test-folder, so got a No such file or directory error. Both were good reminders that the shell does not guess what you meant, it only does exactly what you typed.

## Commands used

```bash
whoami
pwd
ls
ls -l
touch testfile.txt
ls -l
mkdir test-folder
cd test-folder
pwd
cd ..
pwd
ls
cd /home/ec2-user/test-folder
pwd
cd /
pwd
cd ~
pwd
```

## Next up

Lab 02 - S3 + IAM
