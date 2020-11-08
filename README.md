Refer: https://medium.com/datadriveninvestor/devops-using-ansible-to-provision-aws-ec2-instances-3d70a1cb155f

1. aws user: ansible_app
2. ssh-keygen -t rsa -b 4096 -f ~/.ssh/sbse_ansible_app
3. mkdir -p ansible_ec2/group_vars/all/
cd ansible_ec2
touch playbook.yml
4. openssl rand -base64 2048 > vault.passansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
5. ansible-vault edit group_vars/all/pass.yml --vault-password-file vault.pass
Vault password:
ec2_access_key: AAAAAAAAAAAAAABBBBBBBBBBBB                              
ec2_secret_key: afjdfadgf$fgajk5ragesfjgjsfdbtirhf
6. Query existing instances:
ansible-playbook playbook.yml --vault-password-file vault.pass
7. create new instances:
ansible-playbook playbook.yml --vault-password-file vault.pass --tags create_ec2 