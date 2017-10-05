---
title: "Windows Phone Silverlight SDK 업그레이드 절차"
description: "Azure Mobile Engagement용 Windows Phone Silverlight SDK 업그레이드 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="e3a40-103">Windows Phone Silverlight SDK 업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="e3a40-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="e3a40-104">이전 버전의 SDK를 응용 프로그램에 이미 통합한 경우에는 SDK를 업그레이드할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="e3a40-105">여러 SDK 버전을 건너뛴 경우에는 여러 절차를 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="e3a40-106">예를 들어 0.10.1에서 0.11.0으로 마이그레이션하는 경우에는 먼저 "0.9.0에서 0.10.1로 마이그레이션" 절차를 수행한 후에 "0.10.1에서 0.11.0으로 마이그레이션" 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="e3a40-107">2.0.0에서 3.3.0으로</span><span class="sxs-lookup"><span data-stu-id="e3a40-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="e3a40-108">테스트 로그</span><span class="sxs-lookup"><span data-stu-id="e3a40-108">Test logs</span></span>
<span data-ttu-id="e3a40-109">이제 SDK에서 생성된 콘솔 로그를 사용/사용 안 함/필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="e3a40-110">이를 사용자 지정하려면 속성 `EngagementAgent.Instance.TestLogEnabled`를 `EngagementTestLogLevel` 열거형에서 사용 가능한 값 중 하나로 업데이트합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="e3a40-111">1.1.1에서 2.0.0으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="e3a40-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="e3a40-112">아래에서는 SDK 통합을 Capptain SAS 제공 Capptain 서비스에서 Azure Mobile Engagement 구동 앱으로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e3a40-113">Capptain과 Mobile Engagement는 같은 서비스가 아니며, 아래에서 제공하는 절차에서는 클라이언트 앱을 마이그레이션하는 방법만 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="e3a40-114">앱에서 SDK를 마이그레이션해도 데이터가 Capptain 서버에서 Mobile Engagement 서버로 마이그레이션되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="e3a40-115">이전 버전에서 마이그레이션하는 경우에는 Capptain 웹 사이트를 참조하여 1.1.1로 먼저 마이그레이션한 후에 다음 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e3a40-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="e3a40-116">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="e3a40-116">Nuget package</span></span>
<span data-ttu-id="e3a40-117">**Capptain.WindowsPhone**을 **MicrosoftAzure.MobileEngagement** Nuget 패키지로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="e3a40-118">Mobile Engagement 적용</span><span class="sxs-lookup"><span data-stu-id="e3a40-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="e3a40-119">SDK에서는 `Engagement`(이)라는 용어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="e3a40-120">이 변경 내용에 맞게 프로젝트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="e3a40-121">현재 Capptain NuGet 패키지는 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="e3a40-122">Capptain 리소스 폴더의 모든 변경 내용도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="e3a40-123">해당 폴더의 파일을 보존하려면 복사본을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="e3a40-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="e3a40-124">그런 다음 새 Microsoft Azure Engagement NuGet 패키지를 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="e3a40-125">해당 패키지는 [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement)에서 직접 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="e3a40-126">이 작업을 수행하면 Engagement에서 사용하는 모든 리소스 파일이 바뀌며 프로젝트 참조에 새 Engagement DLL이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="e3a40-127">Capptain DLL 참조를 삭제하여 프로젝트 참조를 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="e3a40-128">이렇게 하지 않으면 Capptain 버전이 충돌하여 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="e3a40-129">Capptain 리소스를 사용자 지정한 경우 이전 파일 콘텐츠를 복사하여 새 Engagement 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="e3a40-130">xaml 파일과 cs 파일을 모두 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="e3a40-131">해당 단계를 완료한 후에는 이전 Capptain 참조만 새 Engagement 참조로 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="e3a40-132">모든 Capptain 네임스페이스를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="e3a40-133">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="e3a40-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="e3a40-134">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="e3a40-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="e3a40-135">"Capptain"을 포함하는 모든 Capptain 클래스는 이제 "Engagement"를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="e3a40-136">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="e3a40-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="e3a40-137">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="e3a40-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="e3a40-138">xaml 파일에서는 Capptain 네임스페이스와 특성도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="e3a40-139">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="e3a40-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="e3a40-140">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="e3a40-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="e3a40-141">Capptain 그림과 같은 기타 리소스도 "Engagement"를 사용하도록 이름이 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="e3a40-142">응용 프로그램 ID/SDK 키</span><span class="sxs-lookup"><span data-stu-id="e3a40-142">Application ID / SDK Key</span></span>
<span data-ttu-id="e3a40-143">Engagement에서는 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-143">Engagement uses a connection string.</span></span> <span data-ttu-id="e3a40-144">따라서 Mobile Engagement에서는 응용 프로그램 ID와 SDK 키를 지정할 필요가 없으며 연결 문자열만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="e3a40-145">EngagementConfiguration 파일에서 연결 문자열을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="e3a40-146">Engagement 구성은 프로젝트의 `Resources\EngagementConfiguration.xml` 파일에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="e3a40-147">이 파일을 편집하여 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-147">Edit this file to specify:</span></span>

* <span data-ttu-id="e3a40-148">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="e3a40-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="e3a40-149">이 문자열을 런타임에 지정하려는 경우에는 Engagement 에이전트 초기화 전에 다음 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="e3a40-150">응용 프로그램의 연결 문자열은 Azure 클래식 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="e3a40-151">항목 이름 변경</span><span class="sxs-lookup"><span data-stu-id="e3a40-151">Items name change</span></span>
<span data-ttu-id="e3a40-152">*capptain*이라는 모든 항목은 *engagement*라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="e3a40-153">마찬가지로 *Capptain*은 *Engagement*로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="e3a40-154">일반적으로 사용되는 Capptain 항목의 예제:</span><span class="sxs-lookup"><span data-stu-id="e3a40-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="e3a40-155">CapptainConfiguration의 이름은 EngagementConfiguration으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="e3a40-156">CapptainAgent의 이름은 EngagementAgent로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="e3a40-157">CapptainReach의 이름은 EngagementReach로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="e3a40-158">CapptainHttpConfig의 이름은 EngagementHttpConfig로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="e3a40-159">GetCapptainPageName의 이름은 GetEngagementPageName으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="e3a40-160">이와 같이 바뀐 이름은 재정의되는 메서드에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e3a40-160">Note that rename also affects overridden methods.</span></span>

