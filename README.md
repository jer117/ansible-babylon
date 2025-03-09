# Ansible Babylon

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A powerful Ansible automation toolkit for streamlined infrastructure management and deployment.

## 🚀 Features

- Automated infrastructure provisioning
- Configuration management
- Application deployment
- Security compliance automation
- Scalable and modular design

## 📋 Prerequisites

- Ansible 2.9 or higher
- Python 3.6+
- SSH access to target hosts

## 🛠️ Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/ansible-babylon.git
cd ansible-babylon
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## 🔧 Configuration

1. Update your inventory file in `inventory/`
2. Configure variables in `group_vars/` and `host_vars/`
3. Modify playbooks as needed in `playbooks/`

## 🏃‍♂️ Usage

Run playbooks using:
```bash
ansible-playbook playbooks/your-playbook.yml
```

## 📁 Project Structure

```
ansible-babylon/
├── inventory/
├── group_vars/
├── host_vars/
├── playbooks/
├── roles/
└── templates/
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

For questions or support, please open an issue in the repository.

# Secret management.
## 🔐 Secret Management

### Secrets Configuration

Create a file named `secrets.yml` to store your sensitive variables:

```yaml
# secrets.yml
telegram_bot_token: "BotID:TOKEN"
telegram_chat_id: "-channelNumber"
```

### 🛠️ Useful Commands

```bash
# Add operator key with recovery
babylond keys add operator --recover

# Unjail validator
babylond tx slashing unjail \
    --chain-id bbn-test-5 \
    --from operator \
    --gas-adjustment 1.4 \
    --gas auto \
    --fees 210ubbn

# Unjail finality provider
fpd unjail-finality-provider \
    32da5fd22935bcf6b97e83d009b0514eeabe4c503a695937b55b7e99c95aa071 \
    --daemon-address finality-provider:12581
```

## ⚠️ Known Issues and Solutions

### Key Import Requirements
Both keys must be imported to the finality-provider image and eots-manager to prevent the following error:

```
fatal terminating the finality-provider instance due to critical error
{"pk": "32da5fd22935bcf6b97e83d009b0514eeabe4c503a695937b55b7e99c95aa071", 
"error": "failed to generate randomness: rpc error: code = Unknown desc = EOTS key name not found"}
```

### Resolution Steps:
1. Import EOTS key:
```bash
eotsd keys add $MONIKER \
    --recover \
    --keyring-backend test \
    --rpc-client eots-manager:12582
```

2. Import finality provider key:
```bash
fpd keys add finality-provider \
    --keyring-backend test \
    --recover
```

3. If needed, unjail the finality provider:
```bash
fpd unjail-finality-provider \
    32da5fd22935bcf6b97e83d009b0514eeabe4c503a695937b55b7e99c95aa071 \
    --daemon-address finality-provider:12581
```
