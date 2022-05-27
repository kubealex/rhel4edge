# Ansible playbook to provision rhel4edge vms and register into and ACM hub

!!! IMPORTANT - Python > 3.8 must be present 
- Use your built image and move it into the *rhel4edge* folder (image name: r4e-microshift-installer.x86_64.iso)
- Populate vars.yml file with relevant information. Please respect the format.
 
        github_repo: #defaults to microshift-config
        github_username:  
        github_token:  

        rhel4edge_instances:  
        - r4e-printer 
        - r4e-injection 
        - r4e-label 

        manifests_dir: ~/microshift-config/var/lib/microshift/manifests

*rhel4edge_instances* will be the value for both the hostname and cluster name. The playbook will create one VM per instance.

- Add your VM host relevant information into inventory file. **sudo** privilege must be enabled for the user running the automation. Since we are running in an Execution environment, ensure you are able to SSH to the VM Host before you start.
- The default kickstart (present as a template in *templates* folder) uses the id_rsa.pub key in the repo for user **redhat** (password: redhat)
- The kubeconfig of the cluster hosting ACM HUB must be placed in the root folder of the repo

# Build your execution environment

Under execution-environment folder all the files for building the EE are present.

    ansible-builder build  -t r4e-ee

The image name is already configured in **ansible-navigator.yaml** file


# Run the playbook

To run the automation:

    ansible-navigator ansible-navigator run 02_vms-and-registration -m stdout 

