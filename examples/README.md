# Examples

After creating a deployment out of refresh-test blueprint 

if you change any properties from AWS console on subnet or EC2 instance you can reflect the new changes by : 

```shell
cfy executions start refresh_terraform_resources -d examples -p '{"node_ids": ["aws_two_tier_example"]'
```
