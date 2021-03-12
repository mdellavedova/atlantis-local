# Atlantis

Atlantis is a ci/cd system for terraform.

Atlantis runs terraform plan on pull requests, and in the medium term will
be able to apply terraform changes directly from pull requests.  This will
begin the process of centralising core infrastructure changes and will also
give better visibility to developers and SREs.
## Usage

Individual terraform projects are configured in [../atlantis.yaml](../atlantis.yaml).

Ensure you understand this configuration before making changes, as atlantis applies
the config in the Pull request rather than master.

The manifests in [k8s](./k8s) are used to deploy and configure [atlantis](https://www.runatlantis.io/) in
the ops Kubernetes eks cluster in nexmo-dev/eu-west-2
## Custom `nexmo-atlantis`

We build a custom version of atlantis docker image based on `runatlantis/atlantis`. More information about the CI pipeline in [build](./build).
