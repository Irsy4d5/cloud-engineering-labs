# Lab 03 - VPC, Subnets and Security Groups

Built a custom VPC from scratch instead of relying on the default one, then hit and fixed a real security group scoping issue along the way.

## What I did

Used the Create VPC wizard's "VPC and more" option to spin up a full network in one go: a VPC on 10.0.0.0/16, split across 2 Availability Zones with 2 public subnets and 2 private subnets, plus the route tables and internet gateway that go with them. No NAT gateway since this was just for practice and NAT costs money per hour.

Checked the public subnet's route table and confirmed it routes 0.0.0.0/0 to the internet gateway. Checked a private subnet and confirmed it only has the local VPC route, no path to the internet at all - that is the actual difference between public and private subnets in practice, not just a label.

Created a custom security group (lab03-web-sg) allowing HTTP from anywhere and SSH from my IP only, then launched a test EC2 instance into one of the public subnets to confirm everything actually works together end to end.

## The interesting problem

First attempt at creating the VPC only produced the VPC itself with zero subnets - turned out I had "VPC only" selected instead of "VPC and more", so none of the subnets, route tables, or internet gateway got built. Deleted it and recreated properly, this time double-checking the preview panel showed 4 subnets and 3 route tables before clicking create.

Second issue: when I created the security group, the VPC dropdown had quietly defaulted back to my account's default VPC instead of the new lab03 VPC I had just built. The security group got created successfully, but when I went to attach it to my test instance, it did not show up in the list at all. Security groups are tied to whichever VPC they are created in and cannot be moved afterward, so the fix was deleting the wrongly-scoped one and recreating it, this time explicitly selecting irsyad-lab03-vpc from the dropdown before adding any rules.

## Commands / actions used

Fully GUI-based - VPC creation wizard, subnet and route table inspection, security group creation, and EC2 launch all done through the AWS Console.

## Screenshots

subnets-overview.jpg: All 4 subnets (2 public, 2 private) correctly created inside the new VPC

private-route-table.jpg: Private subnet route table showing only the local route, no internet access

security-group-attached.jpg: Final state - correct security group attached to the test instance with both inbound rules
