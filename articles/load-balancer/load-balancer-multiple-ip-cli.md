---
title: "Azure CLI를 사용하여 여러 IP 구성의 부하 분산 | Microsoft Docs"
description: "Azure CLI | Resource Manager를 사용하여 가상 컴퓨터에 여러 IP 주소를 할당하는 방법을 알아봅니다."
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
ms.openlocfilehash: bd15713752ea01ad403d8e3dcfed0c9a7adcc7fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="7548d-103">여러 IP 구성의 부하 분산</span><span class="sxs-lookup"><span data-stu-id="7548d-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7548d-104">포털</span><span class="sxs-lookup"><span data-stu-id="7548d-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="7548d-105">CLI</span><span class="sxs-lookup"><span data-stu-id="7548d-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="7548d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7548d-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="7548d-107">이 문서에서는 보조 NIC(네트워크 인터페이스)에 여러 IP 주소가 있는 Azure Load Balancer를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="7548d-108">이 시나리오에는 Windows를 실행하는 VM이 둘 있고 각각 기본 및 보조 NIC가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="7548d-109">보조 NIC에는 각각 두 가지 IP 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="7548d-110">각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="7548d-111">각 웹 사이트는 보조 NIC의 IP 구성 중 하나에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="7548d-112">Azure Load Balancer를 사용하여 웹 사이트의 각 IP 구성에 트래픽을 분산하기 위해 각 웹 사이트에 하나씩 두 개의 프런트 엔드 IP 주소를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="7548d-113">이 시나리오는 양 쪽 프런트 엔드는 물론 양쪽 백 엔드 풀 IP 주소에 동일한 포트 번호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="7548d-115">여러 IP 구성의 부하를 분산하는 단계</span><span class="sxs-lookup"><span data-stu-id="7548d-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="7548d-116">아래 단계에 따라 이 문서에 설명된 시나리오를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="7548d-117">연결된 문서를 참조하여 [Azure CLI를 설치 및 구성](../cli-install-nodejs.md)하고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-117">[Install and Configure the Azure CLI](../cli-install-nodejs.md) the Azure CLI by following the steps in the linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="7548d-118">위의 설명에 따라 *contosofabrikam*이라는 [리소스 그룹을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group).</span><span class="sxs-lookup"><span data-stu-id="7548d-118">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="7548d-119">두 개의 VM에 대한 [가용성 집합을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set).</span><span class="sxs-lookup"><span data-stu-id="7548d-119">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) to for the two VMs.</span></span> <span data-ttu-id="7548d-120">이 시나리오에서는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-120">For this scenario, use the following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="7548d-121">*myVNet*이라는 [가상 네트워크를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-121">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="7548d-122">*mylb*라는 [부하 분산 장치를 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7548d-122">[Create the load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="7548d-123">부하 분산 장치의 프런트 엔드 IP 구성에 대해 두 개의 동적 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-123">Create two dynamic public IP addresses for the frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="7548d-124">각각 *contosofe* 및 *fabrikamfe*라는 두 개의 프런트 엔드 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-124">Create the two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="7548d-125">*contosopool* 및 *fabrikampool*이라는 백 엔드 주소 풀과 [프로브](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*를 만들고, *HTTPc* 및 *HTTPf*라는 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-125">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="7548d-126">아래 명령을 실행한 후 출력을 확인하여 [부하 분산 장치가 제대로 만들어졌는지 확인](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-126">Run the following command below and then check the output to [verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="7548d-127">아래와 같이 VM1이라는 첫 번째 가상 컴퓨터에 대해 *myPublicIp*라는 [공용 IP를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *mystorageaccont1*이라는 [저장소 계정을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7548d-127">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="7548d-128">아래와 같이 VM1에 대해 [네트워크 인터페이스를 만들고](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) *VM1-ipconfig2*라는 두 번째 IP 구성을 추가하고 [VM을 만듭니다](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="7548d-128">[Create the network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create the VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="7548d-129">두 번째 VM에 대해 10 ~ 11단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-129">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="7548d-130">마지막으로 DNS 리소스 레코드가 부하 분산 장치의 각 프런트 엔드 IP 주소를 가리키도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-130">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="7548d-131">도메인을 Azure DNS에 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7548d-131">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="7548d-132">Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7548d-132">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7548d-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7548d-133">Next steps</span></span>
- <span data-ttu-id="7548d-134">Azure에서 부하 분산 서비스를 결합하는 방법에 대한 자세한 내용은 [Azure에서 부하 분산 서비스 사용](../traffic-manager/traffic-manager-load-balancing-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7548d-134">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="7548d-135">[Azure Load Balancer에 대한 로그 분석](../load-balancer/load-balancer-monitor-log.md)을 통해 Azure에서 부하 분산 장치를 관리하고 문제를 해결하는 데 다양한 유형의 로그를 사용하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7548d-135">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
