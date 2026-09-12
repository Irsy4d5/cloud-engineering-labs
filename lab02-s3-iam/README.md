# Lab 02 - S3 + IAM

## What I did

Created a private S3 bucket (irsyad-lab02-bucket-2026) with all public access blocked by default. Uploaded my Lab 01 screenshots into it as test files, then confirmed the bucket was actually private by grabbing one file's Object URL and opening it directly in a browser tab - got a clean Access Denied error, which is exactly what should happen.

Then moved into IAM: wrote a custom JSON policy (Lab02-S3-Limited-Access) that only allows GetObject, PutObject, and ListBucket, scoped to just this one bucket using its ARN, instead of a broad wildcard policy. Attached it to my cloud-labs-admin group alongside the existing AdministratorAccess policy, just to practice the real workflow of attaching scoped least-privilege policies, even though it did not change my actual permissions.

## Commands / actions used

No CLI this time, fully GUI-based - bucket creation, file upload, and IAM policy JSON all done through the AWS Console.

## Screenshots

policy-attached.jpg: IAM policy attached to the cloud-labs-admin group

bucket-objects.jpg: S3 bucket showing uploaded test files

access-denied.jpg: Public access attempt correctly blocked
