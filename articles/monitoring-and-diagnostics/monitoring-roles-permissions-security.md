---
title: "Azure Monitor에서의 역할, 권한 및 보안 시작 | Microsoft Docs"
description: "Azure Monitor 기본 제공 역할 및 권한을 사용하여 모니터링 리소스에 대한 액세스를 제한하는 방법을 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: a28f971ae898ffdd1168550a909f2a48e1b3b652
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a><span data-ttu-id="d1527-103">Azure Monitor에서의 역할, 권한 및 보안 시작</span><span class="sxs-lookup"><span data-stu-id="d1527-103">Get started with roles, permissions, and security with Azure Monitor</span></span>
<span data-ttu-id="d1527-104">많은 팀에서는 모니터링 데이터 및 설정에 대한 액세스를 엄격히 규제할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-104">Many teams need to strictly regulate access to monitoring data and settings.</span></span> <span data-ttu-id="d1527-105">예를 들어 모니터링에 대해 단독으로 작업하는 팀원(지원 엔지니어, devops 엔지니어)이 있거나, 관리되는 서비스 공급자를 사용할 경우 이들에게 리소스 생성, 수정 또는 삭제 기능은 제한하면서 모니터링 데이터에 대해서만 액세스를 부여하고자 할 수 있씁니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-105">For example, if you have team members who work exclusively on monitoring (support engineers, devops engineers) or if you use a managed service provider, you may want to grant them access to only monitoring data while restricting their ability to create, modify, or delete resources.</span></span> <span data-ttu-id="d1527-106">이 문서에서는 Azure의 사용자에게 기본 제공 모니터링 RBAC 역할을 신속하게 적용하거나 제한된 모니터링 권한이 필요한 사용자에 대해 자체 사용자 지정 역할을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-106">This article shows how to quickly apply a built-in monitoring RBAC role to a user in Azure or build your own custom role for a user who needs limited monitoring permissions.</span></span> <span data-ttu-id="d1527-107">그런 다음 Azure Monitor 관련 리소스에 대한 보안 고려 사항과, 포함된 데이터에 대한 액세스를 제한하는 방법에 대해 논의합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-107">It then discusses security considerations for your Azure Monitor-related resources and how you can limit access to the data they contain.</span></span>

## <a name="built-in-monitoring-roles"></a><span data-ttu-id="d1527-108">기본 제공 모니터링 역할</span><span class="sxs-lookup"><span data-stu-id="d1527-108">Built-in monitoring roles</span></span>
<span data-ttu-id="d1527-109">Azure Monitor의 기본 제공 역할은 구독에서 리소스에 대한 액세스를 제한하면서, 인프라 모니터링을 담당하는 사용자는 필요한 데이터를 확보 및 구성할 수 있게 지원하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-109">Azure Monitor’s built-in roles are designed to help limit access to resources in a subscription while still enabling those responsible for monitoring infrastructure to obtain and configure the data they need.</span></span> <span data-ttu-id="d1527-110">Azure Monitor는 Monitoring Reader와Monitoring Contributor 등, 바로 사용할 수 있는 2가지 역할을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-110">Azure Monitor provides two out-of-the-box roles: A Monitoring Reader and a Monitoring Contributor.</span></span>

### <a name="monitoring-reader"></a><span data-ttu-id="d1527-111">Monitoring Reader</span><span class="sxs-lookup"><span data-stu-id="d1527-111">Monitoring Reader</span></span>
<span data-ttu-id="d1527-112">Monitoring Reader 역할이 할당된 사용자는 구독에서 모든 모니터링 데이터를 볼 수 있지만 리소스를 수정하거나 모니터링 리소스와 관련한 설정은 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-112">People assigned the Monitoring Reader role can view all monitoring data in a subscription but cannot modify any resource or edit any settings related to monitoring resources.</span></span> <span data-ttu-id="d1527-113">이 역할은 다음이 필요한 지원과 같은 조직의 사용자나 운영 엔지니어에게 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-113">This role is appropriate for users in an organization, such as support or operations engineers, who need to be able to:</span></span>

* <span data-ttu-id="d1527-114">포털의 모니터링 대시보드를 확인하고 자체 개별 모니터링 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-114">View monitoring dashboards in the portal and create their own private monitoring dashboards.</span></span>
* <span data-ttu-id="d1527-115">[Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlets](insights-powershell-samples.md) 또는 [플랫폼 간 CLI](insights-cli-samples.md)를 사용하여 메트릭을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-115">Query for metrics using the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlets](insights-powershell-samples.md), or [cross-platform CLI](insights-cli-samples.md).</span></span>
* <span data-ttu-id="d1527-116">포털, Azure Monitor REST API, PowerShell cmdlet 또는 플랫폼 간 CLI를 사용하여 작업 로그를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-116">Query the Activity Log using the portal, Azure Monitor REST API, PowerShell cmdlets, or cross-platform CLI.</span></span>
* <span data-ttu-id="d1527-117">리소스에 대한 [진단 설정](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-117">View the [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.</span></span>
* <span data-ttu-id="d1527-118">구독에 대한 [로그 프로필](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-118">View the [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.</span></span>
* <span data-ttu-id="d1527-119">자동 크기 조정 설정을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-119">View autoscale settings.</span></span>
* <span data-ttu-id="d1527-120">경고 활동 및 설정을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-120">View alert activity and settings.</span></span>
* <span data-ttu-id="d1527-121">Application Insights 데이터에 액세스하고 AI Analytics에서 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-121">Access Application Insights data and view data in AI Analytics.</span></span>
* <span data-ttu-id="d1527-122">작업 영역에 대한 사용 현황 데이터를 포함하여 Log Analytics(OMS) 작업 영역 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-122">Search Log Analytics (OMS) workspace data including usage data for the workspace.</span></span>
* <span data-ttu-id="d1527-123">Log Analytics(OMS) 관리 그룹을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-123">View Log Analytics (OMS) management groups.</span></span>
* <span data-ttu-id="d1527-124">Log Analytics(OMS) 검색 스키마를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-124">Retrieve the Log Analytics (OMS) search schema.</span></span>
* <span data-ttu-id="d1527-125">Log Analytics(OMS) 인텔리전스 팩을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-125">List Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="d1527-126">Log Analytics(OMS) 저장된 검색을 검색 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-126">Retrieve and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="d1527-127">Log Analytics(OMS) 저장소 구성을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-127">Retrieve the Log Analytics (OMS) storage configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="d1527-128">이 역할은 이벤트 허브에 스트리밍되었거나 저장소 계정에 저장된 로그 데이터에 대한 읽기 액세스를 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-128">This role does not give read access to log data that has been streamed to an event hub or stored in a storage account.</span></span> <span data-ttu-id="d1527-129">[아래를 참조하세요](#security-considerations-for-monitoring-data) .</span><span class="sxs-lookup"><span data-stu-id="d1527-129">[See below](#security-considerations-for-monitoring-data) for information on configuring access to these resources.</span></span>
> 
> 

### <a name="monitoring-contributor"></a><span data-ttu-id="d1527-130">Monitoring Contributor</span><span class="sxs-lookup"><span data-stu-id="d1527-130">Monitoring Contributor</span></span>
<span data-ttu-id="d1527-131">Monitoring Reader 역할이 할당된 사용자는 구독의 모든 모니터링 데이터를 볼 수 있으며, 모니터링 설정을 만들거나 수정할 수 있지만 다른 리소스는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-131">People assigned the Monitoring Contributor role can view all monitoring data in a subscription and create or modify monitoring settings, but cannot modify any other resources.</span></span> <span data-ttu-id="d1527-132">이 역할은 Monitoring Reader 역할의 상위 집합이며, 조직의 모니터링 팀 구성원이거나 위의 권한 외에도 다음이 필요한 관리되는 서비스 제공자인 사용자에게 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-132">This role is a superset of the Monitoring Reader role, and is appropriate for members of an organization’s monitoring team or managed service providers who, in addition to the permissions above, also need to be able to:</span></span>

* <span data-ttu-id="d1527-133">공유 대시보드로 모니터링 대시보드를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-133">Publish monitoring dashboards as a shared dashboard.</span></span>
* <span data-ttu-id="d1527-134">리소스에 대한 [진단 설정](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 을 구성합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1527-134">Set [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.*</span></span>
* <span data-ttu-id="d1527-135">구독에 대한 [로그 프로필](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 을 설정합니다.*</span><span class="sxs-lookup"><span data-stu-id="d1527-135">Set the [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.*</span></span>
* <span data-ttu-id="d1527-136">경고 활동 및 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-136">Set alert activity and settings.</span></span>
* <span data-ttu-id="d1527-137">Application Insights 웹 테스트 및 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-137">Create Application Insights web tests and components.</span></span>
* <span data-ttu-id="d1527-138">Log Analytics(OMS) 작업 공간 공유 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-138">List Log Analytics (OMS) workspace shared keys.</span></span>
* <span data-ttu-id="d1527-139">Log Analytics(OMS) 인텔리전스 팩을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-139">Enable or disable Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="d1527-140">Log Analytics(OMS) 저장된 검색을 만들고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-140">Create and delete and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="d1527-141">Log Analytics(OMS) 저장소 구성을 만들고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-141">Create and delete the Log Analytics (OMS) storage configuration.</span></span>

<span data-ttu-id="d1527-142">*사용자가 로그 프로필이나 진단 설정을 구성하려면 대상 리소스(저장소 계정 또는 이벤트 허브 네임스페이스)에 대한 ListKeys 권한도 별도로 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-142">*user must also separately be granted ListKeys permission on the target resource (storage account or event hub namespace) to set a log profile or diagnostic setting.</span></span>

> [!NOTE]
> <span data-ttu-id="d1527-143">이 역할은 이벤트 허브에 스트리밍되었거나 저장소 계정에 저장된 로그 데이터에 대한 읽기 액세스를 부여하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-143">This role does not give read access to log data that has been streamed to an event hub or stored in a storage account.</span></span> <span data-ttu-id="d1527-144">[아래를 참조하세요](#security-considerations-for-monitoring-data) .</span><span class="sxs-lookup"><span data-stu-id="d1527-144">[See below](#security-considerations-for-monitoring-data) for information on configuring access to these resources.</span></span>
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a><span data-ttu-id="d1527-145">권한 및 사용자 지정 RBAC 역할 모니터링</span><span class="sxs-lookup"><span data-stu-id="d1527-145">Monitoring permissions and custom RBAC roles</span></span>
<span data-ttu-id="d1527-146">위의 기본 제공 역할이 팀의 정확한 요구에 부합하지 못할 경우 더 세밀하게 지정한 권한을 갖는 [사용자 지정 RBAC 역할](../active-directory/role-based-access-control-custom-roles.md) 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-146">If the above built-in roles don’t meet the exact needs of your team, you can [create a custom RBAC role](../active-directory/role-based-access-control-custom-roles.md) with more granular permissions.</span></span> <span data-ttu-id="d1527-147">다음은 공통 Azure 모니터 RBAC 작업과 그에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-147">Below are the common Azure Monitor RBAC operations with their descriptions.</span></span>

| <span data-ttu-id="d1527-148">작업</span><span class="sxs-lookup"><span data-stu-id="d1527-148">Operation</span></span> | <span data-ttu-id="d1527-149">설명</span><span class="sxs-lookup"><span data-stu-id="d1527-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1527-150">Microsoft.Insights/AlertRules/[Read, Write, Delete]</span><span class="sxs-lookup"><span data-stu-id="d1527-150">Microsoft.Insights/AlertRules/[Read, Write, Delete]</span></span> |<span data-ttu-id="d1527-151">경고 규칙 읽기/쓰기/삭제</span><span class="sxs-lookup"><span data-stu-id="d1527-151">Read/write/delete alert rules.</span></span> |
| <span data-ttu-id="d1527-152">Microsoft.Insights/AlertRules/Incidents/Read</span><span class="sxs-lookup"><span data-stu-id="d1527-152">Microsoft.Insights/AlertRules/Incidents/Read</span></span> |<span data-ttu-id="d1527-153">경고 규칙에 대한 사건 나열(트리거된 경고 규칙 내역).</span><span class="sxs-lookup"><span data-stu-id="d1527-153">List incidents (history of the alert rule being triggered) for alert rules.</span></span> <span data-ttu-id="d1527-154">포털에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-154">This only applies to the portal.</span></span> |
| <span data-ttu-id="d1527-155">Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete]</span><span class="sxs-lookup"><span data-stu-id="d1527-155">Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="d1527-156">자동 크기 조정 설정 읽기/쓰기/삭제</span><span class="sxs-lookup"><span data-stu-id="d1527-156">Read/write/delete autoscale settings.</span></span> |
| <span data-ttu-id="d1527-157">Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete]</span><span class="sxs-lookup"><span data-stu-id="d1527-157">Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="d1527-158">진단 설정 읽기/쓰기/삭제</span><span class="sxs-lookup"><span data-stu-id="d1527-158">Read/write/delete diagnostic settings.</span></span> |
| <span data-ttu-id="d1527-159">Microsoft.Insights/eventtypes/digestevents/Read</span><span class="sxs-lookup"><span data-stu-id="d1527-159">Microsoft.Insights/eventtypes/digestevents/Read</span></span> |<span data-ttu-id="d1527-160">이 권한은 사용자 포털을 통해 활동 로그에 액세스해야 하는 사용자에게 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-160">This permission is necessary for users who need access to Activity Logs via the portal.</span></span> |
| <span data-ttu-id="d1527-161">Microsoft.Insights/eventtypes/values/Read</span><span class="sxs-lookup"><span data-stu-id="d1527-161">Microsoft.Insights/eventtypes/values/Read</span></span> |<span data-ttu-id="d1527-162">구독에서 활동 로그 이벤트(관리 이벤트)를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-162">List Activity Log events (management events) in a subscription.</span></span> <span data-ttu-id="d1527-163">이 권한은 활동 로그에 대한 프로그래밍 방식 및 포털 액세스 모두에 적용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-163">This permission is applicable to both programmatic and portal access to the Activity Log.</span></span> |
| <span data-ttu-id="d1527-164">Microsoft.Insights/LogDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="d1527-164">Microsoft.Insights/LogDefinitions/Read</span></span> |<span data-ttu-id="d1527-165">이 권한은 사용자 포털을 통해 활동 로그에 액세스해야 하는 사용자에게 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-165">This permission is necessary for users who need access to Activity Logs via the portal.</span></span> |
| <span data-ttu-id="d1527-166">Microsoft.Insights/MetricDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="d1527-166">Microsoft.Insights/MetricDefinitions/Read</span></span> |<span data-ttu-id="d1527-167">메트릭 정의(리소스에 사용 가능한 메트릭 형식 목록)를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-167">Read metric definitions (list of available metric types for a resource).</span></span> |
| <span data-ttu-id="d1527-168">Microsoft.Insights/Metrics/Read</span><span class="sxs-lookup"><span data-stu-id="d1527-168">Microsoft.Insights/Metrics/Read</span></span> |<span data-ttu-id="d1527-169">리소스에 대한 메트릭을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-169">Read metrics for a resource.</span></span> |

> [!NOTE]
> <span data-ttu-id="d1527-170">리소스에 대한 알림, 진단 설정 및 메트릭에 액세스하려면 해당 사용자에게 리소스 형식과 리소스 범위에 대한 읽기 액세스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-170">Access to alerts, diagnostic settings, and metrics for a resource requires that the user has Read access to the resource type and scope of that resource.</span></span> <span data-ttu-id="d1527-171">저장소 계정에 보관하거나 이벤트 허브에 스트리밍하는 진단 설정 또는 로그 프로필을 만들려면 해당 사용자에게 대상 리소스에 대한 ListKeys 권한도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-171">Creating (“write”) a diagnostic setting or log profile that archives to a storage account or streams to event hubs requires the user to also have ListKeys permission on the target resource.</span></span>
> 
> 

<span data-ttu-id="d1527-172">예를 들어, 다음과 같이 위의 표를 사용하여 "활동 로그 판독자"에 대한 사용자 지정 RBAC 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-172">For example, using the above table you could create a custom RBAC role for an “Activity Log Reader” like this:</span></span>

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a><span data-ttu-id="d1527-173">모니터링 데이터에 대한 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d1527-173">Security considerations for monitoring data</span></span>
<span data-ttu-id="d1527-174">모니터링 데이터, 특히 로그 파일에는 IP 주소나 사용자 이름 같은 중요 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-174">Monitoring data—particularly log files—can contain sensitive information, such as IP addresses or user names.</span></span> <span data-ttu-id="d1527-175">Azure의 모니터링 데이터는 다음 3가지 기본 형태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-175">Monitoring data from Azure comes in three basic forms:</span></span>

1. <span data-ttu-id="d1527-176">활동 로그. Azure 구독에서 모든 제어 관련 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-176">The Activity Log, which describes all control-plane actions on your Azure subscription.</span></span>
2. <span data-ttu-id="d1527-177">진단 로그. 리소스가 내보낸 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-177">Diagnostic Logs, which are logs emitted by a resource.</span></span>
3. <span data-ttu-id="d1527-178">메트릭. 리소스가 내보낸 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-178">Metrics, which are emitted by resources.</span></span>

<span data-ttu-id="d1527-179">이 세 데이터 형식은 저장소 계정에 저장되거나 이벤트 허브에 스트리밍되며, 모두 범용 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-179">All three of these data types can be stored in a storage account or streamed to Event Hub, both of which are general-purpose Azure resources.</span></span> <span data-ttu-id="d1527-180">범용 리소스이기 때문에 이 항목의 만들기, 삭제 및 액세스는 권한이 필요한 작업이며 일반적으로 관리자에게 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-180">Because these are general-purpose resources, creating, deleting, and accessing them is a privileged operation usually reserved for an administrator.</span></span> <span data-ttu-id="d1527-181">오용을 방지하기 위해 모니터링 관련 리소스에는 다음 방법을 적용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-181">We suggest that you use the following practices for monitoring-related resources to prevent misuse:</span></span>

* <span data-ttu-id="d1527-182">모니터링 데이터에는 단일 전용 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-182">Use a single, dedicated storage account for monitoring data.</span></span> <span data-ttu-id="d1527-183">모니터링 데이터를 여러 저장소 계정으로 구분해야 할 경우, 모니터링 데이터와 비 모니터링 데이터 간에 저장소 계정을 공유하여 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-183">If you need to separate monitoring data into multiple storage accounts, never share usage of a storage account between monitoring and non-monitoring data, as this may inadvertently give those who only need access to monitoring data (eg.</span></span> <span data-ttu-id="d1527-184">이 경우 모니터링 데이터(예: 타사 SIEM) 액세스만 필요한 사용자에게 의도치 않게 비 모니터링 데이터에 대한 액세스를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-184">a third-party SIEM) access to non-monitoring data.</span></span>
* <span data-ttu-id="d1527-185">같은 이유로 모든 진단 설정에서 단일 전용 서비스 버스 또는 이벤트 허브 네임스페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-185">Use a single, dedicated Service Bus or Event Hub namespace across all diagnostic settings for the same reason as above.</span></span>
* <span data-ttu-id="d1527-186">별도의 리소스 그룹을 유지하여 모니터링 관련 저장소 계정이나 이벤트 허브에 대한 액세스를 제한하고, 모니터링 역할에 [범위를 사용하여](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) 액세스를 해당 리소스 그룹으로만 한정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-186">Limit access to monitoring-related storage accounts or event hubs by keeping them in a separate resource group, and [use scope](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) on your monitoring roles to limit access to only that resource group.</span></span>
* <span data-ttu-id="d1527-187">사용자가 모니터링 데이터 액세스만 필요할 경우 구독에서 이벤트 허브나 저장소 계정에 ListKeys 권한을 부여해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-187">Never grant the ListKeys permission for either storage accounts or event hubs at subscription scope when a user only needs access to monitoring data.</span></span> <span data-ttu-id="d1527-188">그 대신 리소스나 리소스 그룹(전용 모니터링 리소스 그룹이 있는 경우) 범위에서 사용자에게 해당 건한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-188">Instead, give these permissions to the user at a resource or resource group (if you have a dedicated monitoring resource group) scope.</span></span>

### <a name="limiting-access-to-monitoring-related-storage-accounts"></a><span data-ttu-id="d1527-189">모니터링 관련 저장소 계정에 대한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="d1527-189">Limiting access to monitoring-related storage accounts</span></span>
<span data-ttu-id="d1527-190">사용자나 응용 프로그램이 저장소 계정의 모니터링 데이터에 대한 액세스를 필요로 할 경우, Blob 저장소에 대한 서비스 수준 읽기 전용 액세스 권한을 통해 모니터링 데이터를 포함하는 저장소 계정에서 [계정 SAS를 생성](https://msdn.microsoft.com/library/azure/mt584140.aspx) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-190">When a user or application needs access to monitoring data in a storage account, you should [generate an Account SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) on the storage account that contains monitoring data with service-level read-only access to blob storage.</span></span> <span data-ttu-id="d1527-191">PowerShell에서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-191">In PowerShell, this might look like:</span></span>

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

<span data-ttu-id="d1527-192">그런 다음 해당 저장소 계정에서의 읽기가 필요한 개체에게 토큰을 부여하면 해당 저장소 계정의 모든 Blob을 나열하고 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-192">You can then give the token to the entity that needs to read from that storage account, and it can list and read from all blobs in that storage account.</span></span>

<span data-ttu-id="d1527-193">또는 RBAC로 이 권한을 제어해야 할 경우 해당 특정 저장소 계정에서 개체에 Microsoft.Storage/storageAccounts/listkeys/action 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-193">Alternatively, if you need to control this permission with RBAC, you can grant that entity the Microsoft.Storage/storageAccounts/listkeys/action permission on that particular storage account.</span></span> <span data-ttu-id="d1527-194">저장소 계정에 보관하기 위해 로그 프로필이나 진단 설정을 구성할 수 있는 사용자에게 필요한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-194">This is necessary for users who need to be able to set a diagnostic setting or log profile to archive to a storage account.</span></span> <span data-ttu-id="d1527-195">예를 들어, 한 저장소 계정에서 읽기만 필요한 사용자 또는 응용 프로그램에 대해 다음 사용자 지정 RBAC 역할을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-195">For example, you could create the following custom RBAC role for a user or application that only needs to read from one storage account:</span></span>

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get the storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> <span data-ttu-id="d1527-196">ListKeys 권한이 있는 사용자는 기본 및 보조 저장소 계정 키를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-196">The ListKeys permission enables the user to list the primary and secondary storage account keys.</span></span> <span data-ttu-id="d1527-197">이러한 키는 사용자에게 해당 저장소 계정의 모든 서명된 서비스(Blob, 큐, 테이블, 파일) 전체에서 모든 서명된 권한(읽기, 쓰기, Blob 만들기, Blob 삭제 등)을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-197">These keys grant the user all signed permissions (read, write, create blobs, delete blobs, etc.) across all signed services (blob, queue, table, file) in that storage account.</span></span> <span data-ttu-id="d1527-198">가능한 경우 위에서 설명한 계정 SAS를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-198">We recommend using an Account SAS described above when possible.</span></span>
> 
> 

### <a name="limiting-access-to-monitoring-related-event-hubs"></a><span data-ttu-id="d1527-199">모니터링 관련 이벤트 허브에 대한 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="d1527-199">Limiting access to monitoring-related event hubs</span></span>
<span data-ttu-id="d1527-200">이벤트 허브에서도 비슷한 패턴을 따를 수 있지만 먼저 전용 수신 권한 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-200">A similar pattern can be followed with event hubs, but first you need to create a dedicated Listen authorization rule.</span></span> <span data-ttu-id="d1527-201">관련 모니터링 이벤트 허브를 수신 대기 하도록 하는 응용 프로그램에 대한 액세스 권한을 부여 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-201">If you want to grant access to an application that only needs to listen to monitoring-related event hubs, do the following:</span></span>

1. <span data-ttu-id="d1527-202">수신 클레임만으로 모니터링 데이터를 스트리밍하기 위해 생성된 이벤트 허브에서 공유 액세스 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-202">Create a shared access policy on the event hub(s) that were created for streaming monitoring data with only Listen claims.</span></span> <span data-ttu-id="d1527-203">이 작업은 포털에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-203">This can be done in the portal.</span></span> <span data-ttu-id="d1527-204">예를 들어, 이 정책을 “monitoringReadOnly”라고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-204">For example, you might call it “monitoringReadOnly.”</span></span> <span data-ttu-id="d1527-205">가능한 경우 소비자에게 직접 이 키를 제공하고 다음 단계를 건너뛰고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-205">If possible, you will want to give that key directly to the consumer and skip the next step.</span></span>
2. <span data-ttu-id="d1527-206">소비자가 임시로 키를 가져올 수 있어야 할 경우 해당 이벤트 허브에 대해 사용자에게 ListKeys 작업을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-206">If the consumer needs to be able to get the key ad-hoc, grant the user the ListKeys action for that event hub.</span></span> <span data-ttu-id="d1527-207">이벤트 허브에 스트리밍하기 위해 로그 프로필이나 진단 설정을 구성할 수 있어야 하는 사용자에게 필요한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-207">This is also necessary for users who need to be able to set a diagnostic setting or log profile to stream to event hubs.</span></span> <span data-ttu-id="d1527-208">예를 들어, RBAC 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1527-208">For example, you might create an RBAC rule:</span></span>
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get the key to listen to an event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a><span data-ttu-id="d1527-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1527-209">Next steps</span></span>
* [<span data-ttu-id="d1527-210">Resource Manager의 RBAC 및 권한에 대해 읽기</span><span class="sxs-lookup"><span data-stu-id="d1527-210">Read about RBAC and permissions in Resource Manager</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="d1527-211">Azure의 모니터링 개요 읽기</span><span class="sxs-lookup"><span data-stu-id="d1527-211">Read the overview of monitoring in Azure</span></span>](monitoring-overview.md)

