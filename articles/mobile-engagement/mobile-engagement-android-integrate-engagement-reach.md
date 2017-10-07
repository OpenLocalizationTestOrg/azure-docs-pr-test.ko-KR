---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="68832-103">TooIntegrate Engagement Android에 도달 하는 방법</span><span class="sxs-lookup"><span data-stu-id="68832-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="68832-104">이 가이드를 수행 하기 전에 Android에서 Engagement tooIntegrate 문서화 하는 방법을 hello에 설명 된 hello 통합 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="68832-105">표준 통합</span><span class="sxs-lookup"><span data-stu-id="68832-105">Standard integration</span></span>

<span data-ttu-id="68832-106">프로젝트에 hello SDK에서에서 Reach 리소스 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="68832-107">Hello에서 hello 파일 복사 `res/layout` 폴더 hello에 hello SDK로 전달 `res/layout` 응용 프로그램의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="68832-108">Hello에서 hello 파일 복사 `res/drawable` 폴더 hello에 hello SDK로 전달 `res/drawable` 응용 프로그램의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="68832-109">`AndroidManifest.xml` 파일을 다음과 같이 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="68832-110">다음 단원을 hello 추가 (hello 사이 `<application>` 및 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="68832-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* <span data-ttu-id="68832-111">부팅 시 클릭 하지 않은이 사용 권한을 tooreplay 시스템 알림이 필요한 (그렇지 않은 경우 디스크에 보관 되지만 더 이상 표시 되지 않습니다, 저장할 필요가 tooinclude이).</span><span class="sxs-lookup"><span data-stu-id="68832-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="68832-112">복사한 다음 단원을 hello를 편집 하 여 (app 및 시스템 인수 둘 다) 알림에 사용 되는 프로그램 아이콘 지정 (hello 사이 `<application>` 및 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="68832-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="68832-113">도달률 캠페인을 만들 때 시스템 알림을 사용하려는 경우 이 섹션은 **필수** 입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="68832-114">Android는 아이콘이 없는 시스템 알림이 표시되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="68832-115">이 섹션 생략 하면 최종 사용자가 되지 않도록 수 tooreceive 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="68832-116">다음 권한을 tooadd hello 필요한 큰 그림을 사용 하 여 시스템 알림 캠페인을 만드는 경우 (hello 후 `</application>` 태그) 누락 된 경우:</span><span class="sxs-lookup"><span data-stu-id="68832-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="68832-117">Android M에서 응용 프로그램이 Android API level 23 이상을 대상으로 하는 경우 ``WRITE_EXTERNAL_STORAGE`` 권한에 사용자 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="68832-118">[이 섹션](mobile-engagement-android-integrate-engagement.md#android-m-permissions)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="68832-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="68832-119">시스템 알림 hello에 지정할 수 있습니다에 대 한 hello 장치 해야 링 및/또는 진동 경우 캠페인에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="68832-120">에 대 한 toowork, 해야 toomake hello 권한 다음 선언 (hello 후 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="68832-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="68832-121">Android 시스템 알림이 표시 되지 않도록이 권한이 없으면 hello 링 또는 hello hello 도달 캠페인 관리자의 옵션 진동를 선택한 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="68832-122">네이티브 푸시</span><span class="sxs-lookup"><span data-stu-id="68832-122">Native Push</span></span>
<span data-ttu-id="68832-123">Reach 모듈을 구성 했으므로 tooconfigure 네이티브 푸시 toobe 수 tooreceive hello 캠페인 hello 장치에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="68832-124">Android에서는 다음 두 가지 서비스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-124">We support two services on Android:</span></span>

* <span data-ttu-id="68832-125">Google Play 장치: 사용 [Google Cloud Messaging] 다음 hello 여 [tooIntegrate Engagement와 GCM 안내 하는 방법을](mobile-engagement-android-gcm-integrate.md) 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="68832-126">Amazon 장치: 사용 [Amazon 장치 메시징] 다음 hello 여 [tooIntegrate Engagement와 ADM 안내 하는 방법을](mobile-engagement-android-adm-integrate.md) 가이드입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="68832-127">Tootarget 하려면 Google Play와 Amazon 장치, 해당 가능한 toohave 개발에 대 한 1 AndroidManifest.xml/APK 내의 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="68832-128">하지만 GCM 코드를 찾을 경우 응용 프로그램 tooAmazon를 전송할 때 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="68832-129">이러한 경우에는 여러 APK를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="68832-130">**응용 프로그램 준비 tooreceive 및 디스플레이 캠페인에 도달 하는 이제는!**</span><span class="sxs-lookup"><span data-stu-id="68832-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="68832-131">Toohandle 데이터 밀어넣기</span><span class="sxs-lookup"><span data-stu-id="68832-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="68832-132">통합</span><span class="sxs-lookup"><span data-stu-id="68832-132">Integration</span></span>
<span data-ttu-id="68832-133">응용 프로그램 toobe 수 tooreceive Reach 데이터 푸시를 하려면 toocreate의 하위 클래스가 있는 `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` hello에서 참조 하 고 `AndroidManifest.xml` 파일 (hello 사이 `<application>` 및/또는 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="68832-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="68832-134">Hello를 재정의할 수 `onDataPushStringReceived` 및 `onDataPushBase64Received` 콜백 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="68832-135">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="68832-136">Category</span><span class="sxs-lookup"><span data-stu-id="68832-136">Category</span></span>
<span data-ttu-id="68832-137">hello 범주 매개 변수의 선택적 데이터 푸시 캠페인을 만들 때 이며 허용 하면 toofilter 데이터 푸시 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="68832-138">다양 한 유형의 데이터 푸시를 처리 하는 몇 가지 브로드캐스트 수신기가 있는 경우에 유용 하거나 toopush 다양 한 종류의 `Base64` 데이터 및 원하는 tooidentify의 형식으로 구문 분석 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="68832-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="68832-139">콜백의 반환 매개 변수</span><span class="sxs-lookup"><span data-stu-id="68832-139">Callbacks' return parameter</span></span>
<span data-ttu-id="68832-140">다음은 몇 가지 지침 tooproperly 핸들 hello의 반환 매개 변수 `onDataPushStringReceived` 및 `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="68832-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="68832-141">브로드캐스트 수신기를 반환 해야 `null` hello 콜백에서 toohandle 데이터 밀어넣기 알 수 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="68832-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="68832-142">브로드캐스트 수신기 여부 hello 데이터 푸시를 처리 해야 하는지 여부를 범주 toodetermine hello를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="68832-143">Hello 브로드캐스트 수신기 중 하나를 반환 해야 `true` hello 콜백에서 hello 데이터 푸시를 허용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="68832-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="68832-144">Hello 브로드캐스트 수신기 중 하나를 반환 해야 `false` hello 콜백에서 hello 데이터 푸시를 인식 하지만 어떤 이유로 든을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="68832-145">예를 들어 반환 `false` hello 받은 데이터 유효 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="68832-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="68832-146">하나 브로드캐스트 수신기 반환 하는 경우 `true` 다른 하나를 반환 하는 동안 `false` hello 동일한 데이터 푸시, hello 동작을 정의 하지 않으면에 대 한 안됩니다입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="68832-147">반환 형식은 hello hello Reach 통계에 대해서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68832-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="68832-148">`Replied`반환 되 hello 브로드캐스트 수신기 중 하나는 증가 `true` 또는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="68832-149">`Actioned`hello 중 브로드캐스트 수신기를 반환 하는 경우에 증가 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="68832-150">어떻게 toocustomize 캠페인</span><span class="sxs-lookup"><span data-stu-id="68832-150">How toocustomize campaigns</span></span>
<span data-ttu-id="68832-151">toocustomize 캠페인 hello Reach SDK에서에서 제공 하는 hello 레이아웃을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="68832-152">Hello 레이아웃에 사용 되는 모든 hello 식별자를 유지 하 고 뷰 텍스트 및 이미지 뷰에 대 한 특히 된 식별자를 사용 하는 hello 뷰의 hello 형식을 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="68832-153">일부 뷰가 사용된 공간만 toohide 또는 형식별 변경 될 수 있으므로 영역을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68832-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="68832-154">제공 된 hello 레이아웃의 toochange hello 유형의 보기를 가져오려는 경우 hello 소스 코드를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="68832-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="68832-155">알림</span><span class="sxs-lookup"><span data-stu-id="68832-155">Notifications</span></span>
<span data-ttu-id="68832-156">두 가지 유형의 알림 즉, 다른 레이아웃 파일을 사용하는 시스템 알림과 앱 내 알림이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="68832-157">시스템 알림</span><span class="sxs-lookup"><span data-stu-id="68832-157">System notifications</span></span>
<span data-ttu-id="68832-158">toouse hello 필요한 toocustomize 시스템 알림을 **범주**합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="68832-159">너무를 건너뛸 수 있는[범주](#categories)합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="68832-160">앱 내 알림</span><span class="sxs-lookup"><span data-stu-id="68832-160">In-app notifications</span></span>
<span data-ttu-id="68832-161">기본적으로 앱 내 알림이 보기를 동적으로 추가 된 toohello 현재 활동 사용자 인터페이스 감사 toohello Android 메서드가 `addContentView()`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="68832-162">이 보기를 알림 오버레이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-162">This is called a notification overlay.</span></span> <span data-ttu-id="68832-163">알림 오버레이 필요 하지 않습니다 toomodify 하면 응용 프로그램에서 모든 레이아웃 때문에 빠른 통합에 매우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="68832-164">알림 오버레이 toomodify hello 모양을 수정할 수 hello 파일 `engagement_notification_area.xml` tooyour 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="68832-165">hello 파일 `engagement_notification_overlay.xml` 알림 오버레이 hello toocreate 사용된 되는 것은 hello 파일 포함 `engagement_notification_area.xml`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="68832-166">또한 사용자 지정할 수 있습니다 toosuit 요구 사항 (예: hello 오버레이 내 hello 알림 영역 위치 지정).</span><span class="sxs-lookup"><span data-stu-id="68832-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="68832-167">작업 레이아웃의 일부로 알림 레이아웃 포함</span><span class="sxs-lookup"><span data-stu-id="68832-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="68832-168">오버레이는 빠른 통합에 적절하지만 특수한 경우에는 불편해지거나 부작용이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="68832-169">hello 오버레이 시스템은 특수 한 작업에 대 한 쉬운 tooprevent 의도 하는 작업 수준에서 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="68832-170">기존 프로그램 레이아웃 감사 toohello Android에서에서 tooinclude 우리의 알림 레이아웃을 결정할 수 있습니다 **포함** 문.</span><span class="sxs-lookup"><span data-stu-id="68832-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="68832-171">hello 다음은 수정 된의 예가 `ListActivity` 레이아웃만 포함 하는 `ListView`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="68832-172">**Engagement 통합 이전:**</span><span class="sxs-lookup"><span data-stu-id="68832-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="68832-173">**Engagement 통합 이후:**</span><span class="sxs-lookup"><span data-stu-id="68832-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="68832-174">이 예에서 hello 원래 레이아웃 hello 최상위 요소는 목록 보기 사용 있으므로 부모 컨테이너를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="68832-175">또한 추가 `android:layout_weight="1"` toobe 수 tooadd 목록 보기 아래에서 보기를 사용 하 여 구성 `android:layout_height="fill_parent"`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="68832-176">hello Engagement Reach SDK는 해당 hello 알림 레이아웃이이 활동에 포함 되 고이 작업에 대 한 오버레이 추가 하지 않는 것에 자동으로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="68832-177">응용 프로그램에 ListActivity를 사용 하는 경우 표시 Reach 오버레이 수 없게 됩니다 응답할 tooclicked hello 목록 뷰의 항목에서 더 이상.</span><span class="sxs-lookup"><span data-stu-id="68832-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="68832-178">이는 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-178">This is a known issue.</span></span> <span data-ttu-id="68832-179">toowork이이 문제를 해결 하는 좋습니다 hello 이전 샘플에서와 같은 고유한 목록 활동 레이아웃에서 tooembed hello 알림 레이아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="68832-180">작업별 응용 프로그램 알림 비활성화</span><span class="sxs-lookup"><span data-stu-id="68832-180">Disabling application notification per activity</span></span>
<span data-ttu-id="68832-181">Hello를 표시 하지 않으려는 경우 오버레이 toobe tooyour 활동을 추가 하 고 자체 레이아웃에 hello 알림 레이아웃을 포함 하지 않으면,이 활동 hello에 대 한 hello 오버레이 비활성화할 수 있습니다 `AndroidManifest.xml` 추가 하 여 한 `meta-data` hello 다음과에서 같은 섹션 예:</span><span class="sxs-lookup"><span data-stu-id="68832-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="68832-182"><a name="categories"></a> 범주</span><span class="sxs-lookup"><span data-stu-id="68832-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="68832-183">레이아웃을 제공 하는 hello를 수정 하는 경우 모든 알림 hello 모양을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="68832-184">범주를 사용 toodefine 대상 다양 한 알림 (가능 동작)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="68832-185">도달률 캠페인을 만들 때 범주를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="68832-186">범주를 사용하면 알림과 설문 조사도 사용자 지정할 수 있습니다. 여기에 대해서는 이 문서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="68832-187">알림에 대 한 범주 처리기 tooregister 해야 tooadd 호출 hello 응용 프로그램 초기화 될 때.</span><span class="sxs-lookup"><span data-stu-id="68832-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68832-188">Hello android: 프로세스 특성에 대 한 hello 경고를 읽어 보십시오 \<android sdk-engagement 프로세스\> hello에 어떻게 진행 하기 전에 Android 주제에 참여 tooIntegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="68832-189">hello 다음 예에서는 가정 hello 이전 경고를 승인 하 고의 하위 클래스를 사용 하 여 `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="68832-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="68832-190">hello `MyNotifier` 개체는 hello 알림 범주 처리기의 hello 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="68832-191">이 알고리즘은 구현한의 hello `EngagementNotifier` 인터페이스 또는 하위 클래스의 기본 구현은 hello: `EngagementDefaultNotifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="68832-192">같은 알림 hello는 여러 종류를 처리할 수 있는, 다음과 같이 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="68832-193">tooreplace hello 기본 범주 구현 hello 다음 예제에서에서와 같은 구현을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="68832-194">처리기에서 사용 되는 hello 현재 범주에서 재정의할 수 메서드에 대부분 매개 변수로 전달 `EngagementDefaultNotifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="68832-195">그 범주는`String` 매개 변수로 전달되거나 `getCategory()` 메서드가 있는 `EngagementReachContent` 개체에서 간접적으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="68832-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="68832-196">메서드를 재정의 하 여 hello 알림 생성 프로세스의 대부분을 변경할 수 있습니다 `EngagementDefaultNotifier`고급 사용자 지정 느껴집니다 무료 tootake hello 기술 문서 및 hello 소스 코드에서 참조에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="68832-197">앱 내 알림</span><span class="sxs-lookup"><span data-stu-id="68832-197">In-app notifications</span></span>
<span data-ttu-id="68832-198">특정 범주에 대 한 대체 레이아웃 toouse만 하려는 경우 다음 예제는 hello와 같이이 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="68832-199">**`my_notification_overlay.xml`의 예제 :**</span><span class="sxs-lookup"><span data-stu-id="68832-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="68832-200">볼 수 있듯이 hello 오버레이 뷰 식별자는 hello 표준 하나 보다 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="68832-201">각 레이아웃에서 오버레이에 고유 식별자를 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="68832-202">**`my_notification_area.xml`의 예제 :**</span><span class="sxs-lookup"><span data-stu-id="68832-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="68832-203">볼 수 있듯이 hello 알림 영역 보기 식별자는 hello 표준 하나 보다 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="68832-204">각 레이아웃에서 알림 영역에 고유 식별자를 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="68832-205">응용 프로그램 (또는 앱에서) 알림 hello 위쪽 hello 화면에 표시 하는 범주에 속하는 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="68832-206">우리는 hello 표준 식별자 자체 hello 알림 영역에 사용 되는 변경 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="68832-207">Toochange, 있다고 tooredefine hello를 원하는 경우 `EngagementDefaultNotifier.prepareInAppArea` 메서드.</span><span class="sxs-lookup"><span data-stu-id="68832-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="68832-208">것이 좋습니다 toolook hello 기술 문서 및의 hello 소스 코드에서 `EngagementNotifier` 및 `EngagementDefaultNotifier` 하려는 경우이 고급 사용자 지정의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="68832-209">시스템 알림</span><span class="sxs-lookup"><span data-stu-id="68832-209">System notifications</span></span>
<span data-ttu-id="68832-210">확장 하 여 `EngagementDefaultNotifier`를 재정의할 수 있습니다 `onNotificationPrepared` hello 기본 구현에서 사용 했던 tooalter hello 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="68832-211">예:</span><span class="sxs-lookup"><span data-stu-id="68832-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="68832-212">이 예제에서는 hello "진행 중" 범주를 사용할 때 진행 중인 이벤트로 표시 되는 콘텐츠에 대 한 시스템 알림.</span><span class="sxs-lookup"><span data-stu-id="68832-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="68832-213">Toobuild hello를 원하는 경우 `Notification` 개체 처음부터 반환할 수 있습니다 `false` toohello 메서드와 호출 `notify` hello에 직접 `NotificationManager`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="68832-214">유지 해야 하는 경우에 `contentIntent`, `deleteIntent` 알림 식별자에서 사용 하는 hello 및 `EngagementReachReceiver`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="68832-215">다음은 그러한 구현에 대한 올바른 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="68832-216">공지만 알림</span><span class="sxs-lookup"><span data-stu-id="68832-216">Notification only announcements</span></span>
<span data-ttu-id="68832-217">hello hello의 관리를 클릭 하는 알림 전용 알림을 재정의 하 여 사용자 지정할 수 있습니다 `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` 준비 toomodify hello `Intent`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="68832-218">이 메서드를 사용 하 여 있습니다 tootune hello 플래그를 쉽게.</span><span class="sxs-lookup"><span data-stu-id="68832-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="68832-219">예를 들어 tooadd hello `SINGLE_TOP` 플래그:</span><span class="sxs-lookup"><span data-stu-id="68832-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="68832-220">레거시 Engagement 사용자에 대 한 동작 없이 시스템 알림 URL 이제가 실행 하는 hello 응용 프로그램 작업 URL 없이 공지 사항으로이 메서드를 호출할 수 있으므로 백그라운드에서 되었으면 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="68832-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="68832-221">Hello 의도 사용자 지정할 때를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="68832-222">또한 `EngagementNotifier.executeNotifAnnouncementAction` 을(를) 처음부터 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="68832-223">알림 수명 주기</span><span class="sxs-lookup"><span data-stu-id="68832-223">Notification life cycle</span></span>
<span data-ttu-id="68832-224">Hello에서 일부 수명 주기 메서드를 호출 hello 기본 범주를 사용할 경우 `EngagementReachInteractiveContent` tooreport 통계 및 업데이트 hello 캠페인 상태 개체:</span><span class="sxs-lookup"><span data-stu-id="68832-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="68832-225">Hello 알림을 응용 프로그램에 표시 하거나 hello 상태 표시줄에 배치할 때 hello `displayNotification` (보고 하는 통계) 메서드를 호출 하 여 `EngagementReachAgent` 경우 `handleNotification` 반환 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="68832-226">Hello 알림은 해제 하는 경우 hello `exitNotification` 메서드는 통계는 보고 되며 다음 캠페인을 지금 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="68832-227">Hello 알림의 클릭할 경우 `actionNotification` 은 호출 통계는 보고 되 고 연결 된 hello 의도 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68832-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="68832-228">경우 구현 `EngagementNotifier` 바이패스 hello 기본 동작, 혼자서 toocall 이러한 수명 주기 메서드를가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="68832-229">다음 예제는 hello hello 기본 동작이 사용 하지 않을 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="68832-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="68832-230">범주 처리를 처음부터 구현한 경우처럼 `EngagementDefaultNotifier`을(를) 확장하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="68832-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="68832-231">Hello를 문제가 시스템 알림에 대해 `onNotificationPrepared` 수정한 및 `contentIntent` 또는 `deleteIntent` hello에 `Notification` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="68832-232">가 앱에서 알림을 `prepareInAppArea`있는지 toomap 사이, `actionNotification` U.I 컨트롤의 tooone 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="68832-233">경우 `handleNotification` hello 콘텐츠 예외가 throw는 삭제 및 `dropContent` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="68832-234">이 사항은 통계로 보고되며 이제 다음 캠페인을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="68832-235">알림 및 설문 조사</span><span class="sxs-lookup"><span data-stu-id="68832-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="68832-236">레이아웃</span><span class="sxs-lookup"><span data-stu-id="68832-236">Layouts</span></span>
<span data-ttu-id="68832-237">Hello를 수정할 수 있습니다 `engagement_text_announcement.xml`, `engagement_web_announcement.xml` 및 `engagement_poll.xml` toocustomize 텍스트 공지, 웹 공지 및 설문 조사의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="68832-238">이러한 파일 hello 제목 영역 및 hello 단추 영역에 대 한 두 가지 일반적인 레이아웃을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="68832-239">hello 제목에 대 한 hello 레이아웃은 `engagement_content_title.xml` 및 사용 하 여 hello hello 배경에 대 한 호응 그릴 수 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="68832-240">hello hello 작업 및 끝내기 단추 레이아웃은 `engagement_button_bar.xml` 및 사용 하 여 hello hello 배경에 대 한 호응 그릴 수 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="68832-241">에 설문 조사 질문 레이아웃 hello 및 선택 항목은 동적으로 확장 하 여 여러 번 hello를 사용 하 여 `engagement_question.xml` hello 질문과 hello에 대 한 레이아웃 파일 `engagement_choice.xml` hello 선택 항목에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="68832-242">범주</span><span class="sxs-lookup"><span data-stu-id="68832-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="68832-243">대체 레이아웃</span><span class="sxs-lookup"><span data-stu-id="68832-243">Alternate layouts</span></span>
<span data-ttu-id="68832-244">알림, 같이 hello 캠페인의 범주는 공지 및 설문 조사의 toohave 사용 되는 대체 레이아웃 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="68832-245">예를 들어 toocreate 텍스트 공지에 대 한 범주를 확장할 수 있습니다 `EngagementTextAnnouncementActivity` hello 참조 `AndroidManifest.xml` 파일:</span><span class="sxs-lookup"><span data-stu-id="68832-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="68832-246">참고이 hello 범주 hello 의도에 필터를 사용 toomake hello 차이 hello 기본 알림 활동을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="68832-247">Reach SDK hello hello 의도 시스템 tooresolve hello 오른쪽 활동을 사용 하 여 특정 범주에 대 한 및 대체 hello 기본 범주에 hello 확인에 실패 한 경우.</span><span class="sxs-lookup"><span data-stu-id="68832-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="68832-248">Tooimplement 있는 `MyCustomTextAnnouncementActivity`, 방금 toochange hello 레이아웃 (하지만 hello 식별자 동일한 보기 유지), 하기만 하면 같은 toodefine hello 클래스에 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="68832-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="68832-249">텍스트 공지 tooreplace hello 기본 범주를 바꾸면 `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` 구현에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="68832-250">웹 알림 및 설문 조사는 유사한 방식으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="68832-251">확장할 수에 대 한 웹 알림을 `EngagementWebAnnouncementActivity` hello에서 활동이 선언 `AndroidManifest.xml` hello 다음 예제에서에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="68832-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="68832-252">폴링 확장 `EngagementPollActivity` 프로그램에 hello를 선언 하 고 `AndroidManifest.xml` hello 다음 예제에서에서와 같이:</span><span class="sxs-lookup"><span data-stu-id="68832-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="68832-253">처음부터 구현</span><span class="sxs-lookup"><span data-stu-id="68832-253">Implementation from scratch</span></span>
<span data-ttu-id="68832-254">Hello 중 하나를 확장 하지 않고 알림 (및 설문 조사) 작업에 대 한 범주를 구현할 수 `Engagement*Activity` Reach SDK를 hello 클래스에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="68832-255">이 유용한 예를 들어 toodefine hello 표준 레이아웃으로 동일한 뷰 hello를 사용 하지 않는 레이아웃 하려는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="68832-256">와 같은 고급 알림 사용자 지정을 위한 것이 좋습니다 toolook hello 표준 구현의 hello 소스 코드에서.</span><span class="sxs-lookup"><span data-stu-id="68832-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="68832-257">다음 일부의 tookeep 염두에서은: Reach hello 콘텐츠 식별자는 추가 매개 변수가 더하기 hello 활동 특정 의도 (해당 toohello 의도 필터)가 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68832-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="68832-258">때 hello 만들기는 캠페인 hello 웹 사이트에서 사용자 지정한 hello 필드가 포함 된 tooretrieve hello 콘텐츠 개체를 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68832-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="68832-259">Hello에 hello 내용이 표시 되 보고 해야 통계의 경우 `onResume` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="68832-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="68832-260">그런 다음 반드시 toocall 하거나 `actionContent(this)` 또는 `exitContent(this)` hello 활동 배경으로 모드로 전환 되기 전에 hello 콘텐츠 개체에 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="68832-261">호출 하지 않으면 `actionContent` 또는 `exitContent`, 통계 전송 되지 않습니다. (예: hello 캠페인에 없는 분석) 및 더 중요 한 사실은 hello hello 응용 프로그램 프로세스를 다시 시작 될 때까지 다음 캠페인을 받을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="68832-262">방향 또는 기타 구성 변경 내용을 hello 코드 까다로운 toodetermine 여부 hello 활동 배경 진입 여부, 수 있는지 hello 콘텐츠가 보고 되는 hello 사용자가 (하거나 hello 활동 끝났습니다 표준 구현을 사용 하면 hello 키를 누르면 `HOME` 또는 `BACK`) 하지만 not hello 방향을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="68832-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="68832-263">다음은 hello 구현의 hello 흥미로운 부분이입니다.</span><span class="sxs-lookup"><span data-stu-id="68832-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="68832-264">호출 하면 볼 수 있듯이 `actionContent(this)` hello 활동을 완료 한 후 `exitContent(this)` 영향을 주지 않고 안전 하 게 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68832-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon 장치 메시징]:https://developer.amazon.com/sdk/adm.html
