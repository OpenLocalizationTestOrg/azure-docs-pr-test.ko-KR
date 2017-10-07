---
title: "Azure 관리에서 응용 프로그램 마켓플레이스 aaaConsume | Microsoft Docs"
description: "Describeshow toocreate Azure 관리 하는 응용 프로그램 마켓플레이스 hello를 통해 사용할 수 있습니다."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="ce6dd-103">사용할 Azure 마켓플레이스 hello에 대 한 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="ce6dd-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="ce6dd-104">Hello에 설명 된 대로 [관리 되는 응용 프로그램 개요](managed-application-overview.md) 문서, hello 끝 tooend 환경에서 두 가지 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="ce6dd-105">하나는 hello 게시자 또는 알고자 하 toocreate 고객이 사용 하기 위해 관리 되는 응용 프로그램 공급 업체입니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="ce6dd-106">hello는 둘째 hello 최종 고객 또는 hello 관리 되는 응용 프로그램의 hello 소비자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="ce6dd-107">이 문서에서는 hello 두 번째 시나리오에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-107">This article covers hello second scenario.</span></span> <span data-ttu-id="ce6dd-108">Hello Microsoft Azure Marketplace에서에서 관리 되는 응용 프로그램을 배포 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="ce6dd-109">Hello Marketplace에서 만들기</span><span class="sxs-lookup"><span data-stu-id="ce6dd-109">Create from hello Marketplace</span></span>

<span data-ttu-id="ce6dd-110">Hello Marketplace에서에서 관리 되는 응용 프로그램 배포는 hello Marketplace에서에서 리소스의 모든 유형을 비슷한 toodeploying입니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="ce6dd-111">Hello 포털에서 선택 **+ 새로 만들기** 솔루션 toodeploy의 hello 형식으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="ce6dd-112">Hello 사용 가능한 옵션 중에서 필요한 하나 hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-112">From hello available options, select hello one you need.</span></span>

![검색 솔루션](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="ce6dd-114">Hello 응용 프로그램의 hello 요약을 검토 하 고 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-114">Review hello summary of hello application, and select **Create**.</span></span>

![관리되는 응용 프로그램 만들기](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="ce6dd-116">마찬가지로 다른 솔루션에 대 한 필드 tooprovide 값으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="ce6dd-117">이러한 필드는 생성 하는 관리 되는 응용 프로그램의 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="ce6dd-118">지원 정보 보기</span><span class="sxs-lookup"><span data-stu-id="ce6dd-118">View support information</span></span>

<span data-ttu-id="ce6dd-119">관리 되는 응용 프로그램 배포 후에, hello 응용 프로그램에 대 한 hello 지원 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="ce6dd-120">관리 되는 응용 프로그램 블레이드에서 hello hello 지원 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-120">In hello managed application blade, hello support information is listed.</span></span>

![support](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="ce6dd-122">게시자 사용 권한 보기</span><span class="sxs-lookup"><span data-stu-id="ce6dd-122">View publisher permissions</span></span>

<span data-ttu-id="ce6dd-123">응용 프로그램을 관리 하는 hello 공급 업체 tooyour 리소스에 액세스 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="ce6dd-124">이러한 사용 권한은 선택 toosee **권한 부여**합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-124">toosee those permissions, select **Authorizations**.</span></span>

![권한 부여](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="ce6dd-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ce6dd-126">Next steps</span></span>

* <span data-ttu-id="ce6dd-127">Hello 시장에서에서 관리 되는 응용 프로그램을 게시 하는 방법에 대 한 정보를 참조 하십시오. [Azure의에서 관리 응용 프로그램 마켓플레이스](managed-application-author-marketplace.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="ce6dd-128">toopublish 관리 응용 프로그램을 조직에만 사용할 수 있는 toousers 참조 [만들기 및 게시 서비스 카탈로그 관리 되는 응용 프로그램](managed-application-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="ce6dd-129">tooconsume 관리 응용 프로그램을 조직에만 사용할 수 있는 toousers 참조 [서비스 카탈로그 관리 되는 응용 프로그램 소비](managed-application-consumption.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ce6dd-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
