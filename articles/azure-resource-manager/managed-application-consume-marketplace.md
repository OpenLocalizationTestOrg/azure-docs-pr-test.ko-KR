---
title: "Marketplace에서 Azure Managed Application 사용 | Microsoft Docs"
description: "Marketplace를 통해 사용할 수 있는 Azure Managed Application을 만드는 방법을 설명합니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="6aa05-103">Marketplace에서 Azure Managed Application 사용</span><span class="sxs-lookup"><span data-stu-id="6aa05-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="6aa05-104">[Managed Application 개요](managed-application-overview.md) 문서에서 설명한 대로 종단 간 환경에는 두 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="6aa05-105">하나는 관리되는 응용 프로그램을 만들어 고객이 사용할 수 있게 하려는 게시자 또는 공급업체입니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="6aa05-106">다른 하나는 관리되는 응용 프로그램의 최종 고객 또는 소비자입니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="6aa05-107">이 문서에서는 두 번째 시나리오에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-107">This article covers the second scenario.</span></span> <span data-ttu-id="6aa05-108">Microsoft Azure Marketplace의 관리되는 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="6aa05-109">Marketplace에서 만들기</span><span class="sxs-lookup"><span data-stu-id="6aa05-109">Create from the Marketplace</span></span>

<span data-ttu-id="6aa05-110">Marketplace에서 관리되는 응용 프로그램을 배포하는 것은 Marketplace에서 유형에 관계없이 리소스를 배포하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="6aa05-111">포털에서 **+새로 만들기**를 선택하고 배포할 솔루션 유형을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="6aa05-112">사용 가능한 옵션 중에서 필요한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-112">From the available options, select the one you need.</span></span>

![검색 솔루션](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="6aa05-114">응용 프로그램의 요약을 검토하고 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-114">Review the summary of the application, and select **Create**.</span></span>

![관리되는 응용 프로그램 만들기](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="6aa05-116">다른 솔루션과 마찬가지로 값을 제공할 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="6aa05-117">이러한 필드는 생성하는 관리되는 응용 프로그램의 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="6aa05-118">지원 정보 보기</span><span class="sxs-lookup"><span data-stu-id="6aa05-118">View support information</span></span>

<span data-ttu-id="6aa05-119">관리되는 응용 프로그램이 배포된 후에 응용 프로그램에 대한 지원 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="6aa05-120">관리되는 응용 프로그램 블레이드에서 지원 정보가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-120">In the managed application blade, the support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="6aa05-122">게시자 사용 권한 보기</span><span class="sxs-lookup"><span data-stu-id="6aa05-122">View publisher permissions</span></span>

<span data-ttu-id="6aa05-123">응용 프로그램을 관리하는 공급업체에는 리소스에 대한 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="6aa05-124">이러한 사용 권한을 보려면 **권한 부여**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa05-124">To see those permissions, select **Authorizations**.</span></span>

![권한 부여](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="6aa05-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6aa05-126">Next steps</span></span>

* <span data-ttu-id="6aa05-127">Marketplace에서 관리되는 응용 프로그램을 게시하는 방법에 대한 자세한 내용은 [Marketplace의 Azure Managed Application](managed-application-author-marketplace.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa05-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="6aa05-128">조직의 사용자만 사용할 수 있는 관리되는 응용 프로그램을 게시하려면 [서비스 카탈로그 관리되는 응용 프로그램 만들기 및 게시](managed-application-publishing.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa05-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="6aa05-129">조직의 사용자만 사용할 수 있는 관리되는 응용 프로그램을 사용하려면 [서비스 카탈로그 관리되는 응용 프로그램 사용](managed-application-consumption.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa05-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>