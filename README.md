# incident

# Incident Response Playbook Automation Lab

This repository contains a modified AWS CloudFormation template for the Automating Playbooks lab.

## Files

- `bastion.yaml` - Modified CloudFormation template for deploying a bastion host and its supporting network resources.
- `bastionOriginal.yaml` - Original version of the CloudFormation template before modifications.
- `.github/workflows/deploy.yaml` - GitHub Actions workflow that deploys the CloudFormation stack when changes are pushed to the `main` branch.

## Lab Changes

The `bastion.yaml` template was modified to support an incident response containment scenario.

The main changes include:

- Added an isolation security group for the bastion host.
- Added comments describing incident response playbook steps.
- Added a comment above the security group assignment explaining how the bastion host can be isolated during an investigation.
- Updated the bastion instance to use `SecurityGroupIds` and place the instance in the configured subnet.

## Incident Response Scenario

The scenario assumes that automated monitoring detects anomalous network activity from the bastion host. As a containment step, the security group assigned to the bastion host can be changed from the normal inbound access security group to the isolated security group. This prevents inbound and outbound communication while responders preserve evidence and investigate the system.

## Automation

The GitHub Actions workflow in `.github/workflows/deploy.yaml` runs when changes are pushed to the `main` branch. The workflow uses AWS credentials stored as GitHub repository secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`

The workflow deploys the CloudFormation stack named `bastion`.
