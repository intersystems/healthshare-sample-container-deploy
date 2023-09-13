<!-- omit in toc -->
# healthshare-sample-container-deploy

This repository contains sample deployment files to deploy InterSystems HealthShare (HS) applications as container stacks. Note that these are sample files intended to be used along with the [HealthShare user documentation](https://docs.intersystems.com/hs202311/csp/docbook/DocBook.UI.Page.cls).

**These sample files ARE NOT intended for direct usage in production environments.**

A single HealthShare application consists of a stack with two containers:
a Web Gateway container and a HealthShare instance container.
Below we describe the sample files provided in this repository to deploy such HealthShare applications.

- [Structure](#structure)
- [sample\_deploy](#sample_deploy)
  - [docker-compose and container.env](#docker-compose-and-containerenv)
  - [web-gateway](#web-gateway)
  - [config](#config)
    - [hs](#hs)
    - [iris](#iris)
  - [data-ingestion](#data-ingestion)
- [sample\_configs](#sample_configs)


## Structure

This repository is structured into two top level directories: `sample_deploy` and `sample_configs`.
- `sample_deploy` contains the directory structure recommended to deploy an HS container stack. 
While the directory structure can be altered, this requires that you override variables in the environment (.env) files.
- `sample_configs` contain example configuration files for configuring the different
types of HS applications.

## sample_deploy

This directory structure is as follows:
```
📦sample_deploy
 ┣ 📂config
 ┃ ┣ 📂hs
 ┃ ┃ ┗ 📜hs-base-config.json
 ┃ ┗ 📂iris
 ┃ ┃ ┣ 📜iris.key
 ┃ ┃ ┗ 📜merge.cpf
 ┣ 📂data-ingestion
 ┃ ┗ 📂Data
 ┣ 📂web-gateway
 ┃ ┣ 📂certificate
 ┃ ┃ ┣ 📜ssl-cert.key
 ┃ ┃ ┗ 📜ssl-cert.pem
 ┃ ┣ 📜CSP.conf
 ┃ ┗ 📜CSP.ini
 ┣ 📜container.env
 ┗ 📜docker-compose.yml
```

Below we break down the roles of the various directories and files. For directories/
files whose locations can be changed, the corresponding environment variables that 
control the directory locations are also referenced. Note that the directory related 
environment variables are optional. If you do not specify directory-related environment
variable values, then you **must** use the default directory structure referenced in 
the above image and detailed below.

### docker-compose and container.env

To deploy the container stack, the following command is run:
```bash
docker-compose --env-file=container.env up
```

This command will configure a single HS application stack consisting of two containers: Web Gateway and HS instance.

However, before this can be run, the values in `container.env` need to be populated. The file itself describes what each of the variables does and this is further fleshed out in the HS user documentation. 
In below sections, when environment variables are referenced, they will only be referenced
by name and their description can be looked up in one of the above referenced sources.

You will notice that the variables themselves or their corresponding defaults in the `docker-compose.yml` file point to other relative directories/files which are referenced in the next few sections.

### web-gateway

This top level directory contains the files necessary to deploy an InterSystems 
Web Gateway image which is documented in the [InterSystems IRIS Web Gateway documentation](https://docs.intersystems.com/irislatest/csp/docbook/DocBook.UI.Page.cls?KEY=GCGI).

### config

This directory contains all necessary configuration related files used at container 
deployment time.
**NOTE:** Any files under this directory are NOT used during the active lifetime of the 
container. Other storage locations are used for storing data needed during the 
lifetime of a running container.

This directory has two sub-directories:
- `hs`: For HS-specific configuration files
- `iris`: For InterSystems IRIS-specific configuration files

#### hs

This directory MUST consist of a single JSON file named `hs-base-config.json` by default 
(can be overridden using environment variable ISC_HS_CONFIG_BASE_FILENAME).
This JSON file has the following keys in it:
- (REQUIRED) network-config: basic network settings required to communicate with the HS instance.
- (REQUIRED) feature-config: metadata used to configure a HS application namespace (Registry, Edge Gateway etc.)
- (OPTIONAL) oauth-config: metadata used to configure local OAuth related settings (whether OAuth is enabled, additional network info etc.)

Each of those keys has values which are JSON objects detailed in the next sections.

Environment variables related to this directory: 
- `EXTERNAL_HS_CONFIG_DIRECTORY`
- `ISC_HS_CONFIG_DIRECTORY`
- `ISC_HS_CONFIG_BASE_FILENAME`

**NOTE:** the `hs-base-config.json` file is not to be provided when deploying a 
HS backup mirror member. This is detailed in the [HS user documentation](https://docs.intersystems.com/hs202311/csp/docbook/DocBook.UI.Page.cls?KEY=HEMRR_ch_mirroring_existing_environment#HEMRR_mirroring_installing_second_failover_existing).

#### iris

This directory MUST consist of at a minimum, an iris.key file for the license key 
of the corresponding HS image that is being deployed.
It is also recommended that a merge.cpf file be included for any startup related 
configuration settings. The example file provided sets the routine buffer memory 
to 300MB instead of the default which is 25% of the available device memory.

Environment variables related to this directory: 
- `EXTERNAL_IRIS_CONFIG_DIRECTORY`
- `ISC_CONFIG_DIRECTORY`
- `ISC_CPF_MERGE_FILE_NAME`

### data-ingestion

This directory does not exist in the sample directory structure but should be created 
as well as the `Data` sub-directory.

Environment variables related to this directory: 
- `EXTERNAL_DATA_INGESTION_DIRECTORY`
- `ISC_HS_DATA_INGESTION_DIRECTORY`


## sample_configs

This directory contains sample JSON objects for each of the keys of `hs-base-config.json`.