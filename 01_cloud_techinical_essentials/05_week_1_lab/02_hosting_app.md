# Hosting employee app on AWS

## Launching the app
1. Navigate to `EC2` on AWS console
2. Launch instance:
    - Give it a name
    - Select `OS`
    - Select image and architecture
    - Select instance type
    - Configure Key pair for using `ssh` inside the instance
    - Configure network
    - Advanced details:
        - Profiles
        - Domain
        - Initialization script (User data)

## Accessing the app
1. Copy the `IP` address
2. Paste it into a new tab

## Example scripts:

### Amazon Linux 2 user data script:

```{bash}
#!/bin/bash -ex
wget 
https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zip
unzip FlaskApp.zip
cd FlaskApp/
yum -y install python3 mysql
pip3 install -r requirements.txt
amazon-linux-extras install epel
yum -y install stress
export PHOTOS_BUCKET=${SUB_PHOTOS_BUCKET}
export AWS_DEFAULT_REGION=<INSERT REGION HERE>
export DYNAMO_MODE=on
FLASK_APP=application.py /usr/local/bin/flask run --host=0.0.0.0 --port=80
```

### Amazon Linux 2023 user data script: 

```{bash}
#!/bin/bash -ex
wget 
https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/DEV-AWS-MO-GCNv2/FlaskApp.zip
unzip FlaskApp.zip
cd FlaskApp/
yum -y install python3-pip
pip install -r requirements.txt
yum -y install stress
export PHOTOS_BUCKET=${SUB_PHOTOS_BUCKET}
export AWS_DEFAULT_REGION=<INSERT REGION HERE>
export DYNAMO_MODE=on
FLASK_APP=application.py /usr/local/bin/flask run --host=0.0.0.0 --port=80 
```
