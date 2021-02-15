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

Variables should be changed for your GCP account specs.


      gcp_project: segmentify 							- should be your project
      gcp_cred_kind: serviceaccount
      gcp_cred_file: ../segmentify-b1c4f7958044.json 	- your auth json file to the service account
      zone: "europe-west3-c"						 	- zone of your choice
      region: "europe-west3" 							- region of your choice


# doitall.yml

This playbook creates a vm on GCP, checks out a repository from git and builds the code in golang from the repository; and then deploys it to the server with the service, starts the application, checks if port 80 is up.

This playbook builds only a simple golang application, names it helloworld. Startup scripts are also created for this name. To make this playbook work, variables should be edited inside.

      gcp_project: segmentify 											---- GCP project name for vm
      gcp_cred_kind: serviceaccount										---- GCP credential type
      gcp_cred_file: ../segmentify-b1c4f7958044.json 					---- GCP service account credentials
      zone: "europe-west3-c"											---- GCP zone
      region: "europe-west3" 											---- GCP region
      build_repo: https://github.com/bachadir/segmentify_app.git        ---- GIT repository for the application
      build_version: Version-1											---- Version to checkout
      ssh_key_location: /root/.ssh/google 								---- ssh key location to connect to the vm