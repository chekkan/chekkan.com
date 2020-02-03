---
title: iam-policy-perm-for-public-load-balanced-ecs-fargate-on-cdk.md
date: "2020-02-03T12:02:00.000Z"
---

## IAM policy permissions for a public load balanced ecs fargate service on AWS CDK

Using AWS CDK with an admin user is all fine and straight forward. But, when it comes to creating a deployment pipeline with an IAM user specifically created with the actual permission needed, it can take a long time of trialing and failing to get to the final list of IAM policy statements.

For A stack with an Application Load Balanced Fargate Service requires the following IAM permissions as a minimum.

### Give access to the cdk toolkit staging s3 bucket:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:GetAccessPoint",
                "s3:PutAccountPublicAccessBlock",
                "s3:GetAccountPublicAccessBlock",
                "s3:ListAllMyBuckets",
                "s3:ListAccessPoints",
                "s3:ListJobs",
                "s3:CreateJob",
                "s3:HeadBucket"
            ],
            "Resource": "*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::cdktoolkit-stagingbucket-*"
        }
    ]
}
```

### Managed policies
- AWSCloudFormationReadOnlyAccess - `arn:aws:iam::aws:policy/AWSCloudFormationReadOnlyAccess`
- AmazonVPCReadOnlyAccess - `arn:aws:iam::aws:policy/AmazonVPCReadOnlyAccess`

### Remaining Custom Policies

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "lambda:CreateFunction",
                "ec2:AuthorizeSecurityGroupIngress",
                "elasticloadbalancing:ModifyListener",
                "iam:ListRoleTags",
                "iam:UntagRole",
                "iam:TagRole",
                "iam:CreateRole",
                "iam:AttachRolePolicy",
                "lambda:GetFunctionConfiguration",
                "iam:PutRolePolicy",
                "cloudformation:CreateChangeSet",
                "cloudformation:DeleteChangeSet",
                "iam:PassRole",
                "iam:DetachRolePolicy",
                "iam:ListAttachedRolePolicies",
                "iam:DeleteRolePolicy",
                "lambda:DeleteFunction",
                "iam:ListRolePolicies",
                "cloudformation:ExecuteChangeSet",
                "iam:GetRole",
                "lambda:InvokeFunction",
                "lambda:GetFunction",
                "iam:DeleteRole",
                "ec2:RevokeSecurityGroupIngress",
                "iam:GetRolePolicy"
            ],
            "Resource": [
                "arn:aws:iam::{{accountId}}:role/{{stackPrefix}}*",
                "arn:aws:cloudformation:*:{{accountId}}:stack/{{stackPrefix}}*/*",
                "arn:aws:ec2:*:{{accountId}}:security-group/*",
                "arn:aws:elasticloadbalancing:*:{{accountId}}:listener/app/{{lbPrefix}}*/*/*",
                "arn:aws:elasticloadbalancing:*:{{accountId}}:listener/net/{{lbPrefix}}*/*/*",
                "arn:aws:lambda:*:{{accountId}}:function:Compliance*"
            ]
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:DescribeLoadBalancers",
                "route53:GetChange",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeRegions",
                "route53:GetHostedZone",
                "route53:ChangeResourceRecordSets",
                "route53:ListResourceRecordSets",
                "route53:ListHostedZonesByName",
                "ec2:DescribeSecurityGroups"
            ],
            "Resource": "*"
        },
        {
            "Sid": "VisualEditor2",
            "Effect": "Allow",
            "Action": "elasticloadbalancing:ModifyListener",
            "Resource": [
                "arn:aws:elasticloadbalancing:*:{{accountId}}:listener/app/{{lbPrefix}}*/*/*",
                "arn:aws:elasticloadbalancing:*:{{accountId}}:listener/net/{{lbPrefix}}*/*/*"
            ]
        }
    ]
}
```

Replace `{{accountId}}`, `{{stackPrefix}}` and `{{lbPrefix}}` with your values.
