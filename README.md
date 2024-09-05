# cluster-api-workload-cluster

This project works together with the 
[cluster-api-mgmt-cluster](https://gitlab.com/22e88/cluster-api-mgmt-cluster/) project.

It automates creation, deletion and maintenance operations of a Kubernetes
cluster which is managed by a Cluster-API cluster created by the 
[cluster-api-mgmt-cluster](https://gitlab.com/22e88/cluster-api-mgmt-cluster/) project. See there
for details. 
NOTE: 'automates' in this context means that all operations are defined as 
code in this repo, which is then executed by the CICD pipeline (which can 
be manually triggered by you if you want). The code here currently consists
of Ansible playbooks which are run against the Cluster-API management-cluster
which you have created using the 
[cluster-api-mgmt-cluster](https://gitlab.com/22e88/cluster-api-mgmt-cluster/) project. 
 
## How to use
If you want to use this stuff as it is intended, you need your own Gitlab repo
where you can store the files you can download from here. 
You have to define 2 CICD variables in your repo:
* CI_BETA_PRIV_KEY: as in your instance of the cluster-api-mgmt-cluster project,
this variable (type: file) has to hold the private key of the pubkey which is 
already rolled out to your management cluster controlplane. 
* CI_MGMT_PROJ_TOKEN: this has to be a Gitlab project access token, scope guest 
and with API read / write access. (In your management-cluster project, go to 
Settings / Access Tokens to create on). This token is required by your pipeline
to be able to retrieve the Ansible inventory file of the latest successful run 
of the management-cluster pipeline.
Both repos (cluster-api-mgmt-cluster and cluster-api-workload-cluster) are 
organized to be used in kind of 'DEV|STAGE|PROD' environments: the main branch
deploys to a prod environmen, the stage and dev branch can be used to deploy to 
accordingly named different environments. See the README of the 
[cluster-api-mgmt-cluster](https://gitlab.com/22e88/cluster-api-mgmt-cluster/) project 
on how to do this. 
