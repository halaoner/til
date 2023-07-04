# Mounting Docker Volume

When mounting a volume (e.g., directories and files) from host to a Docker container and the files appears to be a directory instead of file, it means that the source destination does not exists --> that is why the file is seen as a directory in target/ container destination.

`host machine` - file exists

```bash
ls -lah
-rw-r--r--     1 oha   test-user   178B Nov  1 13:28 terraform.tfstate
```

You can see that `terraform.tfstate` file is mounted correctly in the `container`

```bash
docker run --rm -it -v $PWD/terraform.tfstate:/root/terraform.tfstate bash /bin/sh
/ # ls -lah /root
total 16K
drwx------    1 root     root        4.0K Apr 27 12:55 .
drwxr-xr-x    1 root     root        4.0K Apr 27 12:55 ..
-rw-------    1 root     root          18 Apr 27 12:55 .ash_history
-rw-r--r--    1 root     root         178 Nov  1 12:28 terraform.tfstate
```

`host machine` - file (`terratfstate`) does not exist, and therefore is mounted as a `directory`

```bash
➜  ~ docker run --rm -it -v $PWD/terratfstate:/root/terraform.tfstate bash /bin/sh
/ # ls -lah /root
total 12K
drwx------    1 root     root        4.0K Apr 27 12:55 .
drwxr-xr-x    1 root     root        4.0K Apr 27 12:55 ..
-rw-------    1 root     root          14 Apr 27 12:55 .ash_history
drwxr-xr-x    2 root     root          64 Apr 27 12:55 terraform.tfstate
```