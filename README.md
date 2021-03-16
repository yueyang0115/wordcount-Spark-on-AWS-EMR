# wordcount-Spark-EMR
This is a word count example using Spark on AWS EMR.

## Reference
Github Tutorial: [Aliga8or/csds-spark-emr](https://github.com/Aliga8or/csds-spark-emr).  
Source code: [apache/spark/examples/src/main/python/wordcount.py](https://github.com/apache/spark/blob/master/examples/src/main/python/wordcount.py).  
Blog Tutorial: [Run a Spark job within Amazon EMR in 15 minutes](https://medium.com/big-data-on-amazon-elastic-mapreduce/run-a-spark-job-within-amazon-emr-in-15-minutes-68b02af1ae16).  

## How to use
To run a word count spark job on Amazon EMR, you can follow these steps:

### Upload data to S3
Open Amazon S3 console, create a new bucket and upload the input.txt file to that bucket.  
Click on the uploaded file and click the Make public button just to make sure.  

### Create a cluster on EMR
Open Amazon EMR console, create a cluster with configurations in [this picture](https://github.com/yueyang0115/wordcount-Spark-EMR/blob/main/setting.JPG). 
**You must set up an EC2 key pair otherwise you can't ssh into the master node.**  
The cluster remains in the 'Starting' state for about 10 - 15 minutes. Once the cluster is ready, the status will change to 'Waiting'. You can then go to use it.  

### Set up master node
Open Amazon EC2 console, click on Security Groups which is under Network & Security from the left panel.  
Click on the group named "ElasticMapReduce-master" and choose to edit inbound rules. Add a rule, select SSH for type and My IP as source.  

### Run spark job on master node
Open Amazon EMR console, click on the newly created cluster.  
In the summary of the cluster, under "Master public DNS", you can find a link to "Connect to the Master Node Using SSH". Click on that, follow the instruction to connect to the master node. Make sure you have the correct location of EC2 key pem.  
Git clone this repo to the master node. Remember to change your s3 bucket link.  
Run spark job using ```spark-submit wordcount.py | tee output.txt```.  
You can copy the output file to your s3 bucket using ```aws s3 cp output.txt s3://my_bucket/my_folder/```.  

### Done!
**Terminate your cluster when you are done.** Once the cluster is terminated, you need to create a new one next time your want to run the job.  
You need to allow inbound SSH traffic on the master every time your machine changes IP, which might happen when you switch between WiFi networks.  
