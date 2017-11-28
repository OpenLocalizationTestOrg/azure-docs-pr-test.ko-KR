---
title: "Mobile Engagement Windows 유니버설 SDK 통합 aaaAzure | Microsoft Docs"
description: "Azure Mobile Engagement의 Windows 유니버설 SDK 통합"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="6ff8a-103">Azure Mobile Engagement의 Windows 유니버설 SDK 통합</span><span class="sxs-lookup"><span data-stu-id="6ff8a-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="6ff8a-104">이 문서에서는 일부 hello 통합 및 구성 옵션을 사용할 hello Azure Mobile Engagement Windows 유니버설 SDK에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-104">This document describes all hello integration and configuration options available for hello Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ff8a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6ff8a-105">Prerequisites</span></span>
<span data-ttu-id="6ff8a-106">이 자습서를 시작하기 전에 먼저 [15분 자습서](mobile-engagement-windows-store-dotnet-get-started.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="6ff8a-107">고급 기능</span><span class="sxs-lookup"><span data-stu-id="6ff8a-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="6ff8a-108">보고 기능</span><span class="sxs-lookup"><span data-stu-id="6ff8a-108">Reporting features</span></span>
<span data-ttu-id="6ff8a-109">이러한 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-109">You can add these features:</span></span>

1. [<span data-ttu-id="6ff8a-110">고급 보고 옵션</span><span class="sxs-lookup"><span data-stu-id="6ff8a-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="6ff8a-111">고급 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="6ff8a-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="6ff8a-112">알림</span><span class="sxs-lookup"><span data-stu-id="6ff8a-112">Notifications</span></span>
[<span data-ttu-id="6ff8a-113">어떻게 Windows 유니버설 앱에서 toointegrate Reach (알림)</span><span class="sxs-lookup"><span data-stu-id="6ff8a-113">How toointegrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="6ff8a-114">태그 계획 구현:</span><span class="sxs-lookup"><span data-stu-id="6ff8a-114">Tag plan implementation:</span></span>
[<span data-ttu-id="6ff8a-115">어떻게 toouse hello 고급 Mobile Engagement API Windows 유니버설 앱에 태그 지정</span><span class="sxs-lookup"><span data-stu-id="6ff8a-115">How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="6ff8a-116">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6ff8a-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="6ff8a-117">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="6ff8a-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="6ff8a-118">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="6ff8a-118">Stability improvements.</span></span>

<span data-ttu-id="6ff8a-119">이전 버전에 대 한 참조 hello [릴리스 정보를 완료 합니다.](mobile-engagement-windows-store-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="6ff8a-119">For earlier versions, see hello [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="6ff8a-120">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="6ff8a-120">Upgrade procedures</span></span>
<span data-ttu-id="6ff8a-121">통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-121">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="6ff8a-122">여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-122">If you missed several versions of hello SDK, you may have toofollow several procedures.</span></span> <span data-ttu-id="6ff8a-123">참조 hello 완료 [업그레이드 절차](mobile-engagement-windows-store-upgrade-procedure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-123">See hello complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="6ff8a-124">예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-124">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

### <a name="from-330-too340"></a><span data-ttu-id="6ff8a-125">3.3.0에서 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="6ff8a-125">From 3.3.0 too3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="6ff8a-126">테스트 로그</span><span class="sxs-lookup"><span data-stu-id="6ff8a-126">Test logs</span></span>
<span data-ttu-id="6ff8a-127">Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-127">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="6ff8a-128">toocustomize, hello 속성 업데이트 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값 tooone `EngagementTestLogLevel` 열거형 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="6ff8a-128">toocustomize, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello values available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="6ff8a-129">리소스</span><span class="sxs-lookup"><span data-stu-id="6ff8a-129">Resources</span></span>
<span data-ttu-id="6ff8a-130">hello Reach 오버레이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-130">hello Reach overlay has been improved.</span></span> <span data-ttu-id="6ff8a-131">Hello SDK NuGet 패키지 리소스의 일부인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-131">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="6ff8a-132">Toohello hello SDK의 새 버전을 업그레이드 하는 동안 여부 hello에서 기존 파일의 리소스 폴더를 오버레이 tookeep 할지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-132">While upgrading toohello new version of hello SDK, you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="6ff8a-133">Hello 이전 오버레이를 작동 하거나 hello를 통합 하는 경우 `WebView` 요소를 수동으로 다음 결정할 수 있습니다 tookeep 종료 프로그램 파일, 계속 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-133">If hello previous overlay is working for you, or you are integrating hello `WebView` elements manually, then you can decide tookeep your exiting files, it will still work.</span></span>
* <span data-ttu-id="6ff8a-134">tooupdate toohello 새 오버레이가 전체 바꾸기 hello `overlay` hello SDK 패키지에서 새 hello로 리소스에서 폴더 (UWP 앱: hello 업그레이드 후 hello 새 오버레이 폴더 % USERPROFILE %에서 얻을 수 있습니다\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-134">tooupdate toohello new overlay, replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="6ff8a-135">Hello 새 오버레이 사용 하 여 hello 이전 버전에서 적용 된 모든 사용자 지정을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="6ff8a-135">Using hello new overlay overwrites any customizations made on hello previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="6ff8a-136">이전 버전에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="6ff8a-136">Upgrade from older versions</span></span>
<span data-ttu-id="6ff8a-137">[Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span><span class="sxs-lookup"><span data-stu-id="6ff8a-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

