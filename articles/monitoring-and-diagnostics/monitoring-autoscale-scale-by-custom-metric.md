---
title: "Azure에서 사용자 지정 메트릭을 기준으로 자동 크기 조정 시작 Microsoft Docs"
description: "Azure에서 사용자 지정 메트릭을 기준으로 리소스 크기를 조정하는 방법에 대해 알아봅니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: de8f7acadc282e4b81c657b1723f00fd3e5fd4f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="3273d-103">Azure에서 사용자 지정 메트릭을 기준으로 자동 크기 조정 시작</span><span class="sxs-lookup"><span data-stu-id="3273d-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="3273d-104">이 문서에서는 Azure Portal에서 사용자 지정 메트릭을 기준으로 리소스 크기를 조정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-104">This article describes how to scale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="3273d-105">Azure Monitor 자동 크기 조정은 VMSS(Virtual Machine Scale Sets), 클라우드 서비스 및 앱 서비스 계획 및 앱 서비스 환경에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="3273d-106">시작</span><span class="sxs-lookup"><span data-stu-id="3273d-106">Lets get started</span></span>
<span data-ttu-id="3273d-107">이 문서에서는 Application Insights가 구성된 웹앱이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="3273d-108">아직 없으면 [ASP.NET 웹 사이트에 대한 Application Insights를 설정할 수 있습니다][1].</span><span class="sxs-lookup"><span data-stu-id="3273d-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="3273d-109">[Azure Portal][2]을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="3273d-110">왼쪽 탐색 창에서 Azure Monitor 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-110">Click on Azure Monitor icon in the left navigation pane.</span></span>
  <span data-ttu-id="3273d-111">![Azure Monitor 시작][3]</span><span class="sxs-lookup"><span data-stu-id="3273d-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="3273d-112">자동 크기 조정 설정을 클릭하여 현재 자동 크기 조정 상태와 함께 자동 크기 조정을 적용할 수 있는 모든 리소스를 확인합니다. ![Azure Monitor에서 자동 크기 조정 검색][4]</span><span class="sxs-lookup"><span data-stu-id="3273d-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="3273d-113">Azure Monitor에서 '자동 크기 조정' 블레이드를 열고 크기를 조정할 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span></span>
> <span data-ttu-id="3273d-114">참고: 아래 단계에서는 앱 정보가 구성된 웹앱과 연결된 앱 서비스 계획을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="3273d-115">리소스에 대한 크기 조정 설정 블레이드에서 현재 인스턴스 수가 하나임을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span></span> <span data-ttu-id="3273d-116">'자동 크기 조정 사용'을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="3273d-117">![새 웹앱에 대한 크기 조정 설정][5]</span><span class="sxs-lookup"><span data-stu-id="3273d-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="3273d-118">크기 조정 설정의 이름을 제공하고 "규칙 추가"를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-118">Provide a name for the scale setting, and the click on "Add a rule".</span></span> <span data-ttu-id="3273d-119">오른쪽에 열리는 컨텍스트 창에서 크기 조정 규칙 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-119">Notice the scale rule options that opens as a context pane in the right hand side.</span></span> <span data-ttu-id="3273d-120">기본적으로 리소스의 CPU 사용률이 70%를 초과하면 인스턴스 수를 하나씩 늘리는 옵션이 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span></span> <span data-ttu-id="3273d-121">위쪽의 메트릭 원본을 'Application Insights'로 변경하고, '리소스' 드롭다운에서 앱 정보를 선택한 다음, 크기 조정하려는 기준에 따라 사용자 지정 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span></span>
  <span data-ttu-id="3273d-122">![사용자 지정 메트릭 기준 크기 조정][6]</span><span class="sxs-lookup"><span data-stu-id="3273d-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="3273d-123">위의 단계와 마찬가지로 규모 축소하고, 사용자 지정 메트릭이 임계값 아래이면 크기 조정 수를 하나씩 줄이는 크기 조정 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span></span>
  <span data-ttu-id="3273d-124">![CPU 기준 크기 조정][7]</span><span class="sxs-lookup"><span data-stu-id="3273d-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="3273d-125">인스턴스 한도를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-125">Set the you instance limits.</span></span> <span data-ttu-id="3273d-126">예를 들어 사용자 지정 메트릭 변동에 따라 2-5개 인스턴스 간에 크기를 조정하려면 '최소'를 '2'로, '최대'를 '5'로, '기본값'을 '2'로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span></span>
> <span data-ttu-id="3273d-127">참고: 리소스 메트릭을 읽는 데 문제가 있고 현재 용량이 기본 용량보다 적으면, 리소스의 가용성을 보장하기 위해 자동 크기 조정이 기본값으로 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span></span> <span data-ttu-id="3273d-128">이미 현재 용량이 기본 용량보다 많은 경우에는 자동 크기 조정이 축소되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="3273d-129">'저장'을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-129">Click on 'Save'</span></span>

<span data-ttu-id="3273d-130">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-130">Congratulations.</span></span> <span data-ttu-id="3273d-131">이제 사용자 지정 메트릭을 기준으로 웹앱의 크기를 자동으로 조정하는 크기 조정 설정을 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-131">You now now succesfully created your scale setting to auto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="3273d-132">참고: VMSS 또는 클라우드 서비스 역할을 시작하는 데에도 동일한 단계를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3273d-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
