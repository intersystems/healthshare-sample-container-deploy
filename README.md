<!-- omit in toc -->
# healthshare-sample-container-deploy

Contains sample deployment files to deploy HealthShare (HS) applications as container stacks.
A single HS application consists of a stack with two containers: a web gateway
container and a HS instance container.

Below we describe the sample files provided in this repository.

- [Structure](#structure)
- [sample\_deploy](#sample_deploy)
- [sample\_configs](#sample_configs)


## Structure

This repository is structured into two top level folders: `sample_deploy` and `sample_configs`.
- `sample_deploy` contains the directory structure recommended to deploy a HS container stack.
While the directory structure can be altered, this would require overriding 
variables in the environment (.env) files.
- `sample_configs` contain example configuration files for configuring the different
types of HS applications.

## sample_deploy

## sample_configs