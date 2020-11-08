# Launching EC2 with Ansible - using vault #

Refer [here](https://medium.com/datadriveninvestor/devops-using-ansible-to-provision-aws-ec2-instances-3d70a1cb155f) and [here](https://www.bogotobogo.com/DevOps/Ansible/Ansible-SSH-Connection-Setup-Run-Command.php)

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

8. Test ssh to ec2 instance:  
  >ssh -i ~/.ssh/sbse_ansible_app centos@<public-ip>  

8. Create the inventory file prod/inventory and update with public ec2 instance ip, generated in step 7  

9. Test connectivity with ping module  
  >ansible -i prod -m ping  --vault-password-file vault.pass  all  

10. Create playbook and roles for apache / php install  

11. Apply playbook
  >ansible-playbook -i prod  --vault-password-file vault.pass playbook-testweb.yml
