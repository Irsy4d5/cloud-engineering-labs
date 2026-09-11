# Lab 01 - EC2 + SSH

Date: September 12, 2026

First real lab: spun up an EC2 instance and connected to it over SSH.

## What I did

Started by setting up a proper IAM user (irsyad-labs) instead of using root for everyday work, since that is the standard security practice. Added it to a cloud-labs-admin group with admin access.

Then launched an EC2 instance - Amazon Linux 2023, t3.micro, Singapore region. Created a new key pair for it and locked the security group down to only allow SSH from my own IP, instead of leaving it open to the whole internet.

Connected in through EC2 Instance Connect (browser-based SSH) and ran a few basic commands to poke around and confirm everything worked.

## The interesting problem

After locking SSH down to my own IP, EC2 Instance Connect stopped working entirely. Took a bit to figure out why: Instance Connect does not actually SSH in from your own IP, it proxies the connection through AWS's own infrastructure. So my My IP only rule was blocking AWS's own connect service.

Fix was to add a second inbound rule for the AWS-managed ec2-instance-connect prefix list (the IPv4 one, not IPv6), alongside the My IP rule. That let Instance Connect through while still keeping the general internet locked out.

## Commands I ran

```bash
whoami
pwd
ls
cat /etc/os-release
sudo dnf update -y
echo "first ec2 instance test!" > myfile.txt
cat myfile.txt
```

## Screenshots

iam-user-page.jpg: the IAM user setup

security-group-fix.jpg: the inbound rules after the fix

instance-running.jpg: instance passing 3/3 status checks

ssh-terminal.png: connected and running commands

## Next up

Lab 02 - S3 + IAM
