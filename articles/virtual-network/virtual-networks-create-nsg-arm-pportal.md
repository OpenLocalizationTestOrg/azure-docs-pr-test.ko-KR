---
title: "네트워크 보안 그룹 만들기 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 네트워크 보안 그룹을 만들고 배포하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 865032f350735d35668bb199ccf1ef3f0fae81de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="2a84f-103">Azure Portal을 사용하여 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="2a84f-103">Create network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="2a84f-104">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="2a84f-105">[클래식 배포 모델에서 NSG를 만들](virtual-networks-create-nsg-classic-ps.md)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="2a84f-106">아래 샘플 PowerShell 명령에는 위의 시나리오를 기반으로 이미 만들어져 있는 단순한 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="2a84f-107">이 문서에 표시된 대로 명령을 실행하려는 경우 먼저 [이 템플릿](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd)을 배포하여 테스트 환경을 구축하고 **Azure에 배포**를 클릭한 다음 필요한 경우 기본 매개 변수 값을 바꾸고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="2a84f-108">아래 단계는 템플릿이 배포된 리소스 그룹의 이름으로 **RG-NSG** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="2a84f-109">NSG-FrontEnd NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="2a84f-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="2a84f-110">위의 시나리오에 나온 것처럼 **NSG-FrontEnd** NSG를 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2a84f-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="2a84f-111">브라우저에서 http://portal.azure.com으로 이동하고, 필요한 경우 Azure 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="2a84f-112">**찾아보기>** > **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="2a84f-114">**네트워크 보안 그룹** 블레이드에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="2a84f-116">**네트워크 보안 그룹 만들기** 블레이드에서 *RG-NSG* 리소스 그룹 안에 *NSG-FrontEnd* 라는 이름의 NSG를 만든 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure Portal - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="2a84f-118">기존 NSG에서 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="2a84f-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="2a84f-119">Azure Portal의 기존 NSG에 규칙을 만들려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="2a84f-120">**찾아보기 >** > **네트워크 보안 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="2a84f-121">NSG 목록에서 **NSG-FrontEnd** > **인바운드 보안 규칙**</span><span class="sxs-lookup"><span data-stu-id="2a84f-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure Portal - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="2a84f-123">**인바운드 보안 규칙**을 배포하여 테스트 환경을 구축하고 **추가**수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure Portal - 규칙 추가](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="2a84f-125">**인바운드 보안 규칙 추가** 블레이드에서 우선순위 *200*의 *web-rule*이라는 규칙을 만들어 *TCP* 및 포트 *80*을 통한 모든 원본의 모든 VM으로 액세스를 허용한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="2a84f-126">이러한 설정 중 대부분은 이미 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure Portal - 규칙 설정](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="2a84f-128">몇 초 후는 NSG에 새 규칙이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Azure Portal - 새 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="2a84f-130">6단계까지 반복하여 *TCP* 및 포트 *3389*를 통해 모든 원본의 모든 VM에 대한 액세스를 허용하는 우선 순위 *250*의 *rdp-rule*이라는 인바운드 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="2a84f-131">NSG를 FrontEnd 서브넷에 연결</span><span class="sxs-lookup"><span data-stu-id="2a84f-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="2a84f-132">**찾아보기 >** > **리소스 그룹** > **RG-NSG**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="2a84f-133">**RG-NSG** 블레이드에서 **...** > **TestVNet**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure Portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="2a84f-135">**설정** 블레이드에서 **서브넷** > **FrontEnd** > **네트워크 보안 그룹** > **NSG-FrontEnd**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure Portal - 서브넷 설정](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="2a84f-137">**FrontEnd** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure Portal - 서브넷 설정](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="2a84f-139">NSG-BackEnd NSG 만들기</span><span class="sxs-lookup"><span data-stu-id="2a84f-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="2a84f-140">**NSG-BackEnd** NSG를 만든 후 **BackEnd** 서브넷에 연결하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="2a84f-141">[NSG-FrontEnd NSG 만들기](#Create-the-NSG-FrontEnd-NSG) 의 단계를 반복하여 *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="2a84f-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="2a84f-142">아래 표에 있는 [인바운드](#Create-rules-in-an-existing-NSG) 규칙을 만들려면 **기존 NSG에서 규칙 만들기** 의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="2a84f-143">인바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="2a84f-143">Inbound rule</span></span> | <span data-ttu-id="2a84f-144">아웃바운드 규칙</span><span class="sxs-lookup"><span data-stu-id="2a84f-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure Portal - 인바운드 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure Portal - 아웃바운드 규칙](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="2a84f-147">**NSG-Backend** NSG를 **BackEnd** 서브넷에 연결하려면 [FrontEnd 서브넷에 NSG 연결](#Associate-the-NSG-to-the-FrontEnd-subnet)의 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="2a84f-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a84f-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2a84f-148">Next Steps</span></span>
* <span data-ttu-id="2a84f-149">[기존 NSG 관리](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2a84f-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="2a84f-150">[로깅을 사용합니다](virtual-network-nsg-manage-log.md).</span><span class="sxs-lookup"><span data-stu-id="2a84f-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

