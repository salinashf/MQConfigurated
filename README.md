# MQConfigurated
Configuración MQ  IBM en Docker 



docker-compose up
docker stop  ibmmqvserver
docker exec -it ibmmqvserver /bin/bash

runmqsc  QMGR

ALTER CHL(DEV.APP.SVRCONN) CHLTYPE(SVRCONN) MCAUSER('admin')

SET AUTHREC PROFILE('SYSTEM.DEFAULT.MODEL.QUEUE') OBJTYPE(QUEUE) PRINCIPAL('admin') AUTHADD(ALL)  
SET AUTHREC PROFILE('SYSTEM.ADMIN.COMMAND.QUEUE') OBJTYPE(QUEUE) PRINCIPAL('admin')  AUTHADD(ALL)
SET AUTHREC PROFILE(SYSTEM.DEFAULT.TOPIC) OBJTYPE(TOPIC) PRINCIPAL('admin') AUTHADD(ALL) 
SET AUTHREC PROFILE(SYSTEM.DEFAULT.QUEUE) OBJTYPE(QUEUE) PRINCIPAL('admin') AUTHADD(ALL) 
SET AUTHREC PROFILE(*) OBJTYPE(QUEUE) PRINCIPAL('admin') AUTHADD(ALL)
SET AUTHREC OBJTYPE(QMGR) PRINCIPAL('admin') AUTHADD(ALL)
SET AUTHREC PROFILE(SYSTEM.MQEXPLORER.REPLY.MODEL) OBJTYPE(QUEUE) PRINCIPAL('admin')  AUTHADD(ALL) 
SET AUTHREC PROFILE(SYSTEM.ADMIN.COMMAND.QUEUE) OBJTYPE(QUEUE) PRINCIPAL('admin')   AUTHADD(ALL) 
SET AUTHREC PROFILE(*) OBJTYPE(QUEUE) PRINCIPAL('admin') AUTHADD(ALL)

ALTER   QMGR CONNAUTH(USE.PW)
DEFINE AUTHINFO(USE.PW) +
AUTHTYPE(IDPWOS) +
FAILDLAY(10) +
CHCKLOCL(OPTIONAL) +
CHCKCLNT(REQUIRED)
REFRESH SECURITY TYPE(CONNAUTH)
REFRESH SECURITY(*) TYPE(CONNAUTH)


setmqaut -m QMGR -t q -n SYSTEM.ADMIN.COMMAND.QUEUE -p admin +inq +browse +get +dsp +put
setmqaut -m QMGR -t qmgr -p admin +connect +inq +dsp
setmqaut -m QMGR -t q -n SYSTEM.DEFAULT.MODEL.QUEUE -p admin +inq +browse +get +dsp
setmqaut -m QMGR -t q -n SYSTEM.ADMIN.COMMAND.QUEUE -p admin +inq +put +dsp
setmqaut -m QMGR -t q -n SYSTEM.MQEXPLORER.REPLY.MODEL -p admin +inq +browse +get +dsp +put

Gestor Colas 
runmqsc QMGR
Ver Gestor Colas
dspmq

Detener
endmqm QMGR

Iniciar
strmqm QMGR

dspmqver QMGR






