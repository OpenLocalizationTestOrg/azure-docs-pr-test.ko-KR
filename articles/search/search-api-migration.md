---
title: "Azure Search 서비스 REST API 버전 2016-09-01로 업그레이드 | Microsoft Docs"
description: "Azure Search 서비스 REST API 버전 2016-09-01로 업그레이드"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="f9801-103">Azure Search 서비스 REST API 버전 2016-09-01로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="f9801-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="f9801-104">[Azure Search 서비스 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx)의 2015-02-28 또는 2015-02-28-Preview 버전을 사용하는 경우 이 문서를 통해 일반적으로 다음 API 버전인 2016-09-01을 사용하기 위해 응용 프로그램을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="f9801-105">REST API의 2016-09-01 버전에는 이전 버전에서 변경된 몇 가가지 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="f9801-106">이는 대부분 이전 버전과 호환되기 때문에 이전에 사용하던 버전에 따라 간단히 코드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="f9801-107">새 API 버전을 사용하는 코드를 변경하는 방법에 대한 지침은 [업그레이드 단계](#UpgradeSteps) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9801-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="f9801-108">Azure Search 서비스 인스턴스는 최신 버전을 포함한 여러 REST API 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="f9801-109">더 이상 최신 버전이 아닌 버전을 계속 사용할 수는 있지만 코드를 마이그레이션하여 최신 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="f9801-110">2016-09-01 버전의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f9801-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="f9801-111">2016-09-01 버전은 Azure Search 서비스 REST API의 두 번째 일반 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="f9801-112">이 API 버전의 새로운 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-112">New features in this API version include:</span></span>

* <span data-ttu-id="f9801-113">[사용자 지정 분석기](https://aka.ms/customanalyzers)를 사용하여 텍스트를 인덱싱 가능하고 검색 가능한 토큰으로 변환하는 프로세스를 제어할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="f9801-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="f9801-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) 및 [Azure Table Storage](search-howto-indexing-azure-tables.md) 인덱서를 사용하여 일정에 따라 또는 요청 시 Azure 저장소에서 Azure Search로 데이터를 쉽게 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="f9801-115">[필드 매핑](search-indexer-field-mappings.md)을 사용하여 인덱서가 Azure Search로 데이터를 가져오는 방법을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="f9801-116">ETag를 사용하여 동시에 안전하게 인덱스, 인덱서 및 데이터 원본의 정의를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="f9801-117">업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="f9801-117">Steps to upgrade</span></span>
<span data-ttu-id="f9801-118">2015-02-28 버전에서 업그레이드하는 경우 버전 번호를 제외하고 코드를 변경하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="f9801-119">코드를 변경해야 하는 유일한 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="f9801-120">인식할 수 없는 속성이 API 응답에 반환되는 경우 코드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="f9801-121">기본적으로 응용 프로그램은 이해하지 못하는 속성을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="f9801-122">코드는 API 요청을 보관하고 새 API 버전으로 다시 전송하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="f9801-123">예를 들어 응용 프로그램이 검색 API에서 반환된 연속 토큰을 보관하는 경우 이런 현상이 발생할 수 있습니다(자세한 내용은 [검색 API 참조](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)의 `@search.nextPageParameters`를 참조).</span><span class="sxs-lookup"><span data-stu-id="f9801-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="f9801-124">이러한 경우에 해당하는 경우 코드를 적절하게 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="f9801-125">2016-09-01 버전의 [새로운 기능](#WhatsNew)을 사용하여 시작하지 않으면 코드를 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="f9801-126">2015-02-28-Preview 버전에서 업그레이드하는 경우, 위 내용이 적용되지만 일부 미리 보기 기능은 2016-09-01 버전에서 사용할 수 없다는 점을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="f9801-127">Azure Blob Storage 인덱서는 CSV 파일과 JSON 배열을 포함하는 Blob을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="f9801-128">동의어</span><span class="sxs-lookup"><span data-stu-id="f9801-128">Synonyms</span></span>
* <span data-ttu-id="f9801-129">"이보다 더 나은" 쿼리</span><span class="sxs-lookup"><span data-stu-id="f9801-129">"More like this" queries</span></span>

<span data-ttu-id="f9801-130">코드가 이러한 기능을 사용하는 경우 기능을 사용하지 않고는 2016-09-01로 업그레이드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9801-131">미리 보기 API는 테스트 및 평가 용도로 제공되며 프로덕션 환경에는 사용되지 않는다는 점을 유념하세요.</span><span class="sxs-lookup"><span data-stu-id="f9801-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="f9801-132">결론</span><span class="sxs-lookup"><span data-stu-id="f9801-132">Conclusion</span></span>
<span data-ttu-id="f9801-133">Azure Search 서비스 REST API 사용에 대한 자세한 정보가 필요한 경우 MSDN의 최근에 업데이트된 [API 참조](https://msdn.microsoft.com/library/azure/dn798935.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9801-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="f9801-134">Azure Search에 대한 귀하의 피드백을 환영합니다.</span><span class="sxs-lookup"><span data-stu-id="f9801-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="f9801-135">문제가 발생하면 [Azure Search MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) 또는 [StackOverflow](http://stackoverflow.com/)를 통해 자유롭게 도움을 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="f9801-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="f9801-136">StackOverflow에서 Azure Search에 대한 질문이 있는 경우, `azure-search`를 사용하여 태그하세요.</span><span class="sxs-lookup"><span data-stu-id="f9801-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="f9801-137">Azure 검색을 이용해 주셔서 감사합니다!</span><span class="sxs-lookup"><span data-stu-id="f9801-137">Thank you for using Azure Search!</span></span>

