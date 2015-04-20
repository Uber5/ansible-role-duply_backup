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
