# What?

This is an [Ansible](http://docs.ansible.com/) role to setup backups via
[Duply](http://duply.net/).

TODO: Currently (duplicity version 0.7.02), it seems necessary to patch duplicity as per
https://bugs.launchpad.net/duplicity/+bug/1434702

# How to Use

## With a simple duply target (e.g. scp)

In your playbook:

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

## With Amazon S3

In your playbook:

```
    - role: duply_backup
      backing_up_user: user1
      pre_script: templates/testing/duply_pre.sh.j2
      backup_password: topSecretPassword
      backup_src: /home/user1/important-stuff
      backup_target: s3://s3-ap-southeast-2.amazonaws.com/backups-bucket/user1
      backup_target_user: 's3-id'
      backup_target_pass: 's3-secret'
```

The bucket needs an appropriate policy. The following works, but may be more
liberal than necessary:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123:user/backups-myhost"
      },
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::backups-bucket"
    },
    {
      "Sid": "",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123:user/backups-myhost"
      },
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::backups-bucket/*"
    }
  ]
}
```
