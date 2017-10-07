---
title: "Microsoft Azure 가상 컴퓨터, 클라우드 서비스 및 웹 앱의 자동 크기 조정의 aaaOverview | Microsoft Docs"
description: "Microsoft Azure의 자동 크기 조정의 개요입니다. TooVirtual 컴퓨터, 클라우드 서비스 및 웹 앱에 적용 됩니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a><span data-ttu-id="2501b-104">Microsoft Azure Microsoft Azure Virtual Machines, Cloud Services 및 Web Apps에서 자동 크기 조정 개요</span><span class="sxs-lookup"><span data-stu-id="2501b-104">Overview of autoscale in Microsoft Azure Virtual Machines, Cloud Services, and Web Apps</span></span>
<span data-ttu-id="2501b-105">이 문서에서는 어떤 Microsoft Azure 자동 크기 조정의 장점 이며, 사용 하 여 tooget을 시작 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-105">This article describes what Microsoft Azure autoscale is, its benefits, and how tooget started using it.</span></span>  

<span data-ttu-id="2501b-106">Azure 모니터의 자동 크기 조정 적용만 너무[가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-106">Azure Monitor autoscale applies only too[Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>

> [!NOTE]
> <span data-ttu-id="2501b-107">Azure에는 두 개의 자동 크기 조정 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-107">Azure has two autoscale methods.</span></span> <span data-ttu-id="2501b-108">이전 버전의 자동 크기 조정 tooVirtual 컴퓨터 (가용성 집합)를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-108">An older version of autoscale applies tooVirtual Machines (availability sets).</span></span> <span data-ttu-id="2501b-109">이 기능은 제한적으로 지원 하 고 보다 빠르고 안정적 자동 크기 조정 지원에 대 한 마이그레이션 toovirtual 컴퓨터 크기를 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-109">This feature has limited support and we recommend migrating toovirtual machine scale sets for faster and more reliable autoscale support.</span></span> <span data-ttu-id="2501b-110">Toouse 이전 기술을 hello 하는 방법에 대 한 링크는이 문서에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-110">A link on how toouse hello older technology is included in this article.</span></span>  
>
>

## <a name="what-is-autoscale"></a><span data-ttu-id="2501b-111">자동 크기 조정이란?</span><span class="sxs-lookup"><span data-stu-id="2501b-111">What is autoscale?</span></span>
<span data-ttu-id="2501b-112">자동 크기 조정 응용 프로그램에서 toohandle hello 부하를 실행 중인 리소스의 toohave hello 올바른 용량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-112">Autoscale allows you toohave hello right amount of resources running toohandle hello load on your application.</span></span> <span data-ttu-id="2501b-113">Tooadd 리소스를 toohandle 증가에 로드 하 고 유휴 상태는 리소스를 제거 하 여 비용을 절감할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-113">It allows you tooadd resources toohandle increases in load and also save money by removing resources that are sitting idle.</span></span> <span data-ttu-id="2501b-114">인스턴스 toorun 최소 및 최대 수를 지정 하 고 추가 하거나 Vm 규칙의 집합에 따라 자동으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-114">You specify a minimum and maximum number of instances toorun and add or remove VMs automatically based on a set of rules.</span></span> <span data-ttu-id="2501b-115">최소값을 설정하면 응용 프로그램이 항상 부하가 적은 상태에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-115">Having a minimum makes sure your application is always running even under no load.</span></span> <span data-ttu-id="2501b-116">최대값을 설정하면 가능한 총 시간 비용이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-116">Having a maximum limits your total possible hourly cost.</span></span> <span data-ttu-id="2501b-117">만든 규칙을 사용하여 이러한 두 극한값 사이를 자동으로 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-117">You automatically scale between these two extremes using rules you create.</span></span>

 ![자동 크기 조정이 설명되었습니다.](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

<span data-ttu-id="2501b-120">규칙 조건이 충족되면 하나 이상의 자동 크기 조정 동작이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-120">When rule conditions are met, one or more autoscale actions are triggered.</span></span> <span data-ttu-id="2501b-121">VM을 추가 및 제거하거나 다른 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-121">You can add and remove VMs, or perform other actions.</span></span> <span data-ttu-id="2501b-122">hello 다음 개념적 다이어그램에서는이 프로세스</span><span class="sxs-lookup"><span data-stu-id="2501b-122">hello following conceptual diagram shows this process.</span></span>  

 ![자동 크기 조정 흐름 다이어그램](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

<span data-ttu-id="2501b-124">hello 아래 설명 적용 toohello 가지 hello 이전 다이어그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-124">hello following explanation applies toohello pieces of hello previous diagram.</span></span>   

## <a name="resource-metrics"></a><span data-ttu-id="2501b-125">리소스 메트릭</span><span class="sxs-lookup"><span data-stu-id="2501b-125">Resource Metrics</span></span>
<span data-ttu-id="2501b-126">리소스에서 메트릭을 내보내며, 이러한 메트릭은 나중에 규칙에 따라 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-126">Resources emit metrics, these metrics are later processed by rules.</span></span> <span data-ttu-id="2501b-127">메트릭은 다른 메서드를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-127">Metrics come via different methods.</span></span>
<span data-ttu-id="2501b-128">가상 컴퓨터 크기 집합 웹 앱 및 클라우드 서비스에 대 한 원격 분석 hello Azure 인프라에서 직접 가져온 반면 Azure 진단 에이전트에서 원격 분석 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-128">Virtual machine scale sets use telemetry data from Azure diagnostics agents whereas telemetry for Web apps and Cloud services comes directly from hello Azure Infrastructure.</span></span> <span data-ttu-id="2501b-129">일부 자주 사용되는 통계는 CPU 사용량, 메모리 사용량, 스레드 수, 큐 길이 및 디스크 사용량을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-129">Some commonly used statistics include CPU Usage, memory usage, thread counts, queue length, and disk usage.</span></span> <span data-ttu-id="2501b-130">사용할 수 있는 원격 분석 데이터 목록은 [자동 크기 조정 공통 메트릭](insights-autoscale-common-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2501b-130">For a list of what telemetry data you can use, see [Autoscale Common Metrics](insights-autoscale-common-metrics.md).</span></span>

## <a name="custom-metrics"></a><span data-ttu-id="2501b-131">사용자 지정 메트릭</span><span class="sxs-lookup"><span data-stu-id="2501b-131">Custom Metrics</span></span>
<span data-ttu-id="2501b-132">응용 프로그램에서 내보낼 수 있는 사용자 지정 메트릭을 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-132">You can also leverage your own custom metrics that your application(s) may be emitting.</span></span> <span data-ttu-id="2501b-133">응용 프로그램 toosend 메트릭 tooApplication 여부에 이러한 메트릭 toomake 결정을 활용할 수 있는 통찰력을 구성한 경우 tooscale 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-133">If you have configured your application(s) toosend metrics tooApplication Insights you can leverage those metrics toomake decisions on whether tooscale or not.</span></span> 

## <a name="time"></a><span data-ttu-id="2501b-134">Time</span><span class="sxs-lookup"><span data-stu-id="2501b-134">Time</span></span>
<span data-ttu-id="2501b-135">일정 기반 규칙은 UTC 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-135">Schedule-based rules are based on UTC.</span></span> <span data-ttu-id="2501b-136">규칙을 설정할 때 표준 시간대를 올바르게 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-136">You must set your time zone properly when setting up your rules.</span></span>  

## <a name="rules"></a><span data-ttu-id="2501b-137">규칙</span><span class="sxs-lookup"><span data-stu-id="2501b-137">Rules</span></span>
<span data-ttu-id="2501b-138">hello 다이어그램 하나만 자동 크기 조정 규칙을 보여주지만 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-138">hello diagram shows only one autoscale rule, but you can have many of them.</span></span> <span data-ttu-id="2501b-139">상황에 필요한 대로 겹치는 복잡한 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-139">You can create complex overlapping rules as needed for your situation.</span></span>  <span data-ttu-id="2501b-140">규칙 형식은 다음을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-140">Rule types include</span></span>  

* <span data-ttu-id="2501b-141">**메트릭 기반** - 예를 들어 CPU 사용률이 50%보다 높으면 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-141">**Metric-based** - For example, do this action when CPU usage is above 50%.</span></span>
* <span data-ttu-id="2501b-142">**시간 기반** - 예를 들어 지정된 표준 시간대에 토요일 오전 8시마다 웹후크를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-142">**Time-based** - For example, trigger a webhook every 8am on Saturday in a given time zone.</span></span>

<span data-ttu-id="2501b-143">메트릭 기반의 규칙은 응용 프로그램 부하를 측정하고 해당 부하를 기반으로 VM을 추가 또는 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-143">Metric-based rules measure application load and add or remove VMs based on that load.</span></span> <span data-ttu-id="2501b-144">일정에 기반 규칙을 사용 하면 tooscale 부하에서 시간 패턴을 파악 하 고 사용할 수 있는 부하 증가 하기 전에 tooscale 또는 감소 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2501b-144">Schedule-based rules allow you tooscale when you see time patterns in your load and want tooscale before a possible load increase or decrease occurs.</span></span>  

## <a name="actions-and-automation"></a><span data-ttu-id="2501b-145">작업 및 자동화</span><span class="sxs-lookup"><span data-stu-id="2501b-145">Actions and automation</span></span>
<span data-ttu-id="2501b-146">규칙은 하나 이상의 형식을 가진 작업을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-146">Rules can trigger one or more types of actions.</span></span>

* <span data-ttu-id="2501b-147">**크기 조정** - VM을 감축 또는 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-147">**Scale** - Scale VMs in or out</span></span>
* <span data-ttu-id="2501b-148">**전자 메일** -toosubscription 관리자 전자 메일, 공동 관리자 및/또는 추가 전자 메일 주소를 지정 하면 보내기</span><span class="sxs-lookup"><span data-stu-id="2501b-148">**Email** - Send email toosubscription admins, co-admins, and/or additional email address you specify</span></span>
* <span data-ttu-id="2501b-149">**Webhook 통해 자동화** - Azure의 내부 또는 외부에서 여러 복잡한 작업을 트리거할 수 있는 웹후크를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-149">**Automate via webhooks** - Call webhooks, which can trigger multiple complex actions inside or outside Azure.</span></span> <span data-ttu-id="2501b-150">Azure에서 Azure Automation runbook, Azure Function 또는 Azure Logic App을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-150">Inside Azure, you can start an Azure Automation runbook, Azure Function, or Azure Logic App.</span></span> <span data-ttu-id="2501b-151">Azure 외부의 타사 URL 예제는 Slack 및 Twilio와 같은 서비스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-151">Example third-party URL outside Azure include services like Slack and Twilio.</span></span>

## <a name="autoscale-settings"></a><span data-ttu-id="2501b-152">자동 크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="2501b-152">Autoscale Settings</span></span>
<span data-ttu-id="2501b-153">자동 크기 조정 hello 다음 이름을 사용해 서 용어와 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-153">Autoscale use hello following terminology and structure.</span></span>

- <span data-ttu-id="2501b-154">**자동 크기 조정 설정** 여부 hello 자동 크기 조정 엔진 toodetermine 읽은 tooscale 위나 아래로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-154">An **autoscale setting** is read by hello autoscale engine toodetermine whether tooscale up or down.</span></span> <span data-ttu-id="2501b-155">하나 자세한 프로필, hello 대상 리소스 및 알림 설정에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-155">It contains one or more profiles, information about hello target resource, and notification settings.</span></span>

    - <span data-ttu-id="2501b-156">**자동 크기 조정 프로필**은 다음 항목의 조합입니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-156">An **autoscale profile** is a combination of a:</span></span>

        - <span data-ttu-id="2501b-157">**용량 설정**, hello 최소, 최대, 나타냅니다 및 기본 인스턴스 수에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-157">**capacity setting**, which indicates hello minimum, maximum, and default values for number of instances.</span></span>
        - <span data-ttu-id="2501b-158">**일련의 집합**은 각 트리거(시간 또는 미터법) 및 크기 조정 작업(위쪽 또는 아래쪽)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-158">**set of rules**, each of which includes a trigger (time or metric) and a scale action (up or down).</span></span>
        - <span data-ttu-id="2501b-159">**되풀이**는 자동 크기 조정에서 이 프로필을 적용할 시기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-159">**recurrence**, which indicates when autoscale should put this profile into effect.</span></span>

        <span data-ttu-id="2501b-160">겹치는 서로 다른 요구 사항 care of tootake 수 있게 해 주는 여러 프로필을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-160">You can have multiple profiles, which allow you tootake care of different overlapping requirements.</span></span> <span data-ttu-id="2501b-161">다른 자동 크기 조정 프로필 하루 또는 한 hello 주 중 일 서로 다른 시간에 대 한 예를 들어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-161">You can have different autoscale profiles for different times of day or days of hello week, for example.</span></span>

    - <span data-ttu-id="2501b-162">A **알림 설정** hello 기준을 hello 자동 크기 조정 설정의 프로필 중 하나를 만족에 따라 자동 크기 조정 이벤트 발생 시 알림을 수행할지 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-162">A **notification setting** defines what notifications should occur when an autoscale event occurs based on satisfying hello criteria of one of hello autoscale setting’s profiles.</span></span> <span data-ttu-id="2501b-163">자동 크기 조정 하나 이상의 전자 메일 주소 또는 호출 tooone 또는 자세한 webhook 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-163">Autoscale can notify one or more email addresses or make calls tooone or more webhooks.</span></span>


![Azure 자동 크기 조정 설정, 프로필 및 규칙 구조](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

<span data-ttu-id="2501b-165">hello 구성 가능한 필드 및 설명의 전체 목록은 영어로 hello [자동 크기 조정 REST API](https://msdn.microsoft.com/library/dn931928.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-165">hello full list of configurable fields and descriptions is available in hello [Autoscale REST API](https://msdn.microsoft.com/library/dn931928.aspx).</span></span>

<span data-ttu-id="2501b-166">코드 예제는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2501b-166">For code examples, see</span></span>

* [<span data-ttu-id="2501b-167">Resource Manager 템플릿을 사용하여 VM 확장 집합에 대한 고급 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="2501b-167">Advanced Autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [<span data-ttu-id="2501b-168">자동 크기 조정 REST API</span><span class="sxs-lookup"><span data-stu-id="2501b-168">Autoscale REST API</span></span>](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a><span data-ttu-id="2501b-169">수평 및 수직적 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2501b-169">Horizontal vs vertical scaling</span></span>
<span data-ttu-id="2501b-170">자동 크기 조정만 확장할 수 수평으로 ("out") 증가 또는 감소 ("")는 hello VM 인스턴스 수에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-170">Autoscale only scales horizontally, which is an increase ("out") or decrease ("in") in hello number of VM instances.</span></span>  <span data-ttu-id="2501b-171">가로 toohandle 부하 Vm의 잠재적으로 수천 toorun 수 있으므로 클라우드 상황에서 더 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-171">Horizontal is more flexible in a cloud situation as it allows you toorun potentially thousands of VMs toohandle load.</span></span>

<span data-ttu-id="2501b-172">반대로 수직적 규모 조정은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-172">In contrast, vertical scaling is different.</span></span> <span data-ttu-id="2501b-173">이 유지 hello 동일한 Vm 수 있지만 hello ("업") 다소간 ("아래쪽") 강력한 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-173">It keeps hello same number of VMs, but makes hello VMs more ("up") or less ("down") powerful.</span></span> <span data-ttu-id="2501b-174">전원은 메모리, CPU 속도, 디스크 공간 등에서 측정됩니다.  수직적 크기 조정에 더 많은 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-174">Power is measured in memory, CPU speed, disk space, etc.  Vertical scaling has more limitations.</span></span> <span data-ttu-id="2501b-175">더 큰 하드웨어를 신속 하 게 상한값에 도달 하 고 지역에 따라 다 수의 hello 가용성에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-175">It's dependent on hello availability of larger hardware, which quickly hits an upper limit and can vary by region.</span></span> <span data-ttu-id="2501b-176">또한 일반적으로 크기 조정을 세로 VM toostop 차지 하며 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-176">Vertical scaling also usually requires a VM toostop and restart.</span></span>

<span data-ttu-id="2501b-177">자세한 내용은 [Azure Automation을 사용하여 Azure 가상 컴퓨터를 수직으로 확장](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2501b-177">For more information, see [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="methods-of-access"></a><span data-ttu-id="2501b-178">액세스 방법</span><span class="sxs-lookup"><span data-stu-id="2501b-178">Methods of access</span></span>
<span data-ttu-id="2501b-179">자동 크기 조정은 다음을 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2501b-179">You can set up autoscale via</span></span>

* [<span data-ttu-id="2501b-180">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="2501b-180">Azure portal</span></span>](insights-how-to-scale.md)
* [<span data-ttu-id="2501b-181">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2501b-181">PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [<span data-ttu-id="2501b-182">플랫폼 간 CLI(명령줄 인터페이스)</span><span class="sxs-lookup"><span data-stu-id="2501b-182">Cross-platform Command Line Interface (CLI)</span></span>](insights-cli-samples.md#autoscale)
* [<span data-ttu-id="2501b-183">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="2501b-183">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a><span data-ttu-id="2501b-184">자동 크기 조정이 지원되는 서비스</span><span class="sxs-lookup"><span data-stu-id="2501b-184">Supported services for autoscale</span></span>
| <span data-ttu-id="2501b-185">부여</span><span class="sxs-lookup"><span data-stu-id="2501b-185">Service</span></span> | <span data-ttu-id="2501b-186">스키마 및 문서</span><span class="sxs-lookup"><span data-stu-id="2501b-186">Schema & Docs</span></span> |
| --- | --- |
| <span data-ttu-id="2501b-187">웹앱</span><span class="sxs-lookup"><span data-stu-id="2501b-187">Web Apps</span></span> |[<span data-ttu-id="2501b-188">웹앱 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2501b-188">Scaling Web Apps</span></span>](insights-how-to-scale.md) |
| <span data-ttu-id="2501b-189">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="2501b-189">Cloud Services</span></span> |[<span data-ttu-id="2501b-190">클라우드 서비스 자동 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2501b-190">Autoscale a Cloud Service</span></span>](../cloud-services/cloud-services-how-to-scale.md) |
| <span data-ttu-id="2501b-191">Virtual Machines: 클래식</span><span class="sxs-lookup"><span data-stu-id="2501b-191">Virtual Machines: Classic</span></span> |[<span data-ttu-id="2501b-192">클래식 가상 컴퓨터 가용성 집합 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2501b-192">Scaling Classic Virtual Machine Availability Sets</span></span>](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| <span data-ttu-id="2501b-193">Virtual Machines: Windows 확장 집합</span><span class="sxs-lookup"><span data-stu-id="2501b-193">Virtual Machines: Windows Scale Sets</span></span> |[<span data-ttu-id="2501b-194">Windows에서 가상 컴퓨터 확장 집합 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2501b-194">Scaling virtual machine scale sets in Windows</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| <span data-ttu-id="2501b-195">Virtual Machines: Linux 확장 집합</span><span class="sxs-lookup"><span data-stu-id="2501b-195">Virtual Machines: Linux Scale Sets</span></span> |[<span data-ttu-id="2501b-196">Linux에서 가상 컴퓨터 확장 집합 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2501b-196">Scaling virtual machine scale sets in Linux</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| <span data-ttu-id="2501b-197">Virtual Machines: Windows 예제</span><span class="sxs-lookup"><span data-stu-id="2501b-197">Virtual Machines: Windows Example</span></span> |[<span data-ttu-id="2501b-198">Resource Manager 템플릿을 사용하여 VM 확장 집합에 대한 고급 자동 크기 조정 구성</span><span class="sxs-lookup"><span data-stu-id="2501b-198">Advanced Autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a><span data-ttu-id="2501b-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2501b-199">Next steps</span></span>
<span data-ttu-id="2501b-200">toolearn 자동 크기 조정에 대 한 자세한 자동 크기 조정 연습 앞에 나열 된 hello를 사용 하거나, toohello 다음 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2501b-200">toolearn more about autoscale, use hello Autoscale Walkthroughs listed previously or refer toohello following resources:</span></span>

* [<span data-ttu-id="2501b-201">Azure Monitor 자동 크기 조정 공용 메트릭</span><span class="sxs-lookup"><span data-stu-id="2501b-201">Azure Monitor autoscale common metrics</span></span>](insights-autoscale-common-metrics.md)
* [<span data-ttu-id="2501b-202">Azure Monitor 자동 크기 조정에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="2501b-202">Best practices for Azure Monitor autoscale</span></span>](insights-autoscale-best-practices.md)
* [<span data-ttu-id="2501b-203">자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용</span><span class="sxs-lookup"><span data-stu-id="2501b-203">Use autoscale actions toosend email and webhook alert notifications</span></span>](insights-autoscale-to-webhook-email.md)
* [<span data-ttu-id="2501b-204">자동 크기 조정 REST API</span><span class="sxs-lookup"><span data-stu-id="2501b-204">Autoscale REST API</span></span>](https://msdn.microsoft.com/library/dn931953.aspx)
* [<span data-ttu-id="2501b-205">가상 컴퓨터 규모 집합 자동 크기 조정 문제 해결</span><span class="sxs-lookup"><span data-stu-id="2501b-205">Troubleshooting Virtual Machine Scale Sets Autoscale</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
