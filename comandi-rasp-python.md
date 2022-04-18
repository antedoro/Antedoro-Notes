Arrestare il sistema:
sudo shutdown -h now

Riavviare il sistema:
sudo reboot

avviare il desktop environent:
startx

Accedere (nuovamente) alla schermata di configurazione Raspbery:
sudo raspi-config

Riprodurre un file audio o video con il riproduttore integrato:
omxplayer -o hdmi "Desktop/Sample.mkv"

Eseguire uno script Python:
sudo python Desktop/helloworld.py

Eseguire uno script con versione Python 3.x:
sudo python3 Desktop/helloworld.py

Ottenere i permessi di esecuzione su uno script (BASH, ecc.):
sudo chmod +x /home/pi/Desktop/script.sh

Eseguire uno script (BASH, ecc.):
sudo /home/pi/Desktop/script.sh

Analisi sui processi attivi:
ps all

Analisi configurazione di rete:
ifconfig

Aggiornare l’indice dei pacchetti:
sudo apt-get update

Aggiornare i pacchetti:
sudo apt-get upgrade

Installare il server VNC “x11vnc” (per il controllo remoto del nostro Raspberry):
sudo apt-get install x11vnc

Installare il server VNC “tightvnc” (per il controllo remoto del nostro Raspberry):
sudo apt-get install tightvncserver

Installare il riproduttore audio/video “VLC”:
sudo apt-get install vlc

Cia sono diversi script python che girano a rotazione. Per saper quale sta girando in questo momento:
ps -aef | grep python
