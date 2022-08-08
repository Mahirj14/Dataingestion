# Dataingestion
ways of fetch data from extrenal source to AWS S3



Let's explore the ways of fetching data source from extrnal sources to aws



# 1. Loading Kaggle dataset to AWS S3 using Boto3




The entire activity of fetching data from Kaggle to S3 has been broken down as different steps. Which includes :

* Step 1: Installation of Kaggle CLI
* Step 2: Installation of AWS CLI
* Step 3: Installation of Boto3
* Step 4: AWS S3 bucket creation using Python Boto3
* Step 5: Kaggle Dataset download
* Step 6: File uploads to AWS S3 using Boto3

###sep A : Install python3

```
sudo apt install python3


### Step 1: Installation of Kaggle CLI

```
pip install kaggle

```
### Step 2: Installation of AWS CLI

```
pip install awscli

```
### Step 3: Installation of Boto3

```
pip install boto3

```
### Step 4: AWS S3 bucket creation using Python Boto3

```
import boto3
s3resource=boto3.client('s3','us-east-1')
s3resource.create_bucket(Bucket='filetransfers3tords')
```
### Step 5: Kaggle Dataset download

```
kaggle datasets list
kaggle datasets download dataset name -p destination -unzip
```
### Step 6: File uploads to AWS S3 using Boto3

```
s3resource.upload_file(KaggleDatasetname,bucket_name,S3storedkaggledatasetname)



```




# 2. Deliver streaming data to S3 bucket using AWS Kinesis Firehose

This activity demonstrates how to deliver the streaming data set to an S3 bucket using amazon's Kinesis Data Firehose.


* Step1: Installation of AWS CLI

```
pip install awscli
```
* Step2: Installation of Boto3

```
pip install boto3
```

* Step3: Creation of Delivery Stream in Kinesis Firehose

You have to mention the below details for creating the delivery stream.
Delivery Stream Name
1. Source: Choose Direct PUT or other sources
2. Data transformation: Disabled (Default)
3. Record format conversion: Disabled (Default)
4. Destination: S3
5. S3 Destination: You have to choose the option to create a new bucket to store the data
6. S3 Buffer Conditions: (Default settings)
7. S3 compression and encryption: (Default settings)
8. Permissions: Select the option to create a new IAM role for the Data firehose
9. Review and create the DeliveryStream.

* Step4: Python Script for data generation

Now we need to develop a python script to generate some streaming data to ingest into the Delivery Stream created above.

This script is given as streaming.py, which generates the streaming data.

In order to connect with the Kinesis Data Firehose using Boto3, we need to use the below commands in the script.

```
Kinesisstream=boto3.client('firehose')
```

* Step5: Stream the Data to KinesisFirehose using PutRecordBatch() API

 To ingest data, we use the Put_Record_Batch() API as given below.

```
result = Kinesisstream.put_record_batch(DeliveryStreamName="SampleNumbers",
                                                   Records=records)
```
Once we run this script, it ingests the generated data to the delivery stream created.


* Step6: Monitor the Firehose dashboard to view data movement.

* Step7: Validate S3 data






```
