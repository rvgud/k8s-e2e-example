## Install Jenkins on GCP instances using Ansible

    1. Add internal and external IP address of GCP instances into inventory file at 
       ./hosts.ini

    2. Deploy Kubespray with Ansible Playbook
       ansible-playbook -i hosts.ini playbook.yaml