# s3-cloudfront-cache-invalidation
An AWS Lambda function that invalidates AWS CloudFront cache when S3 objects are changed.

### Installing and building

Install dependencies with `yarn install`.
Build with `yarn build`.

### AWS Setup
#### Create an AWS Lambda Function

![Create Screenshot](https://github.com/adamking/s3-cloudfront-cache-invalidation/raw/master/screenshots/create.png)

#### Upload `s3-cloudfront-cache-invalidation.zip` to AWS Lambda

![Upload Screenshot](https://github.com/adamking/s3-cloudfront-cache-invalidation/raw/master/screenshots/upload.png)

#### Create policy
![Policy Screenshot](https://github.com/adamking/s3-cloudfront-cache-invalidation/raw/master/screenshots/role-policy.png)

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "acm:ListCertificates",
                "cloudfront:GetDistribution",
                "cloudfront:GetDistributionConfig",
                "cloudfront:ListDistributions",
                "cloudfront:ListCloudFrontOriginAccessIdentities",
                "cloudfront:CreateInvalidation",
                "cloudfront:GetInvalidation",
                "cloudfront:ListInvalidations",
                "elasticloadbalancing:DescribeLoadBalancers",
                "iam:ListServerCertificates",
                "sns:ListSubscriptionsByTopic",
                "sns:ListTopics",
                "waf:GetWebACL",
                "waf:ListWebACLs"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Resource": "*"
        }
    ]
}
```

#### Add trigger to S3 bucket
