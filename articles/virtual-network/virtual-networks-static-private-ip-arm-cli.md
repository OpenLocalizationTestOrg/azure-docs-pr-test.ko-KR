---
title: "VM에 대한 개인 IP 주소 구성 - Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI(명령줄 인터페이스) 2.0을 사용하여 가상 컴퓨터에 대한 개인 IP 주소를 구성하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="8adf2-103">Azure CLI 2.0을 사용하여 가상 컴퓨터에 대한 개인 IP 주소 구성</span><span class="sxs-lookup"><span data-stu-id="8adf2-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8adf2-104">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="8adf2-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="8adf2-105">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="8adf2-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI</span><span class="sxs-lookup"><span data-stu-id="8adf2-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="8adf2-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - 리소스 관리 배포 모델용 차세대 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="8adf2-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8adf2-108">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="8adf2-109">[클래식 배포 모델에서 정적 개인 IP 주소를 관리](virtual-networks-static-private-ip-classic-cli.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="8adf2-110">아래 샘플 Azure CLI 2.0 명령에는 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="8adf2-111">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [vnet 만들기](virtual-networks-create-vnet-arm-cli.md)에 설명된 테스트 환경을 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="8adf2-112">VM을 만들 때 정적 개인 IP 주소 지정</span><span class="sxs-lookup"><span data-stu-id="8adf2-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="8adf2-113">*192.168.1.101*의 정적 개인 IP 주소를 사용하여 *TestVNet*이라는 VNet의 *FrontEnd* 서브넷에 *DNS01*이라는 VM을 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8adf2-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="8adf2-114">아직 설치하지 않은 경우 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치 및 구성하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="8adf2-115">[az network public-ip create](/cli/azure/network/public-ip#create) 명령을 사용하여 VM의 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="8adf2-116">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8adf2-117">사용자 환경에 따라 이 단계 및 이후 단계에 다른 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="8adf2-118">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8adf2-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="8adf2-119">`--resource-group`: 공용 IP를 만들 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="8adf2-120">`--name`: 공용 IP의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="8adf2-121">`--location`: 공용 IP를 만들 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="8adf2-122">[az network nic create](/cli/azure/network/nic#create) 명령을 실행하여 고정 개인 IP를 가진 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="8adf2-123">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="8adf2-124">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8adf2-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="8adf2-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8adf2-125">Parameters:</span></span>

    * <span data-ttu-id="8adf2-126">`--private-ip-address`: NIC에 대한 고정 개인 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="8adf2-127">`--vnet-name`: NIC가 만들어질 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="8adf2-128">`--subnet`: NIC가 만들어질 서브넷의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="8adf2-129">[azure vm create](/cli/azure/vm/nic#create) 명령을 실행하여 위에서 만든 공용 IP 및 NIC를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="8adf2-130">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-130">The list shown after the output explains the parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="8adf2-131">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8adf2-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="8adf2-132">기본 [az vm create](/cli/azure/vm#create) 매개 변수가 아닌 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="8adf2-133">`--nics`: VM이 연결된 NIC의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="8adf2-134">VM의 정적 개인 IP 주소 정보 검색</span><span class="sxs-lookup"><span data-stu-id="8adf2-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="8adf2-135">만든 고정 개인 IP 주소 정보를 보려면 다음 Azure CLI 명령을 실행하고 *개인 IP alloc-method* 및 *개인 IP 주소*에 대한 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="8adf2-136">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8adf2-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="8adf2-137">해당 VM에 대한 NIC의 특정 IP 정보를 표시하려면 NIC를 구체적으로 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="8adf2-138">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="8adf2-139">VM에서 정적 개인 IP 주소 제거</span><span class="sxs-lookup"><span data-stu-id="8adf2-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="8adf2-140">Resource Manager 배포를 위해 Azure CLI의 NIC에서 고정 개인 IP 주소를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="8adf2-141">다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-141">You must:</span></span>
- <span data-ttu-id="8adf2-142">동적 IP를 사용하는 새 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="8adf2-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="8adf2-143">VM의 NIC가 새로 만든 NIC를 수행하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="8adf2-144">위의 명령에 사용된 VM에 대한 NIC를 변경하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8adf2-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="8adf2-145">새 IP 주소를 가진 동적 IP 할당을 사용하여 새 NIC를 만들기 위해 **azure network nic create** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="8adf2-146">IP 주소가 지정되어 있지 않으므로 할당 메서드는 **동적**입니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="8adf2-147">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8adf2-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="8adf2-148">**azure vm set** 명령을 실행하여 VM에 사용된 NIC를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="8adf2-149">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="8adf2-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="8adf2-150">VM에 하나 이상의 NIC가 있을 정도로 충분히 큰 경우 **azure network nic delete** 명령을 실행하여 이전 NIC를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8adf2-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8adf2-151">Next steps</span></span>
* <span data-ttu-id="8adf2-152">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8adf2-153">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8adf2-154">[예약된 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="8adf2-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

