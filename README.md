# ansible-katello-setup

- ansible-playbook install_ansible_foreman_modules.yml
- ansible-playbook setup_katello.yml --vault-password-file ../.vault_pass
- ansible-playbook create_repos_and_envs.yml --vault-password-file ../.vault_pass --extra-vars "@vars/templates/oracle.yml"
