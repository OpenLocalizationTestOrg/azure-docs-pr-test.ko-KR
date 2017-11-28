---
title: "Power BI embedded aaaRow 수준 보안"
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
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="03186-103">Power BI Embedded를 사용하는 행 수준 보안</span><span class="sxs-lookup"><span data-stu-id="03186-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="03186-104">행 수준 보안 (RLS)은 보고서 또는 수 있게 해 주는 여러 개의 서로 다른 사용자가 toouse hello 서로 다른 데이터를 보는 모든 동안 동일한 보고서 데이터 집합 내에서 사용 되는 toorestrict 사용자 액세스 tooparticular 데이터 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="03186-105">이제 Power BI Embedded에서 RLS로 구성된 데이터 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="03186-106">Rls 순서 tootake 혜택에은에서 세 가지 주요 개념인; 이해 사용자, 역할 및 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="03186-107">이러한 개념 각각에 대해 조금 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="03186-108">**사용자가** –이 hello 실제 최종 사용자가 보고서 보기.</span><span class="sxs-lookup"><span data-stu-id="03186-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="03186-109">Power BI 포함에서 사용자가 응용 프로그램 토큰에 hello username 속성으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03186-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="03186-110">**역할** – 사용자가 속한 tooroles 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="03186-111">역할은 규칙에 대한 컨테이너로, "Sales Manager" 또는 "Sales Rep"와 같이 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="03186-112">Power BI 포함에서 사용자 앱 토큰에서 역할 속성 hello로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03186-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="03186-113">**규칙** – 역할이 규칙 및 이러한 규칙은 적용 toobe toohello 데이터가는 hello 실제 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="03186-114">"Country = USA"처럼 간단하거나 훨씬 동적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="03186-115">예제</span><span class="sxs-lookup"><span data-stu-id="03186-115">Example</span></span>

<span data-ttu-id="03186-116">이 문서의 나머지 부분을 hello에 대 한 RLS를 작성 하 고 다음 포함 된 응용 프로그램 내에서 사용 하는 하의 예로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03186-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="03186-117">예제 hello를 사용 하 여 [소매 분석 샘플](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="03186-118">소매점 분석 샘플에서는 특정 소매점 체인에 모든 hello 상점의 판매를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03186-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="03186-119">RLS를 없이 어느 구역에 관계 없이 관리자가 로그인 하 고 뷰 hello 보고서를 볼 수 있습니다 hello 같은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="03186-120">경영 구역 관리자 각 판매 행만 볼 hello 관리 하는 hello 상점과 toodo에 대 한이 결정, RLS를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="03186-121">RLS는 Power BI Desktop으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="03186-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="03186-122">Hello 데이터 집합 및 보고서를 열 때 toodiagram toosee hello 스키마 보기를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="03186-123">다음은이 스키마와 함께 몇 가지 toonotice가입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="03186-124">모든 측정값 같은 **총 판매액**, hello에 저장 된 **Sales** 팩트 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="03186-125">**Item**, **Time**, **Store** 및 **District**의 추가 관련 차원 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="03186-126">hello 관계선에 hello 화살표 어떤 방식으로 필터는 한 테이블 tooanother에서 흐를 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03186-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="03186-127">예를 들어, 필터에 배치 되 면 **시간 [Date]**, hello 현재 스키마에서 값 hello에 이르기까지 필터링만 것 **Sales** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="03186-128">다른 테이블이 없습니다 hello 관계 선 지점 toohello 판매 테이블에서를 제거 하지 hello 화살표의 모든 이후이 필터에 의해 영향을 받을 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="03186-129">hello **구역** 테이블 각 지역에 대해 hello 관리자에 게 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="03186-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="03186-130">필터 toohello 적용이 스키마에 따라 **구역 관리자** 열에 hello 구역 테이블 및 해당 필터는 hello 다운도 필터링 하 고 해당 필터에서 일치 하는 hello 사용자 hello 보고서를 보는 경우 **저장소**및 **Sales** 테이블 tooonly 관리자는 특정 지역에 대 한 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="03186-131">방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-131">Here’s how:</span></span>

1. <span data-ttu-id="03186-132">Hello 모델링 탭을 클릭 **역할 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="03186-133">**관리자**라는 새 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03186-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="03186-134">Hello에 **구역** 테이블에 다음 DAX 식은 hello 입력: **[구역 관리자] username () =**</span><span class="sxs-lookup"><span data-stu-id="03186-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="03186-135">hello에 toomake 있는지 hello 규칙에서 작업 하는 **모델링** 탭을 클릭 **역할로 보기**, hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="03186-136">hello 보고서는 이제 표시로 로그인 한 경우 처럼 **Andrew Ma**합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="03186-137">모든 레코드 hello에 이르기까지 필터링 됩니다 hello 필터, 여기에 수행한 hello 방식으로 적용 **구역**, **저장소**, 및 **Sales** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="03186-138">그러나 간의 hello 관계에 대 한 hello 필터 방향 인해 **Sales** 및 **시간**, **Sales** 및 **항목**, 및 **항목** 및 **시간** 테이블 아래로 필터링 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="03186-139">그러나이 요구 사항을 확인 될 수 있는, 않아도 판매 관리자 toosee 항목을 않도록 하는 경우 수 설정 양방향 교차 필터링 양방향에서 hello 관계 및 흐름 hello 보안 필터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="03186-140">Hello 관계를 편집 하 여이 작업을 수행할 수 있습니다 **Sales** 및 **항목**, 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="03186-141">이제 필터 진행 될 수도 있다는 hello Sales 테이블 toohello에서 **항목** 테이블:</span><span class="sxs-lookup"><span data-stu-id="03186-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="03186-142">DirectQuery 모드에 대 한 데이터를 사용 하는 경우 양방향 교차 필터링이 두 가지 옵션을 선택 하 여 tooenable 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="03186-143">**파일** -> **옵션 및 설정** -> **미리 보기 기능** -> **DirectQuery에 대해 양방향 교차 필터링 활성화**.</span><span class="sxs-lookup"><span data-stu-id="03186-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="03186-144">**파일** -> **옵션 및 설정** -> **DirectQuery** -> **DirectQuery 모드에서 무제한 측정값 허용**.</span><span class="sxs-lookup"><span data-stu-id="03186-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="03186-145">양방향 교차 필터링, 다운로드 hello에 대 한 자세한 toolearn [양방향 교차 필터링 SQL Server Analysis Services 2016 및 Power BI Desktop에서](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) 백서입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="03186-146">이것으로 toobe Power BI Desktop에서 수행 해야 하는 모든 hello 작업 마치 겠습니다 이지만 하나 더 많은 작업을 수행 하는 toobe toomake 필요한 hello RLS 규칙에서 Power BI 포함 작업을 정의 했습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="03186-147">응용 프로그램 토큰은 사용 되는 toogrant 및 사용자를 인증 하 고 응용 프로그램의 승인을 해당 사용자 액세스 tooa 특정 Power BI 포함 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="03186-148">Power BI Embedded는 사용자가 누구인지에 대한 어떠한 특정한 정보도 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="03186-149">RLS toowork에 대 한 응용 프로그램 토큰의 일부로 toopass에 일부 추가 컨텍스트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="03186-150">**사용자 이름** (선택 사항) –이 사용할 수 있는 문자열로 RLS로 사용 되는 RLS 규칙을 적용할 때 toohelp hello 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="03186-151">Power BI Embedded를 사용하는 행 수준 보안 사용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03186-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="03186-152">**역할** – 행 수준 보안 규칙을 적용할 때 hello 역할 tooselect를 포함 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="03186-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="03186-153">둘 이상의 역할을 전달하는 경우 문자열 배열로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="03186-154">Hello를 사용 하 여 hello 토큰을 만들면 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) 메서드.</span><span class="sxs-lookup"><span data-stu-id="03186-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="03186-155">Hello 사용자 이름 속성이 있으면 역할에 하나 이상의 값을 전달할 수도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="03186-156">예를 들어 hello EmbedSample 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="03186-157">DashboardController 줄 55는 다음과 같이 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03186-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="03186-158">to</span><span class="sxs-lookup"><span data-stu-id="03186-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="03186-159">hello 전체 응용 프로그램 토큰에는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03186-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="03186-160">이제 모든 hello 조각을 함께와이 보고서는 응용 프로그램 tooview에는 사용자 로그인 할 때만 할 것 수 toosee hello 데이터 toosee, 허용 되는 행 수준 보안에 정의 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="03186-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="03186-161">참고 항목</span><span class="sxs-lookup"><span data-stu-id="03186-161">See also</span></span>

[<span data-ttu-id="03186-162">Power를 사용하는 RLS(행 수준 보안)</span><span class="sxs-lookup"><span data-stu-id="03186-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="03186-163">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="03186-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="03186-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="03186-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="03186-165">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="03186-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="03186-166">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="03186-166">More questions?</span></span> [<span data-ttu-id="03186-167">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="03186-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

