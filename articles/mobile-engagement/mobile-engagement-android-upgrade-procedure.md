---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="490c5-103">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="490c5-103">Upgrade procedures</span></span>
<span data-ttu-id="490c5-104">통합 한 경우 이미이 SDK의 이전 버전 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="490c5-105">여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="490c5-106">예를 들어 1.4.0에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too1.6.0 "1.4.0에서 too1.5.0" 프로시저 다음 hello "1.5.0가에서 too1.6.0" 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="490c5-107">에서 업그레이드 하는 hello 버전과 상관 없이 해야 tooreplace hello `mobile-engagement-VERSION.jar` 새 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="490c5-108">4.2.0에서 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="490c5-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="490c5-109">실제로 hello SDK의 모든 버전에이 단계를 수행할 수에 보안 향상 Reach 활동을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="490c5-110">이제 추가할지를 묻는 `exported="false"` tooall Reach 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="490c5-111">도달률 활동은 이제 사용자의 `AndroidManifest.xml`에서 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a><span data-ttu-id="490c5-112">4.0.0에서 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="490c5-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="490c5-113">hello SDK 지금 핸들 새 사용 권한 모델 Android M에서입니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="490c5-114">위치 기능 또는 큰 그림 알림을 사용하는 경우 [이 섹션](mobile-engagement-android-integrate-engagement.md#android-m-permissions)을 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="490c5-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="490c5-115">또한 새 사용 권한 모델 toohello 이제 지원 런타임에 위치 기능을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="490c5-116">म hello 매니페스트 매개 변수 위치에 대 한 여전히 호환 되지만 이제 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="490c5-117">toouse 런타임 구성 제거 hello 다음 섹션에서 프로그램 ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="490c5-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="490c5-118">읽을 [프로시저 업데이트](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse 런타임 구성 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="490c5-119">3.0.0에서 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="490c5-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="490c5-120">네이티브 푸시</span><span class="sxs-lookup"><span data-stu-id="490c5-120">Native push</span></span>
<span data-ttu-id="490c5-121">네이티브 푸시 GCM/ADM ()는 이제에 사용 앱 알림에서 때문에 모든 유형의 푸시 캠페인에 대 한 hello 네이티브 푸시 자격 증명을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="490c5-122">아직 하지 않았다면 [이 절차](mobile-engagement-android-integrate-engagement-reach.md#native-push)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="490c5-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="490c5-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="490c5-123">AndroidManifest.xml</span></span>
<span data-ttu-id="490c5-124">도달률 통합이 ``AndroidManifest.xml``에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="490c5-125">다음을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="490c5-126">기준</span><span class="sxs-lookup"><span data-stu-id="490c5-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="490c5-127">이제 공지(텍스트/웹 콘텐츠 포함) 또는 설문 조사를 클릭할 때 로딩 화면이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="490c5-128">에 tooadd이 해당 캠페인 toowork 4.0.0에 대 한</span><span class="sxs-lookup"><span data-stu-id="490c5-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="490c5-129">리소스</span><span class="sxs-lookup"><span data-stu-id="490c5-129">Resources</span></span>
<span data-ttu-id="490c5-130">새 hello 포함 `res/layout/engagement_loading.xml` 하 여 프로젝트에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="490c5-131">2.4.0에서 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="490c5-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="490c5-132">hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="490c5-133">이전 버전에서 마이그레이션하려는 경우 먼저 hello Capptain 웹 사이트 toomigrate too2.4.0를 참조 하십시오 고 절차를 수행 하는 hello를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="490c5-134">Capptain Mobile Engagement 하지 hello 같은 서비스 및 highlights만 아래 어떻게 toomigrate hello 클라이언트 응용 프로그램에 주어진 프로시저 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="490c5-135">Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="490c5-136">JAR 파일</span><span class="sxs-lookup"><span data-stu-id="490c5-136">JAR file</span></span>
<span data-ttu-id="490c5-137">`libs` 폴더에서 `capptain.jar`을(를) `mobile-engagement-VERSION.jar`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="490c5-138">리소스 파일</span><span class="sxs-lookup"><span data-stu-id="490c5-138">Resource files</span></span>
<span data-ttu-id="490c5-139">제공 하는 모든 리소스 파일 (접두사로 `capptain_`) hello 새로 toobe 대체가 (접두사로 `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="490c5-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="490c5-140">Toore 해야 해당 파일을 사용자 지정한 경우-hello 새 파일에서 사용자 지정을 적용 **hello 리소스 파일의 모든 hello 식별자 이름이 바뀐**합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="490c5-141">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="490c5-141">Application ID</span></span>
<span data-ttu-id="490c5-142">이제 Engagement hello 응용 프로그램 식별자와 같은 연결 문자열 tooconfigure hello SDK 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="490c5-143">Toouse 있는 `EngagementAgent.init` 에서 다음과 같이 시작 관리자 활동이 메서드:</span><span class="sxs-lookup"><span data-stu-id="490c5-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="490c5-144">응용 프로그램에 대 한 연결 문자열 hello Azure 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="490c5-145">너무 대 한 모든 호출을 제거 하십시오`CapptainAgent.configure` 으로 `EngagementAgent.init` 해당 메서드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="490c5-146">hello `appId` 더 이상 사용 하 여 구성할 수 `AndroidManifest.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="490c5-147">다음 섹션이 있는 경우 `AndroidManifest.xml`에서 이 섹션을 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="490c5-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="490c5-148">Java API</span><span class="sxs-lookup"><span data-stu-id="490c5-148">Java API</span></span>
<span data-ttu-id="490c5-149">모든 호출 tooany 우리의 SDK의 Java 클래스의 이름을 바꿀 toobe에 예를 들어 `CapptainAgent.getInstance(this)` 바꿔야 `EngagementAgent.getInstance(this)`, `extends CapptainActivity` 바꿔야 `extends EngagementActivity` 등...</span><span class="sxs-lookup"><span data-stu-id="490c5-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="490c5-150">기본 에이전트 기본 설정 파일에 통합 된 경우 hello 기본 파일 이름은 아닌 `engagement.agent` 되며 hello 키 `engagement:agent`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="490c5-151">웹 공지를 만들 때는 hello Javascript 바인더는 이제 `engagementReachContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="490c5-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="490c5-152">AndroidManifest.xml</span></span>
<span data-ttu-id="490c5-153">많이 변경 내용이 있습니다, hello 서비스는 더 이상 공유 되지 않습니다 및 수신자의 많은 더 이상 내보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="490c5-154">hello 서비스 선언을 올바르게 간단 합니다. hello 의도 필터와, 그 안의 모든 메타 데이터를 제거 하 고 추가 `exportable=false`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="490c5-155">또한 이름이 바뀐된 toouse engagement는 모두.</span><span class="sxs-lookup"><span data-stu-id="490c5-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="490c5-156">이제 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="490c5-157">이제 hello 메타 데이터 되었습니다 tooenable 테스트 로그에 하려는 경우 toohello 응용 프로그램 태그를 이동 하 고 이름이 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="490c5-158">모든 다른 메타 데이터의 이름이 변경 되었습니다 방금, (물론 이름 바꾸기만 hello 구성 사용 하면) hello 전체 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="490c5-159">Google Play 및 SmartAd 추적 없어졌습니다. SDK에서 하기만 하면 tooremove이 대체 하지 않고:</span><span class="sxs-lookup"><span data-stu-id="490c5-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="490c5-160">hello Reach 활동은 이제 다음과 같이 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-160">hello Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="490c5-161">유일한 toochange hello 의도 작업 toomatch 하거나 필요한 사용자 지정 범위 활동을 설정한 경우 `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` 또는 `com.microsoft.azure.engagement.reach.intent.action.POLL`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="490c5-162">hello 브로드캐스트 수신기 이름이 바뀐 플러스 이제 추가 `exported=false`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="490c5-163">Hello (물론 이름 바꾸기만 hello 구성 사용 하면) hello 새 사양으로 hello 수신자의 전체 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="490c5-164">추적 수신기 제거 되어, tooremove이이 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="490c5-165">Hello hello의 구현 선언 수신기를 브로드캐스팅하 참고 **EngagementMessageReceiver** hello에서 변경 되었습니다. `AndroidManifest.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="490c5-166">임의 XMPP 임의의 XMPP 엔터티에서 메시지 hello API toosend 및 제거 하기 때문에이 API toosend hello 및 장치 간에 메시지 송수신 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="490c5-167">따라서 있는 또한 toodelete hello에서 콜백을 다음 프로그램 **EngagementMessageReceiver** 구현:</span><span class="sxs-lookup"><span data-stu-id="490c5-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="490c5-168">and</span><span class="sxs-lookup"><span data-stu-id="490c5-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="490c5-169">그런 다음 아래의 **EngagementAgent** 에 대한 모든 호출을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="490c5-170">and</span><span class="sxs-lookup"><span data-stu-id="490c5-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="490c5-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="490c5-171">Proguard</span></span>
<span data-ttu-id="490c5-172">Proguard 구성 방법, 규칙은 이제와 같은 계획 hello 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490c5-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

