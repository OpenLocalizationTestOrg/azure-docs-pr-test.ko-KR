---
title: "Azure Virtual Machines를 사용한 고급 자동 크기 조정 | Microsoft Docs"
description: "크기 조정 작업에 대한 전자 메일을 전송하고 웹후크 URL을 호출하는 여러 규칙 및 프로필에 Resource Manager 및 VM Scale Sets를 사용합니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="d76fd-103">Resource Manager 템플릿을 사용하여 VM Scale Sets에 대한 고급 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="d76fd-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="d76fd-104">되풀이 일정 또는 특정 날짜에 성능 메트릭 임계값을 기반으로 가상 컴퓨터 확장 집합의 규모를 확장 및 감축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="d76fd-105">또한 크기 조정 동작에 대한 전자 메일 및 웹후크 알림을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="d76fd-106">이 연습에서는 VM 확장 집합에서 Resource Manager 템플릿을 사용하여 이 모든 개체를 구성하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="d76fd-107">이 연습에서는 VM Scale Sets에 대한 단계를 설명하지만 동일한 정보가 [Cloud Services](https://azure.microsoft.com/services/cloud-services/) 및 [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/) 자동 크기 조정에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="d76fd-108">CPU와 같은 간단한 성능 메트릭을 기반으로 VM 확장 집합에 대한 간단한 규모 감축/확장 설정을 지정하려면 [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) 및 [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="d76fd-109">연습</span><span class="sxs-lookup"><span data-stu-id="d76fd-109">Walkthrough</span></span>
<span data-ttu-id="d76fd-110">이 연습에서는 [Azure 리소스 탐색기](https://resources.azure.com/)를 사용하여 확장 집합에 대한 자동 크기 조정 설정을 구성 및 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="d76fd-111">Azure 리소스 탐색기는 Resource Manager 템플릿을 통해 Azure 리소스를 관리하는 간편한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="d76fd-112">Azure 리소스 탐색기 도구를 처음 접하는 경우 [이 소개](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/)를 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="d76fd-113">기본 자동 크기 조정 설정으로 새 규모 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="d76fd-114">이 문서에서는 기본 자동 크기 조정 템플릿과 함께 Azure 빠른 시작 갤러리에 있는 Windows 규모 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="d76fd-115">Linux 규모 집합도 동일한 방식으로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="d76fd-116">규모 집합을 만든 후 Azure 리소스 탐색기에서 규모 집합 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="d76fd-117">Microsoft.Insights 노드 아래에 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="d76fd-119">템플릿 실행을 통해 **'autoscalewad'**라는 기본 자동 크기 조정 설정이 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="d76fd-120">오른쪽에서 이 자동 크기 조정 설정의 전체 정의를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="d76fd-121">이 예에서 기본 자동 크기 조정 설정은 CPU% 기반의 규모 확장 및 규모 축소 규칙과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="d76fd-122">이제 일정 또는 특정 요구 사항에 따라 프로필 및 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="d76fd-123">3개의 프로필로 자동 크기 조정 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="d76fd-124">자동 크기 조정의 프로필 및 규칙을 이해하려면 [자동 크기 조정 모범 사례](insights-autoscale-best-practices.md)를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="d76fd-125">프로필 및 규칙</span><span class="sxs-lookup"><span data-stu-id="d76fd-125">Profiles & Rules</span></span> | <span data-ttu-id="d76fd-126">설명</span><span class="sxs-lookup"><span data-stu-id="d76fd-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="d76fd-127">**프로필**</span><span class="sxs-lookup"><span data-stu-id="d76fd-127">**Profile**</span></span> |<span data-ttu-id="d76fd-128">**성능/메트릭 기반**</span><span class="sxs-lookup"><span data-stu-id="d76fd-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="d76fd-129">규칙</span><span class="sxs-lookup"><span data-stu-id="d76fd-129">Rule</span></span> |<span data-ttu-id="d76fd-130">서비스 버스 큐 메시지 수 > x</span><span class="sxs-lookup"><span data-stu-id="d76fd-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="d76fd-131">규칙</span><span class="sxs-lookup"><span data-stu-id="d76fd-131">Rule</span></span> |<span data-ttu-id="d76fd-132">서비스 버스 큐 메시지 수 < y</span><span class="sxs-lookup"><span data-stu-id="d76fd-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="d76fd-133">규칙</span><span class="sxs-lookup"><span data-stu-id="d76fd-133">Rule</span></span> |<span data-ttu-id="d76fd-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="d76fd-134">CPU% > n</span></span> |
    | <span data-ttu-id="d76fd-135">규칙</span><span class="sxs-lookup"><span data-stu-id="d76fd-135">Rule</span></span> |<span data-ttu-id="d76fd-136">CPU% < p</span><span class="sxs-lookup"><span data-stu-id="d76fd-136">CPU% < p</span></span> |
    | <span data-ttu-id="d76fd-137">**프로필**</span><span class="sxs-lookup"><span data-stu-id="d76fd-137">**Profile**</span></span> |<span data-ttu-id="d76fd-138">**평일 오전 시간(규칙 없음)**</span><span class="sxs-lookup"><span data-stu-id="d76fd-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="d76fd-139">**프로필**</span><span class="sxs-lookup"><span data-stu-id="d76fd-139">**Profile**</span></span> |<span data-ttu-id="d76fd-140">**제품 출시일(규칙 없음)**</span><span class="sxs-lookup"><span data-stu-id="d76fd-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="d76fd-141">이 연습에 사용할 가상의 크기 조정 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="d76fd-142">**부하 기반** - 확장 집합에서 호스트되는 응용 프로그램의 부하에 따라 규모를 확장하거나 감축합니다.*</span><span class="sxs-lookup"><span data-stu-id="d76fd-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="d76fd-143">**메시지 큐 크기** - 응용 프로그램으로 들어오는 메시지에 Service Bus 큐를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="d76fd-144">큐의 메시지 수 및 CPU%를 사용하고, 메시지 수 또는 CPU가 임계값에 도달한 경우 크기 조정 동작을 트리거하도록 기본 프로필을 구성합니다.*</span><span class="sxs-lookup"><span data-stu-id="d76fd-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="d76fd-145">**요일과 시간** - '평일 오전 시간'이라는 매주 되풀이되는 '시간' 기반 프로필을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="d76fd-146">기록 데이터에 따라 이 시간 동안 특정 개수의 VM 인스턴스에서 응용 프로그램의 부하를 처리하도록 하는 것이 보다 효율적이라는 것을 알고 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="d76fd-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="d76fd-147">**특정 날짜** - '제품 출시일' 프로필을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="d76fd-148">응용 프로그램이 마케팅 공지 사항으로 인한 부하 및 응용 프로그램에 새 제품이 추가될 경우의 부하를 처리할 준비를 갖추도록 특정 날짜를 미리 계획합니다.*</span><span class="sxs-lookup"><span data-stu-id="d76fd-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="d76fd-149">*마지막 두 프로필 내에도 다른 성능 메트릭 기반 규칙이 있을 수 있습니다. 이 경우 성능 메트릭 기반 규칙을 하나만 유지할 필요가 없으며, 기본 성능 메트릭 기반 규칙에 의존할 수 있습니다. 되풀이 및 날짜 기반 프로필의 경우에는 규칙이 선택 사항입니다.*</span><span class="sxs-lookup"><span data-stu-id="d76fd-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="d76fd-150">프로필 및 규칙에 대한 자동 크기 조정 엔진의 우선 순위 지정은 [자동 크기 조정 모범 사례](insights-autoscale-best-practices.md) 문서에도 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="d76fd-151">자동 크기 조정에 대한 공통 메트릭 목록은 [자동 크기 조정에 대한 공통 메트릭](insights-autoscale-common-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="d76fd-152">리소스 탐색기에서 **읽기/쓰기** 모드에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, 기본 자동 크기 조정 설정](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="d76fd-154">편집을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-154">Click Edit.</span></span> <span data-ttu-id="d76fd-155">자동 크기 조정 설정의 '프로필' 요소를 다음 구성으로 **대체**합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

    ![프로필](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="d76fd-157">지원되는 필드와 해당 값은 [자동 크기 조정 REST API 설명서](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="d76fd-158">이제 자동 크기 조정 설정에 이전에 설명한 3개의 프로필이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="d76fd-159">마지막으로 자동 크기 조정 **알림** 섹션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="d76fd-160">규모 확장 또는 축소 동작이 성공적으로 트리거된 경우 자동 크기 조정 알림을 통해 세 가지 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="d76fd-161">구독의 관리자와 공동 관리자에게 알림</span><span class="sxs-lookup"><span data-stu-id="d76fd-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="d76fd-162">사용자 집합에 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="d76fd-162">Email a set of users</span></span>
   - <span data-ttu-id="d76fd-163">웹후크 호출 트리거.</span><span class="sxs-lookup"><span data-stu-id="d76fd-163">Trigger a webhook call.</span></span> <span data-ttu-id="d76fd-164">실행된 경우 이 웹후크는 자동 크기 조정 조건 및 규칙 집합 리소스에 대한 메타데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="d76fd-165">자동 크기 조정 webhook의 페이로드에 대한 자세한 내용은 [자동 크기 조정의 Webhook 및 메일 알림 구성](insights-autoscale-to-webhook-email.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="d76fd-166">해당 값이 null인 **notification** 요소를 대체하여 자동 크기 조정 설정에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   <span data-ttu-id="d76fd-167">리소스 탐색기에서 **배치** 단추를 눌러 자동 크기 조정 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="d76fd-168">여러 크기 조정 프로필 및 크기 조정 알림을 포함하도록 VM 확장 집합에 대한 자동 크기 조정 설정을 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="d76fd-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d76fd-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d76fd-169">Next Steps</span></span>
<span data-ttu-id="d76fd-170">자동 크기 조정에 대해 자세히 알아보려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d76fd-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="d76fd-171">가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d76fd-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="d76fd-172">자동 크기 조정에 대한 공통 메트릭</span><span class="sxs-lookup"><span data-stu-id="d76fd-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="d76fd-173">Azure 자동 크기 조정에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="d76fd-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="d76fd-174">PowerShell을 사용하여 자동 크기 조정 관리</span><span class="sxs-lookup"><span data-stu-id="d76fd-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="d76fd-175">CLI를 사용하여 자동 크기 조정 관리</span><span class="sxs-lookup"><span data-stu-id="d76fd-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="d76fd-176">자동 크기 조정의 Webhook 및 메일 알림 구성</span><span class="sxs-lookup"><span data-stu-id="d76fd-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
