# Lab 07 - Containers (Docker + ECS)

First container lab - went from a local Docker image all the way to a live, publicly reachable container running in AWS.

## What I did

Installed Docker Desktop and ran a basic nginx container locally to confirm it worked. Then built a custom image from a Dockerfile, copying my own HTML file into the nginx image and serving it on a different local port. Created an ECR repository, tagged and pushed the custom image up to AWS. Created an ECS cluster on Fargate, a task definition pointing at the pushed image, and ran the task with a public IP and a security group allowing HTTP. Opened the public IP in a browser and saw my own custom page being served live from AWS, not just from my laptop.

## The interesting problem

Hit a chain of small but realistic issues in a row: navigated to the wrong folder more than once before finding the actual project path, then got a no such file or directory error on the Dockerfile itself because Windows had silently added a hidden .txt extension to it. After fixing that, the docker push failed with an authentication error because the CLI still had an old, already-deactivated access key configured from a previous lab. Had to rotate the key again, reconfigure the CLI, log in properly to ECR, and only then did the push actually go through.

Also had a repeat lesson from earlier in the roadmap: ended up with AWS credentials visible in a terminal screenshot again. Deactivated that key immediately once it was flagged, and made sure not to publish the raw screenshot with real key values in it.

## Commands / actions used

```bash
docker run -d -p 8080:80 --name my-first-container nginx
docker build -t my-lab07-image .
docker run -d -p 8081:80 --name my-custom-container my-lab07-image
aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 891536279605.dkr.ecr.ap-southeast-1.amazonaws.com
docker tag lab07-my-image:latest 891536279605.dkr.ecr.ap-southeast-1.amazonaws.com/lab07-my-image:latest
docker push 891536279605.dkr.ecr.ap-southeast-1.amazonaws.com/lab07-my-image:latest
docker stop my-first-container my-custom-container
```

## Screenshots

terminal-push-success.png: Terminal showing the successful docker push (credentials redacted)

local-custom-container.png: The same custom page running locally on localhost:8081 before it was ever pushed to AWS

ecr-image-pushed.jpg: ECR repository showing the pushed image

live-container-browser.png: Custom page being served live from the running ECS task's public IP

ecs-task-stopped.jpg: ECS task confirmed stopped to avoid ongoing charges
