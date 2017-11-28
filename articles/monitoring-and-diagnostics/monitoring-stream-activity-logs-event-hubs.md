---
title: "Azure 활동 로그를 이벤트 허브로 스트림 | Microsoft Docs"
description: "Azure 활동 로그를 이벤트 허브로 스트림하는 방법에 대해 알아봅니다."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="7483b-103">Azure 활동 로그를 이벤트 허브로 스트림</span><span class="sxs-lookup"><span data-stu-id="7483b-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="7483b-104">포털에서 기본 제공 "내보내기" 옵션을 사용하거나 Azure PowerShell Cmdlet 또는 Azure CLI를 통해 로그 프로필에서 Service Bus 규칙 ID를 사용하도록 설정하여 [**Azure 활동 로그**](monitoring-overview-activity-logs.md)를 거의 실시간으로 응용 프로그램에 스트림할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="7483b-105">활동 로그 및 이벤트 허브에서 수행할 수 있는 작업</span><span class="sxs-lookup"><span data-stu-id="7483b-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="7483b-106">활동 로그의 스트리밍 기능을 사용할 수 있는 몇 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="7483b-107">**타사 로깅 및 원격 분석 시스템으로 스트림** – 시간이 지나면서 이벤트 허브 스트리밍은 활동 로그를 타사 SIEM 및 로그 분석 솔루션으로 파이핑하기 위한 메커니즘이 되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="7483b-108">**사용자 지정 원격 분석 및 로깅 플랫폼 빌드** – 사용자 지정 빌드 원격 분석 플랫폼이 이미 있거나 플랫폼 빌드에 대해 생각하고 있는 경우 이벤트 허브의 확장성 높은 게시-구독 특성을 통해 활동 로그를 유연하게 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="7483b-109">글로벌 확장 원격 분석 플랫폼에 이벤트 허브 사용에 대해서는 여기 Dan Rosanova의 가이드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7483b-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="7483b-110">활동 로그의 스트리밍 사용</span><span class="sxs-lookup"><span data-stu-id="7483b-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="7483b-111">프로그래밍 방식이나 포털을 통해 활동 로그의 스트리밍을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="7483b-112">어떤 방법으로든 Service Bus 네임스페이스와 네임스페이스에 대한 공유 액세스 정책을 선택하면 처음으로 새로운 활동 로그 이벤트가 발생하면 이 네임스페이스에 Event Hub가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="7483b-113">Service Bus 네임스페이스가 없는 경우 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="7483b-114">이전에 활동 로그 이벤트를 이 Service Bus 네임스페이스로 스트리밍한 경우 이전에 만든 Event Hub를 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="7483b-115">공유 액세스 정책은 스트리밍 메커니즘에서 보유하는 권한을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="7483b-116">현재, 이벤트 허브로 스트리밍하려면 **관리**, **보내기** 및 **수신** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="7483b-117">클래식 포털에서 서비스 버스 네임스페이스에 대한 "구성" 탭 아래에서 서비스 버스 네임스페이스 공유 액세스 정책을 만들거나 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="7483b-118">스트리밍을 포함할 활동 로그 로그 프로필을 업데이트하려면 변경하는 사용자에게 Service Bus 권한 부여 규칙에 대한 ListKey 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="7483b-119">설정을 구성하는 사용자가 두 구독에 대한 적절한 RBAC 액세스를 가진 경우 서비스 버스 또는 이벤트 허브 네임스페이스는 로그를 내보내는 구독과 동일한 구독을 가지고 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="7483b-120">Azure 포털을 통해</span><span class="sxs-lookup"><span data-stu-id="7483b-120">Via Azure portal</span></span>
1. <span data-ttu-id="7483b-121">포털 왼쪽에 있는 메뉴를 사용하여 **활동 로그** 블레이드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![포털에서 활동 로그로 이동](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="7483b-123">블레이드 맨 위에서 **내보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![포털에서 내보내기 단추](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="7483b-125">표시되는 블레이드에서 이벤트를 스트림할 지역, 이러한 이벤트를 스트리밍하기 위해 이벤트 허브를 생성할 서비스 버스 네임스페이스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![활동 로그 내보내기 블레이드](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="7483b-127">**저장**을 클릭하여 이러한 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="7483b-128">해당 설정이 구독에 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="7483b-129">PowerShell Cmdlet을 통해</span><span class="sxs-lookup"><span data-stu-id="7483b-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="7483b-130">로그 프로필이 이미 있는 경우 먼저 해당 프로필을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="7483b-131">`Get-AzureRmLogProfile` 를 사용하여 로그 프로필이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="7483b-132">있는 경우 `Remove-AzureRmLogProfile` 를 사용하여 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="7483b-133">`Set-AzureRmLogProfile` 을 사용하여 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="7483b-134">서비스 버스 규칙 ID는 예를 들어, {service bus resource ID}/authorizationrules/{key name} 형식의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="7483b-135">Azure CLI를 통해</span><span class="sxs-lookup"><span data-stu-id="7483b-135">Via Azure CLI</span></span>
<span data-ttu-id="7483b-136">로그 프로필이 이미 있는 경우 먼저 해당 프로필을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="7483b-137">`azure insights logprofile list` 를 사용하여 로그 프로필이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="7483b-138">있는 경우 `azure insights logprofile delete` 를 사용하여 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="7483b-139">`azure insights logprofile add` 을 사용하여 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="7483b-140">서비스 버스 규칙 ID는 `{service bus resource ID}/authorizationrules/{key name}`형식의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="7483b-141">이벤트 허브에서 로그 데이터를 사용하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="7483b-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="7483b-142">[여기에서 활동 로그에 대한 스키마를 사용할 수 있습니다](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7483b-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="7483b-143">각 이벤트는 "레코드"라는 JSON Blob 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="7483b-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="7483b-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7483b-144">Next Steps</span></span>
* [<span data-ttu-id="7483b-145">저장소 계정에 활동 로그 보관</span><span class="sxs-lookup"><span data-stu-id="7483b-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="7483b-146">Azure 활동 로그 개요 알아보기</span><span class="sxs-lookup"><span data-stu-id="7483b-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="7483b-147">활동 로그 이벤트를 기반으로 경고 설정</span><span class="sxs-lookup"><span data-stu-id="7483b-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

