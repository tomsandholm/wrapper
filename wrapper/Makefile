.ONESHELL:

.PHONEY: all

all: 
	make global-uptime
	make global-diskuse
	make global-ping

global-uptime:
	shc -S -f global-uptime.sh
	mv global-uptime.sh.x global-uptime
	sudo chown root:root global-uptime
	sudo chmod u+s global-uptime
	sudo cp --preserve=mode global-uptime /usr/local/bin/global-uptime

global-diskuse:	
	shc -S -f global-diskuse.sh
	mv global-diskuse.sh.x global-diskuse
	sudo chown root:root global-diskuse
	sudo chmod u+s global-diskuse
	sudo cp --preserve=mode global-diskuse /usr/local/bin/global-diskuse

global-ping:
	shc -S -f global-ping.sh
	mv global-ping.sh.x global-ping
	sudo chown root:root global-ping
	sudo chmod u+s global-ping
	sudo cp --preserve=mode global-ping /usr/local/bin/global-ping

clean:
	sudo rm global-uptime
	sudo rm global-diskuse
	sudo rm global-ping
	sudo rm -rf /usr/local/bin/global-uptime
	sudo rm -rf /usr/local/bin/global-diskuse
	sudo rm -rf /usr/local/bin/global-ping
	sudo rm global-*.sh.x.c
