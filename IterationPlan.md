# Talend-AWS-Cognizant Iteration Plan


Product Backlog - Release 2

* Support Talend 6.4.1
* Use AWS Code Commit
* Add CI Server
* Move Nexus and CI server to separate subnet
* Add support for multiple environments, environments share access to Nexus which is placed in a separate subnet.
* Add option to generate passwords
* Validate PCI template end-to-end
* Add ELB to PCI master.
* Snapshot stack configuration
* Developers guide for utility scripts and factory
* CI test case documents
* Capture launch parameters in aws cli cfn script in credentials bucket
* Load git with App Team’s Talend project

Release 1.0 - Target 9/22


** Iteration 0.5.0 - Self-contained Resources, Capture App Credentials, No AWS Secrets **

* DataSource configuration parameterizatoin
* Add Studio server instance to Talend baseline.
* Update and re-test factory scripts
* Add parameter labels and grouping for entry point templates
* Refactor and simplify the credential lambda function
* Use IAM role with s3fs
* Move s3fs github dependency to talend repo
* Add credentials for git, nexus, and tac to credentials bucket
* Add policies for bucket access to IAM roles
* EMR Shutdown issues documented
* Bastion issue replicated with original bastion stack
* Gitlab project url fixed
* Parameters files and other AWS CI support artifacts.

Iteration 0.4.0 - Servers and Credentials

* Add an Auto-Scaling element for the job server.
* Clean out old RDS from DataSource template.
* Add DataSource to oodle-basic template.
* Add metaservlet scripts to TAC to create users
* Fix Gitlab bug.
* Add error protection retry around yum and apt-get operations
* Remove TUI LicenseUser and LicensePassword parameters
* Credentials Bucket
    * Persist credentials from all servers in separate property files in the same secure bucket
    * Add lambda for Redshift credentials

Iteration 0.3.0 - Self-Contained Scripts and Naming Conventions

* Standardize Outputs
* Standard Tags for EC2 instances
    * StackId
    * StackName
    * Name - role of server, e.g. TAC, Nexus, Jobserver, Logserver, Git 
* Naming  Conventions
    * Parameters: camel case with initial cap
    * Mappings: camel case with initial cap for categories, uppercase for final attribute
    * Conditions: either camel case with ending "Condition", or begin with "is" prefix
    * Resources: camel case with initial cap
    * Outputs: camel case with initial cap for resources or stacks, camel case with initial lowercase for primitives like IP or DNS name
* Autonomous and self-contained
    * Refactor hard coded references for updated_hosts.sh to Mappings
    * Move github script zip file to use just s3 with QSS3Bucket and QSS3KeyPrefix
    * Refactor updates_hossts to use QSS3Bucket and QSS3KeyPrefix
* Git
    * Add Git to Security Group configuration
    * Fix git security group so it is not wide open

Iteration 0.2.0 - Database and Git Bootstrap

TAC Database
* Updated the TAC template to create the TAC and AMC databases.  Add supporting parameters to TAC template as well as Servers and Master templates. (in progress)

Git Integration
* Setup the configuration scripts for Git so that on each boot a git repo is created
* Wire git repo configuration and access credentials to the TAC configuration in the master template
using the talend_servers nested stack parameters. 
* Add Git server to the basic OODLE template (the one using just AWS VPC).
* Move Git server from Datasource template to the its own template.  Move the template from the datasource git repo to its own file under templates in the quickstart-datalake-cognizant-talend folder.

Version Control
* Modify Talend baseline stack to use AWS conventions of qss3bucket.
* Rename templates to .template rather than .json.
* Use qss3prefix for versioning in the s3 bucket folder structure only.  Not used in git structure. 

Iteration 0.1.0 - Initial Internal  Release

This first internal release is included in the corresponding 0.1.0 release of the quickstart-datalake-cognizant-talend. The talend_master template uses the talend_servers template to provision Nexus, Logserver, TAC, and Jobserver instances from their respective templates.

The talend_master wires the talend_network template resources to each of the server templates. The talend_master and talend_network templates are intended to provide a simple integration test fixture for the talend_servers template. The individual servers and the talend_servers template are the unit of deployment used by other Cloud Formation scripts.