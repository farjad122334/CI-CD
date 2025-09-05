# CI CD of REACT project Using Jenkins

This project automates build, integration and deployment process of react project in docker using Jenkins.

## Features/Concepts Used of jenkins

1. Jenkins Declarative Pipelines
2. User defined nodes/agents for running jobs
3. Webhook trigger for automatically trigerring the cicd job

### Plateform Used:
AWS Ec2 for setting up Jenkins server and user defined agents/nodes.

### What the pipeline actually does:
1. Checks out github repo
2. Cleans previous images and containers
3. Builds new docker image
4. Runs the image built

