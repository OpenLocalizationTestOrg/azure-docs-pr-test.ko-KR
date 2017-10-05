---
title: "Azure Mobile Engagement Windows 유니버설 SDK 통합 | Microsoft Docs"
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
ms.openlocfilehash: d616ad58156a19e89b3e106639a38df67cbd0abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="e9947-103">Azure Mobile Engagement의 Windows 유니버설 SDK 통합</span><span class="sxs-lookup"><span data-stu-id="e9947-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="e9947-104">이 문서는 Azure Mobile Engagement Windows 유니버설 SDK에 사용 가능한 모든 통합 및 구성 옵션에 관해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-104">This document describes all the integration and configuration options available for the Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9947-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e9947-105">Prerequisites</span></span>
<span data-ttu-id="e9947-106">이 자습서를 시작하기 전에 먼저 [15분 자습서](mobile-engagement-windows-store-dotnet-get-started.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="e9947-107">고급 기능</span><span class="sxs-lookup"><span data-stu-id="e9947-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="e9947-108">보고 기능</span><span class="sxs-lookup"><span data-stu-id="e9947-108">Reporting features</span></span>
<span data-ttu-id="e9947-109">이러한 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-109">You can add these features:</span></span>

1. [<span data-ttu-id="e9947-110">고급 보고 옵션</span><span class="sxs-lookup"><span data-stu-id="e9947-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="e9947-111">고급 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="e9947-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="e9947-112">알림</span><span class="sxs-lookup"><span data-stu-id="e9947-112">Notifications</span></span>
[<span data-ttu-id="e9947-113">Windows 유니버설 앱에서 도달률(알림)을 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="e9947-113">How to integrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="e9947-114">태그 계획 구현:</span><span class="sxs-lookup"><span data-stu-id="e9947-114">Tag plan implementation:</span></span>
[<span data-ttu-id="e9947-115">Windows 유니버설 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e9947-115">How to use the advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="e9947-116">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="e9947-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="e9947-117">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="e9947-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="e9947-118">안정성 향상</span><span class="sxs-lookup"><span data-stu-id="e9947-118">Stability improvements.</span></span>

<span data-ttu-id="e9947-119">이전 버전에 대한 내용은 [전체 릴리스 정보](mobile-engagement-windows-store-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="e9947-119">For earlier versions, see the [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="e9947-120">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="e9947-120">Upgrade procedures</span></span>
<span data-ttu-id="e9947-121">이전 버전의 Engagement를 응용 프로그램에 이미 통합한 경우에는 SDK를 업그레이드할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-121">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="e9947-122">여러 SDK 버전을 건너뛴 경우에는 여러 절차를 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-122">If you missed several versions of the SDK, you may have to follow several procedures.</span></span> <span data-ttu-id="e9947-123">전체 [업그레이드 절차](mobile-engagement-windows-store-upgrade-procedure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9947-123">See the complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="e9947-124">예를 들어 0.10.1에서 0.11.0으로 마이그레이션하는 경우에는 먼저 "0.9.0에서 0.10.1로 마이그레이션" 절차를 수행한 후에 "0.10.1에서 0.11.0으로 마이그레이션" 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-124">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

### <a name="from-330-to-340"></a><span data-ttu-id="e9947-125">3.3.0에서 3.4.0으로</span><span class="sxs-lookup"><span data-stu-id="e9947-125">From 3.3.0 to 3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="e9947-126">테스트 로그</span><span class="sxs-lookup"><span data-stu-id="e9947-126">Test logs</span></span>
<span data-ttu-id="e9947-127">이제 SDK에서 생성된 콘솔 로그를 사용/사용 안 함/필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-127">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="e9947-128">사용자 지정하려면 속성 `EngagementAgent.Instance.TestLogEnabled`를 `EngagementTestLogLevel` 열거형에서 사용 가능한 값 중 하나로 업데이트합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-128">To customize, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the values available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="e9947-129">리소스</span><span class="sxs-lookup"><span data-stu-id="e9947-129">Resources</span></span>
<span data-ttu-id="e9947-130">도달률 오버레이가 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-130">The Reach overlay has been improved.</span></span> <span data-ttu-id="e9947-131">SDK NuGet 패키지 리소스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-131">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="e9947-132">새 버전의 SDK로 업그레이드하는 동안 리소스의 오버레이 폴더에서 기존 파일을 보관할 것인지 보관하지 않을 것인지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-132">While upgrading to the new version of the SDK, you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="e9947-133">이전 오버레이가 작동 중이거나 `WebView` 요소를 수동으로 통합하는 경우 기존 파일을 보관하도록 결정하여 계속 작동하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-133">If the previous overlay is working for you, or you are integrating the `WebView` elements manually, then you can decide to keep your exiting files, it will still work.</span></span>
* <span data-ttu-id="e9947-134">새 오버레이로 업데이트하려는 경우 리소스의 전체 `overlay` 폴더를 SDK 패키지의 새 폴더로 바꿉니다(UWP 앱: 업그레이드 후 새 오버레이 폴더를 %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources에서 가져올 수 있음).</span><span class="sxs-lookup"><span data-stu-id="e9947-134">To update to the new overlay, replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="e9947-135">새 오버레이를 사용하면 이전 버전에서 설정한 모든 사용자 지정이 덮어 쓰입니다.</span><span class="sxs-lookup"><span data-stu-id="e9947-135">Using the new overlay overwrites any customizations made on the previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="e9947-136">이전 버전에서 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e9947-136">Upgrade from older versions</span></span>
<span data-ttu-id="e9947-137">[Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span><span class="sxs-lookup"><span data-stu-id="e9947-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

