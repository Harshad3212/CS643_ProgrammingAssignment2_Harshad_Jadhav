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
2. Then the **flintrock configure** command. This will give you file location of config.yaml. So go to that location make changes in config file according to the class annoucement using vi or nano command.**Note**: Change cluster type to m5.large. You have to install both spark and hadoop by setting the value True. 
4. For launching cluster use **flintrock launch Cluster-name** command.
5. Finally, login the cluster using **flintrock login Cluster-name** command. You are in your master node now.

## Data into Master node
I had run my code locally using Jupyter notebook. So, I had to upload all the files such as my python code, datasets into master using WINSCP.

## Parallel training implementation
1. You have to add both Trainingdataset.csv and ValidationDataset.csv to hadoop folder. By using **hdfs dfs -ls/data** command.
2. Run the following command to create model and parallel traing implementation across your cluster: spark-submit --master spark://ip-172-31-30-207.ec2.internal:7077 train.py hdfs:///data/TrainingDataset.csv hdfs:///model
3. Then we have to get our model using **hdfs dfs -get /model** command.
## Single machine prediction application 
For single machine predictio we use the following command:
  spark-submit --master local[*] test.py file:///home/ec2-user/ValidationDataset.csv file:///home/ec2-user/model
Here, we can see the Accuracy and F1-score on our local machine.
## Setting up docker on EC2 instance
1. Install most recent docker engine package: sudo amazon-linux-extras install docker or sudo yum install docker
2. Start docker : sudo service docker start
3. Adding ec2-user to docker group: sudo usermod -a -G docker ec2-user
4. Exit the flintrock cluster and login again.
5. verify ec2-user: docker info
6. After setting up login into your docker using : docker login. Here you have to provide you credentials for dockerhub.
7. Build the docker image using : docker build -t harshadjadhav/cs643_programmingassignment2_harshad_jadhav .
8. Run the image using: docker run harshadjadhav/cs643_programmingassignment2_harshad_jadhav driver test.py ValidationDataset.csv model. You will be able to see the accuracy and F1-score.
9. Pushing the image to Docker hub repository: docker push harshadjadhav/cs643_programmingassignment2_harshad_jadhav
## Docker container for prediction application
  1. Launch your ec2-instance and then step-up docker using the above steps.
  2. Place all the files from github into your instance.
  3. Pull the image from repositroy: docker pull harshadjadhav/cs643_programmingassignment2_harshad_jadhav
  4. Run the image using : docker run harshadjadhav/cs643_programmingassignment2_harshad_jadhav driver test.py ValidationDataset.csv model
