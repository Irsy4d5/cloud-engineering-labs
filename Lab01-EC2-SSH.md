# Lab 01 — EC2 + SSH

## What I built

- Created a secure IAM user (`irsyad-labs`) instead of using the AWS root account for daily work, following least-privilege best practice
- Set up a `cloud-labs-admin` IAM group with AdministratorAccess and added the user to it
- Launched an Amazon EC2 instance (`lab01-ec2-ssh`) running Amazon Linux 2023, instance type t3.micro, in the Asia Pacific (Singapore) region
- Created and downloaded an RSA key pair (`.pem`) for secure access
- Configured the instance's security group (firewall) to restrict SSH access to my own IP address only, rather than leaving it open to the entire internet
- Connected to the instance using EC2 Instance Connect (browser-based SSH)
- Ran basic Linux commands to explore and interact with the server
- Stopped the instance afterward to avoid unnecessary compute charges

## Key concepts learned

- **Root vs IAM users:** the root account has unlimited access and should never be used for daily work; a separate IAM user with scoped permissions is the standard, secure approach
- **Key pairs:** how SSH key-based authentication works as a more secure alternative to passwords
- **Security groups:** how AWS firewalls control inbound/outbound traffic, and the tradeoff between convenience ("Anywhere") and security ("My IP")
- **EC2 Instance Connect:** AWS's browser-based SSH client routes traffic through AWS's own IP ranges, not the user's local IP — meaning security groups need to explicitly allow the `ec2-instance-connect` managed prefix list, not just "My IP"

## Commands used

```bash
whoami
pwd
ls
cat /etc/os-release
sudo dnf update -y
echo "first ec2 instance test!" > myfile.txt
cat myfile.txt
```

## Problems I hit & how I fixed them

**Problem:** After locking the security group down to "My IP" for SSH, EC2 Instance Connect failed repeatedly with "Error establishing SSH connection."

**Root cause:** EC2 Instance Connect doesn't SSH in directly from the user's own IP — it proxies the connection through AWS's own infrastructure. So restricting the security group to "My IP" actually blocked AWS's own connect service.

**Fix:** Edited the security group's inbound rule for SSH (port 22) and changed the source from "My IP" to the AWS-managed prefix list `com.amazonaws.ap-southeast-1.ec2-instance-connect` (the IPv4 version, not the IPv6 one). This allows EC2 Instance Connect specifically, while still blocking the general public internet.


