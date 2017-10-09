---
title: "hello Azure CLI 1.0을 사용 하 여 여러 IP 주소와 aaaVM | Microsoft Docs"
description: "여러 IP 해결 하는 tooassign 방법을 알아보려면 Azure CLI 1.0 hello tooa 가상 컴퓨터를 사용 하 여 | 리소스 관리자입니다."
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="a396a-103">Toovirtual 컴퓨터 Azure CLI 1.0을 사용 하 여 여러 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="a396a-104">이 문서에서는 toocreate hello Azure 리소스 관리자 배포 모델을 사용 하 여 가상 컴퓨터 (VM) Azure CLI 1.0 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="a396a-105">Hello 클래식 배포 모델을 통해 만든 tooresources 여러 IP 주소를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="a396a-106">Azure 배포 모델을 읽을 hello에 대 한 자세한 toolearn [배포 모델을 이해](../resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a396a-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="a396a-107"><a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a396a-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="a396a-108">Hello Azure CLI 1.0 (이 문서) 또는 hello를 사용 하 여이 작업을 완료할 수 있습니다 [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="a396a-109">수행 하는 hello 단계 hello 시나리오에 설명 된 대로 toocreate 예로 여러 IP 사용 하 여 VM 해결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="a396a-110">변수 이름과 IP 주소 유형을 구현에 필요한 대로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="a396a-111">에서 설치 및 구성 단계를 다음 hello 하 여 Azure CLI 1.0 hello hello [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서 hello 사용 하 여 Azure 계정에 로그인 합니다 `azure-login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="a396a-112">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="a396a-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="a396a-113">가상 네트워크 만들기:</span><span class="sxs-lookup"><span data-stu-id="a396a-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="a396a-114">Hello 가상 네트워크에 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="a396a-115">Hello VM에 대 한 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="a396a-116">Hello를 실행 하기 전에 다음 명령을, 대체 *mystorageaccount* 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="a396a-117">hello 이름은 Azure 전체에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="a396a-118">Hello IP 구성, NIC를 만들고 hello IP 구성을 toohello NIC. 할당</span><span class="sxs-lookup"><span data-stu-id="a396a-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="a396a-119">추가, 제거 또는 필요에 따라 hello 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="a396a-120">구성을 따르고 hello hello 시나리오에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="a396a-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="a396a-121">**IPConfig-1**</span></span>

    <span data-ttu-id="a396a-122">Toocreate 다음에 나오는 hello 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="a396a-123">고정 공용 IP 주소가 있는 공용 IP 주소 리소스</span><span class="sxs-lookup"><span data-stu-id="a396a-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="a396a-124">NIC를 hello 공용 IP 주소 및 정적 개인 IP 주소 tooit 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="a396a-125">대체 *mypublicdns* hello Azure 위치 내에서 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="a396a-126">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="a396a-127">가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지.</span><span class="sxs-lookup"><span data-stu-id="a396a-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="a396a-128">구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="a396a-129">hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.</span><span class="sxs-lookup"><span data-stu-id="a396a-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="a396a-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="a396a-130">**IPConfig-2**</span></span>

     <span data-ttu-id="a396a-131">새 공용 IP 주소 리소스와 고정 공용 IP 주소 및 정적 개인 IP 주소를 사용 하 여 새 IP 구성이 hello 명령을 toocreate 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="a396a-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="a396a-132">**IPConfig-3**</span></span>

    <span data-ttu-id="a396a-133">Hello 명령을 toocreate IP 구성을 정적 개인 IP 주소와 공용 IP 주소가 없습니다. 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="a396a-134">이 문서에는 모든 IP 구성을 tooa 할당 있지만 단일 NIC를 지정할 수 있습니다 여러 IP 구성은 VM에서 NIC tooany 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="a396a-135">여러 Nic 사용 하 여 VM 읽기 toocreate 방법 toolearn hello 여러 Nic 문서를 사용 하 여 VM 만들기.</span><span class="sxs-lookup"><span data-stu-id="a396a-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="a396a-136">Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="a396a-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="a396a-137">toochange hello VM 크기 tooStandard DS2 v2, 예를 들어 hello 다음 속성을 추가 하기만 하면 `--vm-size Standard_DS3_v2` toohello `azure vm create` 6 단계에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="a396a-138">Hello 명령 tooview hello NIC를 다음을 입력 하 고 hello IP 구성 관련 된 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="a396a-139">추가 hello 개인 IP 주소 수 toohello VM 운영 체제 hello에 운영 체제에 대 한 hello 단계를 완료 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="a396a-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="a396a-140"><a name="add"></a>IP 주소 tooa VM 추가</span><span class="sxs-lookup"><span data-stu-id="a396a-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="a396a-141">추가 개인 및 공용 IP 주소 tooan NIC를 수행 하는 hello 단계를 완료 하 여 기존를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="a396a-142">hello를 바탕으로 hello 예제 [시나리오](#Scenario) 이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="a396a-143">Azure CLI 및이 섹션의 단계를 단일 CLI 세션 내에서 남은 전체 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="a396a-144">전체 hello hello의 단계를 이미 설치 및 구성 하는 Azure CLI 없다면 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 문서 Azure 계정에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="a396a-145">Hello 절, 요구 사항에 따라 다음 중 하나의 hello 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="a396a-146">**개인 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="a396a-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="a396a-147">개인 IP 주소 tooa NIC tooadd 아래 hello 명령을 사용 하 여 IP 구성을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="a396a-148">hello 고정 주소 hello 서브넷에 대 한 사용 되지 않는 주소 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="a396a-149">고유한 구성 이름과 개인 IP 주소를 사용하여 필요한 만큼 구성을 만듭니다(정적 IP 주소를 가진 구성의 경우).</span><span class="sxs-lookup"><span data-stu-id="a396a-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="a396a-150">**공용 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="a396a-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="a396a-151">공용 IP 주소를 tooeither 연결 하 여 추가 되는 새 IP 구성 또는 기존 IP 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="a396a-152">필요한 만큼 따르려면 hello 섹션 중 하나에 hello 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a396a-153">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="a396a-154">가격 책정, 주소 IP에 대 한 자세한 toolearn 읽을 hello [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지.</span><span class="sxs-lookup"><span data-stu-id="a396a-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="a396a-155">구독에서 사용할 수 있는 공용 IP 주소의 제한이 toohello 수가입니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="a396a-156">hello 제한, hello 읽기에 대 한 자세한 toolearn [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서.</span><span class="sxs-lookup"><span data-stu-id="a396a-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="a396a-157">**Hello 리소스 tooa 새 IP 구성에 연결**</span><span class="sxs-lookup"><span data-stu-id="a396a-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="a396a-158">새 IP 구성의 공용 IP 주소를 추가할 때마다 모든 IP 구성 시 개인 IP 주소가 있어야 하기 때문에 개인 IP 주소도 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="a396a-159">기존 공용 IP 주소 리소스를 추가하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="a396a-160">toocreate 한 새 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="a396a-161">개인 고정 IP 주소와 연결 된 hello 새 IP 구성이 toocreate *myPublicIP3* 공용 IP 리소스에 주소를 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="a396a-162">**Hello 리소스 tooan 기존 IP 구성에 연결**</span><span class="sxs-lookup"><span data-stu-id="a396a-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="a396a-163">공용 IP 주소 리소스에 아직 연결 되어 관련된 tooan IP 구성만 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="a396a-164">IP 구성 hello 다음 명령을 입력 하 여 연결 된 공용 IP 주소에 있는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="a396a-165">IPConfig-3에 대 한 출력을 반환 하는 hello에 나오는 줄 비슷한 toohello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="a396a-166">Hello 이후 **공용 IP** 열에 대 한 *IpConfig-3* 은 공백은, 공용 IP 주소 리소스가 현재 연결된 tooit입니다.</span><span class="sxs-lookup"><span data-stu-id="a396a-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="a396a-167">기존 공용 IP 주소 리소스 tooIpConfig-3, 더하거나 명령 toocreate 하나를 수행 하는 hello 입력:</span><span class="sxs-lookup"><span data-stu-id="a396a-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="a396a-168">다음 명령을 tooassociate hello 공용 IP 주소 리소스 toohello 기존 IP 구성 라는 hello 입력 *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="a396a-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="a396a-169">보기 hello 개인 IP 주소 및 다음 명령을 입력 하 여 NIC hello 공용 IP 주소 할당 된 리소스 toohello hello:</span><span class="sxs-lookup"><span data-stu-id="a396a-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="a396a-170">hello 출력은 유사한 toohello 다음 반환:</span><span class="sxs-lookup"><span data-stu-id="a396a-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="a396a-171">Hello에 대 한 hello 지침에 따라 toohello NIC toohello VM 운영 체제를 추가한 hello 개인 IP 주소 추가 [추가 IP 주소 tooa VM 운영 체제](#os-config) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="a396a-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="a396a-172">Hello 공용 IP 주소 toohello 운영 체제를 추가 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a396a-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
