# wordcount-Spark-EMR
This is a word count example using Spark on AWS EMR.

## Reference
Source code: [apache/spark/examples/src/main/python/wordcount.py](https://github.com/apache/spark/blob/master/examples/src/main/python/wordcount.py).  
Github Tutorial: [Aliga8or/csds-spark-emr](https://github.com/Aliga8or/csds-spark-emr).  
Blog Tutorial: [Run a Spark job within Amazon EMR in 15 minutes](https://medium.com/big-data-on-amazon-elastic-mapreduce/run-a-spark-job-within-amazon-emr-in-15-minutes-68b02af1ae16).  

## How to use
To run a word count spark job on Amazon EMR, you can follow these steps:

### Upload data to S3
Open Amazon S3 console, create a new bucket and upload the input.txt file to that bucket.  
Click on the uploaded file and click the Make public button just to make sure.  

### Create a cluster on EMR
Open Amazon EMR console, create a cluster with configurations as below. **You must set up an EC2 key pair otherwise you can't ssh into the master node.**  
![ScreenShot](https://github.com/yueyang0115/wordcount-Spark-EMR//spark on EMR setting.JPG)  
The cluster remains in the 'Starting' state for about 10 - 15 minutes. Once the cluster is ready for use, the status will change to 'Waiting'. You can now go ahead and use it.  
