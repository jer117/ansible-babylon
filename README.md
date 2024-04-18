# ansible-babylon
Ansible role to manage a babylon node

# Secret management.
## Secrets File

Create a file named `secrets.yml` and add your secret variables like `telegram_bot_token` and `telegram_chat_id` with their respective values.

```yaml
# secrets.yml
telegram_bot_token: "BotID:TOKEN"
telegram_chat_id: "-channelNumber"

