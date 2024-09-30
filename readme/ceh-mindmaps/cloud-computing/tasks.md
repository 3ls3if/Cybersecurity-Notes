# Tasks

## Perform S3 Bucket Enumeration

### Enumerate S3 Buckets using lazys3

Use the lazys3 tool to find publicly accessible S3 buckets of a target organization HackerOne. Flag submission is not required for this task, enter "No flag" as the answer.

No flag

```
ruby lazys3.rb

ruby lazys3.rb HackerOne
```



### Enumerate S3 Buckets using S3Scanner

Use the S3Scanner tool to enumerate open S3 buckets. What is the size (in bytes) of a publicly accessible S3 bucket owned by flaws.cloud?

25621

```
python3 ./s3scanner.py sites.txt
```



## Exploit S3 Buckets

### Exploit Open S3 Buckets using AWS CLI

Use the AWS CLI tool to exploit open S3 buckets (certifiedhacker1) in the AWS service. Find the total number of files available in the “certifiedhacker1” S3 bucket. Note: You must create an AWS account (https://aws.amazon.com) to perform this task. Flag submission is not required for this task, enter "No flag" as the answer.

No flag



## Perform Privilege Escalation

### Escalate IAM User Privileges

Escalate IAM user privileges by exploiting a misconfigured user policy. Which aws command will list all user policies?

```
aws iam list-user-policies
```

