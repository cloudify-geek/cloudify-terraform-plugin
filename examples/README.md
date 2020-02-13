# Examples

After creating a deployment out of refresh-test blueprint 

```shell 
cfy deployments capabilities examples
Retrieving capabilities for deployment examples...
 - "subnet_cidr_block":
     Description:
     Value: 10.0.1.0/24
 - "host_ip":
     Description:
     Value: <IP>
 - "host_instance_type":
     Description:
     Value: t2.micro
 - "subnet_availability_zone":
     Description:
     Value: us-west-1a
 - "host_instance_state":
     Description:
     Value: running
 - "host_availability_zone":
     Description:
     Value: us-west-1a
```

From AWS [console/cli] : stopped the instance and changed type to medium  

then to reflect the changes to cloudify 

```shell
cfy executions start refresh_terraform_resources -d examples -p '{"node_ids": ["aws_two_tier_example"]}'
<truncated>
.... INFO: Running: [u'/usr/bin/terraform', 'state', 'pull']
<truncated>
          "aws_instance.web": {
                    <truncated>
                    "primary": {
                        "id": "i-0b6a4a607b8d741fd",
                        "attributes": {
                            <truncated>
                            "instance_state": "stopped",
                            "instance_type": "t2.medium",
                            <truncated>
                            "public_ip": "",
                            <truncated>
                        },
```
if we check the capabilites after 
```shell
cfy deployments capabilities examples
Retrieving capabilities for deployment examples...
 - "subnet_cidr_block":
     Description:
     Value: 10.0.1.0/24
 - "host_ip":
     Description:
     Value:
 - "host_instance_type":
     Description:
     Value: t2.medium
 - "subnet_availability_zone":
     Description:
     Value: us-west-1a
 - "host_instance_state":
     Description:
     Value: stopped
 - "host_availability_zone":
     Description:
     Value: us-west-1a
```
