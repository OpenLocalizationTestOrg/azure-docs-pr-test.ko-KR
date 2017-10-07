---
title: "Azure에서 Analysis Services 서버 aaaCreate | Microsoft Docs"
description: "Azure에서 toocreate Analysis Services 서버 인스턴스 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="cac18-103">Azure Portal에서 Azure Analysis Services 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="cac18-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="cac18-104">이 문서에서는 Azure 구독에서 Analysis Services 서버 리소스를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cac18-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cac18-105">Before you begin</span></span>
<span data-ttu-id="cac18-106">toocomplete 해야이 빠른 시작:</span><span class="sxs-lookup"><span data-stu-id="cac18-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="cac18-107">**Azure 구독**: 방문 [Azure 무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate 계정.</span><span class="sxs-lookup"><span data-stu-id="cac18-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="cac18-108">**Azure Active Directory**: 구독이 Azure Active Directory와 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="cac18-109">고 toobe tooAzure Azure Active Directory의 계정으로 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="cac18-110">Microsoft 계정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="cac18-111">toolearn 더 참조 [인증 및 사용자 권한을](analysis-services-manage-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="cac18-112">**리소스 그룹**: 기존 리소스 그룹을 사용하거나 [새 리소스 그룹을 만듭니다](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cac18-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cac18-113">서버를 만들면 새로운 유료 서비스가 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="cac18-114">toolearn 더 참조 [Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="cac18-115">Azure 포털에서 서버 toocreate</span><span class="sxs-lookup"><span data-stu-id="cac18-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="cac18-116">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="cac18-117">**+새로 만들기** > **데이터 + 분석** > **Analysis Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="cac18-118">Hello에 **Analysis Services** 블레이드에서 필수 hello 필드를 입력 하 고 다음 키를 누릅니다 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![서버 만들기](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="cac18-120">**서버 이름**: 사용 된 고유 이름을 tooreference hello 서버를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="cac18-121">**구독**:이 서버에 청구 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="cac18-122">**리소스 그룹**: 이러한 컨테이너는 디자인 된 toohelp Azure 리소스 컬렉션을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="cac18-123">toolearn 더 참조 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="cac18-124">**위치**:이 Azure 데이터 센터 위치 호스트 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="cac18-125">가장 큰 사용자 기반에 가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="cac18-126">**가격 책정 계층**: 가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="cac18-127">Too400 GB 테이블 형식 모델 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="cac18-128">toolearn 더 참조 [Azure Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="cac18-129">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-129">Click **Create**.</span></span>

<span data-ttu-id="cac18-130">만드는 데 1분 이내, 대개 몇 초가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="cac18-131">선택한 경우 **tooPortal 추가**, tooyour 포털 toosee 새 서버로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="cac18-132">너무 이동 또는**더 많은 서비스** > **Analysis Services** toosee 서버를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![대시보드](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="cac18-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cac18-134">Next steps</span></span>
<span data-ttu-id="cac18-135">서버를 만든 후 [모델 배포](analysis-services-deploy.md) tooit SSMS 또는 SSDT를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="cac18-136">Tooinstall 필요한 tooyour 서버를 배포 하는 모델 tooon 온-프레미스 데이터 원본에 연결 된 경우는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md) 네트워크의 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cac18-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

