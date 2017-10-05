---
title: "Azure Virtual Machines의 여러 IP 주소 - 포털 | Microsoft Docs"
description: "Azure Portal | Resource Manager를 사용하여 가상 컴퓨터에 여러 IP 주소를 할당하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: d264bd47d76db8015a64f09248c57c94572e2693
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-portal"></a><span data-ttu-id="40822-103">Azure Portal을 사용하여 가상 컴퓨터에 여러 IP 주소 할당</span><span class="sxs-lookup"><span data-stu-id="40822-103">Assign multiple IP addresses to virtual machines using the Azure portal</span></span>

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
<span data-ttu-id="40822-104">이 문서는 Azure Portal을 사용하여 Azure Resource Manager 배포 모델을 통해 VM(가상 컴퓨터)을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure portal.</span></span> <span data-ttu-id="40822-105">클래식 배포 모델을 통해 생성된 리소스에 여러 IP 주소를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="40822-106">Azure 배포 모델에 대해 자세히 알아보려면 [배포 모델 이해](../resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40822-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="40822-107"><a name = "create"></a>여러 IP 주소를 사용하여 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="40822-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="40822-108">여러 IP 주소 또는 고정 개인 IP 주소를 사용하여 VM을 만들려면 PowerShell 또는 Azure CLI를 사용하여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-108">If you want to create a VM with multiple IP addresses, or a static private IP address, you must create it using PowerShell or the Azure CLI.</span></span> <span data-ttu-id="40822-109">방법을 보려면 이 문서 맨 위에 있는 PowerShell 또는 CLI 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-109">Click the PowerShell or CLI options at the top of this article to learn how.</span></span> <span data-ttu-id="40822-110">[Windows VM 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md) 또는 [Linux VM 만들기](../virtual-machines/linux/quick-create-portal.md) 문서의 단계에 따라 포털을 사용하여 단일 동적 개인 IP 주소 및 (선택적으로) 단일 공용 IP 주소를 사용하여 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-110">You can create a VM with a single dynamic private IP address and (optionally) a single public IP address using the portal by following the steps in the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="40822-111">VM을 만든 후에 이 문서의 [VM에 IP 주소 추가](#add) 섹션에 나오는 단계에 따라 포털을 사용하여 IP 주소 형식을 동적에서 고정으로 변경하고 추가 IP 주소를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-111">After you create the VM, you can change the IP address type from dynamic to static and add additional IP addresses using the portal by following steps in the [Add IP addresses to a VM](#add) section of this article.</span></span>

## <span data-ttu-id="40822-112"><a name="add"></a>VM에 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="40822-112"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="40822-113">다음 단계를 완료하여 개인 및 공용 IP 주소를 NIC에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-113">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="40822-114">다음 섹션의 예제는 이 문서의 [시나리오](#Scenario)에서 설명한 3개의 IP로 구성된 VM이 이미 있다는 가정 하에 진행하되 필수 사항은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="40822-114">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

### <span data-ttu-id="40822-115"><a name="coreadd"></a>핵심 단계</span><span class="sxs-lookup"><span data-stu-id="40822-115"><a name="coreadd"></a>Core steps</span></span>

1. <span data-ttu-id="40822-116">https://portal.azure.com의 Azure Portal로 이동한 후 필요한 경우 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-116">Browse to the Azure portal at https://portal.azure.com and sign into it, if necessary.</span></span>
2. <span data-ttu-id="40822-117">포털에서 **더 많은 서비스**를 클릭하고 필터 상자에 *가상 컴퓨터*를 입력하고 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-117">In the portal, click **More services** > type *virtual machines* in the filter box, and then click **Virtual machines**.</span></span>
3. <span data-ttu-id="40822-118">**가상 컴퓨터** 블레이드에서 IP 주소를 추가하려는 VM을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-118">In the **Virtual machines** blade, click the VM you want to add IP addresses to.</span></span> <span data-ttu-id="40822-119">나타나는 가상 컴퓨터 블레이드에서 **네트워크 인터페이스**를 클릭한 다음 IP 주소를 추가할 네트워크 인터페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-119">Click **Network interfaces** in the virtual machine blade that appears, and then select the network interface you want to add the IP addresses to.</span></span> <span data-ttu-id="40822-120">다음 그림의 예제에서는 *myVM*이라는 VM에서 *myNIC*라는 NIC가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="40822-120">In the example shown in the following picture, the NIC named *myNIC* from the VM named *myVM* is selected:</span></span>

    ![네트워크 인터페이스](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. <span data-ttu-id="40822-122">선택한 NIC에 대해 표시되는 블레이드에서 **IP 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-122">In the blade that appears for the NIC you selected, click **IP configurations**.</span></span>

<span data-ttu-id="40822-123">추가할 IP 주소 형식에 따라, 이어지는 섹션 중 하나의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-123">Complete the steps in one of the sections that follow, based on the type of IP address you want to add.</span></span>

### <a name="add-a-private-ip-address"></a><span data-ttu-id="40822-124">**개인 IP 주소 추가**</span><span class="sxs-lookup"><span data-stu-id="40822-124">**Add a private IP address**</span></span>

<span data-ttu-id="40822-125">새 개인 IP 주소를 추가하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-125">Complete the following steps to add a new private IP address:</span></span>

1. <span data-ttu-id="40822-126">이 문서의 [핵심 단계](#coreadd) 섹션에 나오는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-126">Complete the steps in the [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="40822-127">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-127">Click **Add**.</span></span> <span data-ttu-id="40822-128">나타나는 **IP 구성 추가** 블레이드에서 *고정* 개인 IP 주소가 *10.0.0.7*인 *IPConfig 4*라는 IP 구성을 만든 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-128">In the **Add IP configuration** blade that appears, create an IP configuration named *IPConfig-4* with *10.0.0.7* as a *Static* private IP address, then click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="40822-129">고정 IP 주소를 추가할 경우 NIC가 연결된 서브넷의 사용하지 않은 유효한 주소를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-129">When adding a static IP address, you must specify an unused, valid address on the subnet the NIC is connected to.</span></span> <span data-ttu-id="40822-130">선택한 주소를 사용할 수 없는 경우 포털에 IP 주소로 X가 표시되며 다른 주소를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-130">If the address you select is not available, the portal will show an X for the IP address and you'll need to select a different one.</span></span>

3. <span data-ttu-id="40822-131">확인을 클릭하면 블레이드가 닫히고 새 IP 구성이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="40822-131">Once you click OK, the blade will close and you'll see the new IP configuration listed.</span></span> <span data-ttu-id="40822-132">**확인**을 클릭하여 **IP 구성 추가** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-132">Click **OK** to close the **Add IP configuration** blade.</span></span>
4. <span data-ttu-id="40822-133">**추가**를 클릭하여 다른 IP 구성을 추가하거나 열려 있는 모든 블레이드를 닫아 IP 주소 추가를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-133">You can click **Add** to add additional IP configurations, or close all open blades to finish adding IP addresses.</span></span>
5. <span data-ttu-id="40822-134">이 문서의 [VM 운영 체제에 IP 주소 추가](#os-config) 섹션에 나오는 사용자 운영 체제별 단계를 완료하여 개인 IP 주소를 VM 운영 체제에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-134">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

### <a name="add-a-public-ip-address"></a><span data-ttu-id="40822-135">공용 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="40822-135">Add a public IP address</span></span>

<span data-ttu-id="40822-136">공용 IP 주소 리소스를 새 IP 구성 또는 기존 IP 구성에 연결하면 공용 IP 주소가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="40822-136">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="40822-137">공용 IP 주소에는 명목 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="40822-137">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="40822-138">IP 주소 가격에 대한 자세한 내용은 [IP 주소 가격](https://azure.microsoft.com/pricing/details/ip-addresses) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40822-138">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="40822-139">구독 내에서 사용할 수 있는 공용 IP 주소의 수는 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-139">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="40822-140">이러한 한에 대한 자세한 내용은 [Azure 제한](../azure-subscription-service-limits.md#networking-limits) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="40822-140">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
> 

### <span data-ttu-id="40822-141"><a name="create-public-ip"></a>공용 IP 주소 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="40822-141"><a name="create-public-ip"></a>Create a public IP address resource</span></span>

<span data-ttu-id="40822-142">공용 IP 주소는 공용 IP 주소 리소스에 대한 한 가지 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="40822-142">A public IP address is one setting for a public IP address resource.</span></span> <span data-ttu-id="40822-143">IP 구성에 연결하려는 IP 구성에 현재 연결되어 있지 않은 공용 IP 주소 리소스가 있는 경우 다음 단계를 건너뛰고 필요에 따라 이어지는 섹션 중 하나에 나와 있는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-143">If you have a public IP address resource that is not currently associated to an IP configuration that you want to associate to an IP configuration, skip the following steps and complete the steps in one of the sections that follow, as you require.</span></span> <span data-ttu-id="40822-144">사용 가능한 공용 IP 주소 리소스가 없는 경우 다음 단계를 완료하여 리소스를 하나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40822-144">If you don't have an available public IP address resource, complete the following steps to create one:</span></span>

1. <span data-ttu-id="40822-145">https://portal.azure.com의 Azure Portal로 이동한 후 필요한 경우 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-145">Browse to the Azure portal at https://portal.azure.com and sign into it, if necessary.</span></span>
3. <span data-ttu-id="40822-146">포털에서 **새로 만들기** > **네트워킹** > **공용 IP 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-146">In the portal, click **New** > **Networking** > **Public IP address**.</span></span>
4. <span data-ttu-id="40822-147">다음 그림에 표시된 것처럼 나타나는 **공용 IP 주소 만들기** 블레이드에서 **이름**을 입력하고 **IP 주소 할당** 형식, **구독**, **리소스 그룹** 및 **위치**를 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-147">In the **Create public IP address** blade that appears, enter a **Name**, select an **IP address assignment** type, a **Subscription**, a **Resource group**, and a **Location**, then click **Create**, as shown in the following picture:</span></span>

    ![공용 IP 주소 리소스 만들기](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. <span data-ttu-id="40822-149">공용 IP 주소 리소스를 IP 구성에 연결하려면 이어지는 섹션 중 하나에 나와 있는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-149">Complete the steps in one of the sections that follow to associate the public IP address resource to an IP configuration.</span></span>

#### <a name="associate-the-public-ip-address-resource-to-a-new-ip-configuration"></a><span data-ttu-id="40822-150">새 IP 구성에 공용 IP 주소 리소스 연결</span><span class="sxs-lookup"><span data-stu-id="40822-150">Associate the public IP address resource to a new IP configuration</span></span>

1. <span data-ttu-id="40822-151">이 문서의 [핵심 단계](#coreadd) 섹션에 나오는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-151">Complete the steps in the [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="40822-152">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-152">Click **Add**.</span></span> <span data-ttu-id="40822-153">나타나는 **IP 구성 추가** 블레이드에서 *IPConfig-4*라는 IP 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="40822-153">In the **Add IP configuration** blade that appears, create an IP configuration named *IPConfig-4*.</span></span> <span data-ttu-id="40822-154">나타나는 **공용 IP 주소 선택** 블레이드에서 **공용 IP 주소**를 사용하도록 설정하고 사용 가능한 기존 공용 IP 주소 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-154">Enable the **Public IP address** and select an existing, available public IP address resource from the **Choose public IP address** blade that appears.</span></span>

    <span data-ttu-id="40822-155">공용 IP 주소 리소스를 선택한 후 **확인**을 클릭하여 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-155">Once you've selected the public IP address resource, click **OK** and the blade will close.</span></span> <span data-ttu-id="40822-156">기존 공용 IP 주소가 없는 경우 이 문서의 [공용 IP 주소 리소스 만들기](#create-public-ip) 섹션에 나와 있는 단계를 완료하여 주소를 하나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-156">If you don't have an existing public IP address, you can create one by completing the steps in the [Create a public IP address resource](#create-public-ip) section of this article.</span></span> 

3. <span data-ttu-id="40822-157">새 IP 구성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-157">Review the new IP configuration.</span></span> <span data-ttu-id="40822-158">개인 IP 주소가 명시적으로 할당되지 않았더라도 모든 IP 구성에는 개인 IP 주소가 있어야 하므로 IP 구성에 자동으로 주소가 하나 할당되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-158">Even though a private IP address wasn't explicitly assigned, one was automatically assigned to the IP configuration, because all IP configurations must have a private IP address.</span></span>
4. <span data-ttu-id="40822-159">**추가**를 클릭하여 다른 IP 구성을 추가하거나 열려 있는 모든 블레이드를 닫아 IP 주소 추가를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-159">You can click **Add** to add additional IP configurations, or close all open blades to finish adding IP addresses.</span></span>
5. <span data-ttu-id="40822-160">이 문서의 [VM 운영 체제에 IP 주소 추가](#os-config) 섹션에 나오는 사용자 운영 체제별 단계를 완료하여 개인 IP 주소를 VM 운영 체제에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-160">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="40822-161">운영 체제에 공용 IP 주소를 추가하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="40822-161">Do not add the public IP address to the operating system.</span></span>

#### <a name="associate-the-public-ip-address-resource-to-an-existing-ip-configuration"></a><span data-ttu-id="40822-162">기존 IP 구성에 공용 IP 주소 리소스 연결</span><span class="sxs-lookup"><span data-stu-id="40822-162">Associate the public IP address resource to an existing IP configuration</span></span>

1. <span data-ttu-id="40822-163">이 문서의 [핵심 단계](#coreadd) 섹션에 나오는 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-163">Complete the steps in the [Core steps](#coreadd) section of this article.</span></span>
2. <span data-ttu-id="40822-164">공용 IP 주소 리소스를 추가할 IP 구성을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-164">Click the IP configuration you want to add the public IP address resource to.</span></span>
3. <span data-ttu-id="40822-165">나타나는 IPConfig 블레이드에서 **IP 주소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-165">In the IPConfig blade that appears, click **IP address**.</span></span>
4. <span data-ttu-id="40822-166">나타나는 **공용 IP 주소 선택** 블레이드에서 공용 IP 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-166">In the **Choose public IP address** blade that appears, select a public IP address.</span></span>
5. <span data-ttu-id="40822-167">**저장**을 클릭합니다. 그러면 블레이드가 닫힙니다.</span><span class="sxs-lookup"><span data-stu-id="40822-167">Click **Save** and the blades will close.</span></span> <span data-ttu-id="40822-168">기존 공용 IP 주소가 없는 경우 이 문서의 [공용 IP 주소 리소스 만들기](#create-public-ip) 섹션에 나와 있는 단계를 완료하여 주소를 하나 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-168">If you don't have an existing public IP address, you can create one by completing the steps in the [Create a public IP address resource](#create-public-ip) section of this article.</span></span>
3. <span data-ttu-id="40822-169">새 IP 구성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="40822-169">Review the new IP configuration.</span></span>
4. <span data-ttu-id="40822-170">**추가**를 클릭하여 다른 IP 구성을 추가하거나 열려 있는 모든 블레이드를 닫아 IP 주소 추가를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40822-170">You can click **Add** to add additional IP configurations, or close all open blades to finish adding IP addresses.</span></span> <span data-ttu-id="40822-171">운영 체제에 공용 IP 주소를 추가하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="40822-171">Do not add the public IP address to the operating system.</span></span>


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
