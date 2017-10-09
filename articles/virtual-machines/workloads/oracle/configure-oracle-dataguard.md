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
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="b9a8c-103">Azure Linux 가상 컴퓨터에서 Oracle Data Guard 구현</span><span class="sxs-lookup"><span data-stu-id="b9a8c-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="b9a8c-104">Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="b9a8c-105">이 문서에서는 toouse Azure CLI toodeploy Oracle 데이터베이스 12c hello Azure 마켓플레이스 이미지 로부터 데이터베이스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="b9a8c-106">이 문서의 다음 방법을 보여 줍니다, 단계별 방법 tooinstall 및 Azure 가상 컴퓨터 (VM)에서 Data Guard를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="b9a8c-107">시작하기 전에 Azure CLI가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="b9a8c-108">자세한 내용은 참조 hello [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="b9a8c-109">Hello 환경 준비</span><span class="sxs-lookup"><span data-stu-id="b9a8c-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="b9a8c-110">가정</span><span class="sxs-lookup"><span data-stu-id="b9a8c-110">Assumptions</span></span>

<span data-ttu-id="b9a8c-111">hello에 toocreate 2 Azure Vm을 필요한 Oracle Data Guard tooinstall 동일한 가용성 집합:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="b9a8c-112">hello 기본 VM (myVM1)에 실행 중인 Oracle 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="b9a8c-113">hello 대기 VM (myVM2)에 hello Oracle 소프트웨어가 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="b9a8c-114">hello 마켓플레이스 이미지 toocreate hello Vm을 사용 하는 Oracle: Oracle-데이터베이스-Ee:12.1.0.2:latest 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="b9a8c-115">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="b9a8c-115">Sign in tooAzure</span></span> 

<span data-ttu-id="b9a8c-116">Hello를 사용 하 여 Azure 구독 tooyour 로그인 [az 로그인](/cli/azure/#login) 명령 열고 지시를 따른 hello 화면에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="b9a8c-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b9a8c-117">Create a resource group</span></span>

<span data-ttu-id="b9a8c-118">Hello를 사용 하 여 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="b9a8c-119">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b9a8c-120">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="b9a8c-121">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="b9a8c-121">Create an availability set</span></span>

<span data-ttu-id="b9a8c-122">가용성 집합 만들기는 선택 사항이지만 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="b9a8c-123">자세한 내용은 [Azure 가용성 집합 지침](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="b9a8c-124">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b9a8c-124">Create a virtual machine</span></span>

<span data-ttu-id="b9a8c-125">Hello를 사용 하 여 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="b9a8c-126">hello 다음 예제에서는 라는 두 개의 Vm `myVM1` 및 `myVM2`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="b9a8c-127">또한 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="b9a8c-128">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="b9a8c-129">myVM1(기본) 만들기:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="b9a8c-130">Hello VM을 만든 후 Azure CLI 정보 비슷한 toohello를 다음 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="b9a8c-131">Hello 값을 기록해 둡니다 `publicIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="b9a8c-132">VM이 주소 tooaccess hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="b9a8c-133">myVM2(대기)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="b9a8c-134">Hello 값을 기록해 둡니다 `publicIpAddress` myVM2을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="b9a8c-135">연결에 대 한 hello TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="b9a8c-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="b9a8c-136">이 단계에서는 원격 액세스 toohello Oracle 데이터베이스를 허용 하는 외부 끝점을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="b9a8c-137">MyVM1 hello 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="b9a8c-138">hello 결과 응답 다음 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="b9a8c-139">MyVM2 hello 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="b9a8c-140">Toohello 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="b9a8c-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="b9a8c-141">사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="b9a8c-142">Hello로 hello IP 주소를 교체 `publicIpAddress` 가상 컴퓨터에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="b9a8c-143">Hello 데이터베이스를 만드는 위치 myVM1 (기본)</span><span class="sxs-lookup"><span data-stu-id="b9a8c-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="b9a8c-144">Oracle 소프트웨어 hello 있으므로 hello 다음 단계는 tooinstall hello 데이터베이스 hello 마켓플레이스 이미지에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="b9a8c-145">Toohello Oracle superuser을 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="b9a8c-146">hello 데이터베이스 만드는 위치:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-146">Create hello database:</span></span>

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
<span data-ttu-id="b9a8c-147">출력에는 다음 응답 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="b9a8c-148">Hello ORACLE_SID 및 ORACLE_HOME 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="b9a8c-149">필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 ORACLE_HOME 및 ORACLE_SID toohello /home/oracle/.bashrc 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="b9a8c-150">Data Guard 구성</span><span class="sxs-lookup"><span data-stu-id="b9a8c-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="b9a8c-151">myVM1(기본)에서 보관 로그 모드 사용</span><span class="sxs-lookup"><span data-stu-id="b9a8c-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="b9a8c-152">강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="b9a8c-153">대기 다시 실행 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="b9a8c-154">(하면을 복구 훨씬 쉽게) 플래시 백을 설정 하 고 대기 모드를 설정\_파일\_관리 tooauto 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="b9a8c-155">그런 다음 SQL*Plus를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="b9a8c-156">myVM1(기본)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="b9a8c-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="b9a8c-157">편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello tnsnames.ora 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b9a8c-158">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-158">Add hello following entries:</span></span>

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

<span data-ttu-id="b9a8c-159">편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello listener.ora 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b9a8c-160">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-160">Add hello following entries:</span></span>

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

<span data-ttu-id="b9a8c-161">Data Guard Broker를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="b9a8c-162">Hello 수신기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="b9a8c-163">myVM2(대기)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="b9a8c-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="b9a8c-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="b9a8c-165">Oracle로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="b9a8c-166">편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello tnsnames.ora 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b9a8c-167">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-167">Add hello following entries:</span></span>

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

<span data-ttu-id="b9a8c-168">편집 하거나 hello $ORACLE_HOME\network\admin 폴더에 있는 hello listener.ora 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="b9a8c-169">Hello 다음 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-169">Add hello following entries:</span></span>

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

<span data-ttu-id="b9a8c-170">Hello 수신기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="b9a8c-171">Hello 데이터베이스 toomyVM2 복원 (대기)</span><span class="sxs-lookup"><span data-stu-id="b9a8c-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="b9a8c-172">Hello 매개 변수 파일 /tmp/initcdb1_stby.ora를 내용을 따라 hello로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="b9a8c-173">폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="b9a8c-174">암호 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="b9a8c-175">MyVM2 시작 hello 데이터베이스 위치:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="b9a8c-176">Hello RMAN 도구를 사용 하 여 hello 데이터베이스를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="b9a8c-177">Hello 다음 RMAN에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="b9a8c-178">Hello 명령이 완료 되 면 비슷한 toohello 다음 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="b9a8c-179">RMAN을 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="b9a8c-180">필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 ORACLE_HOME 및 ORACLE_SID toohello /home/oracle/.bashrc 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="b9a8c-181">Data Guard Broker를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="b9a8c-182">myVM1(기본)에서 Data Guard Broker 구성</span><span class="sxs-lookup"><span data-stu-id="b9a8c-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="b9a8c-183">Data Guard Manager를 시작하고 SYS 및 암호를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="b9a8c-184">OS 인증을 사용하지 마세요. Hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="b9a8c-185">Hello 구성 검토:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-185">Review hello configuration:</span></span>
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

<span data-ttu-id="b9a8c-186">Hello Oracle Data Guard 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="b9a8c-187">hello 다음 섹션에는 tootest hello 연결 하 고 전환 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="b9a8c-188">Hello 데이터베이스 hello 클라이언트 컴퓨터에서 연결</span><span class="sxs-lookup"><span data-stu-id="b9a8c-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="b9a8c-189">업데이트 또는 클라이언트 컴퓨터의 hello tnsnames.ora 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="b9a8c-190">이 파일은 일반적으로 $ORACLE_HOME\network\admin에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="b9a8c-191">Hello IP 주소를 교체 하면 `publicIpAddress` myVM1 및 myVM2 값:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="b9a8c-192">SQL*Plus를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="b9a8c-193">테스트 hello Data Guard 구성</span><span class="sxs-lookup"><span data-stu-id="b9a8c-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="b9a8c-194">(기본) myVM1 hello 데이터베이스 전환</span><span class="sxs-lookup"><span data-stu-id="b9a8c-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="b9a8c-195">기본 toostandby (cdb1 toocdb1_stby)에서 tooswitch:</span><span class="sxs-lookup"><span data-stu-id="b9a8c-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="b9a8c-196">Toohello 대기 데이터베이스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="b9a8c-197">SQL*Plus를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="b9a8c-198">MyVM2 hello 데이터베이스 전환 (대기)</span><span class="sxs-lookup"><span data-stu-id="b9a8c-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="b9a8c-199">조치 tooswitch myVM2 hello 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="b9a8c-200">다시 한 번 수 tooconnect toohello 주 데이터베이스 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="b9a8c-201">SQL*Plus를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="b9a8c-202">Oracle Linux에서 Data Guard의 hello 설치 및 구성 작업을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="b9a8c-203">Hello 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="b9a8c-203">Delete hello virtual machine</span></span>

<span data-ttu-id="b9a8c-204">더 이상 VM hello 필요 hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스에 따라 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9a8c-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b9a8c-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9a8c-205">Next steps</span></span>

[<span data-ttu-id="b9a8c-206">자습서: 고가용성 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="b9a8c-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="b9a8c-207">VM 배포 Azure CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="b9a8c-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
