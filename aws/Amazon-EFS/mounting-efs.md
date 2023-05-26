## mount point does not exist

```bash
sh-4.2$ sudo mount -t efs -o tls fs-0786be468941a3c5d:/ efs
mount: efs: mount point does not exist.
```

How to fix:

1. Create folder `efs`
2. Repeat mounting command

## How to mount Amazon EFS dynamically 

1. Amazon EFS is created
1. Run custom script when creating EC2
    - Get `FileSystemId`

    ```bash
   aws efs describe-mount-targets --file-system-id fs-0312da0f8017c2f7a  | jq -r '.FileSystems[0].FileSystemId'

    fs-0312da0f8017c2f7a
    ```

    - Get `IpAddress`:
    ```bash
    aws efs describe-mount-targets --file-system-id fs-0312da0f8017c2f7a | jq -r '.MountTargets[].IpAddress'
    172.31.25.232
    ```
1. Check if EFS is created

1. Mount EFS to EC2

```bash
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 172.31.25.232:/ efs
```

## mount.nfs4: Failed to resolve server

Mounting the EFS to EC2:

```bash
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-07d53dd52ac9e7fea.efs.eu-central-1.amazonaws.com:/ efs
mount.nfs4: Failed to resolve server fs-07d53dd52ac9e7fea.efs.eu-central-1.amazonaws.com: Name or service not known
mount.nfs4: Operation already in progress
```

How to solve the error:
- check your VPC and make sure that `DNS hostnames: Enable`


## mount: /efs: bad option

Error:

```bash
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport 10.0.1.132:/ efs
mount: /efs: bad option; for several filesystems (e.g. nfs, cifs) you might need a /sbin/mount.<type> helper program.
```

Install `nfs-common` utilities:

```bash
sudo apt install nfs-common
```
