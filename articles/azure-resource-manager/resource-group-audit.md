---
title: "리소스 모니터링을 위해 Azure 활동 로그 보기 | Microsoft Docs"
description: "활동 로그를 사용하여 사용자 작업 및 오류를 검토합니다. Azure 포털, PowerShell, Azure CLI 및 REST를 보여 줍니다."
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
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="15255-104">리소스에 대한 작업을 감사하기 위해 활동 로그 보기</span><span class="sxs-lookup"><span data-stu-id="15255-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="15255-105">활동 로그를 통해 다음 사항을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="15255-106">구독의 리소스에서 수행된 작업</span><span class="sxs-lookup"><span data-stu-id="15255-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="15255-107">작업을 시작한 사람(백 엔드 서비스에 의해 시작된 작업이라도 사용자를 호출자로 반환하지 않음)</span><span class="sxs-lookup"><span data-stu-id="15255-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="15255-108">작업이 발생한 시간</span><span class="sxs-lookup"><span data-stu-id="15255-108">when the operation occurred</span></span>
* <span data-ttu-id="15255-109">작업의 상태</span><span class="sxs-lookup"><span data-stu-id="15255-109">the status of the operation</span></span>
* <span data-ttu-id="15255-110">작업을 조사하는 데 도움이 될 수 있는 기타 속성 값</span><span class="sxs-lookup"><span data-stu-id="15255-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="15255-111">포털, PowerShell, Azure CLI, Insights REST API 또는 [Insights .NET 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Insights/)를 통해 활동 로그에서 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="15255-112">포털</span><span class="sxs-lookup"><span data-stu-id="15255-112">Portal</span></span>
1. <span data-ttu-id="15255-113">포털을 통해 활동 로그를 보려면 **모니터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![활동 로그 선택](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="15255-115">또는 특정 리소스 또는 리소스 그룹에 대해 활동 로그를 자동으로 필터링하려면 해당 리소스 블레이드에서 **활동 로그** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="15255-116">활동 로그는 선택한 리소스에 의해 자동으로 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="15255-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![리소스로 필터링](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="15255-118">**활동 로그** 블레이드에 최근 작업에 대한 요약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15255-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![작업 표시](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="15255-120">여러 조건을 선택하여 표시되는 작업의 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="15255-121">예를 들어 다음 이미지는 지난 달에 특정 사용자 또는 응용 프로그램이 수행한 작업을 표시하도록 변경된 **시간 간격** 및 **이벤트를 시작한 사람** 필드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="15255-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="15255-122">쿼리 결과를 확인하려면 **적용** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-122">Select **Apply** to view the results of your query.</span></span>
   
    ![필터 옵션 설정](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="15255-124">나중에 쿼리를 다시 실행해야 하는 경우 **저장** 을 선택하고 쿼리 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![쿼리 저장](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="15255-126">쿼리를 신속하게 실행하려면 기본 제공되는 쿼리 중 하나(예: 실패한 배포)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![쿼리 선택](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="15255-128">선택된 쿼리가 필요한 필터 값을 자동으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-128">The selected query automatically sets the required filter values.</span></span>

    ![배포 오류 보기](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="15255-130">이벤트에 대한 요약을 보려면 작업 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-130">Select one of the operations to see a summary of the event.</span></span>

    ![작업 보기](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="15255-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15255-132">PowerShell</span></span>
1. <span data-ttu-id="15255-133">로그 항목을 검색하려면 **Get-AzureRmLog** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="15255-134">항목의 목록을 필터링하는 추가 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="15255-135">시작 및 종료 시간을 지정하지 않으면 지난 시간에 대한 항목이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="15255-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="15255-136">예를 들어 지난 1시간 동안 리소스 그룹에 대해 수행된 작업을 검색하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="15255-137">다음 예제에서는 지정된 시간 동안 수행된 작업을 조사하는 활동 로그를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15255-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="15255-138">시작 및 종료 날짜는 날짜 형식으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="15255-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="15255-139">또는 날짜 기능을 사용하여 지난 14일 같은 날짜 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="15255-140">지정한 시작 시간에 따라 이전 명령은 해당 리소스 그룹에 대한 긴 목록 작업을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="15255-141">검색 조건을 제공하여 찾고자 하는 결과를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="15255-142">예를 들어 웹앱이 중지된 이유를 조사하려는 경우 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="15255-143">이 예에서는 중지 작업이 someone@contoso.com에 의해 수행되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15255-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="15255-144">더 이상 존재하지 않는 리소스 그룹에 대해서도 특정 사용자가 수행한 작업을 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="15255-145">실패한 작업을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="15255-146">해당 항목에 대한 상태 메시지를 보고 한 가지 오류에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="15255-147">반환하는 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="15255-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15255-148">Azure CLI</span></span>
* <span data-ttu-id="15255-149">로그 항목을 검색하려면 **Azure 그룹 로그 표시** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15255-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="15255-150">REST API</span><span class="sxs-lookup"><span data-stu-id="15255-150">REST API</span></span>
<span data-ttu-id="15255-151">활동 로그로 작업하기 위한 REST 작업은 [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="15255-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="15255-152">활동 로그 이벤트를 검색하려면 [구독에서 관리 이벤트 나열](https://msdn.microsoft.com/library/azure/dn931934.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15255-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15255-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15255-153">Next steps</span></span>
* <span data-ttu-id="15255-154">Power BI와 함께 Azure 활동 로그를 사용하면 구독의 작업을 면밀하게 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15255-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="15255-155">[Power BI 등에서 Azure 활동 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15255-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="15255-156">보안 정책 설정에 대해 자세히 알아보려면 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15255-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="15255-157">배포 작업을 보는 명령에 대해 자세히 알아보려면 [배포 작업 보기](resource-manager-deployment-operations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15255-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="15255-158">모든 사용자의 리소스에서 삭제 작업을 방지하는 방법을 알아보려면 [Azure Resource Manager를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15255-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

