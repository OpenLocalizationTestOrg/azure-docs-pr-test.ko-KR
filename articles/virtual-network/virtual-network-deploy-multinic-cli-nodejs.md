---
title: "다중 NIC가 있는 VM 만들기 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 다중 NIC가 있는 VM을 만드는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b95bcb38664718bf25ec6981c803415790c6da3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="7365d-103">Azure CLI 1.0을 사용하여 다중 NIC가 있는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="7365d-103">Create a VM with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7365d-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7365d-105">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 [클래식 배포 모델](virtual-network-deploy-multinic-classic-cli.md) 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="7365d-106">다음 단계에서는 WEB 서버에 *IaaSStory*라는 리소스 그룹을, DB 서버에 *IaaSStory-BackEnd*라는 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-106">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span> <span data-ttu-id="7365d-107">Azure CLI 1.0(이 문서) 또는 [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)을 사용하여 이 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-107">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="7365d-108">다음 단계에서 변수에 대한 ""의 값은 시나리오의 설정을 사용하여 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-108">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="7365d-109">사용자 환경에 적절한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-109">Change the values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7365d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7365d-110">Prerequisites</span></span>
<span data-ttu-id="7365d-111">DB 서버를 만들려면 먼저 이 시나리오에 필요한 모든 리소스로 *IaaSStory* 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-111">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="7365d-112">이러한 리소스를 만들려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-112">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="7365d-113">[템플릿 페이지](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-113">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="7365d-114">템플릿 페이지에서 **Parent resource group(부모 리소스 그룹)** 오른쪽에 있는 **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-114">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="7365d-115">필요한 경우 매개 변수 값을 변경한 다음 Azure Preview 포털의 단계에 따라 리소스 그룹을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-115">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7365d-116">저장소 계정 이름이 고유한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="7365d-117">Azure에서 중복된 저장소 계정 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="7365d-118">백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="7365d-118">Create the back-end VMs</span></span>
<span data-ttu-id="7365d-119">백 엔드 VM은 만드는 리소스에 따라 다음과 같이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-119">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="7365d-120">**데이터 디스크용 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="7365d-120">**Storage account for data disks**.</span></span> <span data-ttu-id="7365d-121">성능 향상을 위해 데이터베이스 서버의 데이터 디스크는 SSD(반도체 드라이브) 기술을 사용하며, 이 기술에는 프리미엄 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-121">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="7365d-122">배포할 Azure 위치에서 프리미엄 저장소가 지원되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7365d-122">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="7365d-123">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="7365d-123">**NICs**.</span></span> <span data-ttu-id="7365d-124">각 VM에 데이터베이스 액세스용으로 하나, 그리고 관리용으로 하나씩, 두 개의 NIC가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="7365d-125">**가용성 집합**.</span><span class="sxs-lookup"><span data-stu-id="7365d-125">**Availability set**.</span></span> <span data-ttu-id="7365d-126">모든 데이터베이스 서버가 단일 가용성 집합에 추가되어, 유지 관리 도중에 하나 이상의 VM이 실행 중이도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="7365d-127">1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="7365d-127">Step 1 - Start your script</span></span>
<span data-ttu-id="7365d-128">사용되는 전체 bash 스크립트를 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-128">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="7365d-129">다음 단계에 따라 스크립트를 사용자 환경에서 작동하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="7365d-130">위의 [필수 조건](#Prerequisites)에서 배포한 기존 리소스 그룹을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="7365d-131">백 엔드 배포에 사용하려는 값을 기반으로 다음 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="7365d-132">VM을 만들 `BackEnd` 서브넷의 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-132">Retrieve the ID for the `BackEnd` subnet where the VMs will be created.</span></span> <span data-ttu-id="7365d-133">이 단계를 수행해야 하는 이유는 이 서브넷에 연결할 NIC이 다른 리소스 그룹에 속해 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-133">You need to do this since the NICs to be associated to this subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="7365d-134">위의 첫 번째 명령은 [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) 및 [문자열 조작](http://tldp.org/LDP/abs/html/string-manipulation.html)(구체적으로 말하면, 하위 문자열 제거)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-134">The first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="7365d-135">`NSG-RemoteAccess` NSG의 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-135">Retrieve the ID for the `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="7365d-136">이 단계를 수행해야 하는 이유는 이 NSG에 연결할 NIC이 다른 리소스 그룹에 속해 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-136">You need to do this since the NICs to be associated to this NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="7365d-137">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="7365d-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="7365d-138">모든 백 엔드 리소스를 위한 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="7365d-139">리소스 그룹 이름에 `$backendRGName` 변수가, Azure 지역에 대해서는 `$location`이 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-139">Notice the use of the `$backendRGName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="7365d-140">VM에서 사용할 OS 및 데이터 디스크에 대해 프리미엄 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-140">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="7365d-141">VM의 가용성 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-141">Create an availability set for the VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="7365d-142">3단계 - NIC 및 백 엔드 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="7365d-142">Step 3 - Create the NICs and back-end VMs</span></span>

1. <span data-ttu-id="7365d-143">`numberOfVMs` 변수를 기반으로 하여 여러 VM을 만드는 루프를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-143">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="7365d-144">각 VM에 대해 데이터베이스 액세스를 위한 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="7365d-145">각 VM에 대해 원격 액세스를 위한 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="7365d-146">NIC를 NSG에 연결하는 데 `--network-security-group` 매개 변수가 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-146">Notice the `--network-security-group` parameter, used to associate the NIC to an NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="7365d-147">VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-147">Create the VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="7365d-148">각 VM에 대해 두 개의 데이터 디스크를 만들고 `done` 명령을 사용하여 루프를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-148">For each VM, create two data disks, and end the loop with the `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="7365d-149">4단계 - 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="7365d-149">Step 4 - Run the script</span></span>
<span data-ttu-id="7365d-150">스크립트를 다운로드하여 요구에 맞게 변경했으므로, 이제 이 스크립트를 실행하여 여러 NIC를 사용하여 백 엔드 데이터베이스 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-150">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="7365d-151">스크립트를 저장하고 **Bash** 터미널에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="7365d-152">아래와 같이 초기 출력에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-152">You will see the initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up the availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up the network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up the network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB1"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB1-DA"
        info:    Looking up the NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="7365d-153">몇 분 후에 실행이 종료되고 아래와 같이 출력의 나머지 부분이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7365d-153">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB1"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up the network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up the network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up the VM "DB2"
        info:    Using the VM Size "Standard_DS3"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account wtestvnetstorageprm
        info:    Looking up the availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up the NIC "NICDB2-DA"
        info:    Looking up the NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up the VM "DB2"
        info:    Looking up the storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

