# Github - AWS CodeCommit - Mirror

Script for mirroring all repositories of an organization from Github to AWS CodeCommit. This script is intended to run as a cronjob, typically.

## Installation
Python >= 3.5 is required. The command **gh-cc-mirror** will get installed.

```sh
pip install gh-cc-mirror
```

## Usage

```sh
$ gh-cc-mirror -h
usage:

This command will mirror all repositories of an organization from Github to AWS CodeCommit.
This script is intended to run as a cronjob, typically.

       [-h] --cc-user CC_USER --cc-password CC_PASSWORD --github-user
       GITHUB_USER --github-token GITHUB_TOKEN --github-organization
       GITHUB_ORGANIZATION [--dir DIR] [--aws-access-key AWS_ACCESS_KEY]
       [--aws-secret-access-key AWS_SECRET_ACCESS_KEY]
       [--aws-region AWS_REGION] [--pushed-within PUSHED_WITHIN]

optional arguments:
  -h, --help            show this help message and exit
  --dir DIR             Working directory
  --aws-access-key AWS_ACCESS_KEY
                        AWS access key
  --aws-secret-access-key AWS_SECRET_ACCESS_KEY
                        AWS secret access key
  --aws-region AWS_REGION
                        AWS region
  --pushed-within PUSHED_WITHIN
                        Limit repositories with changes pushed with given
                        period, in minutes!

required named arguments:
  --cc-user CC_USER     CodeCommit user name
  --cc-password CC_PASSWORD
                        CodeCommit password
  --github-user GITHUB_USER
                        Github user account
  --github-token GITHUB_TOKEN
                        Github personal API access token
  --github-organization GITHUB_ORGANIZATION
                        Github organization
```

## Authentication

Git connections to **Github** and **AWS CodeCommit** are made via **https://**. For authentication at Github, a [Personal Access Token](https://github.com/settings/tokens) is needed. [HTTPS credentials for CodeCommit](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-gc.html) have to be generated via [AWS IAM](https://console.aws.amazon.com/iam/home).

## IAM rules

Access rights needed by AWS, for listing and creating CodeCommit repositoires:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "codecommit:CreateRepository",
                "codecommit:List*"
            ],
            "Resource": "*"
        }
    ]
}


```
## License
Copyright 2017 dpa-infocom GmbH

Apache License, Version 2.0 - see LICENSE for details
