---
title: "aaaMicrosoft Power BI 포함-tooa 데이터 원본 연결"
description: "Power BI 포함, toodata 소스 연결"
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="3035b-103">Tooa 데이터 원본에 연결</span><span class="sxs-lookup"><span data-stu-id="3035b-103">Connect tooa data source</span></span>
<span data-ttu-id="3035b-104">**Power BI Embedded**를 사용하여 사용자 고유의 앱에 보고서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="3035b-105">앱에 Power BI 보고서를 포함 하는 경우 hello 보고서 toohello 내부에서 데이터를 연결 하는 **가져오기** hello 데이터 또는 복사본 **직접 연결** toohello 데이터 소스를 사용 하 여  **DirectQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="3035b-106">다음은 hello를 사용 하 여 차이점 **가져오기** 및 **DirectQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="3035b-107">가져오기</span><span class="sxs-lookup"><span data-stu-id="3035b-107">Import</span></span> | <span data-ttu-id="3035b-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="3035b-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="3035b-109">테이블, 열, *및 데이터* 가져오거나 hello 보고서의 데이터 집합에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="3035b-110">toosee 해당 오류가 발생 했습니다 toohello 기본 데이터 변경, 새로 고침 또는, 완전 하 고 현재 데이터 집합 가져오기 다시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="3035b-111">만 *테이블 및 열* 가져오거나 hello 보고서의 데이터 집합에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="3035b-112">항상 hello 최신 데이터를 볼 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-112">You always view hello most current data.</span></span> |

<span data-ttu-id="3035b-113">Power BI Embedded를 사용하면 클라우드 데이터 원본에서 DirectQuery를 사용할 수 있지만, 현재 온-프레미스 데이터 원본에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="3035b-114">hello 온-프레미스 데이터 게이트웨이 지원 되지 않습니다 Power BI embedded이 이번에.</span><span class="sxs-lookup"><span data-stu-id="3035b-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="3035b-115">즉, DirectQuery를 온-프레미스 데이터 원본과 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="3035b-116">지원되는 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="3035b-116">Supported data sources</span></span>

<span data-ttu-id="3035b-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="3035b-117">**DirectQuery**</span></span>
* <span data-ttu-id="3035b-118">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3035b-118">Azure SQL database</span></span>
* <span data-ttu-id="3035b-119">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="3035b-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="3035b-120">**가져오기**</span><span class="sxs-lookup"><span data-stu-id="3035b-120">**Import**</span></span>

<span data-ttu-id="3035b-121">모든 Power BI Desktop 내에서 사용 가능한 데이터 원본 hello 사용 하 여 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="3035b-122">**하지** 수 toorefresh 내 Power BI 포함 해당 데이터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="3035b-123">Tooupload 변경 해야 tooyour PBIX 파일 tooPower BI 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="3035b-124">사용 가능한 게이트웨이 toono 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="3035b-125">DirectQuery 사용할 경우의 이점</span><span class="sxs-lookup"><span data-stu-id="3035b-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="3035b-126">**DirectQuery**를 사용할 경우 다음 두 가지 주요 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="3035b-127">**DirectQuery** 작성할 수 있습니다 시각화 여기서 그렇지 않은 경우는 것이 실행할 수 없는 toofirst 가져오기 매우 큰 데이터 집합을 통해 모든 데이터 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="3035b-128">기본 데이터를 변경 하면 데이터 새로 고침 필요할 수 있습니다 하며 일부 보고서에 대 한 hello 필요 toodisplay 현재 데이터 수 대량 데이터 전송에 있으므로 데이터 다시 가져오기를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="3035b-129">반면, **DirectQuery** 보고서는 항상 현재 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="3035b-130">DirectQuery의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="3035b-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="3035b-131">몇 가지 제한 사항이 toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="3035b-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="3035b-132">모든 테이블을 단일 데이터베이스에서 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="3035b-133">Hello 쿼리가 지나치게 복잡 한 경우 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="3035b-134">tooremedy hello 오류는 덜 복잡 하므로 hello 쿼리를 리팩터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="3035b-135">사용 하지 않고 tooimport hello 데이터 할 hello 쿼리 해야 복잡할 경우 **DirectQuery**합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="3035b-136">관계 필터링은 양방향이 아닌 단일 방향 tooa 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="3035b-137">Hello 데이터 형식의 열을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="3035b-138">기본적으로 제한은 측정값에 허용되는 DAX 식에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="3035b-139">[DirectQuery 및 측정값](#measures)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3035b-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="3035b-140">DirectQuery 및 측정값</span><span class="sxs-lookup"><span data-stu-id="3035b-140">DirectQuery and measures</span></span>
<span data-ttu-id="3035b-141">기본 데이터 원본의 toohello 전송 tooensure 쿼리의 성능이 적절 한지, 측정값에 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="3035b-142">사용 하는 경우 **Power BI Desktop**, 고급 사용자가 선택할 수 toobypass이이 제한을 선택 하 여 **파일 > 옵션 및 설정 > 옵션**합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="3035b-143">Hello에 **옵션** 대화 상자에서 선택 **DirectQuery**, hello 옵션을 선택 하 고 **DirectQuery 모드에서 제한 되지 않은 측정값 허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="3035b-144">이 옵션을 선택하면 측정값에 유효한 모든 DAX 식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="3035b-145">사용자가 알고; 있어야 합니다. 그러나 쿼리가 매우 느려질 toohello 백 엔드 발생할 수 있습니다는 일부 식은 하는 때 매우 잘 수행 hello 데이터를 가져올 때 원본 **DirectQuery** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="3035b-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="3035b-146">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3035b-146">See Also</span></span>
* [<span data-ttu-id="3035b-147">Microsoft Power BI Embedded 시작</span><span class="sxs-lookup"><span data-stu-id="3035b-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="3035b-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3035b-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="3035b-149">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="3035b-149">More questions?</span></span> [<span data-ttu-id="3035b-150">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3035b-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

