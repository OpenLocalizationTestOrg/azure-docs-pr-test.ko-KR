---
title: "Windows 유니버설 앱 Engagement SDK에 대한 고급 구성"
description: "Windows 유니버설 앱과 Azure Mobile Engagement 사용에 대한 고급 구성 옵션"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="1197b-103">Windows 유니버설 앱 Engagement SDK에 대한 고급 구성</span><span class="sxs-lookup"><span data-stu-id="1197b-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1197b-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="1197b-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="1197b-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1197b-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="1197b-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1197b-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="1197b-107">Android</span><span class="sxs-lookup"><span data-stu-id="1197b-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="1197b-108">이 절차에서는 Azure Mobile Engagement Android 앱에 대한 다양한 고급 구성 옵션을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1197b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1197b-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="1197b-110">고급 구성</span><span class="sxs-lookup"><span data-stu-id="1197b-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="1197b-111">자동 작동 중단 보고를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="1197b-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="1197b-112">Engagement의 자동 작동 중단 보고를 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="1197b-113">그러면 처리되지 않은 예외가 발생할 때 Engagement에서 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="1197b-114">이 기능을 사용하지 않도록 설정하면 앱에서 처리되지 않은 작동 중단이 발생해도 Engagement에서 작동 중단을 전송하지 않으며 **또한** 세션 및 작업도 닫지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="1197b-115">자동 작동 중단 보고를 사용하지 않도록 설정하려면 구성을 선언한 방식에 따라 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="1197b-116">`EngagementConfiguration.xml` 파일에서</span><span class="sxs-lookup"><span data-stu-id="1197b-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="1197b-117">`<reportCrash>` 및 `</reportCrash>` 태그 간의 작동 중단 보고를 `false`(으)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="1197b-118">런타임에 `EngagementConfiguration` 개체에서</span><span class="sxs-lookup"><span data-stu-id="1197b-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="1197b-119">EngagementConfiguration 개체를 사용하여 작동 중단 보고를 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="1197b-120">실시간 보고 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="1197b-120">Disable real time reporting</span></span>
<span data-ttu-id="1197b-121">기본적으로 Engagement 서비스는 로그를 실시간으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="1197b-122">응용 프로그램이 로그를 자주 보고하는 경우 로그를 버퍼링한 후 정기적으로 한 번에 모두 보고하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="1197b-123">이를 "버스트 모드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-123">This is called “burst mode”.</span></span>

<span data-ttu-id="1197b-124">이 방식을 사용하려면 다음 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="1197b-125">인수는 **밀리초**단위의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="1197b-126">언제든지 실시간 로깅을 다시 활성화하려면 매개 변수를 포함하지 않거나 값을 0으로 설정하여 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="1197b-127">버스트 모드를 사용하는 경우 배터리 수명은 약간 길어지지만 Engagement 모니터에 영향을 주게 됩니다. 모든 세션 및 작업 기간이 버스트 임계값으로 반올림되므로 버스트 임계값보다 짧은 세션과 작업은 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="1197b-128">30000(30초) 이하의 버스트 임계값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="1197b-129">저장된 로그는 300개 항목으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="1197b-130">너무 길게 보내면 일부 로그가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="1197b-131">1초보다 짧은 기간으로 버스트 임계값을 구성할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-131">The burst threshold cannot be configured to a period less than one second.</span></span> <span data-ttu-id="1197b-132">버스트 임계값을 1초보다 짧게 구성하면 SDK에는 오류가 포함된 추적이 표시되며, 값은 자동으로 기본값인 0초로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-132">If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds.</span></span> <span data-ttu-id="1197b-133">그러면 SDK에서 실시간 로그 보고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="1197b-133">This triggers the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
