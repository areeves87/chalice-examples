Testing some chalice ci/cd options

This repo uses these instructions for creating a chalice ci/cd pipeline: https://aws.github.io/chalice/topics/cd.html#configuring-a-github-repository

Some additional instructions are included below specific to this use case.

Note the changes made to accomodate a chalice project helloworld directory. (These changes are not necessary if the chalice project is the root level)
	- buildspec.yml 
		* cd into the helloworld directory on install phase
		* location of the build artifact is helloworld/transformed.yaml
	- pipeline.json
		* create changeset for beta - location of the transformed.yaml is updated

These additional changes were made for passing the access_key and secret_key environment variables:
	- additional secret called AWSCredentials saved to secrets-manager which includes access key and secret key values.
	- in pipeline.json, codebuild policy given full access to secrets-manager actions
	- in buildspec.yml
		* collect access and secret key from secrets-manager 
		* write their values to the environment variables in .chalice/config.json during build phase (so that they are deployed with the chalice lambdas)