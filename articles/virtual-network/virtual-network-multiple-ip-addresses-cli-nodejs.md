---
title: "Azure CLI 1.0을 사용하여 여러 IP 주소가 있는 VM | Microsoft Docs"
description: "Azure CLI 1.0 | Resource Manager를 사용하여 가상 컴퓨터에 여러 IP 주소를 할당하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="27596-103">Azure CLI 1.0을 사용하여 가상 컴퓨터에 여러 IP 주소 할당</span><span class="sxs-lookup"><span data-stu-id="27596-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="27596-104">이 문서는 Azure CLI 1.0을 사용하여 Azure Resource Manager 배포 모델을 통해 VM(가상 컴퓨터)을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="27596-105">클래식 배포 모델을 통해 생성된 리소스에 여러 IP 주소를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="27596-106">Azure 배포 모델에 대해 자세히 알아보려면 [배포 모델 이해](../resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27596-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="27596-107"><a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="27596-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="27596-108">Azure CLI 1.0(이 문서) 또는 [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md)을 사용하여 이 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="27596-109">다음 단계는 시나리오에 설명된 대로 여러 IP 주소를 가진 예시 VM을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="27596-110">변수 이름과 IP 주소 유형을 구현에 필요한 대로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="27596-111">[Azure CLI 설치 및 구성](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서에 나오는 단계에 따라 Azure CLI 1.0을 설치 및 구성하고 `azure-login` 명령을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="27596-112">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="27596-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="27596-113">가상 네트워크 만들기:</span><span class="sxs-lookup"><span data-stu-id="27596-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="27596-114">가상 네트워크에 서브넷 만들기:</span><span class="sxs-lookup"><span data-stu-id="27596-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="27596-115">VM에 대한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27596-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="27596-116">다음 명령을 실행하기 전에 *mystorageaccount*를 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="27596-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="27596-117">이 이름은 Azure에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="27596-118">IP 구성, NIC를 만들고 NIC에 IP 구성을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="27596-119">필요에 따라 구성을 추가, 제거 또는 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="27596-120">다음 구성은 시나리오에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="27596-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="27596-121">**IPConfig-1**</span></span>

    <span data-ttu-id="27596-122">다음을 만들기 위해 수행할 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="27596-123">고정 공용 IP 주소가 있는 공용 IP 주소 리소스</span><span class="sxs-lookup"><span data-stu-id="27596-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="27596-124">NIC: 공용 IP 주소와 정적 개인 IP 주소를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="27596-125">*mypublicdns*를 Azure 위치 내에서 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="27596-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="27596-126">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="27596-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="27596-127">IP 주소 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27596-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="27596-128">구독 내에서 사용할 수 있는 공용 IP 주소의 수는 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="27596-129">이러한 한에 대한 자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27596-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="27596-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="27596-130">**IPConfig-2**</span></span>

     <span data-ttu-id="27596-131">고정 공용 IP 주소와 고정 개인 IP 주소가 있는 새 공용 IP 주소 리소스와 새 IP 구성을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="27596-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="27596-132">**IPConfig-3**</span></span>

    <span data-ttu-id="27596-133">고정 개인 IP 주소가 있고 공용 IP 주소가 없는 IP 구성을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="27596-134">이 문서를 통해 모든 IP 구성을 단일 NIC에 할당하면 여러 IP 구성도 VM의 모든 NIC에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="27596-135">여러 NIC로 VM을 만드는 방법에 대해 자세히 알아보려면 여러 NIC를 사용하여 VM 만들기 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27596-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="27596-136">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="27596-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="27596-137">예를 들어 VM 크기를 표준 DS2 v2로 변경하려면 단순히 다음 속성 `--vm-size Standard_DS3_v2`을 6단계에서 `azure vm create` 명령에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="27596-138">NIC와 연결된 IP 구성을 보려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="27596-139">이 문서의 [VM 운영 체제에 IP 주소 추가](#os-config) 섹션에 나오는 사용자 운영 체제별 단계를 완료하여 개인 IP 주소를 VM 운영 체제에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="27596-140"><a name="add"></a>VM에 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="27596-140"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="27596-141">다음 단계를 완료하여 개인 및 공용 IP 주소를 기존 NIC에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="27596-142">예제는 이 문서에서 설명된 [시나리오](#Scenario)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="27596-143">Azure CLI를 열고 단일 CLI 세션 내에서 이 섹션의 나머지 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="27596-144">아직 Azure CLI를 설치 및 구성하지 않은 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서에 나오는 단계를 완료하고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="27596-145">요구 사항에 따라 다음 섹션 중 하나의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="27596-146">**개인 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="27596-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="27596-147">NIC에 개인 IP 주소를 추가하려면 아래 명령을 사용하여 IP 구성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="27596-148">고정 주소는 서브넷에 사용되지 않는 주소여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="27596-149">고유한 구성 이름과 개인 IP 주소를 사용하여 필요한 만큼 구성을 만듭니다(정적 IP 주소를 가진 구성의 경우).</span><span class="sxs-lookup"><span data-stu-id="27596-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="27596-150">**공용 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="27596-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="27596-151">공용 IP 주소는 새 IP 구성 또는 기존 IP 구성에 연결하면 해당 주소가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="27596-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="27596-152">필요에 따라 이후 섹션 중 하나에 나와 있는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="27596-153">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="27596-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="27596-154">IP 주소 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27596-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="27596-155">구독 내에서 사용할 수 있는 공용 IP 주소의 수는 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="27596-156">이러한 한에 대한 자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27596-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="27596-157">**새 IP 구성에 리소스 연결**</span><span class="sxs-lookup"><span data-stu-id="27596-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="27596-158">새 IP 구성의 공용 IP 주소를 추가할 때마다 모든 IP 구성 시 개인 IP 주소가 있어야 하기 때문에 개인 IP 주소도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="27596-159">기존 공용 IP 주소 리소스를 추가하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="27596-160">새 파일을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="27596-161">고정 개인 IP 주소 및 여기에 연결된 *myPublicP3* 공용 IP 주소 리소스가 있는 새 IP 구성을 만들려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="27596-162">**기존 IP 구성에 리소스 연결**</span><span class="sxs-lookup"><span data-stu-id="27596-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="27596-163">공용 IP 주소 리소스는 아직 연결한 리소스가 없는 IP 구성에만 연결될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="27596-164">다음 명령을 입력하면 IP 구성에 연결된 공용 IP 주소가 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="27596-165">반환된 출력에서 IPConfig-3에 대한 것과 유사한 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="27596-166">*IpConfig 3*에 대한 **공용 IP** 열이 비어 있기 때문에 현재 공용 IP 주소 리소스가 여기에 연결되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="27596-167">IpConfig-3에 기존 공용 IP 주소 리소스를 추가하거나 다음 명령을 입력하여 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27596-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="27596-168">*IPConfig 3*이라는 기존 IP 구성에 공용 IP 주소 리소스를 연결하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="27596-169">NIC에 할당된 개인 IP 주소 및 공용 IP 주소 리소스를 보려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="27596-170">반환되는 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="27596-171">이 문서의 [VM 운영 체제에 IP 주소 추가](#os-config) 섹션에 나오는 지침에 따라 NIC에 추가한 개인 IP 주소를 VM 운영 체제에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27596-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="27596-172">운영 체제에 공용 IP 주소를 추가하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="27596-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
