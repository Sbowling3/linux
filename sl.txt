###########################################################
apt install ffmpeg
mv sl /usr/local/bin/
chmod +x /usr/local/bin/sl
mkdir /home/ad/.stash
chown ad /home/ad/.stash
chmod u+rwx /home/ad/.stash

nano /etc/systemd/system/sl.service
((

[Unit]
Description=Media
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/sl
WorkingDirectory=/home/ad/.stash
User=ad
Group=ad
Restart=on-failure
Environment="STASH_CONFIG_FILE=/home/ad/.stash/config.yml"

[Install]
WantedBy=multi-user.target

))

systemctl daemon-reload
systemctl enable sl.service
systemctl start sl.service
systemctl status sl.service
Log to check for errors: journalctl -u sl.service -b

###############################################################
