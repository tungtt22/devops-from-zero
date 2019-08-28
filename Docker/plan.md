1. setup jenkins 
2. setup sonar
3. create pipeline:
- checkout code: code java sample 
- build : by maven
- scan sonar
- build docker image
- push image to docker hub
- deploy to server (EC2)