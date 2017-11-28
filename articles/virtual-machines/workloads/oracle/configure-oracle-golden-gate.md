---
title: "Azure Linux VM에서 Oracle Golden Gate 구현 | Microsoft Docs"
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
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="ae812-103">Azure Linux VM에서 Oracle Golden Gate 구현</span><span class="sxs-lookup"><span data-stu-id="ae812-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="ae812-104">명령줄 또는 스크립트에서 Azure 리소스를 만들고 관리하는 데 Azure CLI가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="ae812-105">이 가이드에서는 Azure CLI를 사용하여 Azure Marketplace 갤러리 이미지에서 Oracle 12c 데이터베이스를 배포하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="ae812-106">이 문서에서는 Azure VM에서 Oracle Golden Gate를 만들고, 설치 및 구성하는 방법을 단계별로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="ae812-107">시작하기 전에 Azure CLI가 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="ae812-108">자세한 내용은 [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae812-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="ae812-109">환경 준비</span><span class="sxs-lookup"><span data-stu-id="ae812-109">Prepare the environment</span></span>

<span data-ttu-id="ae812-110">Oracle Golden Gate 설치를 수행하려면 동일한 가용성 집합에서 두 개의 Azure VM을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="ae812-111">VM을 만드는 데 사용하는 Marketplace 이미지는 **Oracle:Oracle-Database-Ee:12.1.0.2:latest**입니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="ae812-112">Unix 편집기 vi를 잘 알고 있고 x11(X Windows)을 기본적으로 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="ae812-113">다음은 환경 구성에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="ae812-114">**기본 사이트**</span><span class="sxs-lookup"><span data-stu-id="ae812-114">**Primary site**</span></span> | <span data-ttu-id="ae812-115">**복제 사이트**</span><span class="sxs-lookup"><span data-stu-id="ae812-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="ae812-116">**Oracle 릴리스**</span><span class="sxs-lookup"><span data-stu-id="ae812-116">**Oracle release**</span></span> |<span data-ttu-id="ae812-117">Oracle 12c 릴리스 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="ae812-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="ae812-118">Oracle 12c 릴리스 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="ae812-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="ae812-119">**컴퓨터 이름**</span><span class="sxs-lookup"><span data-stu-id="ae812-119">**Machine name**</span></span> |<span data-ttu-id="ae812-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="ae812-120">myVM1</span></span> |<span data-ttu-id="ae812-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="ae812-121">myVM2</span></span> |
> | <span data-ttu-id="ae812-122">**운영 체제**</span><span class="sxs-lookup"><span data-stu-id="ae812-122">**Operating system**</span></span> |<span data-ttu-id="ae812-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="ae812-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="ae812-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="ae812-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="ae812-125">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="ae812-125">**Oracle SID**</span></span> |<span data-ttu-id="ae812-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="ae812-126">CDB1</span></span> |<span data-ttu-id="ae812-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="ae812-127">CDB1</span></span> |
> | <span data-ttu-id="ae812-128">**복제 스키마**</span><span class="sxs-lookup"><span data-stu-id="ae812-128">**Replication schema**</span></span> |<span data-ttu-id="ae812-129">테스트</span><span class="sxs-lookup"><span data-stu-id="ae812-129">TEST</span></span>|<span data-ttu-id="ae812-130">테스트</span><span class="sxs-lookup"><span data-stu-id="ae812-130">TEST</span></span> |
> | <span data-ttu-id="ae812-131">**Golden Gate 소유자/복제**</span><span class="sxs-lookup"><span data-stu-id="ae812-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="ae812-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="ae812-132">C##GGADMIN</span></span> |<span data-ttu-id="ae812-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="ae812-133">REPUSER</span></span> |
> | <span data-ttu-id="ae812-134">**Golden Gate 프로세스**</span><span class="sxs-lookup"><span data-stu-id="ae812-134">**Golden Gate process**</span></span> |<span data-ttu-id="ae812-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="ae812-135">EXTORA</span></span> |<span data-ttu-id="ae812-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="ae812-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="ae812-137">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="ae812-137">Sign in to Azure</span></span> 

<span data-ttu-id="ae812-138">[az login](/cli/azure/#login) 명령을 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="ae812-139">그런 다음 화면에 나타나는 지침에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="ae812-140">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ae812-140">Create a resource group</span></span>

<span data-ttu-id="ae812-141">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ae812-142">Azure 리소스 그룹은 Azure 리소스가 배포되며 관리될 수 있는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="ae812-143">다음 예제는 `westus` 위치에 `myResourceGroup`이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="ae812-144">가용성 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="ae812-144">Create an availability set</span></span>

<span data-ttu-id="ae812-145">다음 단계는 선택 사항이지만 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-145">The following step is optional but recommended.</span></span> <span data-ttu-id="ae812-146">자세한 내용은 [Windows VM에 대한 Azure 가용성 집합 지침](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae812-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="ae812-147">가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ae812-147">Create a virtual machine</span></span>

<span data-ttu-id="ae812-148">[az vm create](/cli/azure/vm#create) 명령을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="ae812-149">다음 예제에서는 `myVM1` 및 `myVM2`라고 하는 VM 두 개를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="ae812-150">기본 키 위치에 SSH 키가 없는 경우 이 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="ae812-151">특정 키 집합을 사용하려면 `--ssh-key-value` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="ae812-152">myVM1(기본) 만들기:</span><span class="sxs-lookup"><span data-stu-id="ae812-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="ae812-153">VM을 만든 후 Azure CLI는 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="ae812-154">`publicIpAddress`를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="ae812-155">이 주소는 VM에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="ae812-156">myVM2(복제) 만들기:</span><span class="sxs-lookup"><span data-stu-id="ae812-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="ae812-157">VM을 만든 후 `publicIpAddress`도 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="ae812-158">연결에 대한 TCP 포트 열기</span><span class="sxs-lookup"><span data-stu-id="ae812-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="ae812-159">다음 단계에서는 Oracle 데이터베이스에 원격으로 액세스할 수 있는 외부 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="ae812-160">외부 끝점을 구성하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="ae812-161">myVM1에 대한 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="ae812-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="ae812-162">결과는 다음 응답과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="ae812-163">myVM2에 대한 포트 열기:</span><span class="sxs-lookup"><span data-stu-id="ae812-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="ae812-164">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="ae812-164">Connect to the virtual machine</span></span>

<span data-ttu-id="ae812-165">다음 명령을 사용하여 가상 컴퓨터와의 SSH 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="ae812-166">해당 IP 주소를 가상 컴퓨터의 `publicIpAddress`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="ae812-167">myVM1(기본)에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="ae812-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="ae812-168">Oracle 소프트웨어는 Marketplace 이미지에 이미 설치되어 있으므로 다음 단계에서 데이터베이스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="ae812-169">'oracle' 슈퍼 사용자로 소프트웨어 실행:</span><span class="sxs-lookup"><span data-stu-id="ae812-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="ae812-170">데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-170">Create the database:</span></span>

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
<span data-ttu-id="ae812-171">출력은 다음 응답과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="ae812-172">ORACLE_SID 및 ORACLE_HOME 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="ae812-173">필요에 따라 .bashrc 파일에 ORACLE_HOME 및 ORACLE_SID를 추가하여 후속 로그인을 위해 이러한 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="ae812-174">Oracle 수신기 시작</span><span class="sxs-lookup"><span data-stu-id="ae812-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="ae812-175">myVM2(복제)에서 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="ae812-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="ae812-176">데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-176">Create the database:</span></span>

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
<span data-ttu-id="ae812-177">ORACLE_SID 및 ORACLE_HOME 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="ae812-178">필요에 따라 .bashrc 파일에 ORACLE_HOME 및 ORACLE_SID를 추가하여 후속 로그인을 위해 이러한 설정을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="ae812-179">Oracle 수신기 시작</span><span class="sxs-lookup"><span data-stu-id="ae812-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="ae812-180">Golden Gate 구성</span><span class="sxs-lookup"><span data-stu-id="ae812-180">Configure Golden Gate</span></span> 
<span data-ttu-id="ae812-181">Golden Gate를 구성하려면 이 섹션의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="ae812-182">myVM1(기본)에서 보관 로그 모드 사용</span><span class="sxs-lookup"><span data-stu-id="ae812-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="ae812-183">강제 로깅을 사용하도록 설정하고 하나 이상의 로그 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="ae812-184">Golden Gate 소프트웨어 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae812-184">Download Golden Gate software</span></span>
<span data-ttu-id="ae812-185">Oracle Golden Gate 소프트웨어를 다운로드 및 준비하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="ae812-186">[Oracle Golden Gate 다운로드 페이지](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html)에서 **fbo_ggs_Linux_x64_shiphome.zip** 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="ae812-187">다운로드 제목 **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64** 아래에 다운로드할 .zip 파일 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="ae812-188">.zip 파일을 클라이언트 컴퓨터로 다운로드한 후 SCP(Secure Copy Protocol)를 사용하여 파일을 VM으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="ae812-189">.zip 파일을 **/opt** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="ae812-190">그다음에 다음과 같이 파일의 소유자를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="ae812-191">파일의 압축을 풉니다. (Linux 압축 풀기 유틸리티가 설치되어 있지 않은 경우 이를 설치합니다.)</span><span class="sxs-lookup"><span data-stu-id="ae812-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="ae812-192">사용 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="ae812-193">x11을 실행하는 클라이언트 및 VM을 준비합니다(Windows 클라이언트에만 해당).</span><span class="sxs-lookup"><span data-stu-id="ae812-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="ae812-194">선택적 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-194">This is an optional step.</span></span> <span data-ttu-id="ae812-195">Linux 클라이언트를 사용하거나 x11을 이미 설치한 경우 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="ae812-196">Windows 컴퓨터에 PuTTY 및 Xming을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * [<span data-ttu-id="ae812-197">PuTTY 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae812-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="ae812-198">Xming 다운로드</span><span class="sxs-lookup"><span data-stu-id="ae812-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="ae812-199">PuTTY를 PuTTY 폴더(예: C:\Program Files\PuTTY)에 설치한 후 puttygen.exe(PuTTY 키 생성기)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="ae812-200">PuTTY 키 생성기에서,</span><span class="sxs-lookup"><span data-stu-id="ae812-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="ae812-201">키를 생성하려면 **생성** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="ae812-202">키의 콘텐츠를 복사합니다(**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="ae812-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="ae812-203">**개인 키 저장** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="ae812-204">표시되는 경고를 무시하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![PuTTY 키 생성기 페이지의 스크린샷](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="ae812-206">VM에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="ae812-207">**authorized_keys**라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="ae812-208">키의 콘텐츠를 이 파일에 붙여넣은 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ae812-209">키에는 문자열 `ssh-rsa`가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="ae812-210">또한 키의 콘텐츠는 한 줄 텍스트여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="ae812-211">PuTTY를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-211">Start PuTTY.</span></span> <span data-ttu-id="ae812-212">**범주** 창에서 **연결** > **SSH** > **인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="ae812-213">**인증에 대한 개인 키 파일** 상자에서 이전에 생성한 키를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![개인 키 설정 페이지의 스크린샷](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="ae812-215">**범주** 창에서 **연결** > **SSH** > **X11**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="ae812-216">그다음에 **X11 전달을 사용하도록 설정** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![X11 사용 페이지의 스크린샷](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="ae812-218">**카테고리** 창에서 **세션**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="ae812-219">호스트 정보를 입력한 다음 **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-219">Enter the host information, and then select **Open**.</span></span>

  ![세션 페이지의 스크린샷](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="ae812-221">Golden Gate 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="ae812-221">Install Golden Gate software</span></span>

<span data-ttu-id="ae812-222">Oracle Golden Gate를 설치하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="ae812-223">oracle로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-223">Sign in as oracle.</span></span> <span data-ttu-id="ae812-224">(로그인할 때 암호 입력 화면이 나타나지 않아야 합니다.) 설치를 시작하기 전에 Xming이 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="ae812-225">'Oracle GoldenGate for Oracle Database 12c'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="ae812-226">그리고 **다음**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-226">Then select **Next** to continue.</span></span>

  ![설치 관리자 설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="ae812-228">소프트웨어 위치를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-228">Change the software location.</span></span> <span data-ttu-id="ae812-229">그다음에 **관리자 시작** 상자를 선택하고 데이터베이스 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="ae812-230">**다음**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-230">Select **Next** to continue.</span></span>

  ![설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="ae812-232">인벤토리 디렉터리를 변경하고 **다음**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="ae812-234">**요약** 화면에서 **설치**를 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![설치 관리자 설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="ae812-236">스크립트를 'root'로 실행할지 묻는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="ae812-237">메시지가 표시되면 별도의 세션, ssh를 VM으로, sudo를 root로 열고 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="ae812-238">**확인**을 선택하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-238">Select **OK** continue.</span></span>

  ![설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="ae812-240">설치가 완료되면 **닫기**를 선택하여 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![설치 선택 페이지의 스크린샷](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="ae812-242">myVM1(기본)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="ae812-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="ae812-243">tnsnames.ora 파일 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-243">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="ae812-244">Golden Gate 소유자 및 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ae812-245">소유자 계정에는 C## 접두사가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="ae812-246">Golden Gate 테스트 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="ae812-247">extract 매개 변수 파일을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="ae812-248">Golden Gate 명령줄 인터페이스(ggsci)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-248">Start the Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="ae812-249">EXTRACT 매개 변수 파일에 다음을 추가합니다(vi 명령 사용).</span><span class="sxs-lookup"><span data-stu-id="ae812-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="ae812-250">Esc 키, ':wq!'를 눌러</span><span class="sxs-lookup"><span data-stu-id="ae812-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="ae812-251">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-251">to save file.</span></span> 

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
6. <span data-ttu-id="ae812-252">extract--integrated extract를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="ae812-253">extract 검사점을 설정하고 실시간 추출을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="ae812-254">이 단계에서는 나중에 다른 섹션에서 사용되는 시작 SCN을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="ae812-255">myVM2(복제)에서 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="ae812-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="ae812-256">tnsnames.ora 파일 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-256">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="ae812-257">복제 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="ae812-258">Golden Gate 테스트 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="ae812-259">변경 내용을 복제하기 위한 REPLICAT 매개 변수 파일:</span><span class="sxs-lookup"><span data-stu-id="ae812-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="ae812-260">REPORA 매개 변수 파일의 콘텐츠:</span><span class="sxs-lookup"><span data-stu-id="ae812-260">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="ae812-261">replicat 검사점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-261">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="ae812-262">복제 설정(myVM1 및 myVM2)</span><span class="sxs-lookup"><span data-stu-id="ae812-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="ae812-263">1. myVM2(복제)에서 복제 설정</span><span class="sxs-lookup"><span data-stu-id="ae812-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="ae812-264">다음을 사용하여 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="ae812-265">관리자 서비스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="ae812-266">2. myVM1(기본)에서 복제 설정</span><span class="sxs-lookup"><span data-stu-id="ae812-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="ae812-267">초기 로드를 시작하고 오류를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="ae812-268">3. myVM2(복제)에서 복제 설정</span><span class="sxs-lookup"><span data-stu-id="ae812-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="ae812-269">이전에 얻은 번호로 SCN 번호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="ae812-270">복제가 시작되면 새 레코드를 TEST 테이블에 삽입하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="ae812-271">작업 상태 보기 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ae812-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="ae812-272">보고서 보기</span><span class="sxs-lookup"><span data-stu-id="ae812-272">View reports</span></span>
<span data-ttu-id="ae812-273">myVM1에서 보고서를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="ae812-274">myVM2에서 보고서를 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="ae812-275">상태 및 기록 보기</span><span class="sxs-lookup"><span data-stu-id="ae812-275">View status and history</span></span>
<span data-ttu-id="ae812-276">myVM1에서 상태 및 기록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="ae812-277">myVM2에서 상태 및 기록을 보려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="ae812-278">이렇게 하면 Oracle linux에서 Golden Gate의 설치 및 구성이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="ae812-279">가상 컴퓨터 삭제</span><span class="sxs-lookup"><span data-stu-id="ae812-279">Delete the virtual machine</span></span>

<span data-ttu-id="ae812-280">더 이상 필요하지 않은 경우 다음 명령을 사용하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae812-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ae812-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ae812-281">Next steps</span></span>

[<span data-ttu-id="ae812-282">고가용성 가상 컴퓨터 만들기 자습서</span><span class="sxs-lookup"><span data-stu-id="ae812-282">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="ae812-283">VM 배포 CLI 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="ae812-283">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
