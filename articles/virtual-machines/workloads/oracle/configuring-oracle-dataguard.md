---
title: "Azure Linux VM에서 Oracle Data Guard 구현 | Microsoft Docs"
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
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="f58bf-103">Azure Linux VM에서 Oracle Data Guard 구현</span><span class="sxs-lookup"><span data-stu-id="f58bf-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="f58bf-104">명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="f58bf-105">이 가이드에서는 Azure CLI를 사용하여 Marketplace 갤러리 이미지에서 Oracle 12c 데이터베이스를 배포하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="f58bf-106">Oracle 데이터베이스를 만들면 이 문서에서는 Azure VM에서 Data Guard를 설치 및 구성하는 단계별 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="f58bf-107">시작하기 전에 Azure CLI가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="f58bf-108">자세한 내용은 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f58bf-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="f58bf-109">환경 준비</span><span class="sxs-lookup"><span data-stu-id="f58bf-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="f58bf-110">가정</span><span class="sxs-lookup"><span data-stu-id="f58bf-110">Assumptions</span></span>

<span data-ttu-id="f58bf-111">Oracle Data Guard 설치를 수행하려면 동일한 가용성 집합에서 두 개의 Azure VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="f58bf-112">VM을 만드는 데 사용하는 Marketplace 이미지는 "Oracle:Oracle-Database-Ee:12.1.0.2:latest"입니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="f58bf-113">기본 VM(myVM1)에 실행 중인 Oracle 인스턴스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="f58bf-114">대기 VM(myVM2)에는 Oracle 소프트웨어만 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="f58bf-115">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="f58bf-115">Log in to Azure</span></span> 

<span data-ttu-id="f58bf-116">[az login](/cli/azure/#login) 명령으로 Azure 구독에 로그인하고 화면의 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f58bf-117">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-117">Create a resource group</span></span>

<span data-ttu-id="f58bf-118">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f58bf-119">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f58bf-120">다음 예제는 `westus` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="f58bf-121">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-121">Create availability set</span></span>

<span data-ttu-id="f58bf-122">이 단계는 선택 사항이지만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="f58bf-123">자세한 내용은 [Azure 가용성 집합 가이드](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f58bf-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="f58bf-124">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-124">Create virtual machine</span></span>

<span data-ttu-id="f58bf-125">[az vm create](/cli/azure/vm#create) 명령을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f58bf-126">다음 예제에서는 `myVM1` 및 `myVM2`라고 하는 두 개의 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="f58bf-127">기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="f58bf-128">특정 키 집합을 사용하려면 `--ssh-key-value` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="f58bf-129">myVM1(기본) 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="f58bf-130">VM을 만든 후 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다. `publicIpAddress`를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="f58bf-131">이 주소는 VM에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-131">This address is used to access the VM.</span></span>

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

<span data-ttu-id="f58bf-132">myVM2(대기) 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="f58bf-133">만들어지면 `publicIpAddress`도 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="f58bf-134">연결에 대한 TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="f58bf-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="f58bf-135">단계는 Oracle DB를 원격으로 액세스할 수 있도록 하는 외부 끝점을 구성하는 것으로 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="f58bf-136">myVM1에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="f58bf-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="f58bf-137">결과가 다음 응답과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-137">Result should look similar to the following response:</span></span>

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

<span data-ttu-id="f58bf-138">myVM2에 대한 포트 열기</span><span class="sxs-lookup"><span data-stu-id="f58bf-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="f58bf-139">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="f58bf-139">Connect to virtual machine</span></span>

<span data-ttu-id="f58bf-140">다음 명령을 사용하여 가상 컴퓨터와의 SSH 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="f58bf-141">해당 IP 주소를 가상 컴퓨터의 `publicIpAddress`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="f58bf-142">myVM1(기본)에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="f58bf-143">Oracle 소프트웨어는 Marketplace 이미지에 이미 설치되어 있으므로 다음 단계에서 데이터베이스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="f58bf-144">첫 번째 단계는 'oracle' superuser로 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="f58bf-145">데이터베이스 만들기:</span><span class="sxs-lookup"><span data-stu-id="f58bf-145">create the database:</span></span>

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
<span data-ttu-id="f58bf-146">출력은 다음 응답과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-146">Outputs should look similar to the following response:</span></span>

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

<span data-ttu-id="f58bf-147">ORACLE_SID 및 ORACLE_HOME 변수 설정</span><span class="sxs-lookup"><span data-stu-id="f58bf-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="f58bf-148">필요에 따라 .bashrc 파일에 ORACLE_HOME 및 ORACLE_SID를 추가하여 후속 로그인을 위해 이러한 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="f58bf-149">데이터 가드 구성</span><span class="sxs-lookup"><span data-stu-id="f58bf-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="f58bf-150">myVM1(기본)에 보관 로그 모드를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f58bf-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="f58bf-151">강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="f58bf-152">대기 다시 실행 로그 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="f58bf-153">플래시백(복구를 훨씬 이전으로 만듦)을 켜고 STANDBY_FILE_MANAGEMENT를 자동으로 설정</span><span class="sxs-lookup"><span data-stu-id="f58bf-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="f58bf-154">myVM1(기본)에 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="f58bf-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="f58bf-155">$ORACLE_HOME\network\admin 폴더에 있는 tnsnames.ora 파일 편집 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="f58bf-156">다음 항목 추가</span><span class="sxs-lookup"><span data-stu-id="f58bf-156">Add the following entries</span></span>

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

<span data-ttu-id="f58bf-157">$ORACLE_HOME\network\admin 폴더에 있는 listener.ora 파일 편집 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="f58bf-158">다음 항목 추가</span><span class="sxs-lookup"><span data-stu-id="f58bf-158">Add the following entries</span></span>

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

<span data-ttu-id="f58bf-159">수신기 시작</span><span class="sxs-lookup"><span data-stu-id="f58bf-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="f58bf-160">myVM2(대기)에 서비스 설치</span><span class="sxs-lookup"><span data-stu-id="f58bf-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="f58bf-161">$ORACLE_HOME\network\admin 폴더에 있는 tnsnames.ora 파일 편집 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="f58bf-162">다음 항목 추가</span><span class="sxs-lookup"><span data-stu-id="f58bf-162">Add the following entries</span></span>

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

<span data-ttu-id="f58bf-163">$ORACLE_HOME\network\admin 폴더에 있는 listener.ora 파일 편집 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="f58bf-164">다음 항목 추가</span><span class="sxs-lookup"><span data-stu-id="f58bf-164">Add the following entries</span></span>

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

<span data-ttu-id="f58bf-165">수신기 시작</span><span class="sxs-lookup"><span data-stu-id="f58bf-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="f58bf-166">Data Guard Broker를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f58bf-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="f58bf-167">myVM2(대기)로 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="f58bf-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="f58bf-168">다음 내용으로 매개 변수 파일 '/tmp/initcdb1_stby.ora' 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="f58bf-169">폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="f58bf-170">암호 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="f58bf-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="f58bf-171">myVM2에서 데이터베이스 시작</span><span class="sxs-lookup"><span data-stu-id="f58bf-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="f58bf-172">RMAN 유틸리티를 사용하여 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="f58bf-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="f58bf-173">RMAN에서 다음 명령 실행</span><span class="sxs-lookup"><span data-stu-id="f58bf-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="f58bf-174">Data Guard Broker를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f58bf-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="f58bf-175">myVM1(기본)에서 Data Guard Broker 구성</span><span class="sxs-lookup"><span data-stu-id="f58bf-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="f58bf-176">Data Guard 관리자를 시작하고 SYS 및 암호(OS 인증을 사용하지 않음)를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="f58bf-177">다음 수행</span><span class="sxs-lookup"><span data-stu-id="f58bf-177">Perform the followings</span></span>

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

<span data-ttu-id="f58bf-178">구성 검토</span><span class="sxs-lookup"><span data-stu-id="f58bf-178">Review the configuration</span></span>
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

<span data-ttu-id="f58bf-179">Oracle Data Guard 설치를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="f58bf-180">다음 섹션에서는 연결 및 전환을 테스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="f58bf-181">클라이언트 컴퓨터에서 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="f58bf-181">Connect database from client machine</span></span>

<span data-ttu-id="f58bf-182">일반적으로 $ORACLE_HOME\network\admin에 있는 클라이언트 컴퓨터의 tnsnames.ora 파일을 업데이트하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="f58bf-183">myVM1 및 myVM2에 대한 IP를 `publicIpAddress`로 대체</span><span class="sxs-lookup"><span data-stu-id="f58bf-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="f58bf-184">sqlplus 시작</span><span class="sxs-lookup"><span data-stu-id="f58bf-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="f58bf-185">Data Guard 구성 테스트</span><span class="sxs-lookup"><span data-stu-id="f58bf-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="f58bf-186">myVM1(기본)에서 데이터베이스 전환</span><span class="sxs-lookup"><span data-stu-id="f58bf-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="f58bf-187">기본에서 대기로 전환하려면(cdb1에서 cdb1_stby로)</span><span class="sxs-lookup"><span data-stu-id="f58bf-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

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

<span data-ttu-id="f58bf-188">이제 대기 데이터베이스에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="f58bf-189">sqlplus 시작</span><span class="sxs-lookup"><span data-stu-id="f58bf-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="f58bf-190">myVM2(대기)에서 데이터베이스 다시 전환</span><span class="sxs-lookup"><span data-stu-id="f58bf-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="f58bf-191">다시 전환하려면 myVM2에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-191">To switch back, run the followings on myVM2</span></span>
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

<span data-ttu-id="f58bf-192">다시 한 번, 이제 주 데이터베이스에 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="f58bf-193">sqlplus 시작</span><span class="sxs-lookup"><span data-stu-id="f58bf-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="f58bf-194">Oracle linux에서 Data Guard의 설치 및 구성을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="f58bf-195">가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="f58bf-195">Delete virtual machine</span></span>

<span data-ttu-id="f58bf-196">더 이상 필요하지 않은 경우 다음 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f58bf-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f58bf-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f58bf-197">Next steps</span></span>

[<span data-ttu-id="f58bf-198">고가용성 가상 컴퓨터 만들기 자습서</span><span class="sxs-lookup"><span data-stu-id="f58bf-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="f58bf-199">VM 배포 CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="f58bf-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
