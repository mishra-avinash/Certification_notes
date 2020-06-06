Recently i passed AWS Machine Learning Speciality exam with score 950/1000. Below, i am putting all my notes, resources and how did i approached the exam.

Exam questions are divided in to four sections. Data Engineering, Data Exploration, Modeling and Model Deployment.

## Resources

1. This is the official [exam guide](<https://d1.awsstatic.com/training-and-certification/docs-ml/AWS%20Certified%20Machine%20Learning%20-%20Specialty_Exam%20Guide%20(1).pdf>) read it carefully to understand the exam pattern.
2. Exam [Sample Questions](https://d1.awsstatic.com/training-and-certification/docs-ml/AWS-Certified-Machine-Learning-Specialty_Sample-Questions.pdf)
3. Udemy ML Specialty Preparation [Course](https://www.udemy.com/course/aws-machine-learning/). I found it really helpful to understand the overall expectations and a good starting points for exam material.
4. Udemy ML Specialty [Practice exam](Udemy ML Specialty Practice exam) Do this practice test after first round of prepration. If you in first do not worry, you will pass with confidence in third round.
5. Whizlab practice [exams](https://www.whizlabs.com/aws-certified-machine-learning-specialty/)
6. [AWS blog](https://aws.amazon.com/blogs/?awsf.blog-master-category=category%23artificial-intelligence), read this blogs to understand the different concepts used in different use case scenarios.
7. SageMaker [Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html). Go through the documentation of different algorithms and other concepts. Use this for reference.
8. Examtopics [sample questions](https://www.examtopics.com/exams/amazon/aws-certified-machine-learning-specialty/). These questions have some previous AWS exam question that were also in my exam. DO NOT SKIP THESE QUESTIONS. Practice at least once before the exam. Though they do not have correct answers, you need to read the discussion and use your knowledge to understand to choose the right answers.

## Approach

I prepared the exam in three stages.

1. Stage 1:
   1. I went through the Udemy course once and did all the labs.
   2. I took notes and prepare content from course slides. They covered the important concept and slides is a good resource for quick review of concepts
   3. Read SageMaker documents, AWS services hoepages and internet resources, if you did not understand some concepts.
   4. Attemped the Full test from the the same course providers and i failed.
   5. Checked the concepts where i was lagging or made mistake and read more about these concepts and took notes.
2. Stage 2
   1. Visited relevant AWS Services and read about the use cases or examples and took notes
   2. Attempted the Whizlab full test one
   3. Read through the explanation of every question even for those where i was correct. These explainations have link for the concepts that i read to have more understanding.
   4. Attempted the Whizlab full test two and did the same as previous step.
   5. At this stage i was quite confident about different concepts. I took alot of notes that i have put in later section
3. Stage 3
   1. In the last week before my exam, I took one week to read AWS ML blogs, other online resources to have clear understanding of different concepts and which service is better in which scenario.
   2. Attempted again all three full tests and found the concepts where i need to read more
   3. At the end i went through these samples [questions](https://www.examtopics.com/exams/amazon/aws-certified-machine-learning-specialty/). These are some real AWS exam questions
   4. Now after all this i was feeling very confident.

## Tips

1. Read Question and options very carefully. Try to read question two times. Since this exam duration is 3 hours, you will have sufficinet time for each question.
2. Check the objective of the question. Is there something that need to be optimized, like cost, time etc.
3. Most of the time, you can discard two options and then answer you can decide by what need to be optimized.
4. Flag, question that you have doubt, come later and check these questions again. Sometimes another question has answer/hint for flagged question.
5. Keep calm, you have enough time

# Notes

## Data Engineering(20%)

Below are the expected concepts that are covered under this section

1. Storage Topics
   - S3 Data Lakes
   - Dynamo DB
2. Data transformation
   - Glue
   - Glue ETL
   - Lambda Function
3. Streaming
   - Kinesis
   - Kinesis Video Streams
4. Workflow
   - Data Pipeline
   - AWS Batch
   - Step Functions

### AWS Storage Gateway

- AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.
- Customers use Storage Gateway to simplify storage management and reduce costs for key hybrid cloud storage use cases.
- These include moving tape backups to the cloud, reducing on-premises storage with cloud-backed file shares, providing low latency access to data in AWS for on-premises applications, as well as various migration, archiving, processing, and disaster recovery use cases.

### Security

#### VPC

- An endpoint is a network component that connects EC2 instances in a VPC to certain AWS services without requiring public IP addresses.(keep traffic within the AWS network)
- With a VPC endpoint, instances don't need a NAT device, VPN connection, internet gateway
- Two types of VPC Endpoints
  - Interface Endpoint
    - allows a private IP address in a subnet to connect VPC resources to a number of AWS services (ex Sagemaker)
    - Traffic from VPC resources to --> endpoint network interface,AWS PrivateLink then enables the endpoint to connect the → traffic to other services without going over the internet.
  - Gateway Endpoint
    - a target for a route in a route table to connect VPC resources to S3 or DynamoDB.
    - Traffic is then routed from instances in a subnet to one of these two services.
    - Gateway endpoints do not use PrivateLink
- **Subnet**
  - A subnet, or subnetwork, is a segmented piece of a larger network or VPC here
  - If a subnet's traffic is routed to an internet gateway, the subnet is known as a public subnet.
  - If a subnet doesn't have a route to the internet gateway, the subnet is known as a private subnet.

### Kinesis Data Stream

- low latency streaming ingest at scale
- Streams divided into shards
  - Each shard has a sequence of data records.
  - Data records are composed of a sequence number, a partition key, and a data blob
  - A partition key is used to group data by shard within a stream
  - Sequence number is unique per partition-key within its shard
  - The longer the time period between write requests, the larger the sequence numbers become
  - Record can be upto 1 MB
- Data Retention is 24 hours by default and can go upto 7 days
- Multiple apps can consume same data
- These consumers are known as Amazon Kinesis Data Streams Application.
- Once data is inserted in Kinesis it cant be deleted
- Kinesis Client Library (KCL)
  - It is compiled into your application to enable fault-tolerant consumption of data from the stream
- Two types of consumers: shared fan-out and enhanced fan-out consumers.
- Monitor the stream service with CloudWatch
- **PutRecord**:
  - Write a single data record into an Amazon Kinesis data stream.
  - Call PutRecord to send data into the stream for real-time ingestion and subsequent processing, one record at a time

#### **Scenarios for using Kinesis Data Streams:**

- Accelerated log and data feed intake and processing
- Real-time metrics and reporting
- Real-time data analytics
- Complex stream processing
  - This typically involves putting data from multiple Kinesis Data Streams applications into another stream for downstream processing by a different Kinesis Data Streams application.

#### **Benefits of Using Kinesis Data Streams**

- A common use is the real-time aggregation of data followed by loading the aggregate data into a data warehouse or map-reduce cluster.
- The delay between the time a record is put into the stream and the time it can be retrieved (put-to-get delay) is typically less than 1 second
- **Its fully managed and that makes it very flexible for increasing and decreasing data stream capacity**

#### Security in Kinesis Data Stream

**Server-side encryption**

- It automatically encrypts data before it's at rest by using an AWS KMS customer master key (CMK) you specify.
- Data is encrypted before it's written to the Kinesis stream storage layer, and decrypted after it’s retrieved from storage

### Kinesis Data Analytics:

- perform real time analytics on streaming using SQL
  Amazon Kinesis Data Analytics provides built-in functions to filter, aggregate, and transform streaming data for advanced analytics with SQL or Flink
- 2 ML services that works inside/along with it
  - Random_cut_forest
    - Anomaly detection
  - HOTSPOT
    - Locate and return dense region of the data
- create a Kinesis data analytics application that continuously reads and processes streaming data
- The service supports ingesting data from Amazon Kinesis Data Streams and Amazon Kinesis Data Firehose streaming sources.

- Amazon Kinesis Data Analytics needs permissions to read records from a streaming source and write application output to the external destinations. You use IAM roles to grant these permissions.
- Kinesis Data Analytics automatically provides an in-application error stream for each application.
- Amazon Kinesis Data Analytics ensures that your application output records are written to the configured destination. It uses an "at least once" processing and delivery model

### Kinesis Firehose:

- It can capture, transform, and load streaming data in to S3, Readshift, ElasticSearch & Splunk
  - Amazon Kinesis Data Firehose CAN CONVERT THE FORMAT OF YOUR input data from JSON to Apache Parquet or Apache ORC before storing the data in Amazon S3.
  - If you want to convert an input format OTHER THAN JSON, SUCH AS CSV or structured text, you can use AWS Lambda to transform it to JSON first.
- Fully managed
- It can also batch, compress, transform, and encrypt the data before loading it, minimizing the amount of storage
- You can also configure your delivery stream to automatically convert the incoming data to columnar formats like Apache Parquet and Apache ORC, before the data is delivered to Amazon S3, for cost-effective storage and analytics.
- **Data Injection not streaming**
- **Near Real Time**
- If record format conversion is enabled, Kinesis Data Firehose can deliver data to Amazon S3 only.

- Kinesis Data Firehose delivery stream
- Use Kinesis Data Firehose by creating a Kinesis Data Firehose delivery stream and then sending data to it
- Kinesis Data Firehose buffers incoming streaming data to a certain size or for a certain period of time before delivering it to destinations. Buffer Size is in MBs and Buffer Interval is in seconds.
- For Amazon Redshift destinations, streaming data is delivered to your S3 bucket first. Kinesis Data Firehose then issues an Amazon Redshift COPY command to load data from your S3 bucket to your Amazon Redshift cluster.
- Record: The data of interest that your data producer sends to a Kinesis Data Firehose delivery stream. A record can be as large as 1,000 KB
- Use the following access policy to enable Kinesis Data Firehose to access your S3 bucket and AWS KMS key. **If you don't own the S3 bucket, add s3:PutObjectAcl to the list of Amazon S3 actions**, which grants the bucket owner full access to the objects delivered by Kinesis Data Firehose
- Kinesis Data Firehose can invoke your Lambda function to transform incoming source data and deliver the transformed data to destinations
- The buffer interval hints range from **60 seconds to 900 seconds**

### GLUE

- AWS Glue is serverless. Uses other AWS services to **orchestrate your ETL jobs** to build a data warehouse. It is designed to work with **semi-structured** data.
- It introduces a component called a **dynamic frame**, which you can use in your ETL scripts. A dynamic frame is similar to an Apache Spark dataframe, except that each record is self-describing, so no schema is required initially.

- Serverless ETL jobs run in Isolation
  - During provisioning of an ETL job, you provide input data sources and output data targets in your virtual private cloud (VPC).
  - In addition, you provide the IAM role, VPC ID, subnet ID, and security group that are needed to access data sources and targets.
  - For each tuple (customer account ID, IAM role, subnet ID, and security group), AWS Glue creates a new Spark environment that is isolated at the network and management level from all other Spark environments inside the AWS Glue service account.
- Glue has crawlers and classifiers that it use to find the schema of a data source.
- Classifiers
  - Determines the schema of data use classifiers when you crawl a data store to define metadata tables in the AWS Glue Data Catalog.
  - AWS Glue provides classifiers for common file types, such as CSV, JSON, AVRO, XML, and others
  - It also provides classifiers for common relational database management systems using a JDBC connection.
  - You can write your own classifier by using a grok pattern or by specifying a row tag in an XML document.
- Crawlers
  - A program that connects to a data store (source or target), progresses through a prioritized list of classifiers to determine the schema for your data, and then creates metadata tables in the AWS Glue Data Catalog
  - Crawlers can crawl both file-based and table-based data stores.

**What happens when a crawler runs?**

- Classifies data to determine the format, schema, and associated properties of the raw data
  - You can configure the results of classification by creating a custom classifier.
- Groups data into tables or partitions
- Write Metadata to the data catalog
  - You can configure how the crawler adds, updates, and deletes tables and partitions.
  - When the majority of schemas at a folder level are similar, the crawler creates partitions of a table instead of two separate tables.
  - To influence the crawler to create separate tables, add each table's root folder as a separate data store when you define the crawler.

**How Does a Crawler Determine When to Create Partitions?**

When an AWS Glue crawler scans Amazon S3 and detects multiple folders in a bucket, it determines the root of a table in the folder structure and which folders are partitions of a table

**How classifiers in a crawler work?**

- A classifier reads the data in a data store. If it recognizes the format of the data, it generates a schema with a certentity number to indicate how certain the format recognition was.
- AWS Glue invokes custom classifiers first, in the order that you specify in your crawler definition. Depending on the results that are returned from custom classifiers, AWS Glue might also invoke built-in classifiers.
- If a classifier returns certainty=1.0 during processing, AWS Glue then uses the output of that classifier.
- If no classifier returns certainty=1.0, AWS Glue uses the output of the classifier that has the highest certainty.
- If no classifier returns a certainty greater than 0.0, AWS Glue returns the default classification string of UNKNOWN.
- If you change a classifier definition, any data that was previously crawled using the classifier is not reclassified.

#### Glue ETL

- AWS Glue can generate a script to transform your data. Or, you can provide the script in the AWS Glue console or API
  - Generate code in different language Python, Pyspark
- Bundled Transformation: DropFields, DropNullFienls, filter join and map
- Nothing to worry about Spark cluster, because it is fully managed
- Transformation
  - ML transformation:
    1. FindMatchML: identify duplicate or matching records in dataset, even they do not match exactly
    2. Each FindMatches transform must be taught what should be considered a match and what should not be considered a match. You teach your transform by adding labels to a file and uploading your choices to AWS Glue.
    3. Each FindMatches transform contains an accuracy-cost parameter. You can use this parameter to specify one of the following:
       - If you are more concerned with the transform accurately reporting that two records match, then you should emphasize accuracy
       - If you are more concerned about the cost or speed of running the transform, then you should emphasize lower cost.
       - The labelling file must be encoded as UTF-8 without BOM(byte order mask)
       - Labelling file in CSV format

#### When Should i use GLUE?

1. Use AWS Glue to organize, cleanse, validate, and format data for storage in a data warehouse or data lake
   - Transform and move AWS Cloud data into your data store
   - Load data from disparate sources into your data warehouse or data lake for regular reporting and analysis
2. When you run serverless queries against your Amazon S3 data lake
   - AWS Glue can catalog your Amazon S3 data, making it available for querying with Amazon Athena and Amazon Redshift Spectrum.
   - With crawlers, your metadata stays in sync with the underlying data.
   - Access and analyze data through one unified interface without loading it into multiple data silos.
3. Create event-driven ETL pipelines with AWS Glue
   - Run your ETL jobs as soon as new data becomes available in Amazon S3 by invoking your AWS Glue ETL jobs from an AWS Lambda function.
   - Register this new dataset in the AWS Glue Data Catalog as part of your ETL jobs.
4. Use AWS Glue to understand your data assets
   - Store data using various AWS services and still maintain a unified view of your data using the AWS Glue Data Catalog
   - View the Data Catalog to quickly search and discover the datasets that you own, and maintain the relevant metadata in one central repository.

### Data Pipeline

- AWS Data Pipeline is a web service that you can use to automate the movement and transformation of data
- With AWS Data Pipeline, you can define data-driven workflows, so that tasks can be dependent on the successful completion of previous tasks
- Pipeline Definition: A pipeline definition is how you communicate your business logic to AWS Data Pipeline
  - From your pipeline definition, AWS Data Pipeline determines the tasks, schedules them, and assigns them to task runners.
  - If a task is not completed successfully, AWS Data Pipeline retries the task according to your instructions and, if necessary, reassigns it to another task runner.

#### Use case example

Use AWS Data Pipeline to archive your web server's logs to Amazon S3 each day and then run a weekly Amazon EMR (Amazon EMR) cluster over those logs to generate traffic reports. AWS Data Pipeline schedules the daily tasks to copy data and the weekly task to launch the Amazon EMR cluster. AWS Data Pipeline also ensures that Amazon EMR waits for the final day's data to be uploaded to Amazon S3 before it begins its analysis, even if there is an unforeseen delay in uploading the logs.

![Use Case](./images/pipeline.jpg)

### AWS Batch

- AWS Batch enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS
- Serverless
- Run batch as docker images
- Prefer non ETL jobs in batch
  - Configure resources and schedule data analytics
- For any computing job regardless of the job
- Using EC2 instances

![AWS Batch](./images/batch.jpg)

### AWS Step Function

- To design each step of the execution, workflow.
- Build Distributed Applications Using Visual Workflows.
- AWS Step Functions makes it easy to coordinate the components of distributed applications and microservices using visual workflows.
- Use to design workflow
- Audit of history workflow
- Advanced error and try mechanism
- In batch job where we check success and failure

## Exploratory Data Analysis(24%)

**Key Performance Indicator**

- **Net Promoter Score (NPS)**:How likely is it for a customer to recommend your product or service to a friend?
- **Customer Profitability Score (CPS)**: How much profit does a customer bring to your business after deducting customer acquisition and customer retention costs?
- **Conversion Rate**: How many leads get converted to customers?
  Relative Market Share: How big is your slice of the pie compared to your competitors in the market?
- **Net Profit Margin:** The percent of your revenue which is net profit.

**Relationships Plot**

- Scatter Plot (**For two variables**):
  Relating Marketing Spend to Sales Revenue. Here you could show Marketing Spend on the X-axis and Sales Revenue on the Y-axis.
- Bubble Chart (**Three variables**):
  Relating ROI, Investment Time, and Investment Size. Here the X-axis would be the Investment Time, the Y-axis would be ROI, and the size of the Bubble would be Investment Size.

### AWS Athena

- An interactive query service to analyse data in S3 without loading data, data stays in S3
- Serverless
- Support different data formats
- It can be integrated with Jupyter, Zeppelin etc
- Use Case: Web logs, CloudTrail, querying staging data before loading to a data warehouse
- Integrate with QuickSight and other tool with JDBC/ODBC
- **Keeping data in columnar format or compressed like Parquet format reduce the cost because it can find data directly what it need**
- Example pipeline with Glue+Athena+Quicksight
- **Do not use Athena for Highly formatted reports because QuickSight do that**

### QuickSight

- Business Analytics Platform
- A simple user in an org can use it for data insight
- Serverless
- Provides some limited ETL
- SPICE
  - Powerful in memory calculation engine for QuickSight
  - Each user gets 10 GB of SPICE
  - Scalable
- USE Cases
  - Dashboard and KPI
  - Can connect to different other tools like SaaS
- Machine Learning Insights: Feature in QuickSight
  - Anomaly Detection
  - Forecasting
  - Auto-narratives: Build Story from data automatically
- Visual Types
  - Heat Maps: Correlation
  - Pie Charts: Aggregation
  - Tree map: Hierarchical Aggregation: Pie charts within pie charts
  - Bar Charts: Comparison and distribution
  - Line Graph: Changes over time
    \*Scatter Map: For correlation

### Different Visualization Types

![visualization](images/visualization.png)

## Modeling(36%)

### SageMaker

- Amazon SageMaker Studio
  - An integrated machine learning environment where you can build, train, deploy, and analyze your models all in the same application.
- Amazon SageMaker Ground Truth
  - High-quality training datasets by using workers along with machine learning to create labeled datasets.
- Amazon Augmented AI
  - Human-in-the-loop reviews
- Amazon SageMaker Studio Notebooks
  - The next generation of Amazon SageMaker notebooks that include SSO integration, fast start-up times, and single-click sharing.
- Preprocessing
  - Analyze and pre-process data, tackle feature engineering, and evaluate models.
- Amazon SageMaker Experiments
  - Experiment management and tracking. You can use the tracked data to reconstruct an experiment, incrementally build on experiments conducted by peers, and trace model lineage for compliance and audit verifications.
- Amazon SageMaker Debugger
  - Inspect training parameters and data throughout the training process. Automatically detect and alert users to commonly occurring errors such as parameter values getting too large or small.
  - Custom rules to detect unwanted conditions while training
- Amazon SageMaker Autopilot
  - Users without machine learning knowledge can quickly build classification and regression models.
- Reinforcement Learning
  - Maximize the long-term reward that an agent receives as a result of its actions.
- Batch Transform
  - Preprocess datasets, run inference when you don't need a persistent endpoint
  - To get predictions for an entire dataset, use Amazon SageMaker batch transform.
- Amazon SageMaker Model Monitor
  - Monitor and analyze models in production (endpoints) to detect data drift and deviations in model quality.
- Amazon SageMaker Neo
  - Train machine learning models once, then run anywhere in the cloud and at the edge.
- Amazon SageMaker Elastic Inference
  - Speed up the throughput and decrease the latency of getting real-time inferences.
  - Attach low cost GPU-powered acceleration to EC2, SM instances or ECS tasks.
  - scale the amount of inference acceleration up and down using Amazon EC2 Auto Scaling groups
  - Reduce cost of inference by 70%

### Built-in Algorithms/Services

#### Factorization Machines Algorithm

- General purpose supervised learning algo that can be used
  Classification
- Binary classification problem, the algorithm predicts a score and a label
- Regression
- It is good for tasks dealing with High Dimensional Sparse Dataset.
- Recommended training and inference with CPU instances for both sparse and dense datasets
- Example use case: click prediction and item recommendations

#### Linear Learner Algorithm

- Supervised learning algorithm
- Used for classification and regression problem
  - Use threshold function for classification
  - Can do binary and multi-class
- Mail campaign, can classify digits
- Inference format: Classification model: score and class
- **Data must be normalized**
- By default score can be interpreted as probabilities because loss is Logistics for binary and softmax for multiclass classification
- If loss is set to hinge_loss, then the score cannot be interpreted as a probability. This is because hinge loss corresponds to a Support Vector Classifier, which does not produce probability estimates.
- Steps:
  - Preporcess: For best results, ensure your data is shuffled before training. Training with unshuffled data may cause training to fail.
  - It has a normalization option that could be used to normalize data before training.
  - Normalization is enabled by default for both features and labels for regression.
  - Train
    - SGD for optimization by default
    - supports both recordIO-wrapped protobuf(Float32 only) and CSV formats, File and Pipe mode( stream in from S3 for large data)
    - When its taking to long to start with training that means data is not loaded and there we can use Pipe Mode
- By default, the linear learner algorithm tunes hyperparameters by training multiple models in parallel.
- Training: Multi GPU does not help, though single and multi machine CPU and GPU could be used

**Important Hyperparameters**

- **Optimizer:**
  - _auto_—The default value.
  - _sgd—Stochastic_ gradient descent.
  - _adam_—Adaptive momentum estimation
  - _rmsprop_—A gradient-based optimization technique that uses a moving average of squared gradients to normalize the gradient
  - _Default value_: auto. The default setting for auto is adam.
- **Positive_example_weight_mult**
  - The weight assigned to positive examples when training a binary classifier
  - If you want the algorithm to choose a weight so that errors in classifying negative vs. positive examples have equal impact on training loss, specify balanced.
  - If you want the algorithm to choose the weight that optimizes performance, specify auto.
- **Loss**
  - If the _predictor_type_ is set to _regressor_, the available options are
    - Auto: The default value for auto is squared_loss.
    - Squared_loss
    - Absolute_loss
    - Eps_insensitive_squared_loss
    - Eps_insensitive_absolute_loss
    - Quantile_loss
    - huber_loss.
  - If the _predictor_type_ is set to _binary_classifier_, the available options are
    - _Auto_: The default value for auto is logistic.
    - Logistic
    - hinge_loss
  - If the _predictor_type_ is set to _multiclass_classifier_, the available options are
    - _Auto_: The default value for auto is softmax_loss.
    - softmax_loss

#### XGBoost

As a framework: XGBoost algorithm can be used as a built-in algorithm or as a framework such as TensorFlow

- more flexible than using it as a built-in algorithm
  enables more advanced scenarios that allow pre-processing and post-processing scripts to be incorporated into your training script.

- Newer version(0.9) because inbuilt has old one(0.72 )
- We have to specify framework version while using it, not set default
- Feature importance is defined only for base learner or tree booster, not defined for linear learner
- **Inference point built using XGBoost only support test/csv or text/libsvm
  **
  **Hyperparameter**

## Machine Learning Implementation and Operation (20%)

![SageMaker](images/sagemaker-architecture.png)

**Training Data Format**

- To use data in CSV format for training, in the input data channel specification, specify text/csv as the ContentType.
- Amazon SageMaker requires that a CSV file doesn't have a header record and that the target variable is in the first column
- To run unsupervised learning algorithms that don't have a target, specify the number of label columns in the content type. For example, in this case 'text/csv;label_size=0'
- Most Amazon SageMaker algorithms work best when you use the optimized protobuf recordIO format for the training data.
- Using this format allows you to take advantage of Pipe mode when training the algorithms that support it
- _Pipe Mode_
  - In Pipe mode, your training job streams data directly from Amazon S3.
  - Streaming can provide faster start times for training jobs and better throughput.
  - It reduces the size of the Amazon Elastic Block Store volumes for your training instances.
  - Pipe mode needs only enough disk space to store your final model artifacts
- _File Mode_
  - loads all of your data from Amazon Simple Storage Service (Amazon S3) to the training instance volumes.
  - File mode needs disk space to store both your final model artifacts and your full training dataset
- **All models in SageMaker is hosted in a docker containers**
- **Distributed training via Horovod for Tensorflow**
- Use Production Variant to test multiple model on live traffic (first test with 5% and then ramp up to 100% if everythings works well)

### Inference pipeline

- Sagemaker inference pipeline allows user to bundle and export pre and post processing steps from training process and deploy them as inference pipeline
- It is fully managed service
- Inference pipeline are immutable
- Use *UpdateEndpoint API *to change a running inference pipeline

### How Amazon SageMaker Runs Custom (not built in model) Inference Image

#### Load model artifacts

- In your CreateModel request, the container definition includes the ModelDataUrl parameter, which identifies the S3 location where model artifacts are stored.
- It copies the artifacts to the /opt/ml/model directory for use by your inference code
- Set environment in docker file by setting SAGEMAKER_PROGRAM train.py
- SAGEMAKER_PROGRAM train.py defines train.py as the name of the entrypoint script that is located in the /opt/ml/code folder for the container. This is the only environmental variable that you must specify when you are using your own container.
- The ModelDataUrl must point to a tar.gz file. Otherwise, Amazon SageMaker won't download the file.

#### Serve Requests

- Containers need to implement a web server that responds to /invocations and /ping on port 8080

**_How Container respond to Inference Request_**

- To obtain inferences, the client application sends a POST request to the Amazon SageMaker endpoint
- Amazon SageMaker strips all POST headers except those supported by InvokeEndpoint. Amazon SageMaker might add additional headers. Inference containers must be able to safely ignore these additional headers.
- To receive inference requests, the container must have a web server listening on port 8080 and must accept POST requests to the /invocations endpoint.
- **A customer's model containers must accept socket connection requests within 250 ms.**
- **A customer's model containers must respond to requests within 60 seconds**. The model itself can have a maximum processing time of 60 seconds before responding to the /invocations. If your model is going to take 50-60 seconds of processing time, the SDK socket timeout should be set to be 70 seconds

**_How Container Should Respond to Health Check (Ping) Requests_**

- GET requests to the /ping endpoint
- The simplest requirement on the container is to respond with an HTTP 200 status code and an empty body. This indicates to Amazon SageMaker that the container is ready to accept inference requests at the /invocations endpoint.

### SageMaker on the Edge

- Amazon Neo for Edge devices.
- Train on AWS and compile with Neo that could further used with GreenGrass
  Amazon GreenGrass for IoT devices

### SageMaker Security

#### Secure model building data

1. Use Encrypted S3 for ML storage and use KMS key to Sagemaker while communicating with different services such as notebooks, processing jobs, training jobs, hyperparameter tuning jobs, batch transform jobs, and endpoints
2. How do different services handle security?
   - Processing, batch transform, and training job containers; when the job completes output is uploaded to S3 using KMS Key and instance is torn down
   - Sagemaker automatically saves Notebook data in ML storage volume /home/ec2-user/SageMaker
3. Give IAM permission to SageMaker to access

_How Amazon SageMaker works with IAM?_

- Amazon SageMaker doesn't support service-linked roles
- Amazon SageMaker does not support resource-based policies
- Authorization based on SageMaker Tags

#### Secure Transit Data

_How to secure internode training communications and what are their implications?_

- Enable internode encryption (TLS 1.2)
  - Increase training time and cost. Especially for distributed deep learning algorithms.
  - Training time for built-in algorithms such as XGBoost, DeepAR and linear learner are not affected
- There is no internode communication for batch processing

#### Infrastructure Security

1. If you disable direct internet access, the notebook instance won't be able to train or host models unless your VPC has an interface endpoint (PrivateLink) or a NAT gateway and your security groups allow outbound connections.
2. As a root user of Notebook, users have access for installing packages and other pertinent software. To limit the access, grant a user access to a notebook with an IAM policy

**Training and Inference Containers Run in Internet Free Mode**

- Amazon SageMaker training and deployed inference containers are internet-enabled by default.
- Use network isolation to restrict internet access
- Use network isolation with VPC
  - In this scenario, download and upload of customer data and model artifacts are routed via your VPC subnet.
  - However, the training and inference containers themselves continue to be isolated from the network, and do not have access to any resource within your VPC or on the internet.

#### SageMaker and VPC Configuration

_IT IS VERY IMP TO UNDERSTAND THIS CONCEPT, THERE WERE 4-5 QUESTIONS RELATED TO THIS CONCEPT_

- Amazon SageMaker notebook instances can be launched with or without your [Virtual Private Cloud (VPC)](https://aws.amazon.com/vpc/) attached.
- When launched with your VPC attached, the notebook can either be configured with or without direct internet access.
- _With VPC and Direct Internet Access_
  - SageMaker provides a network interface that allows the notebook to communicate with the internet through a VPC managed by Amazon SageMaker.
  - Traffic to Gateway VPC Endpoints like Amazon S3 and DynamoDB will go through the public internet
  - Traffic to Interface VPC Endpoints will still go through your VPC.
  - If you want to use Gateway VPC Endpoints, you may want to disable direct internet access
- _With VPC and without Internet Access_
  - the notebook instance can still be configured to access the internet
  - It needs to either be in a private subnet with a NAT or to access the internet back through a virtual private gateway.

#### Deployment best practices

- Create robust endpoints while hosting models. to achieve more reliable performances use more small Instance Types in different AZ to host endpoints
  - Distribute instances across multiple Availability zones
  - If you are using VPC, configure VPC with at least two subnets each in different Availability zones
