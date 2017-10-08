---
title: "Azure 가상 컴퓨터를 사용 하 여 자동 크기 조정 aaaAdvanced | Microsoft Docs"
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
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="dfc6c-103">Resource Manager 템플릿을 사용하여 VM Scale Sets에 대한 고급 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="dfc6c-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="dfc6c-104">되풀이 일정 또는 특정 날짜에 성능 메트릭 임계값을 기반으로 가상 컴퓨터 확장 집합의 규모를 확장 및 감축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="dfc6c-105">또한 크기 조정 동작에 대한 전자 메일 및 웹후크 알림을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="dfc6c-106">이 연습에서는 VM 확장 집합에서 Resource Manager 템플릿을 사용하여 이 모든 개체를 구성하는 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="dfc6c-107">VM 크기 집합에 대 한 hello 단계를 설명 하는이 연습에서는, 동안 hello 동일한 정보 적용 tooautoscaling [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="dfc6c-108">CPU와 같은 간단한 성능 메트릭에 기반으로 하는 간단한 소수/VM 크기 집합에 대 한 설정을, 참조 toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) 및 [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) 문서</span><span class="sxs-lookup"><span data-stu-id="dfc6c-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="dfc6c-109">연습</span><span class="sxs-lookup"><span data-stu-id="dfc6c-109">Walkthrough</span></span>
<span data-ttu-id="dfc6c-110">이 연습을 사용 하 여 [Azure 리소스 탐색기](https://resources.azure.com/) 크기 집합에 대 한 hello 자동 크기 조정 설정 tooconfigure 및 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="dfc6c-111">Azure 리소스 탐색기는 쉽게 toomanage 리소스 관리자 템플릿을 통해 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="dfc6c-112">새로운 tooAzure 리소스 탐색기 도구 인 경우 읽기 [이 소개](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="dfc6c-113">기본 자동 크기 조정 설정으로 새 규모 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="dfc6c-114">이 문서에서는 windows Azure 빠른 시작 갤러리 hello에서 hello 하나 표시줄이 기본 자동 크기 조정 템플릿을 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="dfc6c-115">Linux 배율 설정 작업 hello 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="dfc6c-116">Hello 크기 집합을 만든 후 Azure 리소스 탐색기에서 toohello 눈금 집합 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="dfc6c-117">Hello 다음 Microsoft.Insights 노드에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="dfc6c-119">hello 템플릿 실행 hello 이름의 기본 자동 크기 조정 설정을 만들었습니다 **'autoscalewad'**합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="dfc6c-120">Hello 오른쪽에 hello이 자동 크기 조정 설정의 전체 정의 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="dfc6c-121">이 경우 hello 기본 자동 크기 조정 설정 CPU % 기반 확장 및 확장의 규칙 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="dfc6c-122">이제 추가 프로필 및 hello 일정 또는 특정 요구 사항에 따라 규칙을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="dfc6c-123">3개의 프로필로 자동 크기 조정 설정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="dfc6c-124">toounderstand 프로필과의 자동 크기 조정 규칙 검토 [자동 크기 조정에 대 한 유용한 정보](insights-autoscale-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="dfc6c-125">프로필 및 규칙</span><span class="sxs-lookup"><span data-stu-id="dfc6c-125">Profiles & Rules</span></span> | <span data-ttu-id="dfc6c-126">설명</span><span class="sxs-lookup"><span data-stu-id="dfc6c-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="dfc6c-127">**프로필**</span><span class="sxs-lookup"><span data-stu-id="dfc6c-127">**Profile**</span></span> |<span data-ttu-id="dfc6c-128">**성능/메트릭 기반**</span><span class="sxs-lookup"><span data-stu-id="dfc6c-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="dfc6c-129">규칙</span><span class="sxs-lookup"><span data-stu-id="dfc6c-129">Rule</span></span> |<span data-ttu-id="dfc6c-130">서비스 버스 큐 메시지 수 > x</span><span class="sxs-lookup"><span data-stu-id="dfc6c-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="dfc6c-131">규칙</span><span class="sxs-lookup"><span data-stu-id="dfc6c-131">Rule</span></span> |<span data-ttu-id="dfc6c-132">서비스 버스 큐 메시지 수 < y</span><span class="sxs-lookup"><span data-stu-id="dfc6c-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="dfc6c-133">규칙</span><span class="sxs-lookup"><span data-stu-id="dfc6c-133">Rule</span></span> |<span data-ttu-id="dfc6c-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="dfc6c-134">CPU% > n</span></span> |
    | <span data-ttu-id="dfc6c-135">규칙</span><span class="sxs-lookup"><span data-stu-id="dfc6c-135">Rule</span></span> |<span data-ttu-id="dfc6c-136">CPU% < p</span><span class="sxs-lookup"><span data-stu-id="dfc6c-136">CPU% < p</span></span> |
    | <span data-ttu-id="dfc6c-137">**프로필**</span><span class="sxs-lookup"><span data-stu-id="dfc6c-137">**Profile**</span></span> |<span data-ttu-id="dfc6c-138">**평일 오전 시간(규칙 없음)**</span><span class="sxs-lookup"><span data-stu-id="dfc6c-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="dfc6c-139">**프로필**</span><span class="sxs-lookup"><span data-stu-id="dfc6c-139">**Profile**</span></span> |<span data-ttu-id="dfc6c-140">**제품 출시일(규칙 없음)**</span><span class="sxs-lookup"><span data-stu-id="dfc6c-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="dfc6c-141">이 연습에 사용할 가상의 크기 조정 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="dfc6c-142">**기반 부하** -싶습니다 tooscale 걸러 내 거 나에서 눈금 set.* 내에서 호스트 하는 응용 프로그램 내에서 hello 부하에 따라</span><span class="sxs-lookup"><span data-stu-id="dfc6c-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="dfc6c-143">**메시지 큐 크기** -hello 들어오는 메시지 toomy 응용 프로그램에 대 한 서비스 버스 큐를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="dfc6c-144">Hello 큐의 메시지 수 및 CPU (%)를 사용 하 고 적중 threshold.* hello 메시지 수 또는 CPU 경우 기본 프로필 tootrigger 크기 조정 작업을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="dfc6c-145">**주 및 일의 시간** -매주 되풀이 '시간이 hello 하루 중' 기반 프로필 ' 평일 오전 시간 '를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="dfc6c-146">기록 데이터에 따라, 알 수 있습니까 것이 더 나은 toohave 특정 VM 인스턴스의 수 toohandle 내 응용 프로그램의 부하가이 time.* 중</span><span class="sxs-lookup"><span data-stu-id="dfc6c-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="dfc6c-147">**특정 날짜** - '제품 출시일' 프로필을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="dfc6c-148">I 미리 계획 특정 날짜에 대 한 마케팅 공지 인해 준비 toohandle hello 부하 및 hello application.*에 새 제품에서는 삽입 했을 때 응용 프로그램 이므로</span><span class="sxs-lookup"><span data-stu-id="dfc6c-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="dfc6c-149">*hello 마지막 두 개의 프로필 다른 성능 메트릭 기반된 규칙 내에 있을 수도 있습니다. 이 경우 하나 toohave 하지 하기로 결정 하 고 대신 hello 기본 성능 메트릭에 toorely 기반의 규칙. 규칙은 hello 되풀이 및 날짜 기반 프로필에 대 한 선택 사항입니다.*</span><span class="sxs-lookup"><span data-stu-id="dfc6c-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="dfc6c-150">Hello 프로필 및 규칙의 우선 순위를 자동 크기 조정 엔진의 hello에도 캡처된 [자동 크기 조정에 대 한 유용한 정보](insights-autoscale-best-practices.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="dfc6c-151">자동 크기 조정에 대한 공통 메트릭 목록은 [자동 크기 조정에 대한 공통 메트릭](insights-autoscale-common-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="dfc6c-152">Hello 선택 되어 있는지 확인 **읽기/쓰기** 모드의 리소스 탐색기</span><span class="sxs-lookup"><span data-stu-id="dfc6c-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, 기본 자동 크기 조정 설정](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="dfc6c-154">편집을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-154">Click Edit.</span></span> <span data-ttu-id="dfc6c-155">**대체** 같은 구성이 hello로 자동 크기 조정 설정에 프로필' hello' 요소:</span><span class="sxs-lookup"><span data-stu-id="dfc6c-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

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
    <span data-ttu-id="dfc6c-157">지원되는 필드와 해당 값은 [자동 크기 조정 REST API 설명서](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="dfc6c-158">이제 자동 크기 조정 설정에는 설명한 hello 3 개 프로필을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="dfc6c-159">마지막으로, 자동 크기 조정 hello를 살펴보고 **알림** 섹션.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="dfc6c-160">자동 크기 조정 알림 하면 toodo 다음 세 가지 경우를 확장 하거나 작업에 성공적으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="dfc6c-161">Admin 님 안녕하세요 및 구독의 공동 관리자에 게 알림</span><span class="sxs-lookup"><span data-stu-id="dfc6c-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="dfc6c-162">사용자 집합에 전자 메일 보내기</span><span class="sxs-lookup"><span data-stu-id="dfc6c-162">Email a set of users</span></span>
   - <span data-ttu-id="dfc6c-163">웹후크 호출 트리거.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-163">Trigger a webhook call.</span></span> <span data-ttu-id="dfc6c-164">발생 하면이 webhook hello 자동 크기 조정 상태에 대 한 메타 데이터 보내고 hello 눈금 리소스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="dfc6c-165">자동 크기 조정 webhook의 hello 페이로드에 대 한 자세한 정보는 toolearn 참조 [Webhook 구성 및 자동 크기 조정에 대 한 전자 메일 알림을](insights-autoscale-to-webhook-email.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="dfc6c-166">Hello toohello 자동 크기 조정 설정 대체 다음 추가 프로그램 **알림** 값이 null 인 요소</span><span class="sxs-lookup"><span data-stu-id="dfc6c-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="dfc6c-167">적중 **배치** 리소스 탐색기 tooupdate hello 자동 크기 조정 설정에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="dfc6c-168">VM 크기 집합 tooinclude에 여러 크기 조정 프로필을 설정 하는 자동 크기 조정 업데이트 및 알림을 크기를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc6c-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfc6c-169">Next Steps</span></span>
<span data-ttu-id="dfc6c-170">이러한 링크 toolearn 자동 크기 조정에 대 한 자세한 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc6c-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="dfc6c-171">가상 컴퓨터 규모 집합을 사용하여 자동 크기 조정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="dfc6c-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="dfc6c-172">자동 크기 조정에 대한 공통 메트릭</span><span class="sxs-lookup"><span data-stu-id="dfc6c-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="dfc6c-173">Azure 자동 크기 조정에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="dfc6c-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="dfc6c-174">PowerShell을 사용하여 자동 크기 조정 관리</span><span class="sxs-lookup"><span data-stu-id="dfc6c-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="dfc6c-175">CLI를 사용하여 자동 크기 조정 관리</span><span class="sxs-lookup"><span data-stu-id="dfc6c-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="dfc6c-176">자동 크기 조정의 Webhook 및 메일 알림 구성</span><span class="sxs-lookup"><span data-stu-id="dfc6c-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
