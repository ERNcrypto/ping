# ping
Install
# Update system and install python
sudo apt update
sudo apt install python3 python3-pip git python-telegram-bot
pip install toml
# Clone repository
git clone https://github.com/muhaylosemenyuk/ping.git
cd ~/ping
# Add servers and telegram data to the config.toml
nano config.toml
image

Enter your TELEGRAM_API_KEY

How to get Telegram bot API token

Enter your MONITORING_CHAT_ID

How to get a group chat id?

# Create service file
sudo tee /etc/systemd/system/ping.service > /dev/null <<EOF
[Unit]
Description=Ping Bot Service
After=network.target

[Service]
User=root
ExecStart=/usr/bin/python3 /root/ping/ping.py
WorkingDirectory=/root/ping/
Restart=always
RestartSec=5

[Install]
WantedBy=default.target

EOF
systemctl daemon-reload
systemctl enable ping
systemctl restart ping
# Check logs
journalctl -u ping -f -o cat
