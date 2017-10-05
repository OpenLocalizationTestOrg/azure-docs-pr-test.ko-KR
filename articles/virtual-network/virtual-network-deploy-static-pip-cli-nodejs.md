---
title: "고정 공용 IP가 있는 VM 만들기 - Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 1.0을 사용하여 고정 공용 IP 주소가 있는 VM을 만드는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a373c32271096308678fe3402e8420cc14fe5935
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-cli-10"></a><span data-ttu-id="6f7b4-103">Azure CLI 1.0을 사용하여 고정 공용 IP 주소가 있는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="6f7b4-103">Create a VM with a static public IP address using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f7b4-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="6f7b4-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="6f7b4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f7b4-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="6f7b4-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6f7b4-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="6f7b4-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6f7b4-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="6f7b4-108">템플릿</span><span class="sxs-lookup"><span data-stu-id="6f7b4-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="6f7b4-109">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="6f7b4-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="6f7b4-110">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6f7b4-111">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-111">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

<span data-ttu-id="6f7b4-112">Azure CLI 1.0(이 문서) 또는 [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md)을 사용하여 이 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-112">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> 

## <span data-ttu-id="6f7b4-113"><a name = "create"></a>1단계 - 스크립트 시작</span><span class="sxs-lookup"><span data-stu-id="6f7b4-113"><a name = "create"></a>Step 1 - Start your script</span></span>
<span data-ttu-id="6f7b4-114">사용되는 전체 bash 스크립트를 [여기](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-cli.sh)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-114">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-cli.sh).</span></span> <span data-ttu-id="6f7b4-115">다음 단계에 완료하여 스크립트가 사용자 환경에서 작동하도록 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-115">Complete the following steps to change the script to work in your environment:</span></span>

<span data-ttu-id="6f7b4-116">배포에 사용하려는 값을 기반으로 아래 변수 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-116">Change the values of the variables below based on the values you want to use for your deployment.</span></span> <span data-ttu-id="6f7b4-117">다음 값은 이 문서에 사용되는 시나리오에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-117">The following values map to the scenario used in this article:</span></span>

```azurecli
# Set variables for the new resource group
rgName="IaaSStory"
location="westus"

# Set variables for VNet
vnetName="TestVNet"
vnetPrefix="192.168.0.0/16"
subnetName="FrontEnd"
subnetPrefix="192.168.1.0/24"

# Set variables for storage
stdStorageAccountName="iaasstorystorage"

# Set variables for VM
vmSize="Standard_A1"
diskSize=127
publisher="Canonical"
offer="UbuntuServer"
sku="14.04.2-LTS"
version="latest"
vmName="WEB1"
osDiskName="osdisk"
nicName="NICWEB1"
privateIPAddress="192.168.1.101"
username='adminuser'
password='adminP@ssw0rd'
pipName="PIPWEB1"
dnsName="iaasstoryws1"
```

## <a name="step-2---create-the-necessary-resources-for-your-vm"></a><span data-ttu-id="6f7b4-118">2단계 - VM에 필요한 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="6f7b4-118">Step 2 - Create the necessary resources for your VM</span></span>
<span data-ttu-id="6f7b4-119">VM을 만들기 전에 VM에서 사용할 리소스 그룹, VNet, 공용 IP 및 NIC가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-119">Before creating a VM, you need a resource group, VNet, public IP, and NIC to be used by the VM.</span></span>

1. <span data-ttu-id="6f7b4-120">새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-120">Create a new resource group.</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="6f7b4-121">VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-121">Create the VNet and subnet.</span></span>

    ```azurecli
    azure network vnet create --resource-group $rgName \
        --name $vnetName \
        --address-prefixes $vnetPrefix \
        --location $location
    azure network vnet subnet create --resource-group $rgName \
        --vnet-name $vnetName \
        --name $subnetName \
        --address-prefix $subnetPrefix
    ```

3. <span data-ttu-id="6f7b4-122">공용 IP 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-122">Create the public IP resource.</span></span>

    ```azurecli
    azure network public-ip create --resource-group $rgName \
        --name $pipName \
        --location $location \
        --allocation-method Static \
        --domain-name-label $dnsName
    ```

4. <span data-ttu-id="6f7b4-123">공용 IP를 사용하여 위에서 만든 서브넷의 VM에 대한 NIC(네트워크 인터페이스)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-123">Create the network interface (NIC) for the VM in the subnet created above, with the public IP.</span></span> <span data-ttu-id="6f7b4-124">명령의 첫 번째 집합을 사용하여 위에서 만든 서브넷의 **ID** 를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-124">Notice the first set of commands are used to retrieve the **Id** of the subnet created above.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $rgName \
        --vnet-name $vnetName \
        --name $subnetName|grep Id)"

    subnetId=${subnetId#*/}

    azure network nic create --name $nicName \
        --resource-group $rgName \
        --location $location \
        --private-ip-address $privateIPAddress \
        --subnet-id $subnetId \
        --public-ip-name $pipName
    ```

   > [!TIP]
   > <span data-ttu-id="6f7b4-125">위의 첫 번째 명령은 [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) 및 [문자열 조작](http://tldp.org/LDP/abs/html/string-manipulation.html)(구체적으로 말하면, 하위 문자열 제거)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-125">The first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

5. <span data-ttu-id="6f7b4-126">VM OS 드라이브를 호스트하는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-126">Create a storage account to host the VM OS drive.</span></span>

    ```azurecli
    azure storage account create $stdStorageAccountName \
        --resource-group $rgName \
        --location $location --type LRS
    ```

## <a name="step-3---create-the-vm"></a><span data-ttu-id="6f7b4-127">3단계 - VM 만들기</span><span class="sxs-lookup"><span data-stu-id="6f7b4-127">Step 3 - Create the VM</span></span>
<span data-ttu-id="6f7b4-128">이제 필요한 모든 리소스를 배치했으므로 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-128">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="6f7b4-129">VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-129">Create the VM.</span></span>

    ```azurecli
    azure vm create --resource-group $rgName \
        --name $vmName \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --nic-names $nicName \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $stdStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName.vhd \
        --admin-username $username \
        --admin-password $password
    ```
2. <span data-ttu-id="6f7b4-130">스크립트 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-130">Save the script file.</span></span>

## <a name="step-4---run-the-script"></a><span data-ttu-id="6f7b4-131">4단계 - 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="6f7b4-131">Step 4 - Run the script</span></span>
<span data-ttu-id="6f7b4-132">필요한 내용을 변경하고 위에 표시된 스크립트를 파악한 후 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-132">After making any necessary changes, and understanding the script show above, run the script.</span></span>

1. <span data-ttu-id="6f7b4-133">Bash 콘솔에서 위의 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-133">From a bash console, run the script above.</span></span>

    ```azurecli
    sh myscript.sh
    ```

2. <span data-ttu-id="6f7b4-134">몇 분 후에 아래 출력이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f7b4-134">The output below should be displayed after a few minutes.</span></span>

        info:    Executing command group create
        info:    Getting resource group IaaSStory
        info:    Creating resource group IaaSStory
        info:    Created resource group IaaSStory
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
        data:    Name:                IaaSStory
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command network vnet create
        info:    Looking up virtual network "TestVNet"
        info:    Creating virtual network "TestVNet"
        info:    Loading virtual network state
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/TestVNet
        data:    Name                            : TestVNet
        data:    Type                            : Microsoft.Network/virtualNetworks
        data:    Location                        : westus
        data:    ProvisioningState               : Succeeded
        data:    Address prefixes:
        data:      192.168.0.0/16
        info:    network vnet create command OK
        info:    Executing command network vnet subnet create
        info:    Looking up the subnet "FrontEnd"
        info:    Creating subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:
        info:    network vnet subnet create command OK
        info:    Executing command network public-ip create
        info:    Looking up the public ip "PIPWEB1"
        info:    Creating public ip address "PIPWEB1"
        info:    Looking up the public ip "PIPWEB1"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
        data:    Name                            : PIPWEB1
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Static
        data:    Idle timeout                    : 4
        data:    IP Address                      : 40.78.63.253
        data:    Domain name label               : iaasstoryws1
        data:    FQDN                            : iaasstoryws1.westus.cloudapp.azure.com
        info:    network public-ip create command OK
        info:    Executing command network nic create
        info:    Looking up the network interface "NICWEB1"
        info:    Looking up the public ip "PIPWEB1"
        info:    Creating network interface "NICWEB1"
        info:    Looking up the network interface "NICWEB1"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkInterfaces/NICWEB1
        data:    Name                            : NICWEB1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory2/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up the VM "WEB1"
        info:    Using the VM Size "Standard_A1"
        info:    The [OS, Data] Disk or image configuration requires storage account
        info:    Looking up the storage account iaasstorystorage
        info:    Looking up the NIC "NICWEB1"
        info:    Creating VM "WEB1"
        info:    vm create command OK
