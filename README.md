# Asterisk_21_Installation_Guide
Asterisk_21_Installation_Guide
<pre>

  docker run -u root --privileged -it -d -p 5060:5060/tcp -p 5060:5060/udp ubuntu:latest

docker exec -it <contName> bash



sudo apt-get update -y
sudo apt-get upgrade -y


sudo apt-get install -y build-essential git-core subversion wget libjansson-dev sqlite autoconf automake libxml2-dev libncurses5-dev libtool

cd /usr/src/

sudo wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-21-current.tar.gz
sudo tar zxf asterisk-21-current.tar.gz

cd asterisk-*/

sudo contrib/scripts/get_mp3_source.sh

sudo contrib/scripts/install_prereq install

sudo ./configure


sudo make menuselect
	selecting format_mp3:

sudo make -j2

sudo make install

sudo make samples

sudo make basic-pbx

sudo make config

sudo ldconfig

sudo adduser --system --group --home /var/lib/asterisk --no-create-home --gecos "Asterisk PBX" asterisk

vim /etc/default/asterisk

uncomment 
AST_USER="asterisk"
AST_GROUP="asterisk"

ESC : WQ enter

sudo usermod -a -G dialout,audio asterisk

sudo chown -R asterisk: /var/{lib,log,run,spool}/asterisk /usr/lib/asterisk /etc/asterisk
sudo chmod -R 750 /var/{lib,log,run,spool}/asterisk /usr/lib/asterisk /etc/asterisk

sudo systemctl enable asterisk

sudo systemctl start asterisk
or
service asterisk start

sudo asterisk -vvvr
or
asterisk -vrrr


sudo ufw allow 5060/udp

sudo ufw allow 10000:20000/udp


</pre>
