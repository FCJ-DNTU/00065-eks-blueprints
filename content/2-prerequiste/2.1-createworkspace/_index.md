---
title : "Create workspace"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Create workspace

1.  Go to [AWS Management Console](https://aws.amazon.com/en/console/)
    
    *   Find **Cloud9**
    *   Select **Cloud9**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0001.png?featherlight=false&width=90pc)

2.  Select **Create environment**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0002.png?featherlight=false&width=90pc)

3.  In the **Create environment** interface
    
    *   **Name**, enter **`eks-blueprints-cdk-workshop`**
    *   Select **Next step**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0003.png?featherlight=false&width=90pc)

4.  In the **Configure settings** interface
    
    *   Select **Create a new EC2 instance for environment (direct access)**
    *   Select **t3.small (2 GiB RAM + 2 vCPU)**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0004.png?featherlight=false&width=90pc)

5.  Select **Next step**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0005.png?featherlight=false&width=90pc)

6.  Select **Create environment**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0006.png?featherlight=false&width=90pc)

7.  Finish creating **Cloud9** environment.

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0007.png?featherlight=false&width=90pc)

#### Increase disk size for Cloud9 instance

To execute **Copy** code, we use **Ctrl + V** for **Windows** or **Command + V** for **Mac**

1.  Copy the following code and paste it into **Cloud9**

```
pip3 install --user --upgrade boto3
export instance_id=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
python -c "import boto3
import os
from botocore.exceptions import ClientError 
ec2 = boto3.client('ec2')
volume_info = ec2.describe_volumes(
    Filters=[
        {
            'Name': 'attachment.instance-id',
            'Values': [
                os.getenv('instance_id')
            ]
        }
    ]
)
volume_id = volume_info['Volumes'][0]['VolumeId']
try:
    resize = ec2.modify_volume(    
            VolumeId=volume_id,    
            Size=30
    )
    print(resize)
except ClientError as e:
    if e.response['Error']['Code'] == 'InvalidParameterValue':
        print('ERROR MESSAGE: {}'.format(e))"
if [ $? -eq 0 ]; then
    sudo reboot
fi
```

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0008.png?featherlight=false&width=90pc)