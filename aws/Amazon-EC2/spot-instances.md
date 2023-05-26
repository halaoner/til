# Caveats of Spot Instances

> This topic is related to [Autoscaling GitLab Runner on AWS EC2](https://docs.gitlab.com/runner/configuration/.runner_autoscale_aws/)

The spot instances can be terminated at any time by AWS. 

It may happen that the CI/ CD pipeline hangs for several minutes (time out is 1 hour). This is caused by insufficient amount of requested spot instances. The error may look like the follows:

```bash
[ec2-user@ip-10-0-142-19 ~]$ sudo docker-machine ls
NAME                                                        ACTIVE   DRIVER      STATE   URL   SWARM   DOCKER    ERRORS
runner-x7pdju-v-gitlab-docker-machine-1684162302-78197f1c   -        amazonec2   Error                 Unknown   MissingParameter: The request must contain the parameter InstanceId
                                                            status code: 400, request id: 587029a1-475d-4f55-b020-e1f30009b162
```

or

```bash
[ec2-user@ip-10-0-142-19 ~]$ sudo tail -f /var/log/messages | grep runner
May 15 14:58:24 ip-10-0-142-19 gitlab-runner[73498]: #033[37;1mFailed to process runner                          #033[0;m  #033[37;1mbuilds#033[0;m=0 #033[37;1merror#033[0;m=failed to update executor: no free machines that can process builds #033[37;1mexecutor#033[0;m=docker+machine #033[37;1mrunner#033[0;m=x7PDjU-V
```

## Cannot Provision Spot Instance

> 💡 **INFO** 💡
>
>See the official GitLab documentaton: [Caveats of Spot instances](https://docs.gitlab.com/runner/configuration/runner_autoscale_aws/#caveats-of-spot-instances)

1. You can check AWS Managament Console: `EC2 --> Spot Requests`

2. You can perform a further troubleshooting by running the following command with `--debug` flag (which is actually executed by GitLab Runner Manager when provisioning new docker-machines (EC2 instances)).

```bash
[ec2-user@ip-10-0-142-19 ~]$ sudo docker-machine \
    --debug 
    --bugsnag-api-token=no-report create \
    --driver amazonec2 \
    --amazonec2-access-key=ACCESS_KEY \
    --amazonec2-secret-key=SECRET_KEY \
    --amazonec2-region=eu-central-1 \
    --amazonec2-vpc-id=vpc-123df99ceca1591bd \
    --amazonec2-subnet-id=subnet-dasd33d96ea148a3e \
    --amazonec2-use-private-address=true \
    --amazonec2-tags=aws-gitlab-runner \
    --amazonec2-instance-type=t2.2xlarge \
    --amazonec2-private-address-only=true \
    --amazonec2-request-spot-instance=true \
    --amazonec2-spot-price=0.50 \
    --amazonec2-userdata=/home/ec2-user/runner_userdata.sh test-machine
```

Output (see `<message>There is no Spot capacity available that matches your request.</message>`):

```bash
....
....
....
(test03) DBG | 2023/05/15 15:02:13 <?xml version="1.0" encoding="UTF-8"?>
(test03) DBG | <DescribeSpotInstanceRequestsResponse xmlns="http://ec2.amazonaws.com/doc/2016-11-15/">
(test03) DBG |     <requestId>4e487665-cad3-4ce7-b7fd-d81f79b8466c</requestId>
(test03) DBG |     <spotInstanceRequestSet>
(test03) DBG |         <item>
(test03) DBG |             <spotInstanceRequestId>sir-i1m6hmwn</spotInstanceRequestId>
(test03) DBG |             <spotPrice>0.500000</spotPrice>
(test03) DBG |             <type>one-time</type>
(test03) DBG |             <state>open</state>
(test03) DBG |             <status>
(test03) DBG |                 <code>capacity-not-available</code>
(test03) DBG |                 <updateTime>2023-05-15T15:01:43.000Z</updateTime>
(test03) DBG |                 <message>There is no Spot capacity available that matches your request.</message>
(test03) DBG |             </status>
(test03) DBG |             <validUntil>2023-05-22T15:01:43.000Z</validUntil>
(test03) DBG |             <launchSpecification>
(test03) DBG |                 <imageId>ami-02584c1c9d05efa69</imageId>
(test03) DBG |                 <keyName>test03</keyName>
(test03) DBG |                 <groupSet>
(test03) DBG |                     <item>
(test03) DBG |                         <groupId>sg-0a078f2ee0932b966</groupId>
(test03) DBG |                         <groupName>docker-machine</groupName>
(test03) DBG |                     </item>
(test03) DBG |                 </groupSet>
(test03) DBG |                 <instanceType>t2.2xlarge</instanceType>
(test03) DBG |                 <placement>
(test03) DBG |                     <availabilityZone>eu-central-1a</availabilityZone>
(test03) DBG |                 </placement>
(test03) DBG |                 <blockDeviceMapping>
(test03) DBG |                     <item>
(test03) DBG |                         <deviceName>/dev/sda1</deviceName>
(test03) DBG |                         <ebs>
(test03) DBG |                             <volumeSize>16</volumeSize>
(test03) DBG |                             <deleteOnTermination>true</deleteOnTermination>
(test03) DBG |                             <volumeType>gp2</volumeType>
(test03) DBG |                         </ebs>
(test03) DBG |                     </item>
(test03) DBG |                 </blockDeviceMapping>
(test03) DBG |                 <monitoring>
(test03) DBG |                     <enabled>false</enabled>
(test03) DBG |                 </monitoring>
(test03) DBG |                 <networkInterfaceSet>
(test03) DBG |                     <item>
(test03) DBG |                         <deviceIndex>0</deviceIndex>
(test03) DBG |                         <subnetId>subnet-09f2d3d96ea148a3e</subnetId>
(test03) DBG |                         <groupSet/>
(test03) DBG |                         <associatePublicIpAddress>false</associatePublicIpAddress>
(test03) DBG |                     </item>
(test03) DBG |                 </networkInterfaceSet>
(test03) DBG |                 <iamInstanceProfile>
(test03) DBG |                     <name></name>
(test03) DBG |                 </iamInstanceProfile>
(test03) DBG |                 <ebsOptimized>false</ebsOptimized>
(test03) DBG |             </launchSpecification>
(test03) DBG |             <createTime>2023-05-15T15:01:43.000Z</createTime>
(test03) DBG |             <productDescription>Linux/UNIX</productDescription>
(test03) DBG |             <tagSet/>
(test03) DBG |             <instanceInterruptionBehavior>terminate</instanceInterruptionBehavior>
(test03) DBG |         </item>
(test03) DBG |     </spotInstanceRequestSet>
(test03) DBG | </DescribeSpotInstanceRequestsResponse>
....
....
....
```