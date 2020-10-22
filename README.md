*Thingsboard Installation*

I Install Python 3.6 https://installvirtual.com/install-python-3-on-raspberry-pi-raspbian/
1. apt-get update
2. sudo apt-get install -y build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev libffi-dev
3. wget https://www.python.org/ftp/python/3.6.8/Python-3.6.8.tgz
4. sudo tar zxf Python-3.6.8.tgz
5. cd Python-3.6.8
6. ./configure
7. make -j 4
8. make altinstall
9. python3.6 -V

II Install thingsboard
1. sudo apt install python3-dev python3-pip libglib2.0-dev 
2. git clone https://github.com/thingsboard/thingsboard-gateway.git
3. cd thingsboard-gateway
4. python3 setup.py install
5. sudo pip3 install thingsboard-gateway
6. wget https://github.com/thingsboard/thingsboard-gateway/releases/download/2.0/configs.tar.gz
7. sudo mkdir /etc/thingsboard-gateway
8. sudo mkdir /var/log/thingsboard-gateway
9. sudo tar -xvzf configs.tar.gz -C /etc/thingsboard-gateway
10. thingsboard-gateway

*Telegraf Installation*
1. curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
2. echo "deb https://repos.influxdata.com/debian buster stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
3. sudo apt-get update
4. sudo apt-get install -y influxdb telegraf
5. sudo systemctl enable influxdb telegraf
6. sudo systemctl start influxdb telegraf

*Run telegraf and thingsboard gateway on boot*
1. crontab -e
2. put command in the bottom line
- @reboot telegraf
- @reboot /usr/bin/python3 /usr/local/bin/thingsboard-gateway

*Cara download dan setup configuration file dari github*
1. Create Folder in root
- mkdir telegraf_configuration
- cd telegraf_configuration
2. Make it git repository
- git init
3. Clone telegraf configuration from github
- git clone https://github.com/albertshanhandoko/SUN.git
4. Create backup folder for existing configuration*
- mkdir backup
5. Copy existing configuration to backup folder
- cd /etc/telegraf
- cp telegraf.conf /root/telegraf_configuration/SUN/backup
6. Copy and rename new configuration file
- cd /root/telegraf_configuration/SUN
- cp GOP6.txt /etc/telegraf
- cd /etc/telegraf
- rm telegraf.conf
- mv GOP6.txt telegraf.conf
- reboot

*Cara push configuration file ke github*
1. Create Folder in root
- mkdir thingsboard_configuration
- cd thingsboard_configuration
2. Make it git repository
- git init
3. Copy existing configuration to repository
- cd /etc/thingsboard-gateway/config
- cp tb_gateway.yaml /root/thingsboard_configuration
4. Add and commit configuration file
- git add tb_gateway.yaml
- git status
- git commit -m 'comment'
5. Register remote repository
- git remote add albertgit https://albertshanhandoko:4Lbertshan1234@github.com/albertshanhandoko/SUN.git
6. Push file to remote repository
- git push -u albertgit master

*Configuration Files Directory*
1. Telegraf = /etc/telegraf/telegraf.conf
2. Thingsboard = /etc/thingsboard-gateway/config/tb_gateway.yaml

*Troubleshoot modbus telegraf*
1. telegraf -input-filter modbus -test


Credential =
1. Access token Thingsboard
- GOP 6 = BOEe0LbvO894wk7nrnEb
- GOP 9 = GrUBdnxb1tqix2o4SC8w
- SML   = yMLNpmbRy5wTPFy0vyuQ

2. Thingsboard server
- Hostname  = 153.92.5.95
- Port      = 2883

3. Link instalasi dataplicity
- GOP 6 = curl -s https://www.dataplicity.com/qkvm6l9i.py | sudo python
- GOP 9 = curl -s https://www.dataplicity.com/ld2osp32.py | sudo python
- SML   = curl -s https://www.dataplicity.com/zlxx0rmt.py | sudo python 
