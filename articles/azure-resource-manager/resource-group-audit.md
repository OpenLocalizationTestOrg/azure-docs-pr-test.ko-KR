---
title: "aaaView Azure 활동 로그 toomonitor 리소스 | Microsoft Docs"
description: "사용 하 여 hello 활동 tooreview 사용자 동작 및 오류를 기록합니다. Azure 포털, PowerShell, Azure CLI 및 REST를 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="b0eef-104">리소스에 tooaudit 작업을 기록 하는 활동 보기</span><span class="sxs-lookup"><span data-stu-id="b0eef-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="b0eef-105">활동 로그를 통해 다음 사항을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="b0eef-106">구독에서 리소스 hello에 수행 된 작업</span><span class="sxs-lookup"><span data-stu-id="b0eef-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="b0eef-107">(하지만 백 엔드 서비스에 의해 시작 된 작업 hello 호출자로 사용자를 반환 하지 않는) hello 작업을 시작한 사람</span><span class="sxs-lookup"><span data-stu-id="b0eef-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="b0eef-108">hello 작업이 발생 한 경우</span><span class="sxs-lookup"><span data-stu-id="b0eef-108">when hello operation occurred</span></span>
* <span data-ttu-id="b0eef-109">hello 작업의 hello 상태</span><span class="sxs-lookup"><span data-stu-id="b0eef-109">hello status of hello operation</span></span>
* <span data-ttu-id="b0eef-110">hello 작업을 조사 하는 데 도움이 되는 다른 속성의 hello 값</span><span class="sxs-lookup"><span data-stu-id="b0eef-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="b0eef-111">Hello 포털, PowerShell, CLI Azure Insights REST API를 통해 hello 활동 로그에서 정보를 검색할 수 있습니다 또는 [Insights.NET 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Insights/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="b0eef-112">포털</span><span class="sxs-lookup"><span data-stu-id="b0eef-112">Portal</span></span>
1. <span data-ttu-id="b0eef-113">hello 포털을 통해 tooview hello 활동 로그 선택 **모니터**합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![활동 로그 선택](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="b0eef-115">또는 특정 리소스 또는 리소스 그룹에 대 한 필터 hello 활동 로그 tooautomatically **활동 로그** 해당 리소스 블레이드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="b0eef-116">해당 hello 활동 로그는 자동으로 선택 하는 hello 자원별 필터링을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![리소스로 필터링](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="b0eef-118">Hello에 **활동 로그** 블레이드, 최근 작업에 대 한 요약을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![작업 표시](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="b0eef-120">표시 되는 작업의 toorestrict hello 수에는 다른 조건을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="b0eef-121">예를 들어 hello 다음 이미지에서는 hello **Timespan** 및 **이벤트에 의해 시작** 특정 사용자 또는 응용 프로그램 hello에 대 한 지난 달에 의해 수행 tooview hello 작업을 변경 하는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="b0eef-122">선택 **적용** tooview hello 쿼리 결과 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![필터 옵션 설정](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="b0eef-124">Toorun hello 쿼리를 나중에 다시 필요 하면 선택 **저장** hello 쿼리 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![쿼리 저장](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="b0eef-126">쿼리를 실행 하는 tooquickly, 같은 배포에 실패 한 hello 기본 제공 쿼리 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![쿼리 선택](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="b0eef-128">hello 선택한 쿼리는 자동으로 hello 필요한 필터 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-128">hello selected query automatically sets hello required filter values.</span></span>

    ![배포 오류 보기](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="b0eef-130">Hello 작업 toosee 간략하게 설명 hello 이벤트 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![작업 보기](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="b0eef-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0eef-132">PowerShell</span></span>
1. <span data-ttu-id="b0eef-133">tooretrieve 로그 항목을 hello 실행 **Get AzureRmLog** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="b0eef-134">항목 목록이 toofilter hello 추가 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="b0eef-135">시작 및 종료 시간을 지정 하지 않으면 지난 1 시간 동안 hello에 대 한 항목이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="b0eef-136">예를 들어 hello 지난 시간 동안 리소스 그룹에 대 한 tooretrieve hello 작업 실행:</span><span class="sxs-lookup"><span data-stu-id="b0eef-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="b0eef-137">다음 예제는 hello toouse hello 활동에서 지정된 된 시간 동안 수행 된 tooresearch operations를 로그 하는 방법은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="b0eef-138">hello 시작 및 종료 날짜에에서 지정 된 날짜 형식.</span><span class="sxs-lookup"><span data-stu-id="b0eef-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="b0eef-139">또는 날짜 함수 toospecify hello 날짜 범위를 hello 같은 지난 14 일 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="b0eef-140">지정한 hello 시작 시간에 따라 hello 이전 명령 목록이 긴 hello 리소스 그룹에 대 한 작업을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="b0eef-141">검색 조건을 제공 하 여 찾고 기능에 대 한 hello 결과 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="b0eef-142">예를 들어 웹 응용 프로그램 중지 tooresearch을 시도 하는 경우 hello 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="b0eef-143">이 예에서는 중지 작업이 someone@contoso.com에 의해 수행되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="b0eef-144">더 이상 존재 하는 리소스 그룹에도 특정 사용자가 수행한 작업을 hello 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="b0eef-145">실패한 작업을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="b0eef-146">해당 항목에 대 한 hello 상태 메시지를 보고 한 오류에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="b0eef-147">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="b0eef-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b0eef-148">Azure CLI</span></span>
* <span data-ttu-id="b0eef-149">hello 실행 tooretrieve 로그 항목 **으로 azure 그룹 로그 표시** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="b0eef-150">REST API</span><span class="sxs-lookup"><span data-stu-id="b0eef-150">REST API</span></span>
<span data-ttu-id="b0eef-151">hello 활동 로그를 사용 하기 위한 REST 작업 hello hello의 일부인 [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="b0eef-152">tooretrieve 활동 로그 이벤트 참조 [구독에서 hello 관리 이벤트 나열](https://msdn.microsoft.com/library/azure/dn931934.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0eef-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b0eef-153">Next steps</span></span>
* <span data-ttu-id="b0eef-154">Power BI 구독에 hello 동작에 대 한 큰 insights toogain azure 활동 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="b0eef-155">[Power BI 등에서 Azure 활동 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0eef-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="b0eef-156">보안 정책 설정에 대 한 toolearn 참조 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="b0eef-157">배포 작업을 보기 위한 hello 명령에 대 한 toolearn 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b0eef-158">모든 사용자에 대 한 리소스에 tooprevent 삭제를 확인 하려면 어떻게 toolearn [Azure 리소스 관리자와 리소스를 잠글](resource-group-lock-resources.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0eef-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

