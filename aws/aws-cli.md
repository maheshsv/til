# AWS CLI

> AWS Command Line Interface(AWS CLI) is an open source tool that enables you to interact with AWS services using commands in your command-line shell.

### Configuration

Credentials and configurations are stored in `~/.aws/credentials` and `~/.aws/config`. And it supports multiple named profiles.

### Environment variables

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_SESSION_TOKEN
- AWS_DEFAULT_REGION
- AWS_DEFAULT_OUTPUT
- AWS_PROFILE
- AWS_ROLE_SESSION_NAME
- AWS_CA_BUNDLE
- AWS_SHARED_CREDENTIALS_FILE
- AWS_CONFIG_FILE

The environment variables take precedence if present.

### Command structure

```shell
aws <command> <subcommand> [options and parameters]
```

### Some Useful commands

Delete EC2 key pairs in batch

```shell
aws ec2 describe-key-pairs | jq -r '.KeyPairs[].KeyName' | xargs -I {} sh -c "aws ec2 delete-key-pair --key-name {}"
```

Get current caller account ID

```shell
aws sts get-caller-identity --output text --query Account
```

--- 

For other cool features, check out the doc [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html).
