---
title: "Azure CLI를 사용 하 여 여러 IP 구성에서 분산 aaaLoad | Microsoft Docs"
description: "여러 IP 해결 하는 tooassign 방법을 알아보려면 Azure CLI를 사용 하 여 tooa 가상 컴퓨터 | 리소스 관리자입니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="da895-103">여러 IP 구성의 부하 분산</span><span class="sxs-lookup"><span data-stu-id="da895-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="da895-104">포털</span><span class="sxs-lookup"><span data-stu-id="da895-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="da895-105">CLI</span><span class="sxs-lookup"><span data-stu-id="da895-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="da895-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da895-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="da895-107">이 문서에서는 Azure 부하 분산 장치에서 여러 ip toouse 보조 네트워크 인터페이스 (NIC)에서 해결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="da895-108">이 시나리오에는 Windows를 실행하는 VM이 둘 있고 각각 기본 및 보조 NIC가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da895-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="da895-109">각 보조 hello Nic가 두 개의 IP 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="da895-110">각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다. 각 웹 사이트는 hello 보조 NIC에서 hello IP 구성의 바인딩된 tooone</span><span class="sxs-lookup"><span data-stu-id="da895-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="da895-111">Azure 부하 분산 장치 tooexpose 두 개의 프런트 엔드 IP 주소를 각 웹 사이트에 hello 웹 사이트에 대 한 toodistribute 트래픽 toohello 각 IP 구성에 대 한 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="da895-112">이 시나리오에서는으로 백 엔드 풀 IP 주소 모두 같은 포트 번호 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="da895-114">여러 IP 구성에 대 한 단계 tooload 잔액</span><span class="sxs-lookup"><span data-stu-id="da895-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="da895-115">이 문서에 설명 된 tooachieve hello 시나리오 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="da895-116">[설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) Azure 계정에 연결 된 문서 hello와 로그에 hello 단계에 따라 Azure CLI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="da895-117">위의 설명에 따라 *contosofabrikam*이라는 [리소스 그룹을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group).</span><span class="sxs-lookup"><span data-stu-id="da895-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="da895-118">[가용성 집합 만들기](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello 두 개의 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="da895-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="da895-119">이 시나리오에 대 한 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="da895-120">*myVNet*이라는 [가상 네트워크를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da895-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="da895-121">[Hello 부하 분산 장치 만들기](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 호출 *mylb*:</span><span class="sxs-lookup"><span data-stu-id="da895-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="da895-122">동적 부하 분산 장치의 프런트 엔드 IP 구성 hello에 대 한 공용 두 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da895-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="da895-123">Hello 두 프런트 엔드 IP 구성을 만들 *contosofe* 및 *fabrikamfe* 각각:</span><span class="sxs-lookup"><span data-stu-id="da895-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="da895-124">*contosopool* 및 *fabrikampool*이라는 백 엔드 주소 풀과 [프로브](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*를 만들고, *HTTPc* 및 *HTTPf*라는 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="da895-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="da895-125">실행된 hello 다음 아래 명령을 클릭 한 다음 hello 출력을 너무 확인[부하 분산 장치 확인](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 올바로 생성 되었는지:</span><span class="sxs-lookup"><span data-stu-id="da895-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="da895-126">아래와 같이 VM1이라는 첫 번째 가상 컴퓨터에 대해 *myPublicIp*라는 [공용 IP를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *mystorageaccont1*이라는 [저장소 계정을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da895-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="da895-127">[Hello 네트워크 인터페이스를 만들](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) v m 1에 대 한 두 번째 IP 구성을 추가 하 고 *VM1 ipconfig2*, 및 [hello VM을 만들](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="da895-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="da895-128">두 번째 VM에 대해 10 ~ 11단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="da895-129">마지막으로 DNS 리소스 레코드 toopoint toohello 각 프런트 엔드 IP 주소를 hello 부하 분산 장치를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="da895-130">도메인을 Azure DNS에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da895-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="da895-131">Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="da895-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da895-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da895-132">Next steps</span></span>
- <span data-ttu-id="da895-133">에 Azure에서 서비스 toocombine 부하 분산 방법에 대 한 자세한 [부하 분산 서비스를 사용 하 여 Azure에서](../traffic-manager/traffic-manager-load-balancing-azure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="da895-134">다른 유형의 로그를 사용 하 여 Azure toomanage에 부하 분산 장치에 문제를 해결 하는 방법에 대해 알아봅니다 [Azure 부하 분산 장치에 대 한 로그 분석](../load-balancer/load-balancer-monitor-log.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da895-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
