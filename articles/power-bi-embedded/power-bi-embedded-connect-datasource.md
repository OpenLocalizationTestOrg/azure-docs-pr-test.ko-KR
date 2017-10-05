---
title: "Microsoft Power BI Embedded - 데이터 원본에 연결"
description: "Power BI Embedded, 데이터 원본에 연결"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="f9bcd-103">데이터 원본에 연결</span><span class="sxs-lookup"><span data-stu-id="f9bcd-103">Connect to a data source</span></span>
<span data-ttu-id="f9bcd-104">**Power BI Embedded**를 사용하여 사용자 고유의 앱에 보고서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="f9bcd-105">Power BI 보고서를 앱에 포함하면 데이터의 복사본을 **가져오거나** **DirectQuery**를 통해 데이터 원본에 **직접 연결**하여 기본 데이터에 보고서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="f9bcd-106">**가져오기**와 **DirectQuery** 사용 간의 차이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="f9bcd-107">가져오기</span><span class="sxs-lookup"><span data-stu-id="f9bcd-107">Import</span></span> | <span data-ttu-id="f9bcd-108">직접 연결</span><span class="sxs-lookup"><span data-stu-id="f9bcd-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="f9bcd-109">테이블, 열 *및 데이터* 를 보고서의 데이터 집합으로 가져오거나 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="f9bcd-110">기본 데이터에서 발생한 변경 내용을 보려면 현재 데이터 집합을 다시 새로 고치거나 가져오거나 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="f9bcd-111">*테이블 및 열* 만 보고서의 데이터 집합으로 가져오거나 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="f9bcd-112">항상 최신 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-112">You always view the most current data.</span></span> |

<span data-ttu-id="f9bcd-113">Power BI Embedded를 사용하면 클라우드 데이터 원본에서 DirectQuery를 사용할 수 있지만, 현재 온-프레미스 데이터 원본에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="f9bcd-114">현재 온-프레미스 데이터 게이트웨이는 Power BI embedded와 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="f9bcd-115">즉, DirectQuery를 온-프레미스 데이터 원본과 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="f9bcd-116">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="f9bcd-116">Supported data sources</span></span>

<span data-ttu-id="f9bcd-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="f9bcd-117">**DirectQuery**</span></span>
* <span data-ttu-id="f9bcd-118">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="f9bcd-118">Azure SQL database</span></span>
* <span data-ttu-id="f9bcd-119">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="f9bcd-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="f9bcd-120">**가져오기**</span><span class="sxs-lookup"><span data-stu-id="f9bcd-120">**Import**</span></span>

<span data-ttu-id="f9bcd-121">Power BI Desktop 내에서 모든 사용 가능한 데이터 원본을 사용하여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="f9bcd-122">Power BI Embedded 내의 데이터는 새로 고칠 수 **없습니다**.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="f9bcd-123">Power BI embedded에 대한 PBIX 파일에 변경 내용을 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="f9bcd-124">이는 사용 가능한 게이트웨이가 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="f9bcd-125">DirectQuery 사용할 경우의 이점</span><span class="sxs-lookup"><span data-stu-id="f9bcd-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="f9bcd-126">**DirectQuery**를 사용할 경우 다음 두 가지 주요 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="f9bcd-127">**DirectQuery**를 사용하면 대규모 데이터 집합에서 시각화를 빌드할 수 있습니다. 그렇지 않으면 먼저 모든 데이터를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="f9bcd-128">기본 데이터 변경에는 데이터 새로 고침이 필요할 수 있으며, 일부 보고서의 경우 현재 데이터를 표시하려면 대용량 데이터 전송이 필요할 수 있습니다. 이 경우 데이터를 다시 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="f9bcd-129">반면, **DirectQuery** 보고서는 항상 현재 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="f9bcd-130">DirectQuery의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="f9bcd-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="f9bcd-131">**DirectQuery**사용에 대한 몇 가지 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="f9bcd-132">모든 테이블을 단일 데이터베이스에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="f9bcd-133">쿼리가 지나치게 복잡한 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="f9bcd-134">이 오류를 해결하려면 복잡하지 않도록 쿼리를 리팩터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="f9bcd-135">쿼리가 복잡한 경우 **DirectQuery**를 사용하는 대신 데이터를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="f9bcd-136">관계 필터링은 양방향이 아니라 단방향으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="f9bcd-137">열의 데이터 형식을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="f9bcd-138">기본적으로 제한은 측정값에 허용되는 DAX 식에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="f9bcd-139">[DirectQuery 및 측정값](#measures)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="f9bcd-140">DirectQuery 및 측정값</span><span class="sxs-lookup"><span data-stu-id="f9bcd-140">DirectQuery and measures</span></span>
<span data-ttu-id="f9bcd-141">기본 데이터 원본으로 전송되는 쿼리가 허용되는 성능을 유지하도록 하기 위해 측정값에 대한 제한 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="f9bcd-142">**Power BI Desktop**을 사용할 때 고급 사용자는 **파일 > 옵션 및 설정 > 옵션**을 선택하여 이 제한 사항을 무시하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="f9bcd-143">**옵션** 대화 상자에서 **DirectQuery**를 선택한 다음 **DirectQuery 모드에서 무제한 측정값 허용** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="f9bcd-144">이 옵션을 선택하면 측정값에 유효한 모든 DAX 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="f9bcd-145">그러나 데이터를 가져올 때 성능이 뛰어난 일부 식이 **DirectQuery** 모드에서는 백 엔드 원본에 대한 쿼리 속도가 매우 느려질 수 있음을 사용자가 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="f9bcd-146">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f9bcd-146">See Also</span></span>
* [<span data-ttu-id="f9bcd-147">Microsoft Power BI Embedded 시작</span><span class="sxs-lookup"><span data-stu-id="f9bcd-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="f9bcd-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="f9bcd-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="f9bcd-149">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="f9bcd-149">More questions?</span></span> [<span data-ttu-id="f9bcd-150">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="f9bcd-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

