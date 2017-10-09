---
title: "Azure VM에서 Oracle 데이터베이스 aaaCreate | Microsoft Docs"
description: "Azure 환경에서 Oracle Database 12c 데이터베이스를 신속하게 가동하고 실행합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Azure VM에서 Oracle 데이터베이스 만들기

Hello Azure CLI toodeploy hello에서 Azure 가상 컴퓨터를 사용 하 여이 가이드 정보 [Oracle 마켓플레이스 갤러리 이미지](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) 의 순서로 toocreate Oracle 12c 데이터베이스입니다. Hello 서버 배포 되 면 SSH를 통해 순서 tooconfigure hello Oracle 데이터베이스에 연결 합니다. 

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

이 퀵 스타트의 2.0.4 hello Azure CLI 버전을 실행 되 고 있는지 필요 tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여 이후 버전입니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다. 

hello 다음 예제에서는 명명 된 리소스 그룹 *myResourceGroup* hello에 *eastus* 위치 합니다.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기

가상 컴퓨터 (VM) toocreate hello를 사용 하 여 [az vm 만들기](/cli/azure/vm#create) 명령입니다. 

hello 다음 예제에서는 V `myVM`합니다. 또한 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다. toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Hello VM을 만든 후 Azure CLI 정보 비슷한 toohello를 다음 예제에서는 표시 됩니다. Hello 값을 확인 `publicIpAddress`합니다. VM이 주소 tooaccess hello를 사용 합니다.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Toohello VM 연결

VM hello로 SSH 세션 toocreate hello 다음 명령을 사용 합니다. Hello로 hello IP 주소를 교체 `publicIpAddress` VM에 대 한 값입니다.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Hello 데이터베이스 만들기

hello Oracle 소프트웨어는 hello 마켓플레이스 이미지에 이미 설치 되어 있습니다. 다음과 같이 샘플 데이터베이스를 만듭니다. 

1.  Toohello 전환 *oracle* superuser, 다음 로깅에 대 한 hello 수신기를 초기화 합니다.

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    hello 출력은 toohello 다음과 유사 합니다.

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  hello 데이터베이스 만드는 위치:

    ```bash
    dbca -silent \
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

    몇 분 toocreate hello 데이터베이스가 필요합니다.

3. Oracle 변수를 설정합니다.

Tooset 두 환경 변수를 연결 하기 전에 필요한: *ORACLE_HOME* 및 *ORACLE_SID*합니다.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
또한 ORACLE_HOME 및 ORACLE_SID 변수 toohello.bashrc 파일을 추가할 수 있습니다. 향후 로그인을 위한 hello 환경 변수를 저장은이 합니다. Hello 다음 확인 문이 toohello 추가 되었는지 `~/.bashrc` 원하는 편집기를 사용 하 여 파일입니다.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Oracle EM Express 연결

사용할 수 있는 GUI 관리 도구에 대 한 tooexplore hello 데이터베이스 Oracle EM Express를 설정 합니다. tooconnect tooOracle EM Express를 먼저 설정 해야 Oracle에서 hello 포트입니다. 

1. Sqlplus를 사용 하 여 tooyour 데이터베이스를 연결 합니다.

    ```bash
    sqlplus / as sysdba
    ```

2. 연결 되 면 hello 포트 5502 EM Express에 대 한 설정

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. 열기 hello 컨테이너 PDB1 없다면 hello 상태를 이미 열려 있지만 첫 번째 확인.

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    hello 출력은 toohello 다음과 유사 합니다.

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. 경우에 대 한 OPEN_MODE hello `PDB1` 읽기/쓰기, 그러고 나 서 다음 명령을 tooopen hello PDB1 않습니다:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Tootype 해야 `quit` tooend hello sqlplus 세션 유형과 `exit` hello oracle 사용자의 toologout 합니다.

## <a name="automate-database-startup-and-shutdown"></a>데이터베이스 시작 및 종료 자동화

기본적으로 hello Oracle 데이터베이스 hello VM을 다시 시작할 때에 자동으로 시작 하지 않습니다. tooset hello Oracle 데이터베이스 toostart 자동으로에 처음 로그인 루트 라고 합니다. 그런 다음 일부 시스템 파일을 만들고 업데이트합니다.

1. 루트로 로그인합니다.
    ```bash
    sudo su -
    ```

2.  Hello 파일을 편집 하 여 원하는 편집기를 사용 하 여 `/etc/oratab` hello 기본값을 변경 하 고 `N` 너무`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  라는 파일을 만들어 `/etc/init.d/dbora` 붙여넣기 hello 내용에 따라:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  *chmod*를 사용하여 다음과 같이 파일에 대한 권한을 변경합니다.

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  다음과 같이 시작 및 종료에 대한 기호 링크를 만듭니다.

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest 변경 내용을 hello VM을 다시 시작 합니다.

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>연결을 위한 포트 열기

hello 마지막 작업은 tooconfigure 일부 외부 끝점입니다. tooset hello hello VM을 보호 하는 Azure 네트워크 보안 그룹, 먼저 hello (해야 퇴장 당 했습니다 SSH에서 이전 단계에서 다시 부팅 하는 경우) 하는 VM에에서 SSH 세션을 종료 합니다. 

1.  tooopen hello 끝점 tooaccess hello Oracle 데이터베이스를 원격으로 사용 된 네트워크 보안 그룹 규칙을 만들 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 다음과 같습니다. 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  Oracle EM Express tooaccess을 원격으로 사용 하는 tooopen hello 끝점 사용 하는 네트워크 보안 그룹 규칙을 만드십시오 [az 네트워크 nsg 규칙 만들기](/cli/azure/network/nsg/rule#create) 다음과 같습니다.

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. 필요한 경우 다시 사용 하 여 VM의 hello 공용 IP 주소를 가져올 [az 네트워크 공개 ip 표시](/cli/azure/network/public-ip#show) 다음과 같습니다.

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  브라우저에서 EM Express를 연결합니다. 브라우저가 EM Express와 호환되는지 확인합니다(Flash 설치 필요). 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Hello를 사용 하 여 로그인 할 수 있습니다 **SYS** 계정을 한 hello 확인 **sysdba로** 확인란을 선택 합니다. 사용 하 여 hello 암호 **OraPasswd1** 설치 중 설정 합니다. 

![Hello Oracle OEM Express 로그인 페이지의 스크린샷](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>리소스 정리

Hello 했으면 Azure에서 Oracle 데이터베이스를 탐색 하 고 hello VM은 더 이상 필요 하지을 사용할 수 없습니다 [az 그룹 삭제](/cli/azure/group#delete) tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 명령입니다.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>다음 단계

[Azure의 다른 Oracle 솔루션](oracle-considerations.md)에 대해 알아봅니다. 

Hello 시도 [설치 및 저장소 관리를 자동화 된 Oracle 구성](configure-oracle-asm.md) 자습서입니다.
