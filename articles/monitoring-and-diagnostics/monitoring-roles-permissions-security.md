---
title: "역할, 권한 및 보안 Azure 모니터로 aaaGet 시작 | Microsoft Docs"
description: "Toouse Azure 모니터의 기본 제공 역할 및 사용 권한 toorestrict toomonitoring 리소스에 액세스할 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a><span data-ttu-id="4f6ee-103">Azure Monitor에서의 역할, 권한 및 보안 시작</span><span class="sxs-lookup"><span data-stu-id="4f6ee-103">Get started with roles, permissions, and security with Azure Monitor</span></span>
<span data-ttu-id="4f6ee-104">많은 팀 필요 toostrictly toomonitoring 데이터 액세스 및 설정을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-104">Many teams need toostrictly regulate access toomonitoring data and settings.</span></span> <span data-ttu-id="4f6ee-105">예를 들어 관리 되는 서비스 공급자를 사용할 경우 toogrant tooonly 자신의 능력 toocreate 제한 하면서 모니터링 데이터 액세스 권한을 (기술 지원 엔지니어, devops 엔지니어) 모니터링에 작업 하는 팀 멤버가 있는 경우 수정, 또는 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-105">For example, if you have team members who work exclusively on monitoring (support engineers, devops engineers) or if you use a managed service provider, you may want toogrant them access tooonly monitoring data while restricting their ability toocreate, modify, or delete resources.</span></span> <span data-ttu-id="4f6ee-106">이 문서에서는 tooquickly 기본 제공 모니터링 RBAC 역할 tooa 사용자가 Azure에서 적용 또는 고유한 사용자 지정 역할 모니터링 제한 된 권한이 필요로 하는 사용자에 대 한 빌드 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-106">This article shows how tooquickly apply a built-in monitoring RBAC role tooa user in Azure or build your own custom role for a user who needs limited monitoring permissions.</span></span> <span data-ttu-id="4f6ee-107">Azure 모니터와 관련 된 리소스에 대 한 보안 고려 사항에 설명 합니다 하며 포함 방법 toohello 데이터 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-107">It then discusses security considerations for your Azure Monitor-related resources and how you can limit access toohello data they contain.</span></span>

## <a name="built-in-monitoring-roles"></a><span data-ttu-id="4f6ee-108">기본 제공 모니터링 역할</span><span class="sxs-lookup"><span data-stu-id="4f6ee-108">Built-in monitoring roles</span></span>
<span data-ttu-id="4f6ee-109">Azure 모니터의 기본 제공 역할이 계속 하는 것을 사용 하도록 설정 하는 동안 구독에서 설계 된 toohelp 제한 액세스 tooresources tooobtain 인프라를 모니터링 하는 일을 담당 하 고 필요한 hello 데이터를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-109">Azure Monitor’s built-in roles are designed toohelp limit access tooresources in a subscription while still enabling those responsible for monitoring infrastructure tooobtain and configure hello data they need.</span></span> <span data-ttu-id="4f6ee-110">Azure Monitor는 Monitoring Reader와Monitoring Contributor 등, 바로 사용할 수 있는 2가지 역할을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-110">Azure Monitor provides two out-of-the-box roles: A Monitoring Reader and a Monitoring Contributor.</span></span>

### <a name="monitoring-reader"></a><span data-ttu-id="4f6ee-111">Monitoring Reader</span><span class="sxs-lookup"><span data-stu-id="4f6ee-111">Monitoring Reader</span></span>
<span data-ttu-id="4f6ee-112">Hello 모니터링 읽기 역할에 할당 된 사용자 구독에서 모든 모니터링 데이터를 볼 수 있지만 모든 리소스를 수정할 하거나 모든 설정이 관련된 toomonitoring 리소스를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-112">People assigned hello Monitoring Reader role can view all monitoring data in a subscription but cannot modify any resource or edit any settings related toomonitoring resources.</span></span> <span data-ttu-id="4f6ee-113">이 역할은 toobe 할 필요는 지원 또는 작업 엔지니어 같은 조직의 사용자에 게 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-113">This role is appropriate for users in an organization, such as support or operations engineers, who need toobe able to:</span></span>

* <span data-ttu-id="4f6ee-114">Hello 포털에서 모니터링 대시보드를 확인 하 고 자신의 개인 모니터링 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-114">View monitoring dashboards in hello portal and create their own private monitoring dashboards.</span></span>
* <span data-ttu-id="4f6ee-115">Hello를 사용 하 여 메트릭에 대 한 쿼리 [Azure 모니터 REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlet](insights-powershell-samples.md), 또는 [플랫폼 간 CLI](insights-cli-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-115">Query for metrics using hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx), [PowerShell cmdlets](insights-powershell-samples.md), or [cross-platform CLI](insights-cli-samples.md).</span></span>
* <span data-ttu-id="4f6ee-116">쿼리 hello hello 포털, Azure 모니터 REST API, PowerShell cmdlet 또는 플랫폼 간 CLI를 사용 하 여 작업 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-116">Query hello Activity Log using hello portal, Azure Monitor REST API, PowerShell cmdlets, or cross-platform CLI.</span></span>
* <span data-ttu-id="4f6ee-117">보기 hello [진단 설정을](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-117">View hello [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.</span></span>
* <span data-ttu-id="4f6ee-118">보기 hello [프로필 로그](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 구독에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-118">View hello [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.</span></span>
* <span data-ttu-id="4f6ee-119">자동 크기 조정 설정을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-119">View autoscale settings.</span></span>
* <span data-ttu-id="4f6ee-120">경고 활동 및 설정을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-120">View alert activity and settings.</span></span>
* <span data-ttu-id="4f6ee-121">Application Insights 데이터에 액세스하고 AI Analytics에서 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-121">Access Application Insights data and view data in AI Analytics.</span></span>
* <span data-ttu-id="4f6ee-122">Hello 작업 영역에 대 한 사용 현황 데이터를 포함 한 로그 분석 (OMS) 작업 영역 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-122">Search Log Analytics (OMS) workspace data including usage data for hello workspace.</span></span>
* <span data-ttu-id="4f6ee-123">Log Analytics(OMS) 관리 그룹을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-123">View Log Analytics (OMS) management groups.</span></span>
* <span data-ttu-id="4f6ee-124">Hello 로그 분석 (OMS) 검색 스키마를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-124">Retrieve hello Log Analytics (OMS) search schema.</span></span>
* <span data-ttu-id="4f6ee-125">Log Analytics(OMS) 인텔리전스 팩을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-125">List Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="4f6ee-126">Log Analytics(OMS) 저장된 검색을 검색 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-126">Retrieve and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="4f6ee-127">Hello 로그 분석 (OMS) 저장소 구성을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-127">Retrieve hello Log Analytics (OMS) storage configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="4f6ee-128">이 역할에서 저장소 계정에 저장 또는 스트리밍된 tooan 이벤트 허브 된 toolog 데이터 읽기 액세스를 부여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-128">This role does not give read access toolog data that has been streamed tooan event hub or stored in a storage account.</span></span> <span data-ttu-id="4f6ee-129">[아래 참조](#security-considerations-for-monitoring-data) toothese 리소스에 액세스를 구성 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-129">[See below](#security-considerations-for-monitoring-data) for information on configuring access toothese resources.</span></span>
> 
> 

### <a name="monitoring-contributor"></a><span data-ttu-id="4f6ee-130">Monitoring Contributor</span><span class="sxs-lookup"><span data-stu-id="4f6ee-130">Monitoring Contributor</span></span>
<span data-ttu-id="4f6ee-131">할당 된 사람 hello 모니터링 참가자 역할 수는 구독에서 모든 모니터링 데이터를 볼 만들기는 또는 모니터링 설정을 수정 하지만 다른 모든 리소스를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-131">People assigned hello Monitoring Contributor role can view all monitoring data in a subscription and create or modify monitoring settings, but cannot modify any other resources.</span></span> <span data-ttu-id="4f6ee-132">이 역할 hello 모니터링 읽기 역할의 상위 집합 인지 그리고 조직 모니터링 팀 또는 또한 toohello 필요한 사용 권한은 위의 toobe 수 하는 관리 되는 서비스 공급자의 여러 멤버에 대 한 적절 한:</span><span class="sxs-lookup"><span data-stu-id="4f6ee-132">This role is a superset of hello Monitoring Reader role, and is appropriate for members of an organization’s monitoring team or managed service providers who, in addition toohello permissions above, also need toobe able to:</span></span>

* <span data-ttu-id="4f6ee-133">공유 대시보드로 모니터링 대시보드를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-133">Publish monitoring dashboards as a shared dashboard.</span></span>
* <span data-ttu-id="4f6ee-134">리소스에 대한 [진단 설정](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) 을 구성합니다.*</span><span class="sxs-lookup"><span data-stu-id="4f6ee-134">Set [diagnostic settings](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) for a resource.*</span></span>
* <span data-ttu-id="4f6ee-135">집합 hello [프로필 로그](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) 는 subscription.*에 대 한</span><span class="sxs-lookup"><span data-stu-id="4f6ee-135">Set hello [log profile](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) for a subscription.*</span></span>
* <span data-ttu-id="4f6ee-136">경고 활동 및 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-136">Set alert activity and settings.</span></span>
* <span data-ttu-id="4f6ee-137">Application Insights 웹 테스트 및 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-137">Create Application Insights web tests and components.</span></span>
* <span data-ttu-id="4f6ee-138">Log Analytics(OMS) 작업 공간 공유 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-138">List Log Analytics (OMS) workspace shared keys.</span></span>
* <span data-ttu-id="4f6ee-139">Log Analytics(OMS) 인텔리전스 팩을 사용하거나 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-139">Enable or disable Log Analytics (OMS) intelligence packs.</span></span>
* <span data-ttu-id="4f6ee-140">Log Analytics(OMS) 저장된 검색을 만들고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-140">Create and delete and execute Log Analytics (OMS) saved searches.</span></span>
* <span data-ttu-id="4f6ee-141">만들고 hello 로그 분석 (OMS) 저장소 구성을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-141">Create and delete hello Log Analytics (OMS) storage configuration.</span></span>

<span data-ttu-id="4f6ee-142">* 또한 별도로 사용자 hello 대상 리소스 (저장소 계정 또는 이벤트 허브 네임 스페이스) tooset 로그 프로필 또는 진단 설정에 대 한 Listkey 권한이 부여 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-142">*user must also separately be granted ListKeys permission on hello target resource (storage account or event hub namespace) tooset a log profile or diagnostic setting.</span></span>

> [!NOTE]
> <span data-ttu-id="4f6ee-143">이 역할에서 저장소 계정에 저장 또는 스트리밍된 tooan 이벤트 허브 된 toolog 데이터 읽기 액세스를 부여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-143">This role does not give read access toolog data that has been streamed tooan event hub or stored in a storage account.</span></span> <span data-ttu-id="4f6ee-144">[아래 참조](#security-considerations-for-monitoring-data) toothese 리소스에 액세스를 구성 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-144">[See below](#security-considerations-for-monitoring-data) for information on configuring access toothese resources.</span></span>
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a><span data-ttu-id="4f6ee-145">권한 및 사용자 지정 RBAC 역할 모니터링</span><span class="sxs-lookup"><span data-stu-id="4f6ee-145">Monitoring permissions and custom RBAC roles</span></span>
<span data-ttu-id="4f6ee-146">기본 제공 역할 위에 hello 팀의 정확한 요구 hello 없으면 다음을 할 수 있습니다 [사용자 지정 RBAC 역할](../active-directory/role-based-access-control-custom-roles.md) 보다 세부적인 권한을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-146">If hello above built-in roles don’t meet hello exact needs of your team, you can [create a custom RBAC role](../active-directory/role-based-access-control-custom-roles.md) with more granular permissions.</span></span> <span data-ttu-id="4f6ee-147">일반적인 Azure 모니터 RBAC 작업과 해당 설명을 보려면 hello는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-147">Below are hello common Azure Monitor RBAC operations with their descriptions.</span></span>

| <span data-ttu-id="4f6ee-148">작업</span><span class="sxs-lookup"><span data-stu-id="4f6ee-148">Operation</span></span> | <span data-ttu-id="4f6ee-149">설명</span><span class="sxs-lookup"><span data-stu-id="4f6ee-149">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4f6ee-150">Microsoft.Insights/AlertRules/[Read, Write, Delete]</span><span class="sxs-lookup"><span data-stu-id="4f6ee-150">Microsoft.Insights/AlertRules/[Read, Write, Delete]</span></span> |<span data-ttu-id="4f6ee-151">경고 규칙 읽기/쓰기/삭제</span><span class="sxs-lookup"><span data-stu-id="4f6ee-151">Read/write/delete alert rules.</span></span> |
| <span data-ttu-id="4f6ee-152">Microsoft.Insights/AlertRules/Incidents/Read</span><span class="sxs-lookup"><span data-stu-id="4f6ee-152">Microsoft.Insights/AlertRules/Incidents/Read</span></span> |<span data-ttu-id="4f6ee-153">경고 규칙에 대 한 인시던트 (트리거된 hello 경고 규칙의 기록)를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-153">List incidents (history of hello alert rule being triggered) for alert rules.</span></span> <span data-ttu-id="4f6ee-154">이 toohello 포털만을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-154">This only applies toohello portal.</span></span> |
| <span data-ttu-id="4f6ee-155">Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete]</span><span class="sxs-lookup"><span data-stu-id="4f6ee-155">Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="4f6ee-156">자동 크기 조정 설정 읽기/쓰기/삭제</span><span class="sxs-lookup"><span data-stu-id="4f6ee-156">Read/write/delete autoscale settings.</span></span> |
| <span data-ttu-id="4f6ee-157">Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete]</span><span class="sxs-lookup"><span data-stu-id="4f6ee-157">Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete]</span></span> |<span data-ttu-id="4f6ee-158">진단 설정 읽기/쓰기/삭제</span><span class="sxs-lookup"><span data-stu-id="4f6ee-158">Read/write/delete diagnostic settings.</span></span> |
| <span data-ttu-id="4f6ee-159">Microsoft.Insights/eventtypes/digestevents/Read</span><span class="sxs-lookup"><span data-stu-id="4f6ee-159">Microsoft.Insights/eventtypes/digestevents/Read</span></span> |<span data-ttu-id="4f6ee-160">이 권한은 tooActivity 로그 hello 포털을 통해 액세스 해야 하는 사용자에 대 한 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-160">This permission is necessary for users who need access tooActivity Logs via hello portal.</span></span> |
| <span data-ttu-id="4f6ee-161">Microsoft.Insights/eventtypes/values/Read</span><span class="sxs-lookup"><span data-stu-id="4f6ee-161">Microsoft.Insights/eventtypes/values/Read</span></span> |<span data-ttu-id="4f6ee-162">구독에서 활동 로그 이벤트(관리 이벤트)를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-162">List Activity Log events (management events) in a subscription.</span></span> <span data-ttu-id="4f6ee-163">이 권한은 해당 tooboth 프로그래밍 및 포털 액세스 toohello 활동 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-163">This permission is applicable tooboth programmatic and portal access toohello Activity Log.</span></span> |
| <span data-ttu-id="4f6ee-164">Microsoft.Insights/LogDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="4f6ee-164">Microsoft.Insights/LogDefinitions/Read</span></span> |<span data-ttu-id="4f6ee-165">이 권한은 tooActivity 로그 hello 포털을 통해 액세스 해야 하는 사용자에 대 한 필요한입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-165">This permission is necessary for users who need access tooActivity Logs via hello portal.</span></span> |
| <span data-ttu-id="4f6ee-166">Microsoft.Insights/MetricDefinitions/Read</span><span class="sxs-lookup"><span data-stu-id="4f6ee-166">Microsoft.Insights/MetricDefinitions/Read</span></span> |<span data-ttu-id="4f6ee-167">메트릭 정의(리소스에 사용 가능한 메트릭 형식 목록)를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-167">Read metric definitions (list of available metric types for a resource).</span></span> |
| <span data-ttu-id="4f6ee-168">Microsoft.Insights/Metrics/Read</span><span class="sxs-lookup"><span data-stu-id="4f6ee-168">Microsoft.Insights/Metrics/Read</span></span> |<span data-ttu-id="4f6ee-169">리소스에 대한 메트릭을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-169">Read metrics for a resource.</span></span> |

> [!NOTE]
> <span data-ttu-id="4f6ee-170">액세스 tooalerts, 진단 설정 및 리소스에 대 한 메트릭을 해당 hello 사용자에 대 한 읽기 액세스 toohello 리소스 종류 및 해당 리소스의 범위를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-170">Access tooalerts, diagnostic settings, and metrics for a resource requires that hello user has Read access toohello resource type and scope of that resource.</span></span> <span data-ttu-id="4f6ee-171">("쓰기")을 만드는 아카이브 tooa 저장소 계정 또는 스트림 tooevent 허브 hello 사용자 tooalso 필요 하다는 진단 설정 또는 로그 프로필 Listkey에 권한이 hello 대상 리소스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-171">Creating (“write”) a diagnostic setting or log profile that archives tooa storage account or streams tooevent hubs requires hello user tooalso have ListKeys permission on hello target resource.</span></span>
> 
> 

<span data-ttu-id="4f6ee-172">예를 들어 테이블 위에 hello를 사용 하 여 만들 수 있습니다는 사용자 지정 RBAC 역할 판독기에 대 한"활동 로그" 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="4f6ee-172">For example, using hello above table you could create a custom RBAC role for an “Activity Log Reader” like this:</span></span>

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

## <a name="security-considerations-for-monitoring-data"></a><span data-ttu-id="4f6ee-173">모니터링 데이터에 대한 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="4f6ee-173">Security considerations for monitoring data</span></span>
<span data-ttu-id="4f6ee-174">모니터링 데이터, 특히 로그 파일에는 IP 주소나 사용자 이름 같은 중요 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-174">Monitoring data—particularly log files—can contain sensitive information, such as IP addresses or user names.</span></span> <span data-ttu-id="4f6ee-175">Azure의 모니터링 데이터는 다음 3가지 기본 형태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-175">Monitoring data from Azure comes in three basic forms:</span></span>

1. <span data-ttu-id="4f6ee-176">Azure 구독에서 모든 제어 평면 작업을 설명 하는 활동 로그 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-176">hello Activity Log, which describes all control-plane actions on your Azure subscription.</span></span>
2. <span data-ttu-id="4f6ee-177">진단 로그. 리소스가 내보낸 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-177">Diagnostic Logs, which are logs emitted by a resource.</span></span>
3. <span data-ttu-id="4f6ee-178">메트릭. 리소스가 내보낸 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-178">Metrics, which are emitted by resources.</span></span>

<span data-ttu-id="4f6ee-179">이러한 데이터 형식의 세 가지 모두 저장소 계정에 저장할 수 있습니다 또는 범용 Azure 리소스는 둘 다 허브 tooEvent 스트리밍.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-179">All three of these data types can be stored in a storage account or streamed tooEvent Hub, both of which are general-purpose Azure resources.</span></span> <span data-ttu-id="4f6ee-180">범용 리소스이기 때문에 이 항목의 만들기, 삭제 및 액세스는 권한이 필요한 작업이며 일반적으로 관리자에게 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-180">Because these are general-purpose resources, creating, deleting, and accessing them is a privileged operation usually reserved for an administrator.</span></span> <span data-ttu-id="4f6ee-181">모니터링 관련 리소스 tooprevent 오용 사례 hello를 사용 하는 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-181">We suggest that you use hello following practices for monitoring-related resources tooprevent misuse:</span></span>

* <span data-ttu-id="4f6ee-182">모니터링 데이터에는 단일 전용 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-182">Use a single, dedicated storage account for monitoring data.</span></span> <span data-ttu-id="4f6ee-183">Tooseparate 모니터링 데이터를 여러 저장소 계정에 필요한 경우 모니터링 간의 저장소 계정 사용을 공유 하지 않습니다 이며이 아닌 모니터링 데이터만 toomonitoring 데이터 (예: 액세스 해야 하는 사용자를 제공할 실수로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-183">If you need tooseparate monitoring data into multiple storage accounts, never share usage of a storage account between monitoring and non-monitoring data, as this may inadvertently give those who only need access toomonitoring data (eg.</span></span> <span data-ttu-id="4f6ee-184">제 3 자 SIEM) toonon 모니터링 데이터에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-184">a third-party SIEM) access toonon-monitoring data.</span></span>
* <span data-ttu-id="4f6ee-185">위와 같은 이유로 hello에 대 한 모든 진단 설정에서 단일, 전용 서비스 버스 또는 이벤트 허브 네임 스페이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-185">Use a single, dedicated Service Bus or Event Hub namespace across all diagnostic settings for hello same reason as above.</span></span>
* <span data-ttu-id="4f6ee-186">별도 리소스 그룹에 보관 하면 액세스 toomonitoring와 관련 된 저장소 계정 또는 이벤트 허브를 제한 하 고 [범위를 사용 하 여](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) 모니터링 역할 toolimit 액세스할 tooonly 해당 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-186">Limit access toomonitoring-related storage accounts or event hubs by keeping them in a separate resource group, and [use scope](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) on your monitoring roles toolimit access tooonly that resource group.</span></span>
* <span data-ttu-id="4f6ee-187">사용자에만 toomonitoring 데이터에 액세스 해야 하는 경우 저장소 계정 또는 구독 범위에서 이벤트 허브에 대 한 hello Listkey 권한을 부여 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-187">Never grant hello ListKeys permission for either storage accounts or event hubs at subscription scope when a user only needs access toomonitoring data.</span></span> <span data-ttu-id="4f6ee-188">(있는 경우 전용된 모니터링 리소스 그룹) 리소스 또는 리소스 그룹에 이러한 사용 권한을 toohello 사용자를 대신 제공 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-188">Instead, give these permissions toohello user at a resource or resource group (if you have a dedicated monitoring resource group) scope.</span></span>

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a><span data-ttu-id="4f6ee-189">Toomonitoring와 관련 된 저장소 계정 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-189">Limiting access toomonitoring-related storage accounts</span></span>
<span data-ttu-id="4f6ee-190">사용자 또는 응용 프로그램 저장소 계정에 toomonitoring 데이터에 액세스 해야 하는 경우 수행 해야 [계정 SAS를 생성할](https://msdn.microsoft.com/library/azure/mt584140.aspx) tooblob 저장소 서비스 수준 읽기 전용 액세스를 사용 하 여 모니터링 데이터를 포함 하는 hello 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-190">When a user or application needs access toomonitoring data in a storage account, you should [generate an Account SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) on hello storage account that contains monitoring data with service-level read-only access tooblob storage.</span></span> <span data-ttu-id="4f6ee-191">PowerShell에서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-191">In PowerShell, this might look like:</span></span>

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

<span data-ttu-id="4f6ee-192">그런 다음 해당 저장소 계정에서 tooread 필요한 hello 토큰 toohello 엔터티를 제공할 수 있습니다 및 나열 하 고 해당 저장소 계정에서 모든 blob에서 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-192">You can then give hello token toohello entity that needs tooread from that storage account, and it can list and read from all blobs in that storage account.</span></span>

<span data-ttu-id="4f6ee-193">또는이 사용 권한은 RBAC와 toocontrol 해야 할 경우 해당 엔터티 hello 해당 특정 저장소 계정에서 Microsoft.Storage/storageAccounts/listkeys/action 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-193">Alternatively, if you need toocontrol this permission with RBAC, you can grant that entity hello Microsoft.Storage/storageAccounts/listkeys/action permission on that particular storage account.</span></span> <span data-ttu-id="4f6ee-194">이 작업이 toobe 수 tooset 진단 설정 또는 로그 프로필 tooarchive tooa 저장소 계정에 게 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-194">This is necessary for users who need toobe able tooset a diagnostic setting or log profile tooarchive tooa storage account.</span></span> <span data-ttu-id="4f6ee-195">예를 들어 다음 사용자 또는 한 저장소 계정에서 tooread만 하면 되는 응용 프로그램에 대 한 사용자 지정 RBAC 역할 hello를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-195">For example, you could create hello following custom RBAC role for a user or application that only needs tooread from one storage account:</span></span>

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> <span data-ttu-id="4f6ee-196">hello Listkey 권한 hello 사용자 toolist hello 기본 및 보조 저장소 계정 키를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-196">hello ListKeys permission enables hello user toolist hello primary and secondary storage account keys.</span></span> <span data-ttu-id="4f6ee-197">이러한 키를 사용자에 게 부여 hello 서명 된 모든 사용 권한 (읽기, 쓰기, blob 만들기, 삭제 blob 등)에 모든 해당 저장소 계정에서 서비스 (blob, 큐, 테이블, 파일)을 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-197">These keys grant hello user all signed permissions (read, write, create blobs, delete blobs, etc.) across all signed services (blob, queue, table, file) in that storage account.</span></span> <span data-ttu-id="4f6ee-198">가능한 경우 위에서 설명한 계정 SAS를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-198">We recommend using an Account SAS described above when possible.</span></span>
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a><span data-ttu-id="4f6ee-199">액세스 toomonitoring 관련 이벤트 허브를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-199">Limiting access toomonitoring-related event hubs</span></span>
<span data-ttu-id="4f6ee-200">이벤트 허브는 유사한 패턴을 줄 수 있지만 toocreate 전용된 수신 권한 부여 규칙을 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-200">A similar pattern can be followed with event hubs, but first you need toocreate a dedicated Listen authorization rule.</span></span> <span data-ttu-id="4f6ee-201">Toolisten toomonitoring 관련 이벤트 허브는 toogrant access tooan 응용 프로그램을 사용 하도록 하려는 경우 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-201">If you want toogrant access tooan application that only needs toolisten toomonitoring-related event hubs, do hello following:</span></span>

1. <span data-ttu-id="4f6ee-202">Listen 클레임만을 사용 하 여 모니터링 데이터를 스트리밍에 대 한 생성 된 hello 이벤트 허브에서 공유 액세스 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-202">Create a shared access policy on hello event hub(s) that were created for streaming monitoring data with only Listen claims.</span></span> <span data-ttu-id="4f6ee-203">Hello 포털에서이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-203">This can be done in hello portal.</span></span> <span data-ttu-id="4f6ee-204">예를 들어, 이 정책을 “monitoringReadOnly”라고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-204">For example, you might call it “monitoringReadOnly.”</span></span> <span data-ttu-id="4f6ee-205">가능 하면 toogive hello 다음 단계를 건너뛰고 toohello 소비자 키 직접를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-205">If possible, you will want toogive that key directly toohello consumer and skip hello next step.</span></span>
2. <span data-ttu-id="4f6ee-206">Hello 소비자 toobe 수 tooget hello 키 임시 경우, 해당 이벤트 허브에 대 한 hello 사용자 hello Listkey 작업 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-206">If hello consumer needs toobe able tooget hello key ad-hoc, grant hello user hello ListKeys action for that event hub.</span></span> <span data-ttu-id="4f6ee-207">사용자에 게 필요한 toobe 수 tooset 진단 설정 또는 프로필 toostream tooevent 허브 로그에 필요한 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-207">This is also necessary for users who need toobe able tooset a diagnostic setting or log profile toostream tooevent hubs.</span></span> <span data-ttu-id="4f6ee-208">예를 들어, RBAC 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f6ee-208">For example, you might create an RBAC rule:</span></span>
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a><span data-ttu-id="4f6ee-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f6ee-209">Next steps</span></span>
* [<span data-ttu-id="4f6ee-210">Resource Manager의 RBAC 및 권한에 대해 읽기</span><span class="sxs-lookup"><span data-stu-id="4f6ee-210">Read about RBAC and permissions in Resource Manager</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="4f6ee-211">Azure에서 모니터링 읽기 hello 개요</span><span class="sxs-lookup"><span data-stu-id="4f6ee-211">Read hello overview of monitoring in Azure</span></span>](monitoring-overview.md)

