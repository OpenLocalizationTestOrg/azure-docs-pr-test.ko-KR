---
title: "Vm-Azure CLI 2.0에 대 한 aaaConfigure 개인 IP 주소 | Microsoft Docs"
description: "Tooconfigure 개인 IP 주소를 사용 하 여 가상 컴퓨터에 대 한 Azure CLI (명령줄 인터페이스) 2.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="2542d-103">Hello Azure CLI 2.0을 사용 하 여 가상 컴퓨터에 대 한 개인 IP 주소를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2542d-104">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="2542d-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="2542d-105">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="2542d-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI</span><span class="sxs-lookup"><span data-stu-id="2542d-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="2542d-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -우리의 차세대 CLI hello 리소스 관리 배포 모델 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="2542d-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="2542d-108">이 문서에서는 hello 리소스 관리자 배포 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="2542d-109">수도 있습니다 [hello 클래식 배포 모델에 개인 고정 IP 주소 관리](virtual-networks-static-private-ip-classic-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="2542d-110">hello 샘플 Azure CLI 2.0 명령 아래에 이미 만든 단순한 환경이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="2542d-111">이 문서에 표시 된 대로 toorun hello 명령을 원하는 경우 먼저 hello 테스트 환경을 구축에 설명 된 [vnet을 만든](virtual-networks-create-vnet-arm-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="2542d-112">VM을 만들 때 정적 개인 IP 주소 지정</span><span class="sxs-lookup"><span data-stu-id="2542d-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="2542d-113">toocreate 라는 VM *DNS01* hello에 *프런트 엔드* 라는 VNet의 서브넷 *TestVNet* 의 정적 개인 ip *192.168.1.101*, 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="2542d-114">하지 않은 아직 설치 하 고 최신 hello 구성 [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="2542d-115">Hello로 hello VM에 대 한 공용 IP 만들기 [az 네트워크 공용 ip 만들기](/cli/azure/network/public-ip#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="2542d-116">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2542d-117">원하는 또는 사용자 환경에 따라이 인수에 대 한 toouse 다양 한 값과 이후 단계에서는 필요한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="2542d-118">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2542d-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="2542d-119">`--resource-group`: Toocreate hello 공용 ip에서 hello 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="2542d-120">`--name`: Hello 공용 IP의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="2542d-121">`--location`: Toocreate hello 공용 ip에서 azure 지역.</span><span class="sxs-lookup"><span data-stu-id="2542d-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="2542d-122">Hello 실행 [az 네트워크 nic 만들기](/cli/azure/network/nic#create) 명령 toocreate 정적 개인 IP와 NIC 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="2542d-123">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="2542d-124">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2542d-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="2542d-125">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2542d-125">Parameters:</span></span>

    * <span data-ttu-id="2542d-126">`--private-ip-address`: NIC. hello에 대 한 개인 IP 주소 고정</span><span class="sxs-lookup"><span data-stu-id="2542d-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="2542d-127">`--vnet-name`: 어떤 toocreate에 NIC. hello hello VNet의 이름</span><span class="sxs-lookup"><span data-stu-id="2542d-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="2542d-128">`--subnet`: 어떤 toocreate hello NIC.에에서 hello 서브넷의 이름</span><span class="sxs-lookup"><span data-stu-id="2542d-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="2542d-129">Hello 실행 [azure vm 만들기](/cli/azure/vm/nic#create) hello 공용 IP와 NIC를 사용 하 여 VM 위에서 만든 명령 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="2542d-130">hello 출력 뒤에 표시 된 hello 목록 사용 되는 hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="2542d-131">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2542d-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="2542d-132">기본 hello 이외의 매개 변수 [az vm 만들기](/cli/azure/vm#create) 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="2542d-133">`--nics`: Hello NIC toowhich hello VM 이름 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="2542d-134">VM의 정적 개인 IP 주소 정보 검색</span><span class="sxs-lookup"><span data-stu-id="2542d-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="2542d-135">tooview hello 정적 개인 IP 주소를 만든 다음 Azure CLI 명령을 hello를 실행 하 고 hello에 대 한 값이 확인 *개인 IP 할당 메서드* 및 *개인 IP 주소가*:</span><span class="sxs-lookup"><span data-stu-id="2542d-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="2542d-136">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2542d-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="2542d-137">toodisplay 쿼리 hello NIC 해당 VM에 대 한 hello NIC의 특정 IP 정보를 특히 hello:</span><span class="sxs-lookup"><span data-stu-id="2542d-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="2542d-138">hello 출력은 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="2542d-139">VM에서 정적 개인 IP 주소 제거</span><span class="sxs-lookup"><span data-stu-id="2542d-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="2542d-140">Resource Manager 배포를 위해 Azure CLI의 NIC에서 고정 개인 IP 주소를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="2542d-141">다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-141">You must:</span></span>
- <span data-ttu-id="2542d-142">동적 IP를 사용하는 새 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="2542d-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="2542d-143">NIC. 새로 만든 VM hello 수행 하는 hello에 NIC hello 설정</span><span class="sxs-lookup"><span data-stu-id="2542d-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="2542d-144">위의 hello 명령에 사용 된 VM hello에 대 한 toochange hello NIC는 아래의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="2542d-145">Hello 실행 **azure 네트워크 nic 만들** toocreate 동적 IP 할당을 사용 하 여 새 IP 주소를 가진 새 NIC 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="2542d-146">때문에 IP 주소를 지정 hello 할당 방법을 **동적**합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="2542d-147">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2542d-147">Expected output:</span></span>

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

2. <span data-ttu-id="2542d-148">Hello 실행 **azure vm 집합** 명령 toochange hello NIC hello VM에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="2542d-149">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="2542d-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="2542d-150">Hello VM이 충분히 큰 toohave hello를 실행 하는 둘 이상의 NIC **azure 네트워크 nic 삭제** toodelete hello 이전 NIC. 명령</span><span class="sxs-lookup"><span data-stu-id="2542d-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="2542d-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2542d-151">Next steps</span></span>
* <span data-ttu-id="2542d-152">[예약된 공용 IP](virtual-networks-reserved-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="2542d-153">[ILPIP(인스턴스 수준 공용 IP)](virtual-networks-instance-level-public-ip.md) 주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="2542d-154">Hello 참조 [예약 된 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2542d-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

