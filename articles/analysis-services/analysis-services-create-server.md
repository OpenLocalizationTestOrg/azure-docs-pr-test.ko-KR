---
title: "Azure에서 Analysis Services 서버 만들기 | Microsoft Docs"
description: "Azure에서 Analysis Services 서버 인스턴스를 만드는 방법을 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="20cb1-103">Azure Portal에서 Azure Analysis Services 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="20cb1-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="20cb1-104">이 문서에서는 Azure 구독에서 Analysis Services 서버 리소스를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20cb1-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="20cb1-105">Before you begin</span></span>
<span data-ttu-id="20cb1-106">이 빠른 시작을 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="20cb1-107">**Azure 구독**: [Azure 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/)으로 이동하여 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="20cb1-108">**Azure Active Directory**: 구독이 Azure Active Directory와 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="20cb1-109">또한 해당 Azure Active Directory의 계정으로 Azure에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="20cb1-110">Microsoft 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="20cb1-111">자세한 내용은 [인증 및 사용자 권한](analysis-services-manage-users.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20cb1-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="20cb1-112">**리소스 그룹**: 기존 리소스 그룹을 사용하거나 [새 리소스 그룹을 만듭니다](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="20cb1-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="20cb1-113">서버를 만들면 새로운 유료 서비스가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="20cb1-114">자세한 내용은 [Analysis Services 가격 책정](https://azure.microsoft.com/pricing/details/analysis-services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20cb1-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="20cb1-115">Azure Portal에서 서버를 만들려면</span><span class="sxs-lookup"><span data-stu-id="20cb1-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="20cb1-116">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="20cb1-117">**+새로 만들기** > **데이터 + 분석** > **Analysis Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="20cb1-118">**Analysis Services** 블레이드에서 필수 필드를 입력한 다음 **만들기**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![서버 만들기](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="20cb1-120">**서버 이름**: 서버를 참조하는 데 사용되는 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="20cb1-121">**구독**: 이 서버를 청구할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="20cb1-122">**리소스 그룹**: Azure 리소스 컬렉션을 관리할 수 있도록 디자인된 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="20cb1-123">자세한 내용은 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20cb1-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="20cb1-124">**위치**: 이 Azure 데이터 센터 위치는 서버를 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="20cb1-125">가장 큰 사용자 기반에 가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="20cb1-126">**가격 책정 계층**: 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="20cb1-127">최대 400GB의 테이블 형식 모델이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="20cb1-128">자세한 내용은 [Azure Analysis Services 가격 책정](https://azure.microsoft.com/pricing/details/analysis-services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20cb1-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="20cb1-129">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-129">Click **Create**.</span></span>

<span data-ttu-id="20cb1-130">만드는 데 1분 이내, 대개 몇 초가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="20cb1-131">**포털에 추가**를 선택한 경우 새 서버를 보려면 포털로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="20cb1-132">또는 **더 많은 서비스** > **Analysis Services**로 이동하여 서버가 준비되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![대시보드](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="20cb1-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20cb1-134">Next steps</span></span>
<span data-ttu-id="20cb1-135">일단 서버를 만들면 SSMS 또는 SSDT를 사용하여 [모델을 배포](analysis-services-deploy.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="20cb1-136">서버에 배포하는 모델이 온-프레미스 데이터 원본에 연결된 경우 네트워크의 컴퓨터에서 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20cb1-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

