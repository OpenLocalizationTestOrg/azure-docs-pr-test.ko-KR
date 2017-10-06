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
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="195af-103">Azure Linux VM에서 Oracle Data Guard 구현</span><span class="sxs-lookup"><span data-stu-id="195af-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="195af-104">hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="195af-105">Hello Azure CLI toodeploy Oracle 12c hello 마켓플레이스 갤러리 이미지에서 데이터베이스를 사용 하 여이 가이드 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="195af-106">이 문서에서는 hello Oracle 데이터베이스를 만든 후 단계별 방법을 tooinstall 및 Azure VM에서 Data Guard를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="195af-107">시작 하기 전에 해야 Azure CLI 설치가 완료 된 후 해당 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="195af-108">자세한 내용은 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="195af-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="195af-109">Hello 환경 준비</span><span class="sxs-lookup"><span data-stu-id="195af-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="195af-110">가정</span><span class="sxs-lookup"><span data-stu-id="195af-110">Assumptions</span></span>

<span data-ttu-id="195af-111">hello에 toocreate 2 Azure Vm을 필요한 tooperform hello Oracle Data Guard를 설치, 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="195af-112">toocreate hello Vm을 사용 하 여 hello 마켓플레이스 이미지는 "Oracle: Oracle-데이터베이스-Ee:12.1.0.2:latest"입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="195af-113">hello 기본 VM (myVM1)에 실행 중인 Oracle 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="195af-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="195af-114">hello 대기 VM (myVM2)에 hello Oracle 소프트웨어가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="195af-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="195af-115">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="195af-115">Log in tooAzure</span></span> 

<span data-ttu-id="195af-116">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="195af-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-117">Create a resource group</span></span>

<span data-ttu-id="195af-118">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="195af-119">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="195af-120">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="195af-121">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-121">Create availability set</span></span>

<span data-ttu-id="195af-122">이 단계는 선택 사항이지만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="195af-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="195af-123">자세한 내용은 [Azure 가용성 집합 가이드](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="195af-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="195af-124">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-124">Create virtual machine</span></span>

<span data-ttu-id="195af-125">Hello로 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="195af-126">hello 다음 예제에서는 명명 된 2 개의 Vm `myVM1` 및 `myVM2`합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="195af-127">기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="195af-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="195af-128">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="195af-129">myVM1(기본) 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="195af-130">한 번 VM을 만든 hello, Azure CLI hello 정보 비슷한 toohello 다음 예제: hello 기록해 `publicIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="195af-131">이 주소는 사용 되는 tooaccess hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="195af-132">myVM2(대기) 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="195af-133">Hello를 메모해 `publicIpAddress` 생성 한 번도 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="195af-134">연결에 대 한 hello TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="195af-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="195af-135">hello 단계는 tooconfigure 외부 끝점을 허용 하는 Oracle DB hello를 원격으로 액세스 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="195af-136">myVM1에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="195af-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="195af-137">결과는 다음 응답 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="195af-138">myVM2에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="195af-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="195af-139">Toovirtual 컴퓨터 연결</span><span class="sxs-lookup"><span data-stu-id="195af-139">Connect toovirtual machine</span></span>

<span data-ttu-id="195af-140">사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="195af-141">Hello로 hello IP 주소를 교체 `publicIpAddress` 의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="195af-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="195af-142">myVM1(기본)에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="195af-143">Oracle 소프트웨어 hello 있으므로 hello 다음 단계는 tooinstall hello 데이터베이스 hello 마켓플레이스 이미지에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="195af-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="195af-144">hello 첫 번째 단계는 hello 'oracle' superuser로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="195af-145">hello 데이터베이스 만드는 위치:</span><span class="sxs-lookup"><span data-stu-id="195af-145">create hello database:</span></span>

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
<span data-ttu-id="195af-146">출력에는 다음 응답 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-146">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="195af-147">Hello ORACLE_SID 및 ORACLE_HOME 변수를 설정</span><span class="sxs-lookup"><span data-stu-id="195af-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="195af-148">필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 추가 된 ORACLE_HOME 및 ORACLE_SID toohello.bashrc 파일을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="195af-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="195af-149">데이터 가드 구성</span><span class="sxs-lookup"><span data-stu-id="195af-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="195af-150">myVM1(기본)에 보관 로그 모드를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="195af-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="195af-151">강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="195af-152">대기 다시 실행 로그 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="195af-153">(훨씬 이전 hello 복구에 만든)는 플래시 백을 켜려면 STANDBY_FILE_MANAGEMENT tooauto 설정</span><span class="sxs-lookup"><span data-stu-id="195af-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="195af-154">myVM1(기본)에 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="195af-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="195af-155">$ORACLE_HOME\network\admin 폴더에 hello tnsnames.ora 파일을 만들거나 편집</span><span class="sxs-lookup"><span data-stu-id="195af-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="195af-156">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-156">Add hello following entries</span></span>

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

<span data-ttu-id="195af-157">$ORACLE_HOME\network\admin 폴더에 hello listener.ora 파일을 만들거나 편집</span><span class="sxs-lookup"><span data-stu-id="195af-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="195af-158">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-158">Add hello following entries</span></span>

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

<span data-ttu-id="195af-159">Hello 수신기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="195af-160">myVM2(대기)에 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="195af-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="195af-161">$ORACLE_HOME\network\admin 폴더에 hello tnsnames.ora 파일을 만들거나 편집</span><span class="sxs-lookup"><span data-stu-id="195af-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="195af-162">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-162">Add hello following entries</span></span>

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

<span data-ttu-id="195af-163">$ORACLE_HOME\network\admin 폴더에 hello listener.ora 파일을 만들거나 편집</span><span class="sxs-lookup"><span data-stu-id="195af-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="195af-164">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-164">Add hello following entries</span></span>

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

<span data-ttu-id="195af-165">Hello 수신기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="195af-166">Data Guard Broker를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="195af-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="195af-167">데이터베이스 toomyVM2 복원 (대기)</span><span class="sxs-lookup"><span data-stu-id="195af-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="195af-168">매개 변수 파일을 만들 ' / tmp/initcdb1_stby.ora' hello 다음 내용으로</span><span class="sxs-lookup"><span data-stu-id="195af-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="195af-169">폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="195af-170">암호 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="195af-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="195af-171">myVM2에서 데이터베이스 시작</span><span class="sxs-lookup"><span data-stu-id="195af-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="195af-172">RMAN 유틸리티를 사용하여 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="195af-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="195af-173">Hello 다음 RMAN에서 명령 실행</span><span class="sxs-lookup"><span data-stu-id="195af-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="195af-174">Data Guard Broker를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="195af-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="195af-175">myVM1(기본)에서 Data Guard Broker 구성</span><span class="sxs-lookup"><span data-stu-id="195af-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="195af-176">SYS 및 암호 (운영 체제 인증을 사용 하지 안 함)를 사용 하 여 로그인 하 고 hello Data Guard 관리자를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="195af-177">Hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-177">Perform hello followings</span></span>

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

<span data-ttu-id="195af-178">Hello 구성 검토</span><span class="sxs-lookup"><span data-stu-id="195af-178">Review hello configuration</span></span>
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

<span data-ttu-id="195af-179">Hello Oracle Data Guard 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="195af-180">hello 다음 섹션에서는 연결 및 전환 tootest hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="195af-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="195af-181">클라이언트 컴퓨터에서 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="195af-181">Connect database from client machine</span></span>

<span data-ttu-id="195af-182">업데이트 하거나 $ORACLE_HOME\network\admin에 일반적으로 클라이언트 컴퓨터의 hello tnsnames.ora 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="195af-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="195af-183">Hello IP 교체 프로그램 `publicIpAddress` myVM1 및 myVM2</span><span class="sxs-lookup"><span data-stu-id="195af-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="195af-184">sqlplus 시작</span><span class="sxs-lookup"><span data-stu-id="195af-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="195af-185">Data Guard 구성 테스트</span><span class="sxs-lookup"><span data-stu-id="195af-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="195af-186">myVM1(기본)에서 데이터베이스 전환</span><span class="sxs-lookup"><span data-stu-id="195af-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="195af-187">기본 toostandby (cdb1 toocdb1_stby)에서 tooswitch</span><span class="sxs-lookup"><span data-stu-id="195af-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

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

<span data-ttu-id="195af-188">이제 수 tooconnect toohello 대기 데이터베이스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="195af-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="195af-189">sqlplus 시작</span><span class="sxs-lookup"><span data-stu-id="195af-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="195af-190">myVM2(대기)에서 데이터베이스 다시 전환</span><span class="sxs-lookup"><span data-stu-id="195af-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="195af-191">다시, tooswitch myVM2에서 hello 다음 실행</span><span class="sxs-lookup"><span data-stu-id="195af-191">tooswitch back, run hello followings on myVM2</span></span>
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

<span data-ttu-id="195af-192">다시 한 번 수 있어야 수 tooconnect toohello 주 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="195af-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="195af-193">sqlplus 시작</span><span class="sxs-lookup"><span data-stu-id="195af-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="195af-194">이 hello 설치 및 Oracle linux에서 Data Guard의 구성을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="195af-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="195af-195">가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="195af-195">Delete virtual machine</span></span>

<span data-ttu-id="195af-196">Hello 다음 명령을 사용 하는 tooremove hello 리소스 그룹에서 VM을 수 없습니다 더 이상 필요 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="195af-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="195af-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="195af-197">Next steps</span></span>

[<span data-ttu-id="195af-198">고가용성 가상 컴퓨터 만들기 자습서</span><span class="sxs-lookup"><span data-stu-id="195af-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="195af-199">VM 배포 CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="195af-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
