## Cloud Computing
## Programming Assignment 2 - Wine Prediction
## Goal:
The purpose of this individual assignment is to learn how to develop parallel machine learning (ML) applications in Amazon AWS cloud platform. Specifically, you will learn: (1) how to use Apache Spark to train an ML model in parallel on multiple EC2 instances; (2) how to use Spark’s MLlib to develop and use an ML model in the cloud; (3) How to use Docker to create a container for your ML model to simplify model deployment.

GitHub Link: https://github.com/Harshad3212/CS643_ProgrammingAssignment2_Harshad_Jadhav

Docker Link: https://hub.docker.com/r/harshadjadhav/cs643_programmingassignment2_harshad_jadhav

## SSH into EC2 instance
Step-by-Step how to set-up the cloud environment and run the application:
1. You have to create 1 ec2 instance.
2. Now access your ec2 instance using Putty.
3. Configure your AWS credentials.
## Configuring Flintrock
1. First install python and pip on ec2 instance. You can refer the documentation [here](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-linux.html).
2. Then the **flintrock configure** command. This will give you file location of config.yaml. So go to that location make changes in config file according to the class annoucement using vi or nano command..
3. For launching cluster use **flintrock launch Cluster-name** command.
4. Finally, login the cluster using **flintrock login Cluster-name** command. You are in your master node now.

## Data into Master node.
I had run my code locally using Jupyter notebook. So, I had to upload all the files such as my python code, datasets into master using WINSCP. I also had to upload just the datasets into my slave nodes as it was throwing error files not found.

## Parallel training implementation

## Single machine prediction application 

## Docker container for prediction application

## 
