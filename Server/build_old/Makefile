CC 			= gcc
CFLAGS 		= -g -Wall -I ../include/ -I ../../Share/include/ 
VPATH 		= ../:../src/:../../Share/src/:../include/:../../Share/include/
SERVER_RELY = \
			Write_Pi_Log.o \
			sockFrame.o \
			Get_conf.o \
			StrtoInt.o \
			ServerConnect.o \
			dataTransmission.o \
			sendWarningInfo.o \
			heartBeat.o \
			getScriptRunInfo.o \
			runScriptAndSave.o \
			mainServer.o 

Server : ${SERVER_RELY}
	@echo "[\033[1;32mLinking\033[0m] Server"
	@${CC} ${CFLAGS} ${SERVER_RELY} -l pthread -o Server 

mainServer.o : mainServer.c mainServer.h 
	@echo "[\033[1;32mBuilding\033[0m] [CC] mainServer.c"
	@${CC} -c ${CFLAGS} $<

sendWarningInfo.o : sendWarningInfo.c sendWarningInfo.h 
	@echo "[\033[1;32mBuilding\033[0m] [CC] sendWarningInfo.c"
	@${CC} -c ${CFLAGS} $<

getScriptRunInfo.o : getScriptRunInfo.c getScriptRunInfo.h 
	@echo "[\033[1;32mBuilding\033[0m] [CC] getScriptRunInfo.c"
	@${CC} -c ${CFLAGS} $<

ServerConnect.o : ServerConnect.c mainServer.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] ServerConnect.c"
	@${CC} -c ${CFLAGS} -l pthread $<

runScriptAndSave.o : runScriptAndSave.c runScriptAndSave.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] runScriptAndSave.c"
	@${CC} -c ${CFLAGS} -l pthread $<

dataTransmission.o : dataTransmission.c dataTransmission.h 
	@echo "[\033[1;32mBuilding\033[0m] [CC] dataTransmission.c"
	@${CC} -c ${CFLAGS} -l pthread $<

heartBeat.o : heartBeat.c heartBeat.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] heartBeat.c"
	@${CC} -c ${CFLAGS} $<

Get_conf.o : Get_conf.c Get_conf.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] Get_conf.c"
	@${CC} -c ${CFLAGS} $<

StrtoInt.o : StrtoInt.c StrtoInt.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] StrtoInt.c"
	@${CC} -c ${CFLAGS} $<

sockFrame.o : sockFrame.c sockFrame.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] sockFrame.c"
	@${CC} -c ${CFLAGS} $<

Write_Pi_Log.o : Write_Pi_Log.c Write_Pi_Log.h
	@echo "[\033[1;32mBuilding\033[0m] [CC] Write_Pi_Log.c"
	@${CC} -c ${CFLAGS} $<

.PHONY: clean install uninstall

install : 
	mkdir /opt/SHMS-server/ 
	mkdir /etc/SHMS-server/
	mkdir /var/log/SHMS-server/
	touch /var/log/SHMS-server/SHMS-Server.log
	touch /etc/SHMS-server/server.pid
	cp ./Server /opt/SHMS-server/ 
	cp ../server.conf /etc/SHMS-server/
	cp ../SHMS-server.init /opt/SHMS-server/ 
	cp ../SHMS-Server.service /etc/systemd/system/
	chmod 755 /opt/SHMS-server/SHMS-server.init 
	chmod 754 /etc/systemd/system/SHMS-Server.service
	systemctl daemon-reload
	systemctl enable SHMS-Server.service
	systemctl start SHMS-Server.service 

uninstall :
	rm -rf /opt/SHMS-server/
	rm -rf /etc/SHMS-server/
	rm -rf /var/log/SHMS-server/
	systemctl stop SHMS-Server.service
	rm -rf /etc/systemd/system/SHMS-Server.service

clean : 
	@echo "[\033[1;32mClean\033[0m] Clean compile file."
	@rm -rf Server ${SERVER_RELY}


