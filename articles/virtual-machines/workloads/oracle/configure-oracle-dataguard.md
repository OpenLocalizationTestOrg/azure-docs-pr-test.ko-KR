---
title: "Azure Linux 가상 컴퓨터에서 Oracle Data Guard aaaImplement | Microsoft Docs"
description: "Azure 환경에서 Oracle Data Guard를 신속하게 가동하고 실행합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Azure Linux 가상 컴퓨터에서 Oracle Data Guard 구현 

Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. 이 문서에서는 toouse Azure CLI toodeploy Oracle 데이터베이스 12c hello Azure 마켓플레이스 이미지 로부터 데이터베이스를 설명 합니다. 이 문서의 다음 방법을 보여 줍니다, 단계별 방법 tooinstall 및 Azure 가상 컴퓨터 (VM)에서 Data Guard를 구성 합니다.

시작하기 전에 Azure CLI가 설치되어 있는지 확인합니다. 자세한 내용은 참조 hello [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.

## <a name="prepare-hello-environment"></a>Hello 환경 준비
### <a name="assumptions"></a>가정

hello에 toocreate 2 Azure Vm을 필요한 Oracle Data Guard tooinstall 동일한 가용성 집합:

- hello 기본 VM (myVM1)에 실행 중인 Oracle 인스턴스.
- hello 대기 VM (myVM2)에 hello Oracle 소프트웨어가 설치 되어 있습니다.

hello 마켓플레이스 이미지 toocreate hello Vm을 사용 하는 Oracle: Oracle-데이터베이스-Ee:12.1.0.2:latest 합니다.

### <a name="sign-in-tooazure"></a>TooAzure에 로그인 

Hello를 사용 하 여 Azure 구독 tooyour 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello를 사용 하 여 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치:

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>가용성 집합 만들기

가용성 집합 만들기는 선택 사항이지만 만드는 것이 좋습니다. 자세한 내용은 [Azure 가용성 집합 지침](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)을 참조하세요.

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>가상 컴퓨터 만들기

Hello를 사용 하 여 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다. 

hello 다음 예제에서는 라는 두 개의 Vm `myVM1` 및 `myVM2`합니다. 또한 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다. toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.

myVM1(기본) 만들기:
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Hello VM을 만든 후 Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다. Hello 값을 기록해 둡니다 `publicIpAddress`합니다. VM이 주소 tooaccess hello를 사용 합니다.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

myVM2(대기)를 만듭니다.
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Hello 값을 기록해 둡니다 `publicIpAddress` myVM2을 생성 합니다.

### <a name="open-hello-tcp-port-for-connectivity"></a>연결에 대 한 hello TCP 포트 열기

이 단계에서는 원격 액세스 toohello Oracle 데이터베이스를 허용 하는 외부 끝점을 구성 합니다.

MyVM1 hello 포트 열기:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

hello 결과 응답 다음 비슷한 toohello 같아야 합니다.

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

MyVM2 hello 포트 열기:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Toohello 가상 컴퓨터에 연결

사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다. Hello로 hello IP 주소를 교체 `publicIpAddress` 가상 컴퓨터에 대 한 값입니다.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Hello 데이터베이스를 만드는 위치 myVM1 (기본)

Oracle 소프트웨어 hello 있으므로 hello 다음 단계는 tooinstall hello 데이터베이스 hello 마켓플레이스 이미지에 이미 설치 되어 있습니다. 

Toohello Oracle superuser을 전환 합니다.

```bash
$ sudo su - oracle
```

hello 데이터베이스 만드는 위치:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
출력에는 다음 응답 비슷한 toohello 같아야 합니다.

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

Hello ORACLE_SID 및 ORACLE_HOME 변수를 설정 합니다.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 ORACLE_HOME 및 ORACLE_SID toohello /home/oracle/.bashrc 파일을 추가할 수 있습니다.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Data Guard 구성

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>myVM1(기본)에서 보관 로그 모드 사용

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

대기 다시 실행 로그를 만듭니다.

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

(하면을 복구 훨씬 쉽게) 플래시 백을 설정 하 고 대기 모드를 설정\_파일\_관리 tooauto 합니다. 그런 다음 SQL*Plus를 끝냅니다.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>myVM1(기본)에서 서비스 설정

편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello tnsnames.ora 파일을 만듭니다.

Hello 다음 항목을 추가 합니다.

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello listener.ora 파일을 만듭니다.

Hello 다음 항목을 추가 합니다.

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Data Guard Broker를 사용하도록 설정합니다.
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Hello 수신기를 시작 합니다.

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>myVM2(대기)에서 서비스 설정

SSH toomyVM2:

```bash 
$ ssh azureuser@<publicIpAddress>
```

Oracle로 로그인합니다.

```bash
$ sudo su - oracle
```

편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello tnsnames.ora 파일을 만듭니다.

Hello 다음 항목을 추가 합니다.

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello listener.ora 파일을 만듭니다.

Hello 다음 항목을 추가 합니다.

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Hello 수신기를 시작 합니다.

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Hello 데이터베이스 toomyVM2 복원 (대기)

Hello 매개 변수 파일 /tmp/initcdb1_stby.ora를 내용을 따라 hello로 만듭니다.
```bash
*.db_name='cdb1'
```

폴더를 만듭니다.

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

암호 파일을 만듭니다.

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
MyVM2 시작 hello 데이터베이스 위치:

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Hello RMAN 도구를 사용 하 여 hello 데이터베이스를 복원 합니다.

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Hello 다음 RMAN에서 명령을 실행 합니다.
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Hello 명령이 완료 되 면 비슷한 toohello 다음 메시지가 표시 됩니다. RMAN을 끝냅니다.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 ORACLE_HOME 및 ORACLE_SID toohello /home/oracle/.bashrc 파일을 추가할 수 있습니다.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Data Guard Broker를 사용하도록 설정합니다.
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>myVM1(기본)에서 Data Guard Broker 구성

Data Guard Manager를 시작하고 SYS 및 암호를 사용하여 로그인합니다. OS 인증을 사용하지 마세요. Hello 다음을 수행 합니다.

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

Hello 구성 검토:
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

Hello Oracle Data Guard 설치를 완료 합니다. hello 다음 섹션에는 tootest hello 연결 하 고 전환 하는 방법을 보여줍니다.

### <a name="connect-hello-database-from-hello-client-machine"></a>Hello 데이터베이스 hello 클라이언트 컴퓨터에서 연결

업데이트 또는 클라이언트 컴퓨터의 hello tnsnames.ora 파일을 만듭니다. 이 파일은 일반적으로 $ORACLE_HOME\network\admin에 있습니다.

Hello IP 주소를 교체 하면 `publicIpAddress` myVM1 및 myVM2 값:

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

SQL*Plus를 시작합니다.

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>테스트 hello Data Guard 구성

### <a name="switch-over-hello-database-on-myvm1-primary"></a>(기본) myVM1 hello 데이터베이스 전환

기본 toostandby (cdb1 toocdb1_stby)에서 tooswitch:

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

Toohello 대기 데이터베이스를 연결할 수 있습니다.

SQL*Plus를 시작합니다.

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>MyVM2 hello 데이터베이스 전환 (대기)

조치 tooswitch myVM2 hello 다음을 실행 합니다.
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

다시 한 번 수 tooconnect toohello 주 데이터베이스 수 있어야 합니다.

SQL*Plus를 시작합니다.

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Oracle Linux에서 Data Guard의 hello 설치 및 구성 작업을 완료 했습니다.


## <a name="delete-hello-virtual-machine"></a>Hello 가상 컴퓨터 삭제

더 이상 VM hello 필요 hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스에 따라 사용할 수 없습니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

[자습서: 고가용성 가상 컴퓨터 만들기](../../linux/create-cli-complete.md)

[VM 배포 Azure CLI 샘플 탐색](../../linux/cli-samples.md)
