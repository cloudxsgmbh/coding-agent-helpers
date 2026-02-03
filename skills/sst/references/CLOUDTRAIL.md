# AWS CloudTrail

## Overview

AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. With CloudTrail, you can log, continuously monitor, and retain account activity related to actions across your AWS infrastructure.

## Implementation example

We need an S3 bucket to store the CloudTrail logs. The bucket must have a policy that allows CloudTrail to write logs to it, and it should have a lifecycle policy to expire logs after a certain period (e.g., 180 days). Additionally, we need to create a CloudTrail trail that specifies the S3 bucket for log storage and enables features like multi-region logging and log file validation.

```typescript
import config from "./config";

const auditTrailName = "audit";

const auditBucket = new sst.aws.Bucket(`audit`, {
  policy: [
    {
      actions: ["s3:GetBucketAcl"],
      principals: [
        { type: "service", identifiers: ["cloudtrail.amazonaws.com"] },
      ],
      conditions: [
        {
          test: "StringEquals",
          variable: "aws:SourceArn",
          values: [
            `arn:aws:cloudtrail:${config.currentRegion.name}:${config.currentAws.accountId}:trail/${auditTrailName}`,
          ],
        },
      ],
      paths: [""],
    },
    {
      actions: ["s3:PutObject"],
      principals: [
        { type: "service", identifiers: ["cloudtrail.amazonaws.com"] },
      ],
      conditions: [
        {
          test: "StringEquals",
          variable: "s3:x-amz-acl",
          values: ["bucket-owner-full-control"],
        },
        {
          test: "StringEquals",
          variable: "aws:SourceArn",
          values: [
            `arn:aws:cloudtrail:${config.currentRegion.name}:${config.currentAws.accountId}:trail/${auditTrailName}`,
          ],
        },
      ],
      paths: [`prefix/AWSLogs/${config.currentAws.accountId}/*`],
    },
    {
      actions: ["s3:GetBucketAcl"],
      principals: [
        { type: "service", identifiers: ["cloudtrail.amazonaws.com"] },
      ],
      paths: [""],
    },
    {
      actions: ["s3:PutObject"],
      principals: [
        { type: "service", identifiers: ["cloudtrail.amazonaws.com"] },
      ],
      conditions: [
        {
          test: "StringEquals",
          variable: "s3:x-amz-acl",
          values: ["bucket-owner-full-control"],
        },
      ],
      paths: [`prefix/AWSLogs/${config.currentAws.accountId}/*`],
    },
  ],
  lifecycle: [
    {
      id: "cloudtrail-logs-expiration",
      expiresIn: "180 days",
    },
  ],
});

new aws.cloudtrail.Trail(`audit`, {
  name: auditTrailName,
  s3BucketName: auditBucket.name,
  isMultiRegionTrail: true,
  includeGlobalServiceEvents: true,
  enableLogFileValidation: true,
  s3KeyPrefix: "prefix",
});
```
