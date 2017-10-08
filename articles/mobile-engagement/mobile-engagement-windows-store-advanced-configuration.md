---
title: "구성에 대 한 Windows 유니버설 앱 Engagement SDK aaaAdvanced"
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
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="88710-103">Windows 유니버설 앱 Engagement SDK에 대한 고급 구성</span><span class="sxs-lookup"><span data-stu-id="88710-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88710-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="88710-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="88710-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="88710-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="88710-106">iOS</span><span class="sxs-lookup"><span data-stu-id="88710-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="88710-107">Android</span><span class="sxs-lookup"><span data-stu-id="88710-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="88710-108">이 절차에서는 설명 방법을 tooconfigure Azure Mobile Engagement Android 앱에 대 한 다양 한 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="88710-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88710-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="88710-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="88710-110">고급 구성</span><span class="sxs-lookup"><span data-stu-id="88710-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="88710-111">자동 작동 중단 보고를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="88710-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="88710-112">Hello 자동 충돌 보고 서비스의 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="88710-113">그러면 처리되지 않은 예외가 발생할 때 Engagement에서 아무 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="88710-114">이 기능을 사용 하지 않도록 설정할 경우 Engagement hello 크래시를 보내지 않습니다 응용 프로그램에서 처리 되지 않은 충돌이 일어나면 **AND** hello 세션 및 작업 닫히지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="88710-115">toodisable 자동 충돌 보고를 선언한 hello 방식에 따라 구성을 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="88710-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="88710-116">`EngagementConfiguration.xml` 파일에서</span><span class="sxs-lookup"><span data-stu-id="88710-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="88710-117">보고서를 너무 충돌 설정`false` 사이 `<reportCrash>` 및 `</reportCrash>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="88710-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="88710-118">런타임에 `EngagementConfiguration` 개체에서</span><span class="sxs-lookup"><span data-stu-id="88710-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="88710-119">보고서 크래시 toofalse EngagementConfiguration 개체를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="88710-120">실시간 보고 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="88710-120">Disable real time reporting</span></span>
<span data-ttu-id="88710-121">기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="88710-122">더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우를 표준 시간으로 한 번에 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="88710-123">이를 "버스트 모드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-123">This is called “burst mode”.</span></span>

<span data-ttu-id="88710-124">따라서 toodo hello 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="88710-125">hello 인수에는 **밀리초**합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="88710-126">Tooreactivate hello 실시간 로깅 원할 때마다 모든 매개 변수 없이 또는 hello 0 값을 가진 hello 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="88710-127">버스트 모드 약간 hello 배터리 수명 늘어나지만 hello Engagement 모니터에 영향을 주: 모든 세션 및 작업 기간 둥근된 toohello 버스트 임계값 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88710-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="88710-128">30000(30초) 이하의 버스트 임계값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="88710-129">저장 된 로그는 제한 된 too300 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="88710-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="88710-130">너무 길게 보내면 일부 로그가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="88710-131">두 번째 hello 버스트 임계값은 1 보다 작은 구성된 tooa 기간 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="88710-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="88710-132">이렇게 하면 자동으로 toohello 기본값을 다시 0 초로 설정 및는 hello SDK hello 오류와 함께 추적을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="88710-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="88710-133">이 트리거 hello SDK tooreport hello 로그인 실시간 합니다.</span><span class="sxs-lookup"><span data-stu-id="88710-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
