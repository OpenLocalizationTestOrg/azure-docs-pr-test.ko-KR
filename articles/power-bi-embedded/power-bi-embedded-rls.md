---
title: "Power BI Embedded를 사용하는 행 수준 보안"
description: "Power BI Embedded를 사용하는 행 수준 보안에 대한 자세한 내용"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="c5ed2-103">Power BI Embedded를 사용하는 행 수준 보안</span><span class="sxs-lookup"><span data-stu-id="c5ed2-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="c5ed2-104">보고서 또는 데이터 집합 내의 특정 데이터에 대한 사용자 액세스를 제한하는 데 RLS(행 수준 보안)를 사용하여 여러 다양한 사용자가 모두 서로 다른 데이터를 보면서 동일한 보고서를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="c5ed2-105">이제 Power BI Embedded에서 RLS로 구성된 데이터 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="c5ed2-106">RLS를 활용하기 위해서는 사용자, 역할 및 규칙이라는 세 가지 주요 개념을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="c5ed2-107">이러한 개념 각각에 대해 조금 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="c5ed2-108">**사용자** - 보고서를 보는 실제 최종 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="c5ed2-109">Power BI Embedded에서 사용자는 앱 토큰의 사용자 이름 속성으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="c5ed2-110">**역할** - 사용자는 역할에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="c5ed2-111">역할은 규칙에 대한 컨테이너로, "Sales Manager" 또는 "Sales Rep"와 같이 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="c5ed2-112">Power BI Embedded에서 사용자는 앱 토큰의 역할 속성으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="c5ed2-113">**규칙** – 역할에는 규칙이 있고 해당 규칙은 데이터에 적용할 실제 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="c5ed2-114">"Country = USA"처럼 간단하거나 훨씬 동적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="c5ed2-115">예</span><span class="sxs-lookup"><span data-stu-id="c5ed2-115">Example</span></span>

<span data-ttu-id="c5ed2-116">이 문서의 나머지 부분에서는 RLS를 작성하는 예를 제공한 후 포함된 응용 프로그램 내에서 이를 사용하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="c5ed2-117">이 예에서는 [소매 분석 샘플](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="c5ed2-118">소매 분석 샘플은 특정 소매 체인에 속하는 모든 상점에 대한 판매를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="c5ed2-119">RLS가 없다면 어떤 지역 관리자가 로그인하여 보고서를 보든지 동일한 데이터를 보게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="c5ed2-120">고위 경영진은 각 지역 관리자가 자신이 관리하는 상점에 대한 판매만 보도록 결정했으며 이를 위해 RLS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="c5ed2-121">RLS는 Power BI Desktop으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="c5ed2-122">데이터 집합 및 보고서가 열리면 다이어그램 보기로 전환하여 스키마를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="c5ed2-123">이 스키마로 알 수 있는 몇 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="c5ed2-124">**Total Sales**와 같은 모든 측정값은 **Sales** 팩트 테이블에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="c5ed2-125">**Item**, **Time**, **Store** 및 **District**의 추가 관련 차원 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="c5ed2-126">관계선의 화살표는 테이블 간에 필터가 흐를 수 있는 방향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="c5ed2-127">예를 들어, 필터가 **Time[Date]**에 배치되면 현재 스키마에서 **Sales** 테이블의 값만 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="c5ed2-128">관계선에서 모든 화살표가 sales 테이블만 가리키므로 이 필터에 다른 테이블은 영향을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="c5ed2-129">**District** 테이블은 각 지역에 대한 관리자가 누구인지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="c5ed2-130">이 스키마에 따라 District 테이블의 **District Manager** 열에 필터를 적용하는 경우, 해당 필터가 보고서를 보는 사용자와 일치하는 경우 이 필터는 **Store** 및 **Sales** 테이블을 필터링하여 특정 지역 관리자에 대한 데이터만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="c5ed2-131">방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-131">Here’s how:</span></span>

1. <span data-ttu-id="c5ed2-132">모델링 탭에서 **역할 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="c5ed2-133">**관리자**라는 새 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="c5ed2-134">**District** 테이블에서 다음 DAX 식을 입력합니다. **[District Manager] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="c5ed2-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="c5ed2-135">규칙이 작동하는지 확인하려면 **모델링** 탭에서 **역할로 보기**를 클릭한 후 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="c5ed2-136">이제 보고서는 **Andrew Ma**로 로그인한 것처럼 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="c5ed2-137">여기서 수행한 방향으로 필터를 적용하면 **District**, **Store** 및 **Sales** 테이블의 모든 레코드가 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="c5ed2-138">그러나 **Sales** 및 **Time**, **Sales** 및 **Item** 간의 관계에서 필터 방향으로 인해 **Item** 및 **Time** 테이블은 필터링되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="c5ed2-139">이 요구 사항의 경우 문제가 되지 않지만 관리자가 판매 항목이 없는 항목을 보고 싶어하지 않는 경우 관계에 대해 양방향 교차 필터링을 설정할 수 있으며 보안 필터가 두 방향으로 흐를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="c5ed2-140">이 작업은 다음과 같이 **Sales** 및 **Item** 간의 관계를 편집하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="c5ed2-141">이제 필터는 Sales 테이블에서 **Item** 테이블로도 흐를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="c5ed2-142">데이터에 대해 DirectQuery 모드를 사용 중인 경우 다음 두 옵션을 선택하여 양방향 교차 필터링을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="c5ed2-143">**파일** -> **옵션 및 설정** -> **미리 보기 기능** -> **DirectQuery에 대해 양방향 교차 필터링 활성화**.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="c5ed2-144">**파일** -> **옵션 및 설정** -> **DirectQuery** -> **DirectQuery 모드에서 무제한 측정값 허용**.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="c5ed2-145">양방향 교차 필터링에 대해 알아보려면 [SQL Server Analysis Services 2016 및 Power BI Desktop에서 양방향 교차 필터링](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) 백서를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="c5ed2-146">그러면 Power BI Desktop에서 수행해야 할 모든 작업이 마무리되지만 Power BI Embedded에서 작업을 정의한 RLS 규칙을 만들기 위해 몇 가지 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="c5ed2-147">응용 프로그램에서 사용자가 인증 및 권한 부여되고 특정 Power BI Embedded 보고서에 사용자 액세스를 부여하는 데 앱 토큰이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="c5ed2-148">Power BI Embedded는 사용자가 누구인지에 대한 어떠한 특정한 정보도 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="c5ed2-149">RLS가 작동하기 위해서는 앱 토큰의 일부로 추가 컨텍스트를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="c5ed2-150">**username** (선택 사항) – RLS에 사용되며 RLS 규칙을 적용할 때 사용자를 식별하는 데 사용할 수 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="c5ed2-151">Power BI Embedded를 사용하는 행 수준 보안 사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="c5ed2-152">**역할** – 행 수준 보안 규칙을 적용할 때 선택할 역할이 들어 있는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="c5ed2-153">둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="c5ed2-154">[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) 메서드를 사용하여 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="c5ed2-155">사용자 이름 속성이 있으면 역할에 하나 이상의 값을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="c5ed2-156">예를 들어 EmbedSample을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="c5ed2-157">DashboardController 줄 55는 다음과 같이 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="c5ed2-158">to</span><span class="sxs-lookup"><span data-stu-id="c5ed2-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="c5ed2-159">전체 앱 토큰은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-159">The full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="c5ed2-160">이제 종합해보면 누군가가 이 보고서를 보기 위해 응용 프로그램에 로그인하면 행 수준 보안에 정의된 대로 자신에게 보기가 허용된 데이터만 볼 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="c5ed2-161">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c5ed2-161">See also</span></span>

[<span data-ttu-id="c5ed2-162">Power를 사용하는 RLS(행 수준 보안)</span><span class="sxs-lookup"><span data-stu-id="c5ed2-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="c5ed2-163">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="c5ed2-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="c5ed2-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c5ed2-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="c5ed2-165">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="c5ed2-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="c5ed2-166">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="c5ed2-166">More questions?</span></span> [<span data-ttu-id="c5ed2-167">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="c5ed2-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)

