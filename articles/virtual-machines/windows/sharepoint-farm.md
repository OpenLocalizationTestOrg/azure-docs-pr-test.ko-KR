---
title: "Azure에서 SharePoint Server 팜 만들기 | Microsoft Docs"
description: "Azure Portal Marketplace를 사용하여 Azure에서 새 SharePoint 2013 또는 2016 SharePoint 팜을 신속하게 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 00648ee35962b22fb7eeceaa6d9df7305c801abf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a><span data-ttu-id="6fe6f-103">Azure Portal Marketplace를 사용하여 SharePoint 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="6fe6f-103">Create SharePoint server farms using the Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="6fe6f-104">SharePoint 2013 팜</span><span class="sxs-lookup"><span data-stu-id="6fe6f-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="6fe6f-105">Microsoft Azure 포털 마켓플레이스를 사용하면 미리 구성된 SharePoint Server 2013 팜을 신속하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="6fe6f-106">그러면 개발 및 테스팅 환경에 기본 또는 고가용성 SharePoint 팜이 필요하거나 SharePoint Server 2013을 조직의 협력 솔루션으로 평가하는 경우 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="6fe6f-107">Azure 포털에서 Azure 마켓플레이스의 **SharePoint 서버 팜** 항목이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span></span> <span data-ttu-id="6fe6f-108">이 항목은 **SharePoint 2013 비 HA 팜** 및 **SharePoint 2013 HA 팜** 항목으로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="6fe6f-109">기본 SharePoint 팜은 다음 구성의 3가지 가상 컴퓨터로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="6fe6f-111">이 팜 구성을 간소화된 SharePoint 앱 개발 설정이나 SharePoint 2013의 최초 평가에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="6fe6f-112">기본(3-서버) SharePoint 팜을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="6fe6f-112">To create the basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="6fe6f-113">[여기](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="6fe6f-114">**배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="6fe6f-115">**SharePoint 2013 비 HA 팜** 창에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="6fe6f-116">**SharePoint 2013 비 HA 팜** 창의 단계에서 설정을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="6fe6f-117">고가용성 SharePoint 팜은 다음과 같은 구성으로 9개의 가상 컴퓨터로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="6fe6f-119">이 팜 구성을 사용하여 SharePoint 팜에 대해 보다 과도한 클라이언트 부하, 외부 SharePoint 사이트의 고가용성 및 SQL Server AlwaysOn 가용성 그룹을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="6fe6f-120">또한 고가용성 환경에서 SharePoint app 개발에 이 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="6fe6f-121">고가용성(9-서버) SharePoint 팜을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="6fe6f-121">To create the high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="6fe6f-122">[여기](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="6fe6f-123">**배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="6fe6f-124">**SharePoint 2013 HA 팜** 창에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="6fe6f-125">**SharePoint 2013 HA 팜** 창의 7단계에서 설정을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="6fe6f-126">Azure 무료 평가판에서는 **SharePoint 2013 비 HA 팜** 또는 **SharePoint 2013 HA 팜**을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="6fe6f-127">Azure 포털은 인터넷 연결 웹 서비스를 사용하여 클라우드 전용 가상 네트워크에 이러한 팜을 모두 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="6fe6f-128">조직 네트워크에 대한 사이트 간 VPN 또는 ExpressRoute 연결은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="6fe6f-129">Azure Portal을 사용하여 기본 또는 고가용성 SharePoint 팜을 만들 때 기존 리소스 그룹을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="6fe6f-130">이 제한을 해결하려면 Azure PowerShell을 사용하여 이러한 팜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-130">To work around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="6fe6f-131">자세한 내용은 [Azure PowerShell을 사용하여 SharePoint 2013 개발/테스트 팜 만들기](https://technet.microsoft.com/library/mt743093.aspx#powershell)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="6fe6f-132">SharePoint 2016 팜</span><span class="sxs-lookup"><span data-stu-id="6fe6f-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="6fe6f-133">다음 단일 서버 SharePoint Server 2016 팜을 빌드하는 방법에 대한 지침은 [이 문서](https://technet.microsoft.com/library/mt723354.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-the-sharepoint-farms"></a><span data-ttu-id="6fe6f-135">SharePoint 팜 관리</span><span class="sxs-lookup"><span data-stu-id="6fe6f-135">Managing the SharePoint farms</span></span>
<span data-ttu-id="6fe6f-136">원격 데스크톱 연결을 통해 이러한 팜의 서버를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-136">You can administer the servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="6fe6f-137">자세한 내용은 [가상 컴퓨터에 로그온](quick-create-portal.md#connect-to-virtual-machine)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="6fe6f-138">중앙 관리 SharePoint 사이트에서 내 사이트, SharePoint 응용 프로그램 및 기타 기능을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="6fe6f-139">자세한 내용은 [SharePoint 구성](http://technet.microsoft.com/library/ee836142.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fe6f-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6fe6f-140">Next steps</span></span>
* <span data-ttu-id="6fe6f-141">Azure 인프라 서비스에서 추가 [SharePoint 구성](https://technet.microsoft.com/library/dn635309.aspx) 을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6fe6f-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
