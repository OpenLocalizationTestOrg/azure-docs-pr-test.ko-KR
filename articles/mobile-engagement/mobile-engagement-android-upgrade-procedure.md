---
title: "Azure Mobile Engagement Android SDK 통합"
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
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="63dd5-103">업그레이드 절차</span><span class="sxs-lookup"><span data-stu-id="63dd5-103">Upgrade procedures</span></span>
<span data-ttu-id="63dd5-104">이전 버전의 SDK를 응용 프로그램에 이미 통합한 경우에는 SDK를 업그레이드할 때 다음 사항을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="63dd5-105">여러 SDK 버전을 건너뛴 경우에는 여러 절차를 수행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="63dd5-106">예를 들어 1.4.0에서 1.6.0으로 마이그레이션하는 경우 먼저 "1.4.0에서 1.5.0으로" 절차를 따른 다음 "1.5.0에서 1.6.0으로" 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="63dd5-107">업그레이드를 수행하려는 소스 버전이 무엇이든, `mobile-engagement-VERSION.jar` 을 새로운 파일로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="63dd5-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="63dd5-108">4.2.0 ~ 4.2.1</span><span class="sxs-lookup"><span data-stu-id="63dd5-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="63dd5-109">이 단계는 실제로 모든 버전의 SDK에서 실행할 수 있으며 도달률 활동을 통합할 때 보안을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="63dd5-110">이제 모든 도달률 활동에 `exported="false"` 을(를) 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="63dd5-111">도달률 활동은 이제 사용자의 `AndroidManifest.xml`에서 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="63dd5-112">4.0.0에서 4.1.0으로</span><span class="sxs-lookup"><span data-stu-id="63dd5-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="63dd5-113">이제 SDK가 Android M에서 새 권한 모델을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="63dd5-114">위치 기능 또는 큰 그림 알림을 사용하는 경우 [이 섹션](mobile-engagement-android-integrate-engagement.md#android-m-permissions)을 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="63dd5-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="63dd5-115">새 권한 모델 외에도 이제 런타임 시 위치 기능 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="63dd5-116">위치에 대한 매니페스트 매개 변수와 계속 호환 가능하지만 더 이상 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="63dd5-117">런타임 구성을 사용하려면 ``AndroidManifest.xml``에서 다음 섹션을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="63dd5-118">대신 런타임 구성을 사용하려면 [이 업데이트된 절차](mobile-engagement-android-integrate-engagement.md#location-reporting) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="63dd5-119">3.0.0에서 4.0.0으로</span><span class="sxs-lookup"><span data-stu-id="63dd5-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="63dd5-120">네이티브 푸시</span><span class="sxs-lookup"><span data-stu-id="63dd5-120">Native push</span></span>
<span data-ttu-id="63dd5-121">네이티브 푸시(GCM/ADM)가 이제 앱 알림에도 사용되므로 모든 푸시 캠페인 유형에 대한 네이티브 푸시 자격 증명을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="63dd5-122">아직 하지 않았다면 [이 절차](mobile-engagement-android-integrate-engagement-reach.md#native-push)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="63dd5-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="63dd5-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="63dd5-123">AndroidManifest.xml</span></span>
<span data-ttu-id="63dd5-124">도달률 통합이 ``AndroidManifest.xml``에서 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="63dd5-125">다음을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-125">Replace this:</span></span>

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

<span data-ttu-id="63dd5-126">기준</span><span class="sxs-lookup"><span data-stu-id="63dd5-126">By</span></span>

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

<span data-ttu-id="63dd5-127">이제 공지(텍스트/웹 콘텐츠 포함) 또는 설문 조사를 클릭할 때 로딩 화면이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="63dd5-128">해당 캠페인이 4.0.0에서 작동하려면 이를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="63dd5-129">리소스</span><span class="sxs-lookup"><span data-stu-id="63dd5-129">Resources</span></span>
<span data-ttu-id="63dd5-130">새 `res/layout/engagement_loading.xml` 파일을 프로젝트에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="63dd5-131">2.4.0에서 3.0.0으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="63dd5-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="63dd5-132">아래에서는 SDK 통합을 Capptain SAS 제공 Capptain 서비스에서 Azure Mobile Engagement 구동 앱으로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="63dd5-133">이전 버전에서 마이그레이션하는 경우 Capptain 웹 사이트를 참조하여 먼저 2.4.0으로 마이그레이션한 후 다음 절차를 적용하세요.</span><span class="sxs-lookup"><span data-stu-id="63dd5-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63dd5-134">Capptain과 Mobile Engagement는 같은 서비스가 아니며, 아래에서 제공하는 절차에서는 클라이언트 앱을 마이그레이션하는 방법만 중점적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="63dd5-135">앱에서 SDK를 마이그레이션해도 데이터가 Capptain 서버에서 Mobile Engagement 서버로 마이그레이션되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="63dd5-136">JAR 파일</span><span class="sxs-lookup"><span data-stu-id="63dd5-136">JAR file</span></span>
<span data-ttu-id="63dd5-137">`libs` 폴더에서 `capptain.jar`을(를) `mobile-engagement-VERSION.jar`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="63dd5-138">리소스 파일</span><span class="sxs-lookup"><span data-stu-id="63dd5-138">Resource files</span></span>
<span data-ttu-id="63dd5-139">제공하는 모든 리소스 파일(`capptain_`이(가) 접두사로 지정됨)을 새 파일(`engagement_`이(가) 접두사로 지정됨)로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="63dd5-140">해당 파일을 사용자 지정한 경우 새 파일에 대해 모든 사용자 지정 내용을 다시 적용해야 하며, **리소스 파일의 모든 식별자 이름이 바뀝니다**.</span><span class="sxs-lookup"><span data-stu-id="63dd5-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="63dd5-141">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="63dd5-141">Application ID</span></span>
<span data-ttu-id="63dd5-142">이제 Engagement에서 연결 문자열을 사용하여 응용 프로그램 식별자와 같은 SDK 식별자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="63dd5-143">다음과 같은 시작 관리자 작업에서 `EngagementAgent.init` 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="63dd5-144">응용 프로그램의 연결 문자열은 Azure 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="63dd5-145">`EngagementAgent.init`이(가) 해당 메서드를 대체하므로, `CapptainAgent.configure`에 대한 모든 호출을 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="63dd5-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="63dd5-146">`appId`은(는) 더 이상 `AndroidManifest.xml`을(를) 사용하여 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="63dd5-147">다음 섹션이 있는 경우 `AndroidManifest.xml`에서 이 섹션을 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="63dd5-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="63dd5-148">Java API</span><span class="sxs-lookup"><span data-stu-id="63dd5-148">Java API</span></span>
<span data-ttu-id="63dd5-149">SDK의 모든 Java 클래스를 호출할 때마다 이름을 바꿔야 합니다. 예를 들어 `CapptainAgent.getInstance(this)`의 이름은 `EngagementAgent.getInstance(this)`(으)로 바꿔야 하고, `extends CapptainActivity`의 이름은 `extends EngagementActivity`(으)로 바꿔야 하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="63dd5-150">기본 에이전트 기본 설정 파일과 통합된 경우 기본 파일 이름은 이제 `engagement.agent`이고 키는 `engagement:agent`입니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="63dd5-151">웹 공지를 만들 때 Javascript 바인더는 이제 `engagementReachContent`입니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="63dd5-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="63dd5-152">AndroidManifest.xml</span></span>
<span data-ttu-id="63dd5-153">많은 변경이 발생했으며, 서비스가 더 이상 공유되지 않고 많은 수신기를 더 이상 탐색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="63dd5-154">서비스 선언은 더욱 간단합니다. 의도 필터 및 그 안의 모든 메타데이터를 제거한 다음 `exportable=false`을(를) 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="63dd5-155">또한 모든 항목이 Engagement를 사용하도록 이름이 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="63dd5-156">이제 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="63dd5-157">테스트 로그를 활성화하려는 경우 이제 meta-data가 응용 프로그램 태그로 이동되었고 다음과 같이 이름이 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="63dd5-158">모든 다른 meta-data 이름이 바뀌었으며 전체 목록은 다음과 같습니다(이름 바꾸기에서는 사용자가 사용하는 이름만 사용함).</span><span class="sxs-lookup"><span data-stu-id="63dd5-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="63dd5-159">Google Play 및 SmartAd 추적이 SDK에서 제거되었습니다. 대체하지 않고 이 부분을 제거하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="63dd5-160">도달률 활동은 이제 다음과 같이 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-160">The Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="63dd5-161">사용자 지정 도달률 활동이 있는 경우 `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` 또는 `com.microsoft.azure.engagement.reach.intent.action.POLL`와(과) 일치하도록 의도 작업을 변경하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="63dd5-162">브로드캐스트 수신기 이름이 바뀌었으며, 이제 `exported=false`을(를) 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="63dd5-163">새 사양이 포함된 수신기의 전체 목록은 다음과 같습니다(이름 바꾸기에서는 사용자가 사용하는 이름만 사용함).</span><span class="sxs-lookup"><span data-stu-id="63dd5-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="63dd5-164">추적 수신기가 제거되었으므로, 이 섹션을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="63dd5-165">브로드캐스트 수신기의 구현 선언 **EngagementMessageReceiver**가 `AndroidManifest.xml`에서 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="63dd5-166">즉, XMPP 엔터티 및 API에서 임의의 XMPP 보내고 제거하는 API와 장치 간의 메시지를 주고받는 API가 제거되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="63dd5-167">따라서 **EngagementMessageReceiver** 구현에서 다음 콜백을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="63dd5-168">and</span><span class="sxs-lookup"><span data-stu-id="63dd5-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="63dd5-169">그런 다음 아래의 **EngagementAgent** 에 대한 모든 호출을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="63dd5-170">and</span><span class="sxs-lookup"><span data-stu-id="63dd5-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="63dd5-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="63dd5-171">Proguard</span></span>
<span data-ttu-id="63dd5-172">Proguard 구성은 브랜드 재지정의 영향을 받을 수 있으며, 규칙은 이제 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="63dd5-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

