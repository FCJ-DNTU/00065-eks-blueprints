---
title : "Tạo workspace"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Tạo workspace

1.  Truy cập [AWS Management Console](https://aws.amazon.com/vi/console/)
    
    *   Tìm **Cloud9**
    *   Chọn **Cloud9**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0001.png?featherlight=false&width=90pc)

2.  Chọn **Create environment**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0002.png?featherlight=false&width=90pc)

3.  Trong giao diện **Create environment**
    
    *   **Name**, nhập **`eks-blueprints-cdk-workshop`**
    *   Chọn **Next step**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0003.png?featherlight=false&width=90pc)

4.  Trong giao diện **Configure settings**
    
    *   Chọn **Create a new EC2 instance for environment (direct access)**
    *   Chọn **t3.small (2 GiB RAM + 2 vCPU)**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0004.png?featherlight=false&width=90pc)

5.  Chọn **Next step**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0005.png?featherlight=false&width=90pc)

6.  Chọn **Create environment**

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0006.png?featherlight=false&width=90pc)

7.  Hoàn thành tạo **Cloud9** environment.

![Create Workspace](/images/2-Prerequiste/2.1-Createworkspace/0007.png?featherlight=false&width=90pc)

#### Tăng size disk cho Cloud9 instance

Thực hiện **Copy** code, chúng ta sử dụng **Ctrl + V** đối với **Windows** hoặc **Command + V** đối **Mac**

1.  Thực hiện sao chép code sau và dán vào **Cloud9**

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