---
title: "Azure에서 SharePoint 서버 팜의 aaaCreate | Microsoft Docs"
description: "Azure 포털 마켓플레이스 hello를 사용 하 여 Azure에서 새 SharePoint 2016 또는 SharePoint 2013 팜을 빠르게 만듭니다."
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
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="18ef9-103">Azure 포털 마켓플레이스 hello를 사용 하 여 SharePoint 서버 팜 만들기</span><span class="sxs-lookup"><span data-stu-id="18ef9-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="18ef9-104">SharePoint 2013 팜</span><span class="sxs-lookup"><span data-stu-id="18ef9-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="18ef9-105">Hello Microsoft Azure 포털 마켓플레이스 미리 구성 된 SharePoint Server 2013 팜을 신속 하 게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="18ef9-106">그러면 개발 및 테스팅 환경에 기본 또는 고가용성 SharePoint 팜이 필요하거나 SharePoint Server 2013을 조직의 협력 솔루션으로 평가하는 경우 상당한 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="18ef9-107">hello **SharePoint 서버 팜의** hello Azure 포털의 hello Azure Marketplace에서에서 항목이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="18ef9-108">Hello로 대체 되었습니다 **SharePoint 2013 비 HA 팜** 및 **SharePoint 2013 HA 팜** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="18ef9-109">기본 SharePoint 팜 hello이이 구성에서 3 개의 가상 컴퓨터가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="18ef9-111">이 팜 구성을 간소화된 SharePoint 앱 개발 설정이나 SharePoint 2013의 최초 평가에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="18ef9-112">toocreate hello 기본 (3 개 서버) SharePoint 팜:</span><span class="sxs-lookup"><span data-stu-id="18ef9-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="18ef9-113">[여기](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="18ef9-114">**배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="18ef9-115">Hello에 **SharePoint 2013 비 HA 팜** 창에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="18ef9-116">Hello hello 단계에서 설정을 지정 **SharePoint 2013 만들 비 HA 팜** 창과 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="18ef9-117">이 구성에서 9 개의 가상 컴퓨터의 hello 고가용성 SharePoint 팜 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="18ef9-119">SharePoint 팜에 대 한이 팜 구성 tootest 높은 클라이언트 부하, hello 외부 SharePoint 사이트의 고가용성 및 SQL Server AlwaysOn 가용성 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="18ef9-120">또한 고가용성 환경에서 SharePoint app 개발에 이 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="18ef9-121">toocreate hello 고가용성 (9-서버) SharePoint 팜:</span><span class="sxs-lookup"><span data-stu-id="18ef9-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="18ef9-122">[여기](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="18ef9-123">**배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="18ef9-124">Hello에 **SharePoint 2013 HA 팜** 창에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="18ef9-125">Hello hello 7 단계에서 설정을 지정 **SharePoint 2013 HA 팜 만들기** 창과 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="18ef9-126">Hello를 만들 수 없습니다 **SharePoint 2013 비 HA 팜** 또는 **SharePoint 2013 HA 팜** Azure 무료 평가판으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="18ef9-127">hello Azure 포털 인터넷 연결 웹 사이트를 사용 하 여 클라우드 전용 가상 네트워크에 이러한 팜 모두를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="18ef9-128">사이트 간 VPN 또는 express 경로 연결 백 tooyour 조직 네트워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="18ef9-129">Hello 기본 만들거나 빌드하면 고가용성 SharePoint 팜에 hello Azure 포털을 사용 하 여 기존 리소스 그룹을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="18ef9-130">이 제한 해결 toowork Azure PowerShell을 사용한 이러한 팜에는 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="18ef9-131">자세한 내용은 [Azure PowerShell을 사용하여 SharePoint 2013 개발/테스트 팜 만들기](https://technet.microsoft.com/library/mt743093.aspx#powershell)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18ef9-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="18ef9-132">SharePoint 2016 팜</span><span class="sxs-lookup"><span data-stu-id="18ef9-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="18ef9-133">참조 [이 여기서](https://technet.microsoft.com/library/mt723354.aspx) hello 지침 toobuild hello 다음 SharePoint Server 2016이 단일 서버 팜 합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="18ef9-135">Hello SharePoint 팜을 관리</span><span class="sxs-lookup"><span data-stu-id="18ef9-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="18ef9-136">원격 데스크톱 연결을 통해 이러한 팜 hello 서버를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="18ef9-137">자세한 내용은 참조 [toohello 가상 컴퓨터에 로그온](quick-create-portal.md#connect-to-virtual-machine)합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="18ef9-138">Hello 중앙 관리 SharePoint 사이트 내 사이트, SharePoint 응용 프로그램 및 기타 기능을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="18ef9-139">자세한 내용은 [SharePoint 구성](http://technet.microsoft.com/library/ee836142.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18ef9-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18ef9-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18ef9-140">Next steps</span></span>
* <span data-ttu-id="18ef9-141">Azure 인프라 서비스에서 추가 [SharePoint 구성](https://technet.microsoft.com/library/dn635309.aspx) 을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="18ef9-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
