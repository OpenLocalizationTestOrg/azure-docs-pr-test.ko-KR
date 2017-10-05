---
title: "Azure Portal을 사용하여 NSG 관리 | Microsoft Docs"
description: "Azure Portal을 사용하여 NSG를 관리하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="1bea2-103">포털을 사용하여 NSG 관리</span><span class="sxs-lookup"><span data-stu-id="1bea2-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1bea2-104">포털</span><span class="sxs-lookup"><span data-stu-id="1bea2-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="1bea2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bea2-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="1bea2-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1bea2-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="1bea2-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1bea2-108">이 문서에서는 Resource Manager 배포 모델 사용을 설명하며 Microsoft에서는 대부분의 새로운 배포에 대해 클래식 배포 모델 대신 이 모델을 사용하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="1bea2-109">정보 검색</span><span class="sxs-lookup"><span data-stu-id="1bea2-109">Retrieve Information</span></span>
<span data-ttu-id="1bea2-110">기존 NSG를 보고 기존 NSG에 대한 규칙을 검색하며 NSG가 연결된 리소스에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="1bea2-111">기존 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="1bea2-111">View existing NSGs</span></span>

<span data-ttu-id="1bea2-112">구독에서 모든 기존 NSG를 보려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-113">브라우저에서 http://portal.azure.com으로 이동하고, 필요한 경우 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="1bea2-114">**찾아보기>** > **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="1bea2-116">**네트워크 보안 그룹** 블레이드에서 NSG 목록을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="1bea2-118">리소스 그룹에서 NSG 보기</span><span class="sxs-lookup"><span data-stu-id="1bea2-118">View NSGs in a resource group</span></span>

<span data-ttu-id="1bea2-119">**RG-NSG** 리소스 그룹에서 NSG 목록을 보려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-120">**리소스 그룹 >** > **RG-NSG** > **...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="1bea2-122">리소스의 목록에서 아래 **리소스** 블레이드에서처럼 NSG 아이콘을 표시하는 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="1bea2-124">NSG에 대한 모든 규칙 나열</span><span class="sxs-lookup"><span data-stu-id="1bea2-124">List all rules for an NSG</span></span>

<span data-ttu-id="1bea2-125">**NSG-FrontEnd**로 명명된 NSG의 규칙을 보려면 다음 명령을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-126">**네트워크 보안 그룹** 블레이드에서 또는 위에 표시된 **리소스** 블레이드에서 **NSG-FrontEnd**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="1bea2-127">**설정** 탭에서 **인바운드 보안 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="1bea2-129">**인바운드 보안 규칙** 블레이드는 아래와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="1bea2-131">**설정** 탭에서 **아웃바운드 보안 규칙**을 클릭하여 아웃바운드 규칙을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1bea2-132">기본 규칙을 보려면 규칙을 표시하는 블레이드 맨 위에서 **규칙 기본** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="1bea2-133">NSG 연결 보기</span><span class="sxs-lookup"><span data-stu-id="1bea2-133">View NSGs associations</span></span>

<span data-ttu-id="1bea2-134">**NSG-FrontEnd** NSG가 연결된 리소스를 보려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-135">**네트워크 보안 그룹** 블레이드에서 또는 위에 표시된 **리소스** 블레이드에서 **NSG-FrontEnd**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="1bea2-136">**설정** 탭에서 **서브넷**을 클릭하여 NSG에 연결된 서브넷을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="1bea2-138">**설정** 탭에서 **네트워크 인터페이스**를 클릭하여 NSG에 연결된 NIC를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="1bea2-139">규칙 관리</span><span class="sxs-lookup"><span data-stu-id="1bea2-139">Manage rules</span></span>
<span data-ttu-id="1bea2-140">기존 NSG에 규칙을 추가하고 기존 규칙을 편집하며 규칙을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="1bea2-141">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="1bea2-141">Add a rule</span></span>
<span data-ttu-id="1bea2-142">컴퓨터에서 **NSG-FrontEnd** NSG에 포트 **443**에 대한 **인바운드** 트래픽을 허용하는 규칙을 추가하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-143">**네트워크 보안 그룹** 블레이드에서 또는 위에 표시된 **리소스** 블레이드에서 **NSG-FrontEnd**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1bea2-144">**설정** 탭에서 **인바운드 보안 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="1bea2-145">**인바운드 보안 규칙** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="1bea2-146">그런 다음 **인바운드 보안 규칙 추가** 블레이드에서 아래와 같이 값을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="1bea2-148">몇 초 후에 **인바운드 보안 규칙** 블레이드에서 새 규칙이 공지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="1bea2-150">규칙 변경</span><span class="sxs-lookup"><span data-stu-id="1bea2-150">Change a rule</span></span>
<span data-ttu-id="1bea2-151">**인터넷**에서 인바운드 트래픽을 허용하도록 위에서 만든 규칙을 변경하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-152">**네트워크 보안 그룹** 블레이드에서 또는 위에 표시된 **리소스** 블레이드에서 **NSG-FrontEnd**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1bea2-153">**설정** 탭에서 위에서 만든 규칙을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="1bea2-154">**allow-https** 블레이드에서 아래와 같이 **원본** 속성을 변경한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="1bea2-156">규칙 삭제</span><span class="sxs-lookup"><span data-stu-id="1bea2-156">Delete a rule</span></span>

<span data-ttu-id="1bea2-157">위에서 만든 규칙을 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-158">**네트워크 보안 그룹** 블레이드에서 또는 위에 표시된 **리소스** 블레이드에서 **NSG-FrontEnd**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1bea2-159">**설정** 탭에서 위에서 만든 규칙을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="1bea2-160">**allow-https** 블레이드에서 **삭제**를 클릭하고 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="1bea2-162">연결 관리</span><span class="sxs-lookup"><span data-stu-id="1bea2-162">Manage associations</span></span>
<span data-ttu-id="1bea2-163">NSG를 서브넷 및 NIC에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="1bea2-164">또한 연결된 모든 리소스에서 NSG를 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="1bea2-165">NIC에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="1bea2-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="1bea2-166">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에 연결하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-167">**네트워크 보안 그룹** 블레이드에서 또는 위에 표시된 **리소스** 블레이드에서 **NSG-FrontEnd**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1bea2-168">**설정** 탭에서 **네트워크 인터페이스** > **연결** > **TestNICWeb1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="1bea2-170">NIC에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="1bea2-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="1bea2-171">**NSG-FrontEnd** NSG를 **TestNICWeb1** NIC에서 분리하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-172">Azure Portal에서 **리소스 그룹 >** > **RG-NSG** > **...** > **TestNICWeb1**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="1bea2-173">**TestNICWeb1** 블레이드에서 **보안 변경...** > **해당 없음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="1bea2-175">또한 NIC를 기존 NSG에 연결하려면이 블레이드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="1bea2-176">서브넷에서 NSG 분리</span><span class="sxs-lookup"><span data-stu-id="1bea2-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="1bea2-177">**NSG-FrontEnd** NSG를 **FrontEnd** 서브넷에서 분리하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-178">Azure Portal에서 **리소스 그룹 >** > **RG-NSG** > **...** > **TestVNet**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="1bea2-179">**설정** 블레이드에서 **서브넷** > **FrontEnd** > **네트워크 보안 그룹** > **해당 없음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="1bea2-181">**FrontEnd** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Azure 포털 - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="1bea2-183">서브넷에 NSG 연결</span><span class="sxs-lookup"><span data-stu-id="1bea2-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="1bea2-184">**NSG-FrontEnd** NSG를 **FronEnd** 서브넷에 다시 연결하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="1bea2-185">Azure Portal에서 **리소스 그룹 >** > **RG-NSG** > **...** > **TestVNet**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="1bea2-186">**설정** 블레이드에서 **서브넷** > **FrontEnd** > **네트워크 보안 그룹** > **NSG-FrontEnd**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="1bea2-187">**FrontEnd** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="1bea2-188">또한 NSG의 **설정** 블레이드에서 서브넷에 NSG를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="1bea2-189">NSG 삭제</span><span class="sxs-lookup"><span data-stu-id="1bea2-189">Delete an NSG</span></span>
<span data-ttu-id="1bea2-190">리소스에 연결되지 않은 경우 NSG를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="1bea2-191">NSG를 삭제하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="1bea2-192">Azure Portal에서 **리소스 그룹 >** > **RG-NSG** > **...** > **NSG-FrontEnd**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="1bea2-193">**설정** 블레이드에서 **네트워크 인터페이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="1bea2-194">NIC가 나열된 경우 NIC를 클릭하고 [NIC에서 NSG 분리](#Dissociate-an-NSG-from-a-NIC)의 2단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="1bea2-195">각 NIC에 3단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="1bea2-196">**설정** 블레이드에서 **서브넷**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="1bea2-197">서브넷이 나열된 경우 서브넷을 클릭하고 [서브넷에서 NSG 분리](#Dissociate-an-NSG-from-a-subnet)의 2단계 및 3단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="1bea2-198">**NSG-FrontEnd** 블레이드의 왼쪽으로 스크롤한 다음 **삭제** > **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1bea2-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure Portal - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="1bea2-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1bea2-200">Next steps</span></span>
* <span data-ttu-id="1bea2-201">[로깅을 사용합니다](virtual-network-nsg-manage-log.md) .</span><span class="sxs-lookup"><span data-stu-id="1bea2-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
