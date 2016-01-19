#### mnawsinaction

cp7 s3
basic commands
```
aws s3 mb s3://name
aws sync localpath s3://name/path
aws cp --recursive s3://name/path localpath
aws s3 rb --force s3://name(may not delete a versioning bucket)
```
Other config
```
aws s3api put-bucket-versioning --bucket bucketname --versioning-configurition Status=Enabled
aws s3api list-object-versions --bucket bucketname
```

cp8 ebs
tweaking performance
```
(testing write)
dd if=/dev/zero of=/mnt/volume/template bs=1M count=1024 conv=fdatasync,notrunc
(testing read)
dd if=/mnt/volume/tempfile of=/dev/null bs=1M count=1024
```

flushing caches(after writing test, do this before doing reading test)
```
echo 3 | tee /proc/sys/vm/drop_caches
```

cp 11
```
aws ec2 terminate-instances --instance-ids $id
```

describe
```
aws ec2 describe-instances --filters "Name=tag:Name,Values=xx" Name=instance-state-code,Values=16" --query "Reservations[0].Instances[0].[InstanceId,PublicIpAddress,PrivateIpAddress,SubnetId]"
```
clean up
```
aws ec2 describe-images --owners self --query Images[0].[ImageId,BlockDeviceMappings[0].Ebs.SnapshotId]
```
```
aws cloudformation delete-stack --stack-name xx
aws cloudformation describe-stacks --stack-name xx
aws ec2 deregister-image --image-id imgid
aws ec2 delete-snapshot --snapshot-id id
```

- cp12
```
aws s3api put-bucket-policy --bucket xx --policy file://link
```
using sqs:
create a url2png app
```
aws s3 mb s3://name
aws s3 website s3://name --index-document index.html --error-document error.html
```
create sqs:
```
aws sqs create-queue name
```
get attr:
```
aws sqs get-queue-attributes --queue-url x --attribute-names x
```

- cp14
one-time scaling action:
```
aws autoscaling put-scheduled-update-group-action --scheduled-action-name scale4 --auto-scaling-group-name nam --start-time "2016-01-01T12:00:00Z" --desired-capicity 4
```
recurrence scaling action:(every day 20:00 UTC)
```
aws autoscaling put-scheduled-update-group-action --scheduled-action-name scale2 --auto-scaling-group-name nam --recurrence "0 20 * * *" --desired-capicity 2
```

ScalingUpPolicy->ADjustmentType->Three properties:
ChangeInCapacity, PercentChangeInCapacity, ExactCapacity

using apache bench to test load balancer:
```
ab -n 1000 -c 2 $urlloadbalancer (1000 requests, 2 threads)
```


