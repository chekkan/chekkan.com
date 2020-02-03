---
title: iam-policy-perm-for-public-load-balanced-ecs-fargate-on-cdk.md
date: "2020-02-03T12:02:00.000Z"
---

## IAM policy permissions for a public load balanced ecs fargate service on AWS CDK

Using AWS CDK with an admin user is all fine and straight forward. But, when it comes to creating a deployment pipeline with an IAM user specifically created with the actual permission needed, it can take a long time of trialing and failing to get to the final list of IAM policy statements.

A stack with an Application Load Balanced Fargate Service requires the following IAM permissions as a minimum.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "ec2:AuthorizeSecurityGroupIngress",
                "iam:UntagRole",
                "iam:ListRoleTags",
                "iam:TagRole",
                "iam:CreateRole",
                "iam:DeleteRole",
                "iam:AttachRolePolicy",
                "iam:PutRolePolicy",
                "cloudformation:CreateChangeSet",
                "cloudformation:DeleteChangeSet",
                "ec2:RevokeSecurityGroupIngress",
                "iam:DetachRolePolicy",
                "iam:DeleteRolePolicy",
                "cloudformation:ExecuteChangeSet"
            ],
            "Resource": [
                "arn:aws:ec2:*:{{accountId}}:security-group/*",
                "arn:aws:iam::{{accountId}}:role/{{stackPrefix}}*",
                "arn:aws:cloudformation:*:{{accountId}}:stack/{{stackPrefix}}*/*"
            ]
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:DescribeLoadBalancers",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeRegions",
                "route53:GetHostedZone",
                "route53:ListHostedZonesByName",
                "ec2:DescribeSecurityGroups"
            ],
            "Resource": "*"
        }
    ]
}
```

Replace `{{accountId}}` and `{{stackPrefix}}` with your values.
