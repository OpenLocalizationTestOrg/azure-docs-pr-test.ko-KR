---
title: "Azure Linux 가상 컴퓨터에서 Oracle Data Guard 구현 | Microsoft Docs"
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
ms.openlocfilehash: 11492b85e95ddb39489e36c572af2a168b4c7af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="8dd07-103">Azure Linux 가상 컴퓨터에서 Oracle Data Guard 구현</span><span class="sxs-lookup"><span data-stu-id="8dd07-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="8dd07-104">Azure CLI는 명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-104">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="8dd07-105">이 문서에서는 Azure CLI를 사용하여 Azure Marketplace 이미지에서 Oracle Database 12c 데이터베이스를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-105">This article describes how to use Azure CLI to deploy an Oracle Database 12c database from the Azure Marketplace image.</span></span> <span data-ttu-id="8dd07-106">그런 다음 이 문서는 Azure VM(가상 컴퓨터)에서 Data Guard를 설치하고 구성하는 방법을 단계별로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-106">This article then shows you, step by step, how to install and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="8dd07-107">시작하기 전에 Azure CLI가 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="8dd07-108">자세한 내용은 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dd07-108">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="8dd07-109">환경 준비</span><span class="sxs-lookup"><span data-stu-id="8dd07-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="8dd07-110">가정</span><span class="sxs-lookup"><span data-stu-id="8dd07-110">Assumptions</span></span>

<span data-ttu-id="8dd07-111">Oracle Data Guard를 설치하려면 동일한 가용성 집합에서 두 개의 Azure VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-111">To install Oracle Data Guard, you need to create two Azure VMs on the same availability set:</span></span>

- <span data-ttu-id="8dd07-112">기본 VM(myVM1)에 실행 중인 Oracle 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-112">The primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="8dd07-113">대기 VM(myVM2)에는 Oracle 소프트웨어만 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-113">The standby VM (myVM2) has the Oracle software installed only.</span></span>

<span data-ttu-id="8dd07-114">VM을 만드는 데 사용하는 Marketplace 이미지는 Oracle:Oracle-Database-Ee:12.1.0.2:latest입니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-114">The Marketplace image that you use to create the VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="8dd07-115">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="8dd07-115">Sign in to Azure</span></span> 

<span data-ttu-id="8dd07-116">[az login](/cli/azure/#login) 명령을 사용하여 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-116">Sign in to your Azure subscription by using the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="8dd07-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8dd07-117">Create a resource group</span></span>

<span data-ttu-id="8dd07-118">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-118">Create a resource group by using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8dd07-119">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8dd07-120">다음 예제에서는 `westus` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-120">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="8dd07-121">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="8dd07-121">Create an availability set</span></span>

<span data-ttu-id="8dd07-122">가용성 집합 만들기는 선택 사항이지만 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="8dd07-123">자세한 내용은 [Azure 가용성 집합 지침](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8dd07-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="8dd07-124">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8dd07-124">Create a virtual machine</span></span>

<span data-ttu-id="8dd07-125">[az vm create](/cli/azure/vm#create) 명령을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-125">Create a VM by using the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="8dd07-126">다음 예제에서는 `myVM1` 및 `myVM2`라고 하는 VM 두 개를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-126">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="8dd07-127">또한 기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="8dd07-128">특정 키 집합을 사용하려면 `--ssh-key-value` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="8dd07-129">myVM1(기본) 만들기:</span><span class="sxs-lookup"><span data-stu-id="8dd07-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="8dd07-130">VM을 만든 후 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-130">After you create the VM, Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="8dd07-131">`publicIpAddress` 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-131">Note the value of `publicIpAddress`.</span></span> <span data-ttu-id="8dd07-132">이 주소는 VM에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-132">You use this address to access the VM.</span></span>

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

<span data-ttu-id="8dd07-133">myVM2(대기)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="8dd07-134">myVM2를 만든 후 `publicIpAddress` 값을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-134">Note the value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="8dd07-135">연결에 대한 TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="8dd07-135">Open the TCP port for connectivity</span></span>

<span data-ttu-id="8dd07-136">이 단계에서는 Oracle 데이터베이스에 대한 원격 액세스를 허용하는 외부 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-136">This step configures external endpoints, which allow remote access to the Oracle database.</span></span>

<span data-ttu-id="8dd07-137">myVM1에 대한 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="8dd07-137">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="8dd07-138">결과는 다음 응답과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-138">The result should look similar to the following response:</span></span>

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

<span data-ttu-id="8dd07-139">myVM2에 대한 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="8dd07-139">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="8dd07-140">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="8dd07-140">Connect to the virtual machine</span></span>

<span data-ttu-id="8dd07-141">다음 명령을 사용하여 가상 컴퓨터와의 SSH 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-141">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="8dd07-142">해당 IP 주소를 가상 컴퓨터의 `publicIpAddress` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-142">Replace the IP address with the `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="8dd07-143">myVM1(기본)에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="8dd07-143">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="8dd07-144">Oracle 소프트웨어는 Marketplace 이미지에 이미 설치되어 있으므로 다음 단계에서 데이터베이스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-144">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="8dd07-145">Oracle superuser로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-145">Switch to the Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="8dd07-146">데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-146">Create the database:</span></span>

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
<span data-ttu-id="8dd07-147">출력은 다음 응답과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-147">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="8dd07-148">ORACLE_SID 및 ORACLE_HOME 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-148">Set the ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="8dd07-149">필요에 따라 /home/oracle/.bashrc 파일에 ORACLE_HOME 및 ORACLE_SID를 추가하여 후속 로그인을 위해 이러한 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-149">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="8dd07-150">Data Guard 구성</span><span class="sxs-lookup"><span data-stu-id="8dd07-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="8dd07-151">myVM1(기본)에서 보관 로그 모드 사용</span><span class="sxs-lookup"><span data-stu-id="8dd07-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="8dd07-152">강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="8dd07-153">대기 다시 실행 로그를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="8dd07-154">복구가 훨씬 용이해지는 플래시백을 설정하고 STANDBY\_FILE\_MANAGEMENT를 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT to auto.</span></span> <span data-ttu-id="8dd07-155">그런 다음 SQL*Plus를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="8dd07-156">myVM1(기본)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="8dd07-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="8dd07-157">$ORACLE_HOME\network\admin 폴더에서 tnsnames.ora 파일을 편집하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-157">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8dd07-158">다음 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-158">Add the following entries:</span></span>

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

<span data-ttu-id="8dd07-159">$ORACLE_HOME\network\admin 폴더에서 listener.ora 파일을 편집하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-159">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8dd07-160">다음 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-160">Add the following entries:</span></span>

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

<span data-ttu-id="8dd07-161">Data Guard Broker를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="8dd07-162">수신기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-162">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="8dd07-163">myVM2(대기)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="8dd07-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="8dd07-164">myVM2에 대해 SSH를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-164">SSH to myVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="8dd07-165">Oracle로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="8dd07-166">$ORACLE_HOME\network\admin 폴더에서 tnsnames.ora 파일을 편집하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-166">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8dd07-167">다음 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-167">Add the following entries:</span></span>

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

<span data-ttu-id="8dd07-168">$ORACLE_HOME\network\admin 폴더에서 listener.ora 파일을 편집하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-168">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="8dd07-169">다음 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-169">Add the following entries:</span></span>

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

<span data-ttu-id="8dd07-170">수신기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-170">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-the-database-to-myvm2-standby"></a><span data-ttu-id="8dd07-171">myVM2(대기)로 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="8dd07-171">Restore the database to myVM2 (standby)</span></span>

<span data-ttu-id="8dd07-172">다음 콘텐츠로 매개 변수 파일 /tmp/initcdb1_stby.ora를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-172">Create the parameter file /tmp/initcdb1_stby.ora with the following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="8dd07-173">폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="8dd07-174">암호 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="8dd07-175">myVM2에서 데이터베이스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-175">Start the database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="8dd07-176">RMAN 도구를 사용하여 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-176">Restore the database by using the RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="8dd07-177">RMAN에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-177">Run the following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="8dd07-178">명령이 완료되면 다음과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-178">You should see messages similar to the following when the command is completed.</span></span> <span data-ttu-id="8dd07-179">RMAN을 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="8dd07-180">필요에 따라 /home/oracle/.bashrc 파일에 ORACLE_HOME 및 ORACLE_SID를 추가하여 후속 로그인을 위해 이러한 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-180">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="8dd07-181">Data Guard Broker를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="8dd07-182">myVM1(기본)에서 Data Guard Broker 구성</span><span class="sxs-lookup"><span data-stu-id="8dd07-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="8dd07-183">Data Guard Manager를 시작하고 SYS 및 암호를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="8dd07-184">OS 인증을 사용하지 마세요. 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-184">(Do not use OS authentication.) Perform the following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="8dd07-185">구성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-185">Review the configuration:</span></span>
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

<span data-ttu-id="8dd07-186">Oracle Data Guard 설정이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-186">You've completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="8dd07-187">다음 섹션에서는 연결 및 전환을 테스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-187">The next section shows you how to test the connectivity and switch over.</span></span>

### <a name="connect-the-database-from-the-client-machine"></a><span data-ttu-id="8dd07-188">클라이언트 컴퓨터에서 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="8dd07-188">Connect the database from the client machine</span></span>

<span data-ttu-id="8dd07-189">클라이언트 컴퓨터에서 tnsnames.ora 파일을 업데이트하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-189">Update or create the tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="8dd07-190">이 파일은 일반적으로 $ORACLE_HOME\network\admin에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="8dd07-191">해당 IP 주소를 myVM1 및 myVM2의 `publicIpAddress` 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-191">Replace the IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="8dd07-192">SQL*Plus를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-the-data-guard-configuration"></a><span data-ttu-id="8dd07-193">Data Guard 구성 테스트</span><span class="sxs-lookup"><span data-stu-id="8dd07-193">Test the Data Guard configuration</span></span>

### <a name="switch-over-the-database-on-myvm1-primary"></a><span data-ttu-id="8dd07-194">myVM1(기본)에서 데이터베이스 전환</span><span class="sxs-lookup"><span data-stu-id="8dd07-194">Switch over the database on myVM1 (primary)</span></span>

<span data-ttu-id="8dd07-195">기본에서 대기(cdb1에서 cdb1_stby)로 전환하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-195">To switch from primary to standby (cdb1 to cdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="8dd07-196">이제 대기 데이터베이스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-196">You can now connect to the standby database.</span></span>

<span data-ttu-id="8dd07-197">SQL*Plus를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-the-database-on-myvm2-standby"></a><span data-ttu-id="8dd07-198">myVM2(대기)에서 데이터베이스 전환</span><span class="sxs-lookup"><span data-stu-id="8dd07-198">Switch over the database on myVM2 (standby)</span></span>

<span data-ttu-id="8dd07-199">전환하려면 myVM2에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-199">To switch over, run the following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="8dd07-200">다시 한번, 주 데이터베이스에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-200">Once again, you should now be able to connect to the primary database.</span></span>

<span data-ttu-id="8dd07-201">SQL*Plus를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="8dd07-202">Oracle Linux에서 Data Guard의 설치 및 구성을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-202">You've finished the installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="8dd07-203">가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="8dd07-203">Delete the virtual machine</span></span>

<span data-ttu-id="8dd07-204">더 이상 VM이 필요하지 않은 경우 다음 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8dd07-204">When you no longer need the VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8dd07-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8dd07-205">Next steps</span></span>

[<span data-ttu-id="8dd07-206">자습서: 고가용성 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8dd07-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="8dd07-207">VM 배포 Azure CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="8dd07-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
