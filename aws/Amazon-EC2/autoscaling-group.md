# `aws-cli` Commands for Autoscaling Group

## Fetch `instance id`

```bash
aws ec2 describe-instances --instance-ids i-0f0fc236752a0a4dc --query 'Reservations[*].Instances[*].PrivateIpAddress' --output text
``` 

## Get `private ip address`

### AMI filtering

```bash
aws ec2 describe-instances --region eu-central-1 --filters "Name=image-id, Values=ami-08224697d0bdcb5e4" | jq '.Reservations[0].Instances[0].PrivateIpAddress'
```
### Tag filtering

```bash
aws ec2 describe-instances --region eu-central-1 --filters "Name=tag:Name,Values=runner-*" | jq '.Reservations[0].Instances[0].PrivateIpAddress'
```

## Get `instance id`

```bash
aws ec2 describe-instances --region eu-central-1 --filters "Name=tag:Name,Values=test" | jq '.Reservations[0].Instances[0].InstanceId'
```

## Add Instance into Autoscaling Group

```bash
aws autoscaling attach-instances --instance-ids i-0f0fc236752a0a4dc --auto-scaling-group-name test-gitlab-runner
```

## Check if the instances is assign to the autoscaling group

```bash
aws autoscaling describe-auto-scaling-groups --auto-scaling-group-names test-gitlab-runner-ag | jq .'AutoScalingGroups[0].Instances'
```