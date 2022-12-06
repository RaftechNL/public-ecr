# public-ecr
Repository connected to our public ECR available under https://gallery.ecr.aws/p8o7f1g4/

## Images
The following images are created witin this repository:

| Namespace        | image         | Description                                                          |
| ---------------- | ------------- | -------------------------------------------------------------------- |
| platform/tooling | aws-cli-v2    | Alpine image built with AWS CLIv2                                    |
| platform/tooling | k8s           | Contains most common tools to manage automations around CICD and k8s |
| platform/tooling | terraform-gha | Contains tfswitch with tfctm and github-comment - used in GHA        |

## How to use
