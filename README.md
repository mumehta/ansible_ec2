#Launching EC2 with Ansible - using vault#

Refer [here](https://medium.com/datadriveninvestor/devops-using-ansible-to-provision-aws-ec2-instances-3d70a1cb155f)

## Following steps executed ##

1. Create aws user: ansible_app   

2. Generater ssh key for ssh'ing to ec2 server   
  >ssh-keygen -t rsa -b 4096 -f ~/.ssh/sbse_ansible_app  

3. Create playbook   
  >  mkdir -p ansible_ec2/group_vars/all/  
  cd ansible_ec2  
  touch playbook.yml  

4. Generate vault and secure password  
  >openssl rand -base64 2048 > vault.passansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass  

5. Update aws_access_key and aws_secret_key in pass file  
  >ansible-vault edit group_vars/all/pass.yml --vault-password-file vault.pass  

    Vault password:  
  >>ec2_access_key: AAAAAAAAAAAAAABBBBBBBBBBBB                              
  ec2_secret_key: afjdfadgf$fgajk5ragesfjgjsfdbtirhf*  

6. Query existing instances:  
  >ansible-playbook playbook.yml --vault-password-file vault.pass  

7. Launch new instances:  
  >ansible-playbook playbook.yml --vault-password-file vault.pass --tags create_ec2  