# AWS IAM Practice

Hands-on practice with AWS Identity and Access Management (IAM): users, groups,
policies, least privilege, and roles for EC2.

## What I practiced

| Lab | What I did | What it proved |
|---|---|---|
| 1 | Created the group `s3-readers` with `AmazonS3ReadOnlyAccess`, and the user `practice-user` | Permissions come from the group, not the user |
| 2 | Signed in as the user and tested actions | Reading S3 worked; uploading and viewing EC2 were denied |
| 3 | Wrote my own policy in JSON allowing only `s3:PutObject` on one bucket | Upload worked, delete was still denied (least privilege) |
| 4 | Created the role `ec2-s3-read-role` and attached it to an EC2 server | The server reached S3 with no access keys |

## Key concepts

- Everything is denied by default; an explicit Allow opens an action; an explicit Deny always wins.
- Attach policies to groups, not to individual users.
- Give services roles with temporary credentials, never long-lived access keys.
- Least privilege: grant only the actions and resources that are needed.

## The custom policy

See [`policies/upload-to-practice-bucket.json`](policies/upload-to-practice-bucket.json).
It allows `s3:PutObject` only on objects inside one bucket. The bucket name is a placeholder.
The EC2 trust policy is in [`policies/ec2-trust-policy.json`](policies/ec2-trust-policy.json).

## Cleanup

All resources were deleted after the practice: the EC2 server, the role, the bucket,
the user, the group and the custom policy.
