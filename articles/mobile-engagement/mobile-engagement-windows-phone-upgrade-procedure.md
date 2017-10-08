---
title: "aaaWindows Phone Silverlight SDK 업그레이드 절차"
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
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="edd48-103">Windows Phone Silverlight SDK 업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="edd48-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="edd48-104">통합 한 경우 이미이 SDK의 이전 버전 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="edd48-105">여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="edd48-106">예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="edd48-107">2.0.0에서 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="edd48-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="edd48-108">테스트 로그</span><span class="sxs-lookup"><span data-stu-id="edd48-108">Test logs</span></span>
<span data-ttu-id="edd48-109">Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="edd48-110">toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="edd48-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="edd48-111">1.1.1에서 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="edd48-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="edd48-112">hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="edd48-113">Capptain 및 Mobile Engagement는 동일한 서비스 하지 hello 및 아래에 주어진 hello 프로시저 어떻게 toomigrate hello 클라이언트 응용 프로그램을 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="edd48-114">Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="edd48-115">이전 버전에서 마이그레이션하려는 경우 하십시오 hello Capptain 웹 사이트 toomigrate too1.1.1를 먼저 참조 다음 절차를 수행 하는 hello를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="edd48-116">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="edd48-116">Nuget package</span></span>
<span data-ttu-id="edd48-117">**Capptain.WindowsPhone**을 **MicrosoftAzure.MobileEngagement** Nuget 패키지로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="edd48-118">Mobile Engagement 적용</span><span class="sxs-lookup"><span data-stu-id="edd48-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="edd48-119">hello SDK hello 단어를 사용 하 여 `Engagement`합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="edd48-120">Tooupdate 프로젝트 toomatch 해야이 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="edd48-121">Toouninstall 현재 Capptain nuget 패키지를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="edd48-122">Capptain 리소스 폴더의 모든 변경 내용도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="edd48-123">Tookeep 하려는 경우 해당 파일의 복사본을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="edd48-124">그 후 hello 새 Microsoft Azure Engagement nuget 패키지를 프로젝트에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="edd48-125">해당 패키지는 [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement)에서 직접 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="edd48-126">프로젝트 참조를 Engagement에서 사용 되는 및 hello 새 Engagement DLL tooyour 추가 하는 모든 리소스 파일에이 작업으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="edd48-127">해야 tooclean 프로젝트 참조 Capptain DLL 참조를 삭제 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="edd48-128">이 적용 하지 않을 경우 hello 버전 Capptain의 충돌 하는 및 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="edd48-129">Capptain 리소스를 사용자 지정한 경우 이전 파일 내용을 복사한 hello 새 Engagement 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="edd48-130">Xaml 및 cs 파일을 모두 업데이트 toobe 한지 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="edd48-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="edd48-131">이러한 단계가 완료 되 면 hello 새 Engagement 참조에 의해 tooreplace 이전 Capptain 참조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="edd48-132">모든 Capptain 네임 스페이스 업데이트 toobe가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="edd48-133">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="edd48-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="edd48-134">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="edd48-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="edd48-135">"Capptain"을 포함하는 모든 Capptain 클래스는 이제 "Engagement"를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="edd48-136">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="edd48-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="edd48-137">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="edd48-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="edd48-138">xaml 파일에서는 Capptain 네임스페이스와 특성도 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="edd48-139">마이그레이션 전:</span><span class="sxs-lookup"><span data-stu-id="edd48-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="edd48-140">마이그레이션 후:</span><span class="sxs-lookup"><span data-stu-id="edd48-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="edd48-141">Hello Capptain 그림 등의 다른 리소스에 대 한,이 또한 있다가 이름이 바뀐된 toouse "계약" 점에 유의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="edd48-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="edd48-142">응용 프로그램 ID/SDK 키</span><span class="sxs-lookup"><span data-stu-id="edd48-142">Application ID / SDK Key</span></span>
<span data-ttu-id="edd48-143">Engagement에서는 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-143">Engagement uses a connection string.</span></span> <span data-ttu-id="edd48-144">응용 프로그램 ID 및 Mobile Engagement와 SDK 키 toospecify 없는, 하기만 하면 toospecify 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="edd48-145">EngagementConfiguration 파일에서 연결 문자열을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="edd48-146">hello Engagement 구성에서 설정할 수 있습니다 프로그램 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="edd48-147">이 파일 toospecify를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="edd48-148">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="edd48-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="edd48-149">런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:</span><span class="sxs-lookup"><span data-stu-id="edd48-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="edd48-150">응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="edd48-151">항목 이름 변경</span><span class="sxs-lookup"><span data-stu-id="edd48-151">Items name change</span></span>
<span data-ttu-id="edd48-152">*capptain*이라는 모든 항목은 *engagement*라고 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="edd48-153">마찬가지로 *Capptain* 너무*Engagement*합니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="edd48-154">일반적으로 사용되는 Capptain 항목의 예제:</span><span class="sxs-lookup"><span data-stu-id="edd48-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="edd48-155">CapptainConfiguration의 이름은 EngagementConfiguration으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="edd48-156">CapptainAgent의 이름은 EngagementAgent로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="edd48-157">CapptainReach의 이름은 EngagementReach로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="edd48-158">CapptainHttpConfig의 이름은 EngagementHttpConfig로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="edd48-159">GetCapptainPageName의 이름은 GetEngagementPageName으로 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="edd48-160">이와 같이 바뀐 이름은 재정의되는 메서드에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="edd48-160">Note that rename also affects overridden methods.</span></span>

