**Example 1: To launch an instance in EC2-Classic**

The following ``run-instances`` example launches a single instance of type ``c3.large``. The key pair and security group must already exist. ::

    aws ec2 run-instances \
        --image-id ami-1a2b3c4d \
        --count 1 \
        --instance-type c3.large \
        --key-name MyKeyPair \
        --security-groups MySecurityGroup

Output::

    {
        "OwnerId": "123456789012",
        "ReservationId": "r-08626e73c547023b1",
        "Groups": [
            {
                "GroupName": "MySecurityGroup",
                "GroupId": "sg-903004f8"
            }
        ],
        "Instances": [
            {
                "Monitoring": {
                    "State": "disabled"
                },
                "PublicDnsName": null,
                "RootDeviceType": "ebs",
                "State": {
                    "Code": 0,
                    "Name": "pending"
                },
                "EbsOptimized": false,
                "LaunchTime": "2018-05-10T08:03:30.000Z",
                "ProductCodes": [],
                "CpuOptions": {
                  "CoreCount": 1, 
                  "ThreadsPerCore": 2
                }, 
                "StateTransitionReason": null, 
                "InstanceId": "i-1234567890abcdef0",
                "ImageId": "ami-1a2b3c4d",
                "PrivateDnsName": null,
                "KeyName": "MyKeyPair",
                "SecurityGroups": [
                    {
                        "GroupName": "MySecurityGroup",
                        "GroupId": "sg-903004f8"
                    }
                ],
                "ClientToken": null,
                "InstanceType": "c3.large",
                "NetworkInterfaces": [],
                "Placement": {
                    "Tenancy": "default",
                    "GroupName": null,
                    "AvailabilityZone": "us-east-1b"
                },
                "Hypervisor": "xen",
                "BlockDeviceMappings": [],
                "Architecture": "x86_64",
                "StateReason": {
                    "Message": "pending",
                    "Code": "pending"
                },
                "RootDeviceName": "/dev/sda1",
                "VirtualizationType": "hvm",
                "AmiLaunchIndex": 0
            }
        ]
    }

**Example 2: To launch an instance in EC2-VPC**

The following ``run-instances`` example launches a single instance of type ``t2.micro`` into the specified subnet. The key pair and the security group must already exist. ::

    aws ec2 run-instances \
        --image-id ami-abc12345 \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --security-group-ids sg-1a2b3c4d \
        --subnet-id subnet-6e7f829e

Output::

    {
        "Instances": [
            {
                "Monitoring": {
                    "State": "disabled"
                },
                "PublicDnsName": "",
                "StateReason": {
                    "Message": "pending",
                    "Code": "pending"
                },
                "State": {
                    "Code": 0,
                    "Name": "pending"
                },
                "EbsOptimized": false,
                "LaunchTime": "2018-05-10T08:05:20.000Z",
                "PrivateIpAddress": "10.0.0.157",
                "ProductCodes": [],
                "VpcId": "vpc-11223344",
                "CpuOptions": {
                    "CoreCount": 1,
                    "ThreadsPerCore": 1
                },
                "StateTransitionReason": "",
                "InstanceId": "i-1231231230abcdef0",
                "ImageId": "ami-abc12345",
                "PrivateDnsName": "ip-10-0-0-157.ec2.internal",
                "SecurityGroups": [
                    {
                        "GroupName": "MySecurityGroup",
                        "GroupId": "sg-1a2b3c4d"
                    }
                ],
                "ClientToken": "",
                "SubnetId": "subnet-6e7f829e",
                "InstanceType": "t2.micro",
                "NetworkInterfaces": [
                    {
                        "Status": "in-use",
                        "MacAddress": "0a:ab:58:e0:67:e2",
                        "SourceDestCheck": true,
                        "VpcId": "vpc-11223344",
                        "Description": "",
                        "NetworkInterfaceId": "eni-95c6390b",
                        "PrivateIpAddresses": [
                            {
                                "PrivateDnsName": "ip-10-0-0-157.ec2.internal",
                                "Primary": true,
                                "PrivateIpAddress": "10.0.0.157"
                            }
                        ],
                        "PrivateDnsName": "ip-10-0-0-157.ec2.internal",
                        "Attachment": {
                            "Status": "attaching",
                            "DeviceIndex": 0,
                            "DeleteOnTermination": true,
                            "AttachmentId": "eni-attach-bf87ca1f",
                            "AttachTime": "2018-05-10T08:05:20.000Z"
                        },
                        "Groups": [
                            {
                                "GroupName": "MySecurityGroup",
                                "GroupId": "sg-1a2b3c4d"
                            }
                        ],
                        "Ipv6Addresses": [],
                        "OwnerId": "123456789012",
                        "SubnetId": "subnet-6e7f829e",
                        "PrivateIpAddress": "10.0.0.157"
                    }
                ],
                "SourceDestCheck": true,
                "Placement": {
                    "Tenancy": "default",
                    "GroupName": "",
                    "AvailabilityZone": "us-east-1a"
                },
                "Hypervisor": "xen",
                "BlockDeviceMappings": [],
                "Architecture": "x86_64",
                "RootDeviceType": "ebs",
                "RootDeviceName": "/dev/xvda",
                "VirtualizationType": "hvm",
                "AmiLaunchIndex": 0
            }
        ],
        "ReservationId": "r-02a3f596d91211712",
        "Groups": [],
        "OwnerId": "123456789012"
    }

**Example 3: To launch an instance into a non-default subnet and add a public IP address**

The following ``run-instances`` example requests a public IP address for an instance that you're launching into a nondefault subnet. ::

    aws ec2 run-instances \
        --image-id ami-c3b8d6aa \
        --count 1 \
        --instance-type t2.medium \
        --key-name MyKeyPair \
        --security-group-ids sg-903004f8 \
        --subnet-id subnet-6e7f829e \
        --associate-public-ip-address

**Example 4: To launch an instance using a block device mapping**

Add the following parameter to your ``run-instances`` command to specify a file that defines block devices to attach to the new instance::

    --block-device-mappings file://mapping.json

To add an Amazon EBS volume with the device name ``/dev/sdh`` and a volume size of 100, specify the following in mapping.json::

    [
        {
            "DeviceName": "/dev/sdh",
            "Ebs": {
                "VolumeSize": 100
            }
        }
    ]

To add ``ephemeral1`` as an instance store volume with the device name ``/dev/sdc``, specify the following in mapping.json::

    [
        {
            "DeviceName": "/dev/sdc",
            "VirtualName": "ephemeral1"
        }
    ]

To omit a device specified by the AMI used to launch the instance (for example, ``/dev/sdf``), specify the following in mapping.json::

    [
        {
            "DeviceName": "/dev/sdf",
            "NoDevice": ""
        }
    ]

After you create an instance with block devices this way, you can view only the Amazon EBS volumes in your block device mapping by using the console or by running the ``describe-instances`` command. To view all volumes, including the instance store volumes, run the following command from within the instance::

    curl http://169.254.169.254/latest/meta-data/block-device-mapping/

Output::

  ami
  ephemeral1

Note that ``ami`` represents the root volume. To get details about the instance store volume ``ephemeral1``, run the following command from within the instance::

    curl http://169.254.169.254/latest/meta-data/block-device-mapping/ephemeral1

Output::

  sdc

**Example 4: To launch an instance with a modified block device mapping**

You can change individual characteristics of existing AMI block device mappings to suit your needs. Perhaps you want to use an existing AMI, but you want a larger root volume than the usual 8 GiB. Or, you would like to use a General Purpose (SSD) volume for an AMI that currently uses a Magnetic volume.

Start by running the ``describe-images`` command with the image ID of the AMI you want to use to find its existing block device mapping. You should see a block device mapping in the output similar to the following::

    {
        "DeviceName": "/dev/sda1",
        "Ebs": {
            "DeleteOnTermination": true,
            "SnapshotId": "snap-1234567890abcdef0",
            "VolumeSize": 8,
            "VolumeType": "standard",
            "Encrypted": false
        }
    }

You can modify the above mapping by including the modified individual parameters in a block device mapping file. For example, to launch an instance with a modified block device mapping, add the following parameter to your ``run-instances`` command to change the above mapping's volume size and type::

  --block-device-mappings file://mapping.json

Where ``mapping.json`` contains the following (note the change in ``VolumeSize`` from ``8`` to ``100`` and the change in ``VolumeType`` from ``standard`` to ``gp2``)::

    [
        {
            "DeviceName": "/dev/sda1",
            "Ebs": {
                "DeleteOnTermination": true,
                "SnapshotId": "snap-1234567890abcdef0", 
                "VolumeSize": 100,
                "VolumeType": "gp2"
            }
        }
    ]

**Example 5: To launch an instance that includes user data**

You can launch an instance and specify user data that performs instance configuration, or that runs a script. The user data needs to be passed as normal string, base64 encoding is handled internally. The following example passes user data in a file called ``my_script.txt`` that contains a configuration script for your instance. The script runs at launch. ::

    aws ec2 run-instances \
        --image-id ami-abc1234 \
        --count 1 \
        --instance-type m4.large \
        --key-name keypair \
        --user-data file://my_script.txt \
        --subnet-id subnet-abcd1234 \
        --security-group-ids sg-abcd1234 

For more information about launching instances, see `Using Amazon EC2 Instances <http://docs.aws.amazon.com/cli/latest/userguide/cli-ec2-launch.html>`__ in the *AWS Command Line Interface User Guide*.

**Example 6: To launch an instance with an instance profile**

The following ``run-instances`` example shows the use of the ``iam-instance-profile`` option to specify an `IAM instance profile <http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html>`__ by name. ::

    aws ec2 run-instances \
        --iam-instance-profile Name=MyInstanceProfile \
        --image-id ami-1a2b3c4d \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --security-groups MySecurityGroup

**Example 7: To launch an instance with tags**

You can launch an instance and specify tags for the instance, volumes, or both. The following example applies a tag with a key of ``webserver`` and value of ``production`` to the instance. The command also applies a tag with a key of ``cost-center`` and a value of ``cc123`` to any EBS volume that's created (in this case, the root volume). ::

    aws ec2 run-instances \
        --image-id ami-abc12345 \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --subnet-id subnet-6e7f829e \
        --tag-specifications 'ResourceType=instance,Tags=[{Key=webserver,Value=production}]' 'ResourceType=volume,Tags=[{Key=cost-center,Value=cc123}]' 
  
**Example 8: To launch an instance with the credit option for CPU usage of ``unlimited``**
  
You can launch a burstable performance instance (T2 and T3) and specify the credit option for CPU usage for the instance. If you do not specify the credit option, a T2 instance launches with the default ``standard`` credit option and a T3 instance launches with the default ``unlimited`` credit option. The following example launches a t2.micro instance with the ``unlimited`` credit option. ::
  
    aws ec2 run-instances \
        --image-id ami-abc12345 \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --credit-specification CpuCredits=unlimited
  
**Example 9: To launch an instance into a partition placement group**
  
You can launch an instance into a partition placement group without specifying the partition. The following ``run-instances`` example launches the instance into the specified partition placement group. ::

    aws ec2 run-instances \
        --image-id ami-abc12345 \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --subnet-id subnet-6e7f829e \
        --placement "GroupName = HDFS-Group-A"
  
**Example 10: To launch an instance into a specific partition of a partition placement group**
  
You can launch an instance into a specific partition of a partition placement group by specifying the partition number. The following ``run-instances`` example launches the instance into the specified partition placement group and into partition number ``3``. ::
  
    aws ec2 run-instances \
        --image-id ami-abc12345 \
        --count 1 \
        --instance-type t2.micro \
        --key-name MyKeyPair \
        --subnet-id subnet-6e7f829e\
        --placement "GroupName = HDFS-Group-A, PartitionNumber = 3"  

**Example 11: To require the use of Instance Metadata Service Version 2 on a new instance**

The following ``run-instances`` example launches a ``c3.large`` instance with ``metadata-options`` set to ``HttpTokens=required``. Because the secure token header is set to ``required`` for metadata retrieval requests, this opts in the instance to require using IMDSv2 when requesting instance metadata.

**Note:**
- When specifying a value for ``HttpTokens``, you must also set ``HttpEndpoint`` to ``enabled``.
- In the example, the ``--count`` and ``--security-group`` parameters are not included. For ``--count``, the default is ``1``. If you have a default VPC and a default security group, they are used. ::

    aws ec2 run-instances \
        --image-id ami-1a2b3c4d \
        --instance-type c3.large \
        --key-name MyKeyPair \
        --metadata-options "HttpEndpoint=enabled,HttpTokens=required"

For more information, see 'Configuring the Instance Metadata Service <https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#configuring-instance-metadata-service>'__ in the *Amazon Elastic Compute Cloud User Guide for Linux Instances*.

**Example 12: To turn off access to instance metadata on a new instance**

The following ``run-instances`` example launches a ``c3.large`` instance with ``metadata-options`` set to ``HttpEndpoint=disabled``. When the HTTP endpoint of the instance metadata service is set to ``disabled``, access to your instance metadata is turned off regardless of which version of the instance metadata service you are using. You can reverse this change at any time by enabling the HTTP endpoint, using the ``modify-instance-metadata-options`` command.

**Note:** In the example, the ``--count`` and ``--security-group`` parameters are not included. For ``--count``, the default is ``1``. If you have a default VPC and a default security group, they are used. ::

    aws ec2 run-instances \
        --image-id ami-1a2b3c4d \
        --instance-type c3.large \
        --key-name MyKeyPair \
        --metadata-options "HttpEndpoint=disabled"

For more information, see 'Configuring the Instance Metadata Service <https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#configuring-instance-metadata-service>'__ in the *Amazon Elastic Compute Cloud User Guide for Linux Instances*.

**Example 13: To specify the PUT response hop limit on a new instance**

The following ``run-instances`` example launches a ``c3.large`` instance with ``metadata-options`` set to ``HttpTokens=required`` and ``HttpPutResponseHopLimit=3``. Because the secure token header is set to ``required`` for metadata retrieval requests, this opts in the instance to require using IMDSv2 when requesting instance metadata. In this example, ``HttpPutResponseHopLimit=3`` sets the allowable number of network hops for the instance metadata PUT response to ``3``.

**Note:**
- When specifying a value for ``HttpTokens`` or ``HttpPutResponseHopLimit``, you must also set ``HttpEndpoint`` to ``enabled``.
- In the example, the ``--count`` and ``--security-group`` parameters are not included. For ``--count``, the default is ``1``. If you have a default VPC and a default security group, they are used. ::

    aws ec2 run-instances \
        --image-id ami-1a2b3c4d \
        --instance-type c3.large \
        --key-name MyKeyPair \
        --metadata-options "HttpEndpoint=enabled,HttpTokens=required,HttpPutResponseHopLimit=3"

For more information, see 'Configuring the Instance Metadata Service <https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/ec2-instance-metadata.html#configuring-instance-metadata-service>'__ in the *Amazon Elastic Compute Cloud User Guide for Linux Instances*.
