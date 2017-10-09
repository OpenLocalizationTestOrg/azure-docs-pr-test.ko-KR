---
title: "Azure Linux VM에서 Oracle 골든 게이트 aaaImplement | Microsoft Docs"
description: "Oracle Golden Gate를 Azure 환경에서 빠르게 시작하고 실행합니다."
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="94575-103">Azure Linux VM에서 Oracle Golden Gate 구현</span><span class="sxs-lookup"><span data-stu-id="94575-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="94575-104">hello Azure CLI 사용된 toocreate 이며 hello 명령줄에서 또는 스크립트에서 Azure 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="94575-105">이 가이드를 세부 정보 hello Azure 마켓플레이스 갤러리 이미지에서 Oracle 12c toouse hello Azure CLI toodeploy 데이터베이스 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="94575-106">이 문서에서는 단계별 toocreate를 설치 하 고 Azure VM에서 Oracle 골든 게이트를 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="94575-107">시작 하기 전에 해야 Azure CLI 설치가 완료 된 후 해당 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="94575-108">자세한 내용은 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94575-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="94575-109">Hello 환경 준비</span><span class="sxs-lookup"><span data-stu-id="94575-109">Prepare hello environment</span></span>

<span data-ttu-id="94575-110">hello에 toocreate 2 Azure Vm을 필요한 tooperform hello Oracle 골든 게이트 설치 동일한 가용성 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="94575-111">toocreate hello Vm을 사용 하 여 hello 마켓플레이스 이미지는 **Oracle: Oracle-데이터베이스-Ee:12.1.0.2:latest**합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="94575-112">또한 toobe 편집기 vi Unix에 잘 알고 있어야 하 고 x11 (X Windows)에 대 한 기본적인 이해가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="94575-113">hello 다음은 hello 환경 구성 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="94575-114">**기본 사이트**</span><span class="sxs-lookup"><span data-stu-id="94575-114">**Primary site**</span></span> | <span data-ttu-id="94575-115">**복제 사이트**</span><span class="sxs-lookup"><span data-stu-id="94575-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="94575-116">**Oracle 릴리스**</span><span class="sxs-lookup"><span data-stu-id="94575-116">**Oracle release**</span></span> |<span data-ttu-id="94575-117">Oracle 12c 릴리스 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="94575-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="94575-118">Oracle 12c 릴리스 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="94575-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="94575-119">**컴퓨터 이름**</span><span class="sxs-lookup"><span data-stu-id="94575-119">**Machine name**</span></span> |<span data-ttu-id="94575-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="94575-120">myVM1</span></span> |<span data-ttu-id="94575-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="94575-121">myVM2</span></span> |
> | <span data-ttu-id="94575-122">**운영 체제**</span><span class="sxs-lookup"><span data-stu-id="94575-122">**Operating system**</span></span> |<span data-ttu-id="94575-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="94575-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="94575-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="94575-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="94575-125">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="94575-125">**Oracle SID**</span></span> |<span data-ttu-id="94575-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="94575-126">CDB1</span></span> |<span data-ttu-id="94575-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="94575-127">CDB1</span></span> |
> | <span data-ttu-id="94575-128">**복제 스키마**</span><span class="sxs-lookup"><span data-stu-id="94575-128">**Replication schema**</span></span> |<span data-ttu-id="94575-129">테스트</span><span class="sxs-lookup"><span data-stu-id="94575-129">TEST</span></span>|<span data-ttu-id="94575-130">테스트</span><span class="sxs-lookup"><span data-stu-id="94575-130">TEST</span></span> |
> | <span data-ttu-id="94575-131">**Golden Gate 소유자/복제**</span><span class="sxs-lookup"><span data-stu-id="94575-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="94575-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="94575-132">C##GGADMIN</span></span> |<span data-ttu-id="94575-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="94575-133">REPUSER</span></span> |
> | <span data-ttu-id="94575-134">**Golden Gate 프로세스**</span><span class="sxs-lookup"><span data-stu-id="94575-134">**Golden Gate process**</span></span> |<span data-ttu-id="94575-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="94575-135">EXTORA</span></span> |<span data-ttu-id="94575-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="94575-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="94575-137">TooAzure에 로그인</span><span class="sxs-lookup"><span data-stu-id="94575-137">Sign in tooAzure</span></span> 

<span data-ttu-id="94575-138">Tooyour hello로 Azure 구독에에서 로그인 [az 로그인](/cli/azure/#login) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="94575-139">그런 다음 지시 hello 화면에 나타나는 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="94575-140">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="94575-140">Create a resource group</span></span>

<span data-ttu-id="94575-141">Hello로 리소스 그룹 만들기 [az 그룹 만들기](/cli/azure/group#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="94575-142">Azure 리소스 그룹은 Azure 리소스가 배포되며 관리될 수 있는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="94575-143">hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `westus` 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="94575-144">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="94575-144">Create an availability set</span></span>

<span data-ttu-id="94575-145">단계 다음에 나오는 hello 선택 사항 이지만 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94575-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="94575-146">자세한 내용은 [Windows VM에 대한 Azure 가용성 집합 지침](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94575-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="94575-147">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="94575-147">Create a virtual machine</span></span>

<span data-ttu-id="94575-148">Hello로 VM을 만들 [az vm 만들기](/cli/azure/vm#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="94575-149">hello 다음 예제에서는 라는 두 개의 Vm `myVM1` 및 `myVM2`합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="94575-150">기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94575-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="94575-151">toouse 특정 키의 집합, hello를 사용 하 여 `--ssh-key-value` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="94575-152">myVM1(기본) 만들기:</span><span class="sxs-lookup"><span data-stu-id="94575-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="94575-153">VM을 만든 hello, 후 hello Azure CLI 다음 예제와 비슷한 toohello를 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="94575-154">(Hello를 메모해 `publicIpAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="94575-155">이 주소는 사용 되는 tooaccess hello VM입니다.)</span><span class="sxs-lookup"><span data-stu-id="94575-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="94575-156">myVM2(복제) 만들기:</span><span class="sxs-lookup"><span data-stu-id="94575-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="94575-157">Hello를 메모해 `publicIpAddress` 만들어진 후에 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="94575-158">연결에 대 한 hello TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="94575-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="94575-159">hello 다음 단계는 데 사용할 수 있는 tooaccess hello Oracle 데이터베이스 원격으로 tooconfigure 외부 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="94575-160">hello 다음 명령을 실행 tooconfigure hello 외부 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="94575-161">MyVM1 hello 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="94575-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="94575-162">hello 결과 응답 다음 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="94575-163">MyVM2 hello 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="94575-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="94575-164">Toohello 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="94575-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="94575-165">사용 하 여 hello 다음 명령은 toocreate hello 가상 컴퓨터와의 SSH 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="94575-166">Hello로 hello IP 주소를 교체 `publicIpAddress` 의 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="94575-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="94575-167">Hello 데이터베이스를 만드는 위치 myVM1 (기본)</span><span class="sxs-lookup"><span data-stu-id="94575-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="94575-168">Oracle 소프트웨어 hello 있으므로 hello 다음 단계는 tooinstall hello 데이터베이스 hello 마켓플레이스 이미지에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="94575-169">Hello 'oracle' superuser로 hello 소프트웨어를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="94575-170">hello 데이터베이스 만드는 위치:</span><span class="sxs-lookup"><span data-stu-id="94575-170">Create hello database:</span></span>

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
<span data-ttu-id="94575-171">출력에는 다음 응답 비슷한 toohello 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-171">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="94575-172">Hello ORACLE_SID 및 ORACLE_HOME 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="94575-173">필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 ORACLE_HOME 및 ORACLE_SID toohello.bashrc 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="94575-174">Oracle 수신기 시작</span><span class="sxs-lookup"><span data-stu-id="94575-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="94575-175">MyVM2에 hello 데이터베이스 만들기 (복제)</span><span class="sxs-lookup"><span data-stu-id="94575-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="94575-176">hello 데이터베이스 만드는 위치:</span><span class="sxs-lookup"><span data-stu-id="94575-176">Create hello database:</span></span>

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
<span data-ttu-id="94575-177">Hello ORACLE_SID 및 ORACLE_HOME 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="94575-178">필요에 따라는 이후 로그인에 대 한 이러한 설정을 저장할 수 있도록 추가 된 ORACLE_HOME 및 ORACLE_SID toohello.bashrc 파일을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="94575-179">Oracle 수신기 시작</span><span class="sxs-lookup"><span data-stu-id="94575-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="94575-180">Golden Gate 구성</span><span class="sxs-lookup"><span data-stu-id="94575-180">Configure Golden Gate</span></span> 
<span data-ttu-id="94575-181">이 섹션의 hello 단계를 수행 하는 tooconfigure 골든 게이트입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="94575-182">myVM1(기본)에서 보관 로그 모드 사용</span><span class="sxs-lookup"><span data-stu-id="94575-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="94575-183">강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="94575-184">Golden Gate 소프트웨어 다운로드</span><span class="sxs-lookup"><span data-stu-id="94575-184">Download Golden Gate software</span></span>
<span data-ttu-id="94575-185">toodownload hello Oracle 골든 게이트 소프트웨어, 단계를 수행 하는 전체 hello 준비 및:</span><span class="sxs-lookup"><span data-stu-id="94575-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="94575-186">Hello 다운로드 **fbo_ggs_Linux_x64_shiphome.zip** hello에서 파일 [Oracle 골든 게이트 다운로드 페이지](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="94575-187">Hello에서 제목 다운로드 **Oracle Linux x86-64에 대 한 Oracle GoldenGate 12.x.x.x**,.zip 파일 toodownload 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="94575-188">Hello.zip tooyour 클라이언트 컴퓨터 파일을 다운로드 한 후 복사 프로토콜 보안 (SCP) toocopy hello 파일 tooyour VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="94575-189">Hello.zip 파일 toohello 이동 **/opt** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="94575-190">그런 다음 hello 파일의 hello 소유자를 다음과 같이 변경.</span><span class="sxs-lookup"><span data-stu-id="94575-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="94575-191">Hello 파일을 (설치 hello Linux의 압축을 푸는 유틸리티 설치 되어 있지 않은 경우)의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="94575-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="94575-192">사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="94575-193">클라이언트 hello와 준비 VM toorun x11 (Windows 클라이언트에만 해당)</span><span class="sxs-lookup"><span data-stu-id="94575-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="94575-194">선택적 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-194">This is an optional step.</span></span> <span data-ttu-id="94575-195">Linux 클라이언트를 사용하거나 x11을 이미 설치한 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="94575-196">PuTTY 및 Xming tooyour Windows 컴퓨터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="94575-197">PuTTY 다운로드</span><span class="sxs-lookup"><span data-stu-id="94575-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="94575-198">Xming 다운로드</span><span class="sxs-lookup"><span data-stu-id="94575-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="94575-199">PuTTY를 설치한 후에 PuTTY 폴더 (예를 들어 C:\Program Files\PuTTY) hello, puttygen.exe (PuTTY 키 생성기)를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="94575-200">PuTTY 키 생성기에서,</span><span class="sxs-lookup"><span data-stu-id="94575-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="94575-201">키를 선택 hello toogenerate **생성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="94575-202">Hello 키의 hello 내용을 복사 (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="94575-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="94575-203">선택 hello **개인 키 저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="94575-204">다음을 선택 하 고, 나타나는 hello 경고를 무시 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Hello PuTTY 키 생성기 페이지의 스크린샷](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="94575-206">VM에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="94575-207">**authorized_keys**라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94575-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="94575-208">이 파일의 hello 키의 내용을 hello를 붙여 넣고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="94575-209">hello 키 hello 문자열을 포함 해야 `ssh-rsa`합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="94575-210">또한 hello 키의 내용을 hello 텍스트 한 줄 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="94575-211">PuTTY를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-211">Start PuTTY.</span></span> <span data-ttu-id="94575-212">Hello에 **범주** 창 선택 **연결** > **SSH** > **Auth**합니다. Hello에 **인증에 대 한 개인 키 파일** 상자 이전에 생성 toohello 키를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Hello 개인 키 설정 페이지의 스크린샷](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="94575-214">Hello에 **범주** 창 선택 **연결** > **SSH** > **X11**합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="94575-215">다음 hello 선택 **사용 X11 전달** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Hello X11 설정 페이지의 스크린샷](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="94575-217">Hello에 **범주** 창 너무 이동**세션**합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="94575-218">Hello 호스트 정보를 입력 한 다음 선택 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-218">Enter hello host information, and then select **Open**.</span></span>

  ![Hello 세션 페이지의 스크린샷](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="94575-220">Golden Gate 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="94575-220">Install Golden Gate software</span></span>

<span data-ttu-id="94575-221">tooinstall Oracle 골든 게이트 단계를 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="94575-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="94575-222">oracle로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-222">Sign in as oracle.</span></span> <span data-ttu-id="94575-223">(암호를 입력 하지 않고에 수 toosign 수 있어야 합니다.) Hello 설치를 시작 하기 전에 Xming 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="94575-224">'Oracle GoldenGate for Oracle Database 12c'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="94575-225">그런 다음 선택 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-225">Then select **Next** toocontinue.</span></span>

  ![Hello 설치 관리자 선택 설치 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="94575-227">Hello 소프트웨어 위치를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-227">Change hello software location.</span></span> <span data-ttu-id="94575-228">다음 hello 선택 **관리자 시작** 상자 하 고 hello 데이터베이스 위치를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="94575-229">선택 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-229">Select **Next** toocontinue.</span></span>

  ![Hello 설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="94575-231">Hello 인벤토리 디렉터리를 변경 하 고 다음 선택 **다음** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Hello 설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="94575-233">Hello에 **요약** 화면에서 **설치** toocontinue 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Hello 설치 관리자 선택 설치 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="94575-235">'루트'로 입력 정보 요청된 toorun 스크립트 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="94575-236">그렇다면 별도 세션을 열고, ssh toohello VM을 sudo tooroot 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="94575-237">**확인**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-237">Select **OK** continue.</span></span>

  ![Hello 설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="94575-239">Hello 설치가 완료 되 면 선택 **닫기** toocomplete hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Hello 설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="94575-241">myVM1(기본)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="94575-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="94575-242">만들거나 hello tnsnames.ora 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="94575-243">Hello 골든 게이트 소유자 및 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94575-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="94575-244">hello 소유자 계정에는 C# # 접두사가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="94575-245">Hello 골든 게이트 테스트 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94575-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="94575-246">Hello 매개 변수 파일의 압축 해제를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="94575-247">Hello 골든 게이트 명령줄 인터페이스 (ggsci)를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="94575-248">Hello (vi 명령 사용)에서 다음 toohello 추출 매개 변수 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="94575-249">Esc 키, ':wq!'를 눌러</span><span class="sxs-lookup"><span data-stu-id="94575-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="94575-250">toosave 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="94575-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="94575-251">extract--integrated extract를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="94575-252">extract 검사점을 설정하고 실시간 추출을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="94575-253">이 단계에서는 SCN 나중 다른 단원에서 사용 되는 시작 하는 hello를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="94575-254">myVM2(복제)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="94575-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="94575-255">만들거나 hello tnsnames.ora 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="94575-256">복제 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94575-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="94575-257">Golden Gate 테스트 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="94575-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="94575-258">REPLICAT 매개 변수 파일 tooreplicate 변경 내용:</span><span class="sxs-lookup"><span data-stu-id="94575-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="94575-259">REPORA 매개 변수 파일의 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="94575-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="94575-260">replicat 검사점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="94575-261">(MyVM1 및 myVM2) hello 복제 설정</span><span class="sxs-lookup"><span data-stu-id="94575-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="94575-262">1. MyVM2에 hello 복제 설정 (복제)</span><span class="sxs-lookup"><span data-stu-id="94575-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="94575-263">Hello 다음과 같이 hello 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="94575-264">그런 다음 hello 관리자 서비스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="94575-265">2. (기본) myVM1에 hello 복제를 설정</span><span class="sxs-lookup"><span data-stu-id="94575-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="94575-266">Hello 초기 로드 시작 오류를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="94575-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="94575-267">3. MyVM2에 hello 복제 설정 (복제)</span><span class="sxs-lookup"><span data-stu-id="94575-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="94575-268">하기 전에 얻은 hello hello 번호로 SCN 수를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="94575-269">hello 복제를 시작 하 고 새 레코드 tooTEST 테이블을 삽입 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="94575-270">작업 상태 보기 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="94575-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="94575-271">보고서 보기</span><span class="sxs-lookup"><span data-stu-id="94575-271">View reports</span></span>
<span data-ttu-id="94575-272">tooview는 hello 다음 명령을 실행 myVM1을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="94575-273">tooview는 hello 다음 명령을 실행 myVM2을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="94575-274">상태 및 기록 보기</span><span class="sxs-lookup"><span data-stu-id="94575-274">View status and history</span></span>
<span data-ttu-id="94575-275">tooview 상태 및 hello 다음 명령을 실행 myVM1에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="94575-276">tooview 상태 및 hello 다음 명령을 실행 myVM2에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="94575-277">Hello 설치 및 Oracle linux에서 골든 게이트의 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="94575-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="94575-278">Hello 가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="94575-278">Delete hello virtual machine</span></span>

<span data-ttu-id="94575-279">더 이상 필요 hello 다음 명령을 사용 하는 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="94575-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="94575-280">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94575-280">Next steps</span></span>

[<span data-ttu-id="94575-281">고가용성 가상 컴퓨터 만들기 자습서</span><span class="sxs-lookup"><span data-stu-id="94575-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="94575-282">VM 배포 CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="94575-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
