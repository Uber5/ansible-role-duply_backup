# How to Use

```
- hosts: some-hosts
  roles:
    - role: duply_backup
      backing_up_user: user1
      pre_script: templates/duply_pre.sh.j2
      backup_password: veryTopS111cret
      backup_src: /home/user1/important-stuff
      backup_target: scp://backups@my-backup-server.com/user1
```

The backup target can be a S3 bucket, assuming 'my-backups' being a S3 bucket:

```
TARGET_USER='some-s3-key'
TARGET_PASS='some-s3-secret'
TARGET='s3://s3-ap-southeast-2.amazonaws.com/my-backups/some-folder'
```

# Setup Bucket Policy on S3

This policy works, but may be too liberal:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123:user/backups-hetz4"
      },
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::backups-hetz4"
    },
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123:user/backups-hetz4"
      },
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::backups-hetz4/*"
    }
  ]
}
```
