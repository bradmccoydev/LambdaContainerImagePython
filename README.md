# Lambda Container Image - Python 3.9
Lambda container image for Python example

Docker commands
aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 142035491160.dkr.ecr.us-west-2.amazonaws.com

docker build -t bradmccoydev .

docker tag bradmccoydev:latest 142035491160.dkr.ecr.us-west-2.amazonaws.com/bradmccoydev:latest

docker push 142035491160.dkr.ecr.us-west-2.amazonaws.com/bradmccoydev:latest
