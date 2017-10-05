---
title: "Log Analytics 로그 검색의 컴퓨터 그룹 | Microsoft Docs"
description: "Log Analytics의 컴퓨터 그룹을 사용하여 로그 검색 범위를 특정 컴퓨터 집합으로 한정할 수 있습니다.  이 문서에서는 컴퓨터 그룹을 만드는 데 사용할 수 있는 몇 가지 방법과 로그 검색에서의 사용 방법을 설명합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: a2ddc932343d54963a378ee27dc962a790326b2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a><span data-ttu-id="84b5f-104">Log Analytics 로그 검색의 컴퓨터 그룹 </span><span class="sxs-lookup"><span data-stu-id="84b5f-104">Computer groups in Log Analytics log searches</span></span>

>[!NOTE]
> <span data-ttu-id="84b5f-105">이 문서에서는 최신 Log Analytics 쿼리 언어를 사용하는 컴퓨터 그룹 사용 방식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-105">This article describes the use of Computer Groups using the current Log Anayltics query language.</span></span>    <span data-ttu-id="84b5f-106">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 컴퓨터 그룹이 다른 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then Computer Groups work differently.</span></span>  <span data-ttu-id="84b5f-107">이 문서에서는 새 쿼리 언어에서 달라진 구문과 동작에 대해 참고 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-107">Notes are provided in this article with the different syntax and behavior for the new query language.</span></span>  


<span data-ttu-id="84b5f-108">Log Analytics의 컴퓨터 그룹을 사용하여 [로그 검색](log-analytics-log-searches.md) 범위를 특정 컴퓨터 집합으로 한정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-108">Computer groups in Log Analytics allow you to scope [log searches](log-analytics-log-searches.md) to a particular set of computers.</span></span>  <span data-ttu-id="84b5f-109">각 그룹에는 사용자가 정의를 사용하거나 여러 원본에서 그룹을 가져와 컴퓨터가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-109">Each group is populated with computers either using a query that you define or by importing groups from different sources.</span></span>  <span data-ttu-id="84b5f-110">그룹이 로그 검색에 포함된 경우 결과는 그룹의 컴퓨터에 일치하는 레코드로 한정됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-110">When the group is included in a log search, the results are limited to records that match the computers in the group.</span></span>

## <a name="creating-a-computer-group"></a><span data-ttu-id="84b5f-111">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="84b5f-111">Creating a computer group</span></span>
<span data-ttu-id="84b5f-112">Log Analytics에서 다음 표의 방법 중 하나를 통해 컴퓨터 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-112">You can create a computer group in Log Analytics using any of the methods in the following table.</span></span>  <span data-ttu-id="84b5f-113">각 방법에 대한 자세한 내용은 아래 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-113">Details on each method are provided in the sections below.</span></span> 

| <span data-ttu-id="84b5f-114">메서드</span><span class="sxs-lookup"><span data-stu-id="84b5f-114">Method</span></span> | <span data-ttu-id="84b5f-115">설명</span><span class="sxs-lookup"><span data-stu-id="84b5f-115">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="84b5f-116">로그 검색</span><span class="sxs-lookup"><span data-stu-id="84b5f-116">Log search</span></span> |<span data-ttu-id="84b5f-117">컴퓨터 목록을 반환하는 로그 검색을 만들고 결과를 컴퓨터 그룹으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-117">Create a log search that returns a list of computers and save the results as a computer group.</span></span> |
| <span data-ttu-id="84b5f-118">로그 검색 API</span><span class="sxs-lookup"><span data-stu-id="84b5f-118">Log Search API</span></span> |<span data-ttu-id="84b5f-119">로그 검색 API를 사용하여 프로그래밍 방식으로 로그 검색 결과에 따라 컴퓨터 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-119">Use the Log Search API to programmatically create a computer group based on the results of a log search.</span></span> |
| <span data-ttu-id="84b5f-120">Active Directory</span><span class="sxs-lookup"><span data-stu-id="84b5f-120">Active Directory</span></span> |<span data-ttu-id="84b5f-121">Active Directory 도메인의 구성원인 에이전트 컴퓨터의 그룹 구성원을 자동으로 검색하고 각 보안 그룹에 대해 Log Analytics에 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-121">Automatically scan the group membership of any agent computers that are members of an Active Directory domain and create a group in Log Analytics for each security group.</span></span> |
| <span data-ttu-id="84b5f-122">WSUS</span><span class="sxs-lookup"><span data-stu-id="84b5f-122">WSUS</span></span> |<span data-ttu-id="84b5f-123">대상 그룹에 대해 자동으로 WSUS 서버나 클라이언트를 검색하고 각각에 대해 Log Analytics에 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-123">Automatically scan WSUS servers or clients for targeting groups and create a group in Log Analytics for each.</span></span> |

### <a name="log-search"></a><span data-ttu-id="84b5f-124">로그 검색</span><span class="sxs-lookup"><span data-stu-id="84b5f-124">Log search</span></span>
<span data-ttu-id="84b5f-125">로그 검색으로부터 만든 컴퓨터 그룹은 사용자가 정의한 검색 쿼리가 반환한 모든 컴퓨터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-125">Computer groups created from a Log Search contain all of the computers returned by a search query that you define.</span></span>  <span data-ttu-id="84b5f-126">이 쿼리는 컴퓨터 그룹이 사용될 때마다 실행되므로 그룹이 만들어진 이후의 모든 변경 내용이 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-126">This query is run every time the computer group is used so that any changes since the group was created is reflected.</span></span>

<span data-ttu-id="84b5f-127">다음 절차를 통해 로그 검색에서 컴퓨터 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-127">Use the following procedure to create a computer group from a log search.</span></span>

1. <span data-ttu-id="84b5f-128">컴퓨터 목록을 반환하는 [로그 검색 만듭니다](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="84b5f-128">[Create a log search](log-analytics-log-searches.md) that returns a list of computers.</span></span>  <span data-ttu-id="84b5f-129">이 검색은 쿼리에서 **Distinct Computer** 또는 **measure count() by Computer** 등과 같은 항목을 사용하여 컴퓨터의 개별 집합을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-129">The search must return a distinct set of computers by using something like **Distinct Computer** or **measure count() by Computer** in the query.</span></span>  
2. <span data-ttu-id="84b5f-130">화면 위쪽에 있는 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-130">Click the **Save** button at the top of the screen.</span></span>
3. <span data-ttu-id="84b5f-131">**예**를 선택하여 **이 쿼리를 컴퓨터 그룹으로 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-131">Select **Yes** to **Save this query as a computer group**.</span></span>
4. <span data-ttu-id="84b5f-132">그룹의 **이름** 및 **범주**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-132">Type in a **Name** and a **Category** for the group.</span></span>  <span data-ttu-id="84b5f-133">동일한 이름 및 범주를 갖는 검색이 이미 있는 경우 덮어쓴다는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-133">If a search with the same name and category already exists, then you are be prompted to overwrite it.</span></span>  <span data-ttu-id="84b5f-134">다른 카테고리에서는 동일한 이름으로 여러 검색을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-134">You can have multiple searches with the same name in different categories.</span></span> 

<span data-ttu-id="84b5f-135">다음은 컴퓨터 그룹으로 저장할 수 있는 검색의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-135">Following are example searches that you can save as a computer group.</span></span>

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> <span data-ttu-id="84b5f-136">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 새 컴퓨터 그룹을 만드는 절차가 다음과 같이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-136">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md) then the following changes are made to the procedure to create a new computer group.</span></span>
>  
> - <span data-ttu-id="84b5f-137">컴퓨터 그룹을 만드는 쿼리에 `distinct Computer`를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-137">The query to create a computer group must include `distinct Computer`.</span></span>  <span data-ttu-id="84b5f-138">컴퓨터 그룹을 만드는 쿼리의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-138">Following is an example of a query to create a computer group.</span></span><br>`Heartbeat | where Computer contains "srv" `
> - <span data-ttu-id="84b5f-139">새 컴퓨터 그룹을 만들 때는 이름 외에 별칭을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-139">When you create a new computer group, you must specify an alias in addition to the name.</span></span>  <span data-ttu-id="84b5f-140">쿼리에서 컴퓨터 그룹을 사용할 때는 아래 설명에 따라 별칭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-140">You use the alias when using the computer group in a query as described below.</span></span>  

### <a name="log-search-api"></a><span data-ttu-id="84b5f-141">로그 검색 API</span><span class="sxs-lookup"><span data-stu-id="84b5f-141">Log search API</span></span>
<span data-ttu-id="84b5f-142">로그 검색 API를 사용하여 만들어진 컴퓨터 그룹은 로그 검색으로 만든 검색과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-142">Computer groups created with the Log Search API are the same as searches created with a Log Search.</span></span>

<span data-ttu-id="84b5f-143">로그 검색 API를 사용하여 컴퓨터 그룹을 만드는 것에 대한 자세한 내용은 [Log Analytics 로그 검색 REST API의 컴퓨터 그룹](log-analytics-log-search-api.md#computer-groups)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="84b5f-143">For details on creating a computer group using the Log Search API see [Computer Groups in Log Analytics log search REST API](log-analytics-log-search-api.md#computer-groups).</span></span>

### <a name="active-directory"></a><span data-ttu-id="84b5f-144">Active Directory</span><span class="sxs-lookup"><span data-stu-id="84b5f-144">Active Directory</span></span>
<span data-ttu-id="84b5f-145">Active Directory 그룹 멤버 자격을 가져오도록 Log Analytics를 구성하면 OMS 에이전트가 있는 도메인 연결 컴퓨터의 그룹 멤버 자격을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-145">When you configure Log Analytics to import Active Directory group memberships, it analyzes the group membership of any domain joined computers with the OMS agent.</span></span>  <span data-ttu-id="84b5f-146">컴퓨터 그룹은 Log Analytics에서 Active Directory의 각 보안 그룹에 대해 만들어지며 각 컴퓨터는 자신이 속산 보안 그룹에 해당하는 컴퓨터 그룹에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-146">A computer group is created in Log Analytics for each security group in Active Directory, and each computer is added to the computer groups corresponding to the security groups they are members of.</span></span>  <span data-ttu-id="84b5f-147">이 멤버 자격은 4시간 간격으로 계속 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-147">This membership is continuously updated every 4 hours.</span></span>  

<span data-ttu-id="84b5f-148">Log Analytics **설정**의 **컴퓨터 그룹** 메뉴에서 Active Directory 보안 그룹을 가져오도록 Log Analytics를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-148">You configure Log Analytics to import Active Directory security groups from the **Computer Groups** menu in Log Analytics **Settings**.</span></span>  <span data-ttu-id="84b5f-149">**자동화**를 선택한 다음 **컴퓨터에서 Active Directory 그룹 멤버 자격을 가져옵니다**.</span><span class="sxs-lookup"><span data-stu-id="84b5f-149">Select **Automation** and then **Import Active Directory group memberships from computers**.</span></span>  <span data-ttu-id="84b5f-150">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-150">There is no further configuration required.</span></span>

![Active Directory의 컴퓨터 그룹](media/log-analytics-computer-groups/configure-activedirectory.png)

<span data-ttu-id="84b5f-152">그룹을 가져올 때는 검색된 그룹 멤버 자격 및 가져온 그룹 수와 함께 컴퓨터 수가 메뉴에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-152">When groups have been imported, the menu lists the number of computers with group membership detected and the number of groups imported.</span></span>  <span data-ttu-id="84b5f-153">이 링크 중 하나를 클릭하여 **ComputerGroup** 레코드와 이 정보를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-153">You can click on either of these links to return the **ComputerGroup** records with this information.</span></span>

### <a name="windows-server-update-service"></a><span data-ttu-id="84b5f-154">Windows Server 업데이트 서비스</span><span class="sxs-lookup"><span data-stu-id="84b5f-154">Windows Server Update Service</span></span>
<span data-ttu-id="84b5f-155">WSUS 그룹 멤버 자격을 가져오도록 Log Analytics를 구성하면 OMS 에이전트가 있는 컴퓨터의 대상 그룹 멤버 자격을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-155">When you configure Log Analytics to import WSUS group memberships, it analyzes the targeting group membership of any computers with the OMS agent.</span></span>  <span data-ttu-id="84b5f-156">클라이언트 쪽 대상을 사용하는 경우 OMS에 연결되고 WSUS 대상 그룹에 속한 모든 컴퓨터의 그룹 멤버 자격을 Log Analytics로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-156">If you are using client-side targeting, any computer that is connected to OMS and is part of any WSUS targeting groups has its group membership imported to Log Analytics.</span></span> <span data-ttu-id="84b5f-157">서버 쪽을 대상으로 사용하는 경우 그룹 멤버 자격 정보를 OMS로 가져오도록 OMS 에이전트를 WSUS 서버에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-157">If you are using server-side targeting, the OMS agent should be installed on the WSUS server in order for the group membership information to be imported to OMS.</span></span>  <span data-ttu-id="84b5f-158">이 멤버 자격은 4시간 간격으로 계속 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-158">This membership is continuously updated every 4 hours.</span></span> 

<span data-ttu-id="84b5f-159">Log Analytics **설정**의 **컴퓨터 그룹** 메뉴에서 Active Directory 보안 그룹을 가져오도록 Log Analytics를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-159">You configure Log Analytics to import Active Directory security groups from the **Computer Groups** menu in Log Analytics **Settings**.</span></span>  <span data-ttu-id="84b5f-160">**Active Directory**를 선택한 다음 **컴퓨터에서 Active Directory 그룹 멤버 자격을 가져옵니다**.</span><span class="sxs-lookup"><span data-stu-id="84b5f-160">Select **Active Directory** and then **Import Active Directory group memberships from computers**.</span></span>  <span data-ttu-id="84b5f-161">추가 구성은 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-161">There is no further configuration required.</span></span>

![Active Directory의 컴퓨터 그룹](media/log-analytics-computer-groups/configure-wsus.png)

<span data-ttu-id="84b5f-163">그룹을 가져올 때는 검색된 그룹 멤버 자격 및 가져온 그룹 수와 함께 컴퓨터 수가 메뉴에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-163">When groups have been imported, the menu lists the number of computers with group membership detected and the number of groups imported.</span></span>  <span data-ttu-id="84b5f-164">이 링크 중 하나를 클릭하여 **ComputerGroup** 레코드와 이 정보를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-164">You can click on either of these links to return the **ComputerGroup** records with this information.</span></span>

## <a name="managing-computer-groups"></a><span data-ttu-id="84b5f-165">컴퓨터 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="84b5f-165">Managing computer groups</span></span>
<span data-ttu-id="84b5f-166">Log Analytics **설정**의 **컴퓨터 그룹** 메뉴에서 로그 검색 또는 로그 검색 API로부터 생성된 컴퓨터 그룹을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-166">You can view computer groups that were created from a log search or the Log Search API from the **Computer Groups** menu in Log Analytics **Settings**.</span></span>  <span data-ttu-id="84b5f-167">**제거** 열에서 **x**를 클릭하여 컴퓨터 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-167">Click the **x** in the **Remove** column to delete the computer group.</span></span>  <span data-ttu-id="84b5f-168">그룹에 대한 **멤버 보기** 아이콘을 클릭하여 멤버를 반환하는 그룹의 로그 검색을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-168">Click the **View members** icon for a group to run the group's log search that returns its members.</span></span> 

![저장된 컴퓨터 그룹](media/log-analytics-computer-groups/configure-saved.png)

<span data-ttu-id="84b5f-170">그룹을 수정하려면 **범주** 및 **이름**이 같은 새 그룹을 만들어 원래의 그룹을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-170">To modify the group, create a new group with the same **Category** and **Name** to overwrite the original group.</span></span>

## <a name="using-a-computer-group-in-a-log-search"></a><span data-ttu-id="84b5f-171">로그 검색에서 컴퓨터 그룹 사용</span><span class="sxs-lookup"><span data-stu-id="84b5f-171">Using a computer group in a log search</span></span>
<span data-ttu-id="84b5f-172">다음 구문을 사용하여 로그 검색에서 컴퓨터 그룹을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-172">You use the following syntax to refer to a computer group in a log search.</span></span>  <span data-ttu-id="84b5f-173">**범주** 지정은 선택 사항이며 다른 카테고리에 이름이 같은 컴퓨터 그룹이 있는 경우에만 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-173">Specifying the **Category** is optional and only required if you have computer groups with the same name in different categories.</span></span> 

    $ComputerGroups[Category: Name]

<span data-ttu-id="84b5f-174">검색을 실행하면 검색에 포함된 모든 컴퓨터 그룹의 멤버가 먼저 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-174">When a search is run, the members of any computer groups included in the search are first resolved.</span></span>  <span data-ttu-id="84b5f-175">그룹이 로그 검색을 기준으로 할 경우 최상위 로그 검색을 수행하기 전에 그룹의 멤버를 반환하기 위한 검색이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-175">If the group is based on a log search, then that search is run to return the members of the group before performing the top-level log search.</span></span>

<span data-ttu-id="84b5f-176">일반적으로 컴퓨터 그룹은 다음 예제에서처럼 로그 검색에서 **IN** 절에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-176">Computer groups are typically used with the **IN** clause in the log search as in the following example:</span></span>

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> <span data-ttu-id="84b5f-177">작업 영역을 [새 Log Analytics 쿼리 언어](log-analytics-log-search-upgrade.md)로 업그레이드한 경우에는 다음 예제에서와 같이 컴퓨터 그룹의 별칭을 함수로 처리하는 방식으로 쿼리에서 컴퓨터 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-177">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you use a Computer group in a query by treating its alias as a function as in the following example:</span></span>
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a><span data-ttu-id="84b5f-178">컴퓨터 그룹 레코드</span><span class="sxs-lookup"><span data-stu-id="84b5f-178">Computer group records</span></span>
<span data-ttu-id="84b5f-179">Active Directory 또는 WSUS로 만든 각각의 컴퓨터 그룹 멤버 자격에 대해 OMS 저장소에 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-179">A record is created in the OMS repository for each computer group membership created from Active Directory or WSUS.</span></span>  <span data-ttu-id="84b5f-180">이 레코드의 형식은 **ComputerGroup**이며 다음 표의 속성을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-180">These records have a type of **ComputerGroup** and have the properties in the following table.</span></span>  <span data-ttu-id="84b5f-181">로그 검색 기반의 컴퓨터 그룹에 대해서는 레코드가 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-181">Records are not created for computer groups based on log searches.</span></span>

| <span data-ttu-id="84b5f-182">속성</span><span class="sxs-lookup"><span data-stu-id="84b5f-182">Property</span></span> | <span data-ttu-id="84b5f-183">설명</span><span class="sxs-lookup"><span data-stu-id="84b5f-183">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="84b5f-184">형식</span><span class="sxs-lookup"><span data-stu-id="84b5f-184">Type</span></span> |<span data-ttu-id="84b5f-185">*ComputerGroup*</span><span class="sxs-lookup"><span data-stu-id="84b5f-185">*ComputerGroup*</span></span> |
| <span data-ttu-id="84b5f-186">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="84b5f-186">SourceSystem</span></span> |<span data-ttu-id="84b5f-187">*SourceSystem*</span><span class="sxs-lookup"><span data-stu-id="84b5f-187">*SourceSystem*</span></span> |
| <span data-ttu-id="84b5f-188">컴퓨터</span><span class="sxs-lookup"><span data-stu-id="84b5f-188">Computer</span></span> |<span data-ttu-id="84b5f-189">멤버 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-189">Name of the member computer.</span></span> |
| <span data-ttu-id="84b5f-190">그룹</span><span class="sxs-lookup"><span data-stu-id="84b5f-190">Group</span></span> |<span data-ttu-id="84b5f-191">그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-191">Name of the group.</span></span> |
| <span data-ttu-id="84b5f-192">GroupFullName</span><span class="sxs-lookup"><span data-stu-id="84b5f-192">GroupFullName</span></span> |<span data-ttu-id="84b5f-193">원본 및 원본 이름을 포함하는 그룹에 대한 전체 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-193">Full path to the group including the source and source name.</span></span> |
| <span data-ttu-id="84b5f-194">GroupSource</span><span class="sxs-lookup"><span data-stu-id="84b5f-194">GroupSource</span></span> |<span data-ttu-id="84b5f-195">그룹을 수집해 온 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-195">Source that group was collected from.</span></span> <br><br><span data-ttu-id="84b5f-196">ActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="84b5f-196">ActiveDirectory</span></span><br><span data-ttu-id="84b5f-197">WSUS</span><span class="sxs-lookup"><span data-stu-id="84b5f-197">WSUS</span></span><br><span data-ttu-id="84b5f-198">WSUSClientTargeting</span><span class="sxs-lookup"><span data-stu-id="84b5f-198">WSUSClientTargeting</span></span> |
| <span data-ttu-id="84b5f-199">GroupSourceName</span><span class="sxs-lookup"><span data-stu-id="84b5f-199">GroupSourceName</span></span> |<span data-ttu-id="84b5f-200">그룹을 수집해 온 원본의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-200">Name of the source that the group was collected from.</span></span>  <span data-ttu-id="84b5f-201">Active Directory의 경우 도메인 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-201">For Active Directory, this is the domain name.</span></span> |
| <span data-ttu-id="84b5f-202">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="84b5f-202">ManagementGroupName</span></span> |<span data-ttu-id="84b5f-203">SCOM 에이전트의 경우 관리 그룹의 이름.</span><span class="sxs-lookup"><span data-stu-id="84b5f-203">Name of the management group for SCOM agents.</span></span>  <span data-ttu-id="84b5f-204">다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-204">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="84b5f-205">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="84b5f-205">TimeGenerated</span></span> |<span data-ttu-id="84b5f-206">컴퓨터 그룹이 만들어졌거나 업데이트된 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-206">Date and time the computer group was created or updated.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84b5f-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="84b5f-207">Next steps</span></span>
* <span data-ttu-id="84b5f-208">데이터 원본 및 솔루션에서 수집한 데이터를 분석하기 위해 [로그 검색](log-analytics-log-searches.md) 에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="84b5f-208">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>  

