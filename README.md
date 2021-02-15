# segmentify_excercise
Excercise for Segmentify


This project uses Ansible for automation and GCP as cloud provider. Needs requests and google-auth packages. 

<code>
pip install requests google-auth
</code>

You need to pre-define a project on GCP, and pre-load the ssh keys to be able to connect to the instances.

This ansible scripts need ansible 2.9+ with GCP modules installed.

<code>
	ansible-galaxy collection install google.cloud
</code>

You need to create a service account with compute engine access, and get the json auth file from GCP and keep it in the upper directory of the script


Need to configure gcp os login for ssh from outside.

https://cloud.google.com/compute/docs/instances/managing-instance-access#gcloud_1

# createinstance.yml

This playbook creates a VM on GCP with predefined service account and specs.

Should be changed for your GCP account specs.


<code>
	  vars:
      gcp_project: segmentify - should be your project
      gcp_cred_kind: serviceaccount
      gcp_cred_file: ../segmentify-b1c4f7958044.json - your auth json file to the service account
      zone: "europe-west3-c" - zone of your choice
      region: "europe-west3" - region of your choice
</code>


#doitall.yml

This playbook creates a vm on GCP, checks out a repository from git and builds the code in golang from the repository; and then deploys it to the server with the service, starts the application, checks if port 80 is up.

