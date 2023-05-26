# cloud-init directives

**INFO**

[cloud-init](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)

- `cloud-init` is a tool used in Amazon Web Services (AWS) to configure the initial settings of EC2 instances when they are launched. 
- Cloud-init is executed as part of the boot process of the EC2 instance
- perform a wide range of tasks such as:
  - Setting the hostname of the instance.
  - Configuring networking settings. 
  - Installing and configuring software packages.
  - Creating user accounts and setting up their access permissions.
  - Mounting file systems, such as Elastic File System (EFS).
  - Running scripts and executing commands at instance launch time

## Shell script failed on GitLab Runner

Check `cloud-init` ([userdata](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html#user-data-shell-scripts)) of GitLab Runner (EC2 instance) for more information:

```bash
sudo cat /var/log/cloud-init-output.log
```