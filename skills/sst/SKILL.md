---
name: sst
description: Helps to consider the best practices for SST. Use it to get advice on SST configurations and setups. SST is a Infrastructure as code deployment tool.
license: MIT
metadata:
  author: cloudxs GmbH
  version: "1.0"
---

# SST

Use this skill when user asks for help with SST.

## Documentation

Find the documentation: [SST Docs](https://sst.dev/docs)

## Structure

If not mentioned, you should find the SST relevant files in `./infra` or `./infrastructure`. Don't look into any other directory.

The main SST file is `sst.config.ts`.
If you find a transform function in `sst.config.ts`, this usually sets global configurations for a specific resource type.

```typescript
$transform(sst.aws.Function, (args) => {
  args.someproperty = "some value";
});
```

## Best practices

- **CloudTrail**: It is recommended that an SST project should have a CloudTrail trail enabled to log all management data. Recognize a trail by the resource type `aws.cloudtrail.Trail`. If no trail is found, suggest adding one considering the [CloudTrail reference](references/CLOUDTRAIL.md)

## Specific resource best practices

### sst.aws.Router

- deploy a CloudFront distribution. A CloudFront distribution should always have `retainOnDelete` set to `true` to prevent accidental data loss. If this is not set, suggest adding it.
- Create and attach a WAF Web ACL in productive environments: `prd`, `prod`, `production`.

### sst.aws.StaticSite

- deploy a CloudFront distribution. A CloudFront distribution should always have `retainOnDelete` set to `true` to prevent accidental data loss. If this is not set, suggest adding it.

### sst.aws.Function

- To comply with best practices for monitoring and auditing, logging retention must be set:
  - allow values >=`1 day` if it is used as a Lambda@Edge function.
  - allow values >=`6 months` for standard Lambda functions.
- Don't allow retention not to be set.
- Don't allow Logging format not to be set. It **MUST** be set to `json`.

Example:

```typescript
const function = new sst.aws.Function('some name', {
  handler: 'some/handler.path',
  timeout: '<some value>',
  logging: {
    retention: '6 months',
    format: 'json',
  }
});
```

### aws.acm.Certificate

- A certificate must always have `retainOnDelete` set to `true` to prevent accidental data loss. If this is not set, suggest adding it.

## Notes

- `new <provider>.<provider>.<Resource>('some-name')`
  - Consider that a change in name leads to a replacement of resources.
- **ALWAYS** ignore the directories `node_modules`, `.sst`
