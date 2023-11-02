# Asterisk_21_Installation_Guide
Asterisk_21_Installation_Guide
<pre>
docker run -u root --privileged -it -d -p 5060:5060/tcp -p 5060:5060/udp --name astrisk ubuntu:latest
docker container exec -it astrisk bash


apt-get update -y
apt install sudo -y
sudo apt-get upgrade -y

sudo apt install -y software-properties-common build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev python3-full python3-pip zip unzip wget vim nano git-core subversion wget libjansson-dev sqlite autoconf automake libxml2-dev libncurses5-dev libtool

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

vim /etc/asterisk/asterisk.conf
uncomment 
runuser = asterisk
rungroup = asterisk
	
ESC : WQ enter

sudo usermod -a -G dialout,audio asterisk

	

sudo chown -R asterisk: /var/{lib,log,run,spool}/asterisk /usr/lib/asterisk /etc/asterisk
sudo chmod -R 750 /var/{lib,log,run,spool}/asterisk /usr/lib/asterisk /etc/asterisk

sudo systemctl enable asterisk

sudo systemctl start asterisk
or
service asterisk start


cd /etc/asterisk
vim pjsip.conf
Add 2 sip client
;================================
;Aaron Courtney
;Accounting and Records

[1106](endpoint-internal-d70)
auth = 1106
aors = 1106
callerid = 1106

[1106](auth-userpass)
password = 1106
username = 1106

[1106](aor-single-reg)
mailboxes = 1106@example
max_contacts=5 ; Adjust the maximum contacts to a higher numbe

;================================ SALES STAFF ==

;================================
;Garnet Claude
;Sales Associate

[1105](endpoint-internal-d70)
auth = 1105
aors = 1105
callerid = 1105

[1105](auth-userpass)
password = 1105
username = 1105

[1105](aor-single-reg)
mailboxes = 1105@example
max_contacts=5 ; Adjust the maximum contacts to a higher numbe
;================================




sudo asterisk -vvvr
or
asterisk -vrrr

pjsip set logger on
pjsip show registrations


exit


vim extensions.conf
[from-internal]
exten => 1105,1,Answer()
same => n,Playback(welcome)
same => n,Hangup()

exten => 1106,1,Answer()
same => n,Playback(welcome)
same => n,Hangup()


service asterisk restart
systemctl status asterisk

asterisk -rx 'dialplan reload'



Execute with going inside CLI

asterisk -rx 'core restart when convenient'

asterisk -rx 'dialplan reload'
asterisk -rx 'module reload res_pjsip.so'

asterisk -rx 'pjsip show registrations'

asterisk -rx 'core restart now'

asterisk -rx 'pjsip show endpoints'

asterisk -rx 'pjsip reload'

GO inside Asterisk CLI
asterisk -r
pjsip show registrations

module show like sip
core reload

sudo ufw allow 5060/udp

sudo ufw allow 10000:20000/udp

---------------------------------------------------- FREE PBX --------------------------------------------------------------------
apt-get install apache2 mariadb-server libapache2-mod-php php php-pear php-cgi php-common php-curl php-mbstring php-gd php-mysql php-bcmath php-zip php-xml php-imap php-json php-snmp -y

wget http://mirror.freepbx.org/modules/packages/freepbx/freepbx-17.0-latest.tgz
tar -xvzf freepbx-17.0-latest.tgz
rm -rf freepbx-17.0-latest.tgz

vim /etc/asterisk/asterisk.conf
Add at the end of file
[directories]
astetcdir => /etc/asterisk
astmoddir => /usr/lib/asterisk/modules
astvarlibdir => /var/lib/asterisk
astdbdir => /var/lib/asterisk
astkeydir => /var/lib/asterisk
astdatadir => /var/lib/asterisk
astagidir => /var/lib/asterisk/agi-bin
astspooldir => /var/spool/asterisk
astrundir => /var/run/asterisk
astlogdir => /var/log/asterisk

Save n Exit

cd freepbx
apt-get install nodejs npm -y
sudo ./install -n

</pre>
