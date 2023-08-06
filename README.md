# discovery-service

local start-up cmd
-Dspring.profiles.active=local -Dspring.cloud.config.label=develop

dev params
sudo nano /etc/systemd/system/dvdtheque-discovery-server.service


[Unit]
Description=Manage Dvdtheque Spring Discovery Server service

[Service]
WorkingDirectory=/opt/dvdtheque_discovery_server_service
ExecStart=/usr/lib/jvm/java-11-openjdk-armhf/bin/java -jar discovery-service.jar --spring.profiles.active=dev2 --spring.cloud.config.uri=http://192.168.1.103:8888,http://192.168.1.105:8888 --spring.cloud.config.label=develop
User=dvdtheque-user
Type=simple
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target

sudo mkdir /opt/dvdtheque_discovery_server_service

sudo chown -R dvdtheque-user:java-app-gr /opt/dvdtheque_discovery_server_service

sudo chmod -R g+w /opt/dvdtheque_discovery_server_service

sudo systemctl daemon-reload

sudo systemctl start dvdtheque-discovery-server.service

sudo systemctl status dvdtheque-discovery-server.service