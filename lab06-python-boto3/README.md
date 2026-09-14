# Lab 06 - Python and Boto3

First lab written entirely in code instead of clicking through the console - AWS's Python SDK, boto3, doing the same things the UI does but scriptable.

## What I did

Installed boto3 and the AWS CLI, then created a dedicated access key for programmatic access and configured it locally. Wrote three small scripts: one to list all S3 buckets in the account, one to upload a local file into my Lab 02 bucket, and one to list all EC2 instances with their current state. Ran each one from the terminal and confirmed the results matched what showed up in the actual AWS console.

## The interesting problem

Hit a classic relative-path mistake: ran the upload script from a different folder than the one the test file actually lived in, so Python could not find it and threw a FileNotFoundError. Also generated a messy duplicate object in S3 from an earlier attempt where the full Windows file path ended up baked into the S3 key instead of just the filename. Fixed both by cd-ing into the correct folder before running the script, then deleted the badly-named duplicate from the bucket.

Also had a moment early on where I handled an AWS access key carelessly during setup. That key has since been deactivated and deleted for security, and a fresh one was generated in its place - a good reminder that credentials should never be treated as safe once they have been exposed anywhere outside of secure local storage.

## Commands / actions used

```bash
pip install boto3
aws configure
python list_buckets.py
python upload_file.py
python list_instances.py
```

## Screenshots

terminal-output-part1.png: Terminal session showing setup and the FileNotFoundError

terminal-output-part2.png: Terminal session showing the fix and both scripts succeeding

s3-bucket-upload.jpg: S3 bucket showing the file uploaded via script

ec2-instances-list.jpg: EC2 console matching the script's printed instance list
