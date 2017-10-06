---
title: "Azure Linux VM에서 Oracle Data Guard aaaImplement | Microsoft Docs"
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a>Azure Linux VM에서 Oracle Data Guard 구현 

hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다. Hello Azure CLI toodeploy Oracle 12c hello 마켓플레이스 갤러리 이미지에서 데이터베이스를 사용 하 여이 가이드 정보입니다. 이 문서에서는 hello Oracle 데이터베이스를 만든 후 단계별 방법을 tooinstall 및 Azure VM에서 Data Guard를 구성 합니다.

시작 하기 전에 해야 Azure CLI 설치가 완료 된 후 해당 hello 합니다. 자세한 내용은 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.

## <a name="prepare-hello-environment"></a>Hello 환경 준비
### <a name="assumptions"></a>가정

hello에 toocreate 2 Azure Vm을 필요한 tooperform hello Oracle Data Guard를 설치, 동일한 가용성 집합입니다. toocreate hello Vm을 사용 하 여 hello 마켓플레이스 이미지는 "Oracle: Oracle-데이터베이스-Ee:12.1.0.2:latest"입니다.

hello 기본 VM (myVM1)에 실행 중인 Oracle 인스턴스.

hello 대기 VM (myVM2)에 hello Oracle 소프트웨어가 설치 되어 있습니다.

### <a name="log-in-tooazure"></a>TooAzure 로그인 

Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치 합니다.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a>가용성 집합 만들기

이 단계는 선택 사항이지만 권장됩니다. 자세한 내용은 [Azure 가용성 집합 가이드](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)를 참조하세요.

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

Hello로 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다. 

hello 다음 예제에서는 명명 된 2 개의 Vm `myVM1` 및 `myVM2`합니다. 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다. toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.

myVM1(기본) 만들기
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

한 번 VM을 만든 hello, Azure CLI hello 정보 비슷한 toohello 다음 예제: hello 기록해 `publicIpAddress`합니다. 이 주소는 사용 되는 tooaccess hello VM입니다.

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

myVM2(대기) 만들기
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

Hello를 메모해 `publicIpAddress` 생성 한 번도 합니다.

### <a name="open-hello-tcp-port-for-connectivity"></a>연결에 대 한 hello TCP 포트 열기

hello 단계는 tooconfigure 외부 끝점을 허용 하는 Oracle DB hello를 원격으로 액세스 하 고 hello 다음 명령을 실행 합니다.

myVM1에 대한 포트 열기

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

결과는 다음 응답 비슷한 toohello 같아야 합니다.

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

myVM2에 대한 포트 열기

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a>Toovirtual 컴퓨터 연결

사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다. Hello로 hello IP 주소를 교체 `publicIpAddress` 의 가상 컴퓨터.

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a>myVM1(기본)에서 데이터베이스 만들기

Oracle 소프트웨어 hello 있으므로 hello 다음 단계는 tooinstall hello 데이터베이스 hello 마켓플레이스 이미지에 이미 설치 되어 있습니다. hello 첫 번째 단계는 hello 'oracle' superuser로 실행 중입니다.

```bash
sudo su - oracle
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

Hello ORACLE_SID 및 ORACLE_HOME 변수를 설정

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 추가 된 ORACLE_HOME 및 ORACLE_SID toohello.bashrc 파일을 수 있습니다.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a>데이터 가드 구성

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>myVM1(기본)에 보관 로그 모드를 사용하도록 설정

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

대기 다시 실행 로그 만들기

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

(훨씬 이전 hello 복구에 만든)는 플래시 백을 켜려면 STANDBY_FILE_MANAGEMENT tooauto 설정

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a>myVM1(기본)에 서비스 설치

$ORACLE_HOME\network\admin 폴더에 hello tnsnames.ora 파일을 만들거나 편집

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

$ORACLE_HOME\network\admin 폴더에 hello listener.ora 파일을 만들거나 편집

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

Hello 수신기를 시작 합니다.

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a>myVM2(대기)에 서비스 설치

$ORACLE_HOME\network\admin 폴더에 hello tnsnames.ora 파일을 만들거나 편집

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

$ORACLE_HOME\network\admin 폴더에 hello listener.ora 파일을 만들거나 편집

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

Data Guard Broker를 사용하도록 설정
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a>데이터베이스 toomyVM2 복원 (대기)

매개 변수 파일을 만들 ' / tmp/initcdb1_stby.ora' hello 다음 내용으로
```bash
*.db_name='cdb1'
```

폴더 만들기

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

암호 파일 만들기

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
myVM2에서 데이터베이스 시작

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

RMAN 유틸리티를 사용하여 데이터베이스 복원

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Hello 다음 RMAN에서 명령 실행
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Data Guard Broker를 사용하도록 설정
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>myVM1(기본)에서 Data Guard Broker 구성

SYS 및 암호 (운영 체제 인증을 사용 하지 안 함)를 사용 하 여 로그인 하 고 hello Data Guard 관리자를 시작 합니다. Hello 다음을 수행 합니다.

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

Hello 구성 검토
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

Hello Oracle Data Guard 설치를 완료 합니다. hello 다음 섹션에서는 연결 및 전환 tootest hello 하는 방법

### <a name="connect-database-from-client-machine"></a>클라이언트 컴퓨터에서 데이터베이스 연결

업데이트 하거나 $ORACLE_HOME\network\admin에 일반적으로 클라이언트 컴퓨터의 hello tnsnames.ora 파일을 만듭니다.

Hello IP 교체 프로그램 `publicIpAddress` myVM1 및 myVM2

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

sqlplus 시작

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a>Data Guard 구성 테스트

### <a name="database-switchover-on-myvm1-primary"></a>myVM1(기본)에서 데이터베이스 전환

기본 toostandby (cdb1 toocdb1_stby)에서 tooswitch

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

이제 수 tooconnect toohello 대기 데이터베이스 수 있습니다.

sqlplus 시작

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a>myVM2(대기)에서 데이터베이스 다시 전환

다시, tooswitch myVM2에서 hello 다음 실행
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

다시 한 번 수 있어야 수 tooconnect toohello 주 데이터베이스

sqlplus 시작

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

이 hello 설치 및 Oracle linux에서 Data Guard의 구성을 완료 합니다.


## <a name="delete-virtual-machine"></a>가상 컴퓨터 삭제

Hello 다음 명령을 사용 하는 tooremove hello 리소스 그룹에서 VM을 수 없습니다 더 이상 필요 하 고 모든 관련 리소스입니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

[고가용성 가상 컴퓨터 만들기 자습서](../../linux/create-cli-complete.md)

[VM 배포 CLI 샘플 탐색](../../linux/cli-samples.md)
