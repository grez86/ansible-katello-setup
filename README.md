# Ansible Katello Setup

## Overview

This project provides Ansible playbooks to automate the installation and configuration of Foreman-Katello, aiming to streamline the setup process for managing content and subscriptions.

## Prerequisites

- **Ansible**: Ensure that Ansible is installed on your control node.
- **Ansible Vault Password File**: A `.vault_pass` file containing the password to decrypt sensitive variables.
- **Repository Configuration**: A YAML file specifying repository configurations, such as `vars/repository_configs/sample.yml`.

### Important Notes on Ansible Vault
- The provided `vars/vault.yml` file is for reference only.
- Users must recreate the `vault.yml` file using the `ansible-vault` command and include the following two variables:
  - `vault_foreman_password`: The initial password for accessing the Foreman WebUI.
  - `vault_gpg_passphrase`: The passphrase used for generating GPG keys.

## Setup Instructions

1. Install required Ansible modules using the playbook `install_ansible_foreman_modules.yml`.
```bash
ansible-playbook install_ansible_foreman_modules.yml
```
2. Set up Katello using the `setup_katello.yml` playbook and the `.vault_pass` file.
```bash
ansible-playbook setup_katello.yml --vault-password-file ../.vault_pass
```
3. Create repositories and environments by running the `create_repos_and_envs.yml` playbook. Specify the repository configuration YAML file (e.g., `vars/repository_configs/sample.yml`) as an extra variable.
```bash
ansible-playbook create_repos_and_envs.yml --vault-password-file ../.vault_pass --extra-vars "@vars/repository_configs/sample.yml"
```

## File Descriptions

- **`install_ansible_foreman_modules.yml`**: Installs necessary Ansible modules for managing Foreman and Katello.
- **`setup_katello.yml`**: Configures the Katello server, including necessary dependencies and initial settings.
- **`create_repos_and_envs.yml`**: Sets up repositories and environments as defined in the provided configuration file.
- **`hosts`**: Inventory file listing target hosts for Ansible playbooks.
- **`vars/`**: Directory containing variable files, including:
  - `repository_configs/sample.yml`: A sample configuration file for repositories and environments.
  - `vault.yml`: A placeholder file for storing sensitive variables. This must be recreated by the user with the required variables.

## Notes

- The `.vault_pass` file should be securely stored and not included in version control.
- Before running the playbooks, customize the `repository_config.yml` file to match your specific requirements.

## License

This project is licensed under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss potential changes.

## Contact

For questions or support, please contact [Your Name] at [your.email@example.com].
