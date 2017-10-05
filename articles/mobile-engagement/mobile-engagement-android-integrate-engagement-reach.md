---
title: "Azure Mobile Engagement Android SDK 통합"
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
ms.openlocfilehash: 26ba47b19f3a503693d60d344ad39b9eba74fe99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-reach-on-android"></a><span data-ttu-id="55b6a-103">Android에서 Engagement 도달률을 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="55b6a-103">How to Integrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="55b6a-104">이 가이드를 수행하기 전에 Android 문서의 Engagement를 통합하는 방법에 설명된 통합 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="55b6a-105">표준 통합</span><span class="sxs-lookup"><span data-stu-id="55b6a-105">Standard integration</span></span>

<span data-ttu-id="55b6a-106">프로젝트의 SDK에서 도달률 리소스 파일을 다음과 같이 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-106">Copy Reach resource files from the SDK in your project :</span></span>

* <span data-ttu-id="55b6a-107">SDK와 함께 제공된 `res/layout` 폴더의 파일을 응용 프로그램의 `res/layout` 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-107">Copy the files from the `res/layout` folder delivered with the SDK into the `res/layout` folder of your application.</span></span>
* <span data-ttu-id="55b6a-108">SDK와 함께 제공된 `res/drawable` 폴더의 파일을 응용 프로그램의 `res/drawable` 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-108">Copy the files from the `res/drawable` folder delivered with the SDK into the `res/drawable` folder of your application.</span></span>

<span data-ttu-id="55b6a-109">`AndroidManifest.xml` 파일을 다음과 같이 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="55b6a-110">`<application>` 태그와 `</application>` 태그 사이에 다음 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-110">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
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
* <span data-ttu-id="55b6a-111">부팅할 때 클릭하지 않은 시스템 알림을 재생하려면 이 권한이 있어야 합니다. 그렇지 않으면 시스템 알림이 디스크에서 유지되지만 더 이상 표시되지 않습니다. 따라서 실제로 이 권한을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-111">You need this permission to replay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have to include this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="55b6a-112">다음 섹션(`<application>` 태그와 `</application>` 태그 사이)을 복사 및 편집하여 알림(앱과 시스템 둘 다의 알림)에 사용된 아이콘을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-112">Specify an icon used for notifications (both in app and system ones) by copying and editing the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="55b6a-113">도달률 캠페인을 만들 때 시스템 알림을 사용하려는 경우 이 섹션은 **필수** 입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="55b6a-114">Android는 아이콘이 없는 시스템 알림이 표시되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="55b6a-115">따라서 이 섹션을 누락하는 경우 최종 사용자가 해당 시스템 알림을 받을 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-115">So if you omit this section, your end users will not be able to receive them.</span></span>
> 
> 

* <span data-ttu-id="55b6a-116">큰 그림을 사용하는 시스템 알림이 있는 캠페인을 만드는 경우 다음 권한을 `</application>` 태그 뒤에 추가해야 합니다(누락된 경우).</span><span class="sxs-lookup"><span data-stu-id="55b6a-116">If you create campaigns with system notifications using big picture, you need to add the following permissions (after the `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="55b6a-117">Android M에서 응용 프로그램이 Android API level 23 이상을 대상으로 하는 경우 ``WRITE_EXTERNAL_STORAGE`` 권한에 사용자 승인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="55b6a-118">[이 섹션](mobile-engagement-android-integrate-engagement.md#android-m-permissions)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="55b6a-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="55b6a-119">또한 시스템 알림을 위해 장치에서 신호음이 울리거나 진동이 작동해야 하는 경우 도달률 캠페인에서 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-119">For system notifications you can also specify in the Reach campaign if the device should ring and/or vibrate.</span></span> <span data-ttu-id="55b6a-120">신호음이나 진동이 작동하도록 하려면 `</application>` 태그 뒤에 다음 권한을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-120">For it to work, you have to make sure you declared the following permission (after the `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="55b6a-121">도달률 캠페인 관리자에서 신호음 또는 진동 옵션을 선택한 경우 이 권한이 없으면 Android에서 시스템 알림이 표시되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-121">Without this permission, Android prevents system notifications from being shown if you checked the ring or the vibrate option in the Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="55b6a-122">네이티브 푸시</span><span class="sxs-lookup"><span data-stu-id="55b6a-122">Native Push</span></span>
<span data-ttu-id="55b6a-123">이제 도달률 모듈을 구성했으므로 장치에서 캠페인을 받을 수 있도록 네이티브 푸시를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-123">Now that you configured Reach module, you need to configure native push to be able to receive the campaigns on the device.</span></span>

<span data-ttu-id="55b6a-124">Android에서는 다음 두 가지 서비스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-124">We support two services on Android:</span></span>

* <span data-ttu-id="55b6a-125">Google Play 장치: [GCM과 Engagement 통합 방법](mobile-engagement-android-gcm-integrate.md) 가이드에 따라 [Google Cloud Messaging] 사용</span><span class="sxs-lookup"><span data-stu-id="55b6a-125">Google Play devices: Use [Google Cloud Messaging] by following the [How to Integrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="55b6a-126">Amazon 장치: [ADM과 Engagement 통합 방법 가이드](mobile-engagement-android-adm-integrate.md)에 따라 [Amazon Device Messaging] 사용</span><span class="sxs-lookup"><span data-stu-id="55b6a-126">Amazon devices: Use [Amazon Device Messaging] by following the [How to Integrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="55b6a-127">Amazon 및 Google Play 장치를 모두 대상으로 하려는 경우 개발을 위한 단일 AndroidManifest.xml/APK 내에 모든 것을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-127">If you want to target both Amazon and Google Play devices, its possible to have everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="55b6a-128">하지만 Amazon에 제출할 경우 GCM 코드가 발견되면 응용 프로그램이 거부될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-128">But when submitting to Amazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="55b6a-129">이러한 경우에는 여러 APK를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="55b6a-130">**이제 응용 프로그램이 도달률 캠페인을 수신하여 표시할 준비가 되었습니다!**</span><span class="sxs-lookup"><span data-stu-id="55b6a-130">**Your application is now ready to receive and display reach campaigns!**</span></span>

## <a name="how-to-handle-data-push"></a><span data-ttu-id="55b6a-131">데이터 푸시를 처리하는 방법</span><span class="sxs-lookup"><span data-stu-id="55b6a-131">How to handle data push</span></span>
### <a name="integration"></a><span data-ttu-id="55b6a-132">통합</span><span class="sxs-lookup"><span data-stu-id="55b6a-132">Integration</span></span>
<span data-ttu-id="55b6a-133">응용 프로그램을 통해 도달률 데이터 푸시를 받으려면 다음과 같이 `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver`의 하위 클래스를 생성하여 `AndroidManifest.xml` 파일에서 해당 클래스를 참조해야 합니다(`<application>` 및/또는 `</application>` 태그 사이).</span><span class="sxs-lookup"><span data-stu-id="55b6a-133">If you want your application to be able to receive Reach data pushes, you have to create a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in the `AndroidManifest.xml` file (between the `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="55b6a-134">그런 다음 `onDataPushStringReceived` 및 `onDataPushBase64Received` 콜백을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-134">Then you can override the `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="55b6a-135">다음은 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-135">Here is an example:</span></span>

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

### <a name="category"></a><span data-ttu-id="55b6a-136">Category</span><span class="sxs-lookup"><span data-stu-id="55b6a-136">Category</span></span>
<span data-ttu-id="55b6a-137">데이터 푸시 캠페인을 만들 때는 필요에 따라 범주 매개 변수를 포함할 수 있으며, 그러면 데이터 푸시를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-137">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="55b6a-138">범주 매개 변수는 여러 유형의 데이터 푸시를 처리하는 여러 브로드캐스트 수신기가 있는 경우 또는 다른 종류의 `Base64` 데이터를 푸시하면서 구문 분석하기 전에 해당 유형을 식별하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="55b6a-139">콜백의 반환 매개 변수</span><span class="sxs-lookup"><span data-stu-id="55b6a-139">Callbacks' return parameter</span></span>
<span data-ttu-id="55b6a-140">다음은 `onDataPushStringReceived` 및 `onDataPushBase64Received`의 반환 매개 변수를 올바르게 처리하기 위한 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-140">Here are some guidelines to properly handle the return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="55b6a-141">브로드캐스트 수신기가 데이터 푸시의 처리 방법을 모르는 경우 콜백에서 `null`을(를) 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-141">A broadcast receiver should return `null` in the callback if it does not know how to handle a data push.</span></span> <span data-ttu-id="55b6a-142">범주를 사용하여 브로드캐스트 수신기가 데이터 푸시를 처리해야 하는지 여부를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-142">You should use the category to determine whether your broadcast receiver should handle the data push or not.</span></span>
* <span data-ttu-id="55b6a-143">브로드캐스트 수신기 중 하나가 데이터 푸시를 허용하는 경우 콜백에서 `true` 을(를) 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-143">One of the broadcast receiver should return `true` in the callback if it accepts the data push.</span></span>
* <span data-ttu-id="55b6a-144">브로드캐스트 수신기 중 하나가 데이터 푸시를 인식하지만 어떤 이유로든 무시한 경우 콜백에서 `false` 을(를) 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-144">One of the broadcast receiver should return `false` in the callback if it recognizes the data push, but discards it for whatever reason.</span></span> <span data-ttu-id="55b6a-145">예를 들어 수신한 데이터가 잘못된 경우 `false` 을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-145">For example, return `false` when the received data is invalid.</span></span>
* <span data-ttu-id="55b6a-146">하나의 브로드캐스트 수신기가 `true`을(를) 반환하는데 다른 브로드캐스트 수신기가 동일한 데이터 푸시에 대해 `false`을(를) 반환하는 경우 동작이 정의되지 않습니다. 따라서 그렇게 해서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-146">If one broadcast receiver returns `true` while another one returns `false` for the same data push, the behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="55b6a-147">반환 형식은 다음과 같이 도달률 통계에서만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-147">The return type is used only for the Reach statistics:</span></span>

* <span data-ttu-id="55b6a-148">`Replied`은(는) 브로드캐스트 수신기 중 하나가 `true` 또는 `false`을(를) 반환한 경우에 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-148">`Replied` is incremented if one of the broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="55b6a-149">`Actioned`은(는) 브로드캐스트 수신기 중 하나가 `true`을(를) 반환한 경우에만 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-149">`Actioned` is incremented only if one of the broadcast receivers returned `true`.</span></span>

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="55b6a-150">캠페인을 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="55b6a-150">How to customize campaigns</span></span>
<span data-ttu-id="55b6a-151">캠페인을 사용자 지정하기 위해 Reach SDK에서 제공하는 레이아웃을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-151">To customize campaigns, you can modify the layouts provided in the Reach SDK.</span></span>

<span data-ttu-id="55b6a-152">레이아웃에 사용된 모든 식별자를 유지하고, 식별자를 사용하는 뷰의 유형(특히 텍스트 뷰 및 이미지 뷰의 유형)을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-152">You should keep all the identifiers used in the layouts and keep the types of the views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="55b6a-153">일부 뷰는 영역을 표시하거나 숨기는 데에만 사용되므로 해당 유형을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-153">Some views are just used to hide or show areas so their type may be changed.</span></span> <span data-ttu-id="55b6a-154">제공된 레이아웃의 뷰 유형을 변경하려는 경우 소스 코드를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="55b6a-154">Please check the source code if you intend to change the type of a view in the provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="55b6a-155">알림</span><span class="sxs-lookup"><span data-stu-id="55b6a-155">Notifications</span></span>
<span data-ttu-id="55b6a-156">두 가지 유형의 알림 즉, 다른 레이아웃 파일을 사용하는 시스템 알림과 앱 내 알림이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="55b6a-157">시스템 알림</span><span class="sxs-lookup"><span data-stu-id="55b6a-157">System notifications</span></span>
<span data-ttu-id="55b6a-158">시스템 알림을 사용자 지정하려면 **범주**를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-158">To customize system notifications you need to use the **categories**.</span></span> <span data-ttu-id="55b6a-159">[범주](#categories)로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-159">You can jump to [Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="55b6a-160">앱 내 알림</span><span class="sxs-lookup"><span data-stu-id="55b6a-160">In-app notifications</span></span>
<span data-ttu-id="55b6a-161">기본적으로 앱 내 알림은 Android 메서드 `addContentView()`덕분에 현재 작업의 사용자 인터페이스에 동적으로 추가되는 뷰입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-161">By default, an in-app notification is a view that is dynamically added to the current activity user interface thanks to the Android method `addContentView()`.</span></span> <span data-ttu-id="55b6a-162">이 보기를 알림 오버레이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-162">This is called a notification overlay.</span></span> <span data-ttu-id="55b6a-163">알림 오버레이는 응용 프로그램에서 레이아웃을 수정하지 않아도 되므로 빠른 통합에 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-163">Notification overlays are great for a fast integration because they do not require you to modify any layout in your application.</span></span>

<span data-ttu-id="55b6a-164">알림 오버레이의 모양을 수정하려면 요구에 맞게 간단히 파일 `engagement_notification_area.xml`을(를) 수정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-164">To modify the look of your notification overlays, you can simply modify the file `engagement_notification_area.xml` to your needs.</span></span>

> [!NOTE]
> <span data-ttu-id="55b6a-165">파일 `engagement_notification_overlay.xml`은(는) 알림 오버레이를 만드는 데 사용되는 파일이며, 이 파일에는 파일`engagement_notification_area.xml`이(가) 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-165">The file `engagement_notification_overlay.xml` is the one that is used to create a notification overlay, it includes the file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="55b6a-166">또한 요구에 맞게 사용자 지정할 수도 있습니다(예: 오버레이 내에서 알림 영역 위치 지정).</span><span class="sxs-lookup"><span data-stu-id="55b6a-166">You can also customize it to suit your needs (such as for positioning the notification area within the overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="55b6a-167">작업 레이아웃의 일부로 알림 레이아웃 포함</span><span class="sxs-lookup"><span data-stu-id="55b6a-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="55b6a-168">오버레이는 빠른 통합에 적절하지만 특수한 경우에는 불편해지거나 부작용이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="55b6a-169">오버레이 시스템을 작업 수준에서 사용자 지정할 수 있으며 특수한 작업의 부작용을 쉽게 예방할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-169">The overlay system can be customized at an activity level, making it easy to prevent side effects for special activities.</span></span>

<span data-ttu-id="55b6a-170">Android의 **include** 문 덕분에 기존 레이아웃에서 알림 레이아웃을 포함하도록 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-170">You can decide to include our notification layout in your existing layout thanks to the Android **include** statement.</span></span> <span data-ttu-id="55b6a-171">다음은 `ListView`을(를) 포함하는 수정된 `ListActivity` 레이아웃의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-171">The following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="55b6a-172">**Engagement 통합 이전:**</span><span class="sxs-lookup"><span data-stu-id="55b6a-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="55b6a-173">**Engagement 통합 이후:**</span><span class="sxs-lookup"><span data-stu-id="55b6a-173">**After Engagement integration :**</span></span>

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

<span data-ttu-id="55b6a-174">이 예제에서는 원래 레이아웃이 최상위 요소로 목록 보기를 사용하므로 부모 컨테이너를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-174">In this example we added a parent container since the original layout used a list view as the top level element.</span></span> <span data-ttu-id="55b6a-175">또한 `android:layout_weight="1"`을(를) 추가했으므로 `android:layout_height="fill_parent"`(으)로 구성한 목록 보기 아래에 뷰를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-175">We also added `android:layout_weight="1"` to be able to add a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="55b6a-176">Engagement Reach SDK는 알림 레이아웃이 이 작업에 포함되었으며 이 작업의 오버레이를 추가하지 않을 것임을 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-176">The Engagement Reach SDK automatically detects that the notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="55b6a-177">응용 프로그램에서 ListActivity를 사용하는 경우 표시되는 도달률 오버레이는 목록 보기의 클릭된 항목에 더 이상 반응하지 못하도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting to clicked items in the list view anymore.</span></span> <span data-ttu-id="55b6a-178">이는 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-178">This is a known issue.</span></span> <span data-ttu-id="55b6a-179">이 문제를 해결하려면 앞의 샘플에서와 같이 고유한 목록 작업 레이아웃에 알림 레이아웃을 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-179">To work around this problem we suggest you to embed the notification layout in your own list activity layout like in the previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="55b6a-180">작업별 응용 프로그램 알림 비활성화</span><span class="sxs-lookup"><span data-stu-id="55b6a-180">Disabling application notification per activity</span></span>
<span data-ttu-id="55b6a-181">작업에 오버레이를 추가하지 않으려는 경우와 고유 레이아웃에 알림 레이아웃을 포함하지 않은 경우 다음 예제와 같이 `meta-data` 섹션을 추가하여 `AndroidManifest.xml`에서 이 작업의 오버레이를 비활성화하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-181">If you don't want the overlay to be added to your activity, and if you don't include the notification layout in your own layout, you can disable the overlay for this activity in the `AndroidManifest.xml` by adding a `meta-data` section like in the following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="55b6a-182"><a name="categories"></a> 범주</span><span class="sxs-lookup"><span data-stu-id="55b6a-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="55b6a-183">제공된 레이아웃을 수정할 경우 모든 알림 모양을 수정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-183">When you modify the provided layouts, you modify the look of all your notifications.</span></span> <span data-ttu-id="55b6a-184">범주를 사용하면 알림의 여러 대상 모양을 정의할 수 있으며 경우에 따라서는 동작도 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-184">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="55b6a-185">도달률 캠페인을 만들 때 범주를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="55b6a-186">범주를 사용하면 알림과 설문 조사도 사용자 지정할 수 있습니다. 여기에 대해서는 이 문서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="55b6a-187">알림의 범주 처리기를 등록하려면 응용 프로그램이 초기화될 때 호출을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-187">To register a category handler for your notifications, you need to add a call when the application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55b6a-188">계속하기 전에 Android에서 Engagement를 통합하는 방법 항목에서 android:process 특성 \<android-sdk-engagement-process\>에 관한 경고를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="55b6a-188">Please read the warning about the android:process attribute \<android-sdk-engagement-process\> in the How to Integrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="55b6a-189">다음 예제에서는 이전 경고를 확인하였고 `EngagementApplication`의 하위 클래스를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-189">The following example assumes you acknowledged the previous warning and use a sub-class of `EngagementApplication`:</span></span>

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

<span data-ttu-id="55b6a-190">`MyNotifier` 개체는 알림 범주 처리기의 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-190">The `MyNotifier` object is the implementation of the notification category handler.</span></span> <span data-ttu-id="55b6a-191">이 개체는 `EngagementNotifier` 인터페이스의 구현이거나 기본 구현인 `EngagementDefaultNotifier`의 하위 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-191">It is either an implementation of the `EngagementNotifier` interface or a sub class of the default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="55b6a-192">동일한 알림으로 여러 범주를 처리할 수 있습니다. 또한 다음과 같이 해당 범주를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-192">Note that the same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="55b6a-193">기본 범주 구현을 바꾸기 위해 다음 예와 같이 구현을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-193">To replace the default category implementation, you can register your implementation like in the following example:</span></span>

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

<span data-ttu-id="55b6a-194">처리기에서 사용된 현재 범주는 `EngagementDefaultNotifier`에서 재정의할 수 있는 대다수 메서드의 매개 변수로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-194">The current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="55b6a-195">그 범주는`String` 매개 변수로 전달되거나 `getCategory()` 메서드가 있는 `EngagementReachContent` 개체에서 간접적으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="55b6a-196">또한 `EngagementDefaultNotifier`에서 메서드를 다시 정의하여 알림 생성 프로세스의 대부분을 변경할 수 있습니다. 고급 사용자 지정을 더 수행하려면 기술 문서 및 소스 코드를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="55b6a-196">You can change most of the notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free to take a look at the technical documentation and at the source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="55b6a-197">앱 내 알림</span><span class="sxs-lookup"><span data-stu-id="55b6a-197">In-app notifications</span></span>
<span data-ttu-id="55b6a-198">특정 범주에 대체 레이아웃을 사용하려는 경우 다음 예제와 같이 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-198">If you just want to use alternate layouts for a specific category, you can implement this as in the following example:</span></span>

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

<span data-ttu-id="55b6a-199">**`my_notification_overlay.xml`의 예제 :**</span><span class="sxs-lookup"><span data-stu-id="55b6a-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="55b6a-200">여기에서 알 수 있듯이 오버레이 뷰 식별자는 표준 식별자와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-200">As you can see, the overlay view identifier is different than the standard one.</span></span> <span data-ttu-id="55b6a-201">각 레이아웃에서 오버레이에 고유 식별자를 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="55b6a-202">**`my_notification_area.xml`의 예제 :**</span><span class="sxs-lookup"><span data-stu-id="55b6a-202">**Example of `my_notification_area.xml` :**</span></span>

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

<span data-ttu-id="55b6a-203">여기에서 알 수 있듯이 알림 영역 뷰 식별자는 표준 식별자와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-203">As you can see, the notification area view identifier is different than the standard one.</span></span> <span data-ttu-id="55b6a-204">각 레이아웃에서 알림 영역에 고유 식별자를 사용하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="55b6a-205">이 간단한 범주 예제는 화면 상단에 표시되는 응용 프로그램(또는 앱 내) 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-205">This simple example of category makes application (or in-app) notifications displayed at the top of the screen.</span></span> <span data-ttu-id="55b6a-206">알림 영역 자체에 사용되는 표준 식별자는 변경하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-206">We did not change the standard identifiers used in the notification area itself.</span></span>

<span data-ttu-id="55b6a-207">해당 식별자를 변경하려는 경우 `EngagementDefaultNotifier.prepareInAppArea` 메서드를 다시 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-207">If you want to change that, you have to redefine the `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="55b6a-208">이러한 고급 사용자 지정 수준을 원하는 경우 `EngagementNotifier` 및 `EngagementDefaultNotifier`의 기술 문서와 소스 코드를 살펴보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-208">It's recommended to look at the technical documentation and at the source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="55b6a-209">시스템 알림</span><span class="sxs-lookup"><span data-stu-id="55b6a-209">System notifications</span></span>
<span data-ttu-id="55b6a-210">기본 구현에서 준비한 알림을 변경하려면 `EngagementDefaultNotifier`을(를) 확장하여 `onNotificationPrepared`을(를) 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` to alter the notification that was prepared by the default implementation.</span></span>

<span data-ttu-id="55b6a-211">예:</span><span class="sxs-lookup"><span data-stu-id="55b6a-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="55b6a-212">이 예제는 "진행 중" 범주를 사용할 때 진행 중인 이벤트로 표시되는 내용에 대한 시스템 알림을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-212">This example makes a system notification for a content being displayed as an ongoing event when the "ongoing" category is used.</span></span>

<span data-ttu-id="55b6a-213">`Notification` 개체를 처음부터 빌드하려는 경우 메서드에 `false`을(를) 반환하고 `NotificationManager`에서 `notify`을(를) 직접 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-213">If you want to build the `Notification` object from scratch, you can return `false` to the method and call `notify` yourself on the `NotificationManager`.</span></span> <span data-ttu-id="55b6a-214">그런 경우에는 `contentIntent`, `deleteIntent` 및 `EngagementReachReceiver`에 사용되는 알림 식별자를 유지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and the notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="55b6a-215">다음은 그러한 구현에 대한 올바른 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-215">Here is a correct example of such an implementation:</span></span>

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
              manager.notify(getNotificationId(content), myNotification); // notice the call to get the right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="55b6a-216">공지만 알림</span><span class="sxs-lookup"><span data-stu-id="55b6a-216">Notification only announcements</span></span>
<span data-ttu-id="55b6a-217">공지만 알림에 대한 클릭 관리는 `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared`을(를) 재정의하여 준비된 `Intent`을(를) 수정함으로써 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-217">The management of the click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` to modify the prepared `Intent`.</span></span> <span data-ttu-id="55b6a-218">이 메서드를 사용하면 플래그를 쉽게 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-218">Using this method allows you to tune the flags easily.</span></span>

<span data-ttu-id="55b6a-219">다음은 `SINGLE_TOP` 플래그를 추가하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-219">For example to add the `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="55b6a-220">레거시 Engagement 사용자의 경우 실행 URL이 없는 시스템 알림은 응용 프로그램이 백그라운드에 있으면 해당 응용 프로그램을 시작하므로 이 메서드는 실행 URL이 없는 알림과 함께 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-220">For legacy Engagement users, please note that system notifications without action URL now launches the application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="55b6a-221">의도를 사용자 지정할 때 이런 점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-221">You should consider that when customizing the intent.</span></span>

<span data-ttu-id="55b6a-222">또한 `EngagementNotifier.executeNotifAnnouncementAction` 을(를) 처음부터 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="55b6a-223">알림 수명 주기</span><span class="sxs-lookup"><span data-stu-id="55b6a-223">Notification life cycle</span></span>
<span data-ttu-id="55b6a-224">기본 범주를 사용할 때는 통계를 보고하고 캠페인 상태를 업데이트하기 위해 `EngagementReachInteractiveContent` 개체에서 일부 수명 주기 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-224">When using the default category, some life cycle methods are called on the `EngagementReachInteractiveContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="55b6a-225">알림이 응용 프로그램에 표시되거나 상태 표시줄에 나타나는 경우 `handleNotification`이(가) `true`을(를) 반환하면 `displayNotification` 메서드가 `EngagementReachAgent`에서 호출되어 통계를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-225">When the notification is displayed in application or put in the status bar, the `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="55b6a-226">알림을 해제하면 `exitNotification` 메서드가 호출되고 통계가 보고되며 다음 캠페인을 처리할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-226">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="55b6a-227">알림을 클릭하면 `actionNotification` 이(가) 호출되고 통계가 보고되며 연결된 의도가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-227">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated intent is launched.</span></span>

<span data-ttu-id="55b6a-228">만약 `EngagementNotifier` 구현이 기본 동작을 무시하는 경우에는 이러한 수명 주기 메서드를 직접 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-228">If your implementation of `EngagementNotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="55b6a-229">다음 예제에서는 기본 동작을 무시하는 몇 가지 경우를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-229">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="55b6a-230">범주 처리를 처음부터 구현한 경우처럼 `EngagementDefaultNotifier`을(를) 확장하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="55b6a-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="55b6a-231">시스템 알림의 경우 `onNotificationPrepared`을(를) 재정의하고 `Notification` 개체에서 `contentIntent` 또는 `deleteIntent`을(를) 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-231">For system notifications, you overrode the `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in the `Notification` object.</span></span>
* <span data-ttu-id="55b6a-232">앱 내 알림의 경우 `prepareInAppArea`을(를) 재정의합니다. U.I 컨트롤 중 하나에 적어도 `actionNotification`을(를) 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-232">For in-app notifications, you overrode `prepareInAppArea`, be sure to map at least `actionNotification` to one of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="55b6a-233">`handleNotification`에서 예외가 throw되는 경우 콘텐츠는 삭제되고 `dropContent`이(가) 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-233">If `handleNotification` throws an exception, the content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="55b6a-234">이 사항은 통계로 보고되며 이제 다음 캠페인을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="55b6a-235">알림 및 설문 조사</span><span class="sxs-lookup"><span data-stu-id="55b6a-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="55b6a-236">레이아웃</span><span class="sxs-lookup"><span data-stu-id="55b6a-236">Layouts</span></span>
<span data-ttu-id="55b6a-237">`engagement_text_announcement.xml`, `engagement_web_announcement.xml`, `engagement_poll.xml` 파일을 수정하여 텍스트 알림, 웹 알림 및 설문 조사를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-237">You can modify the `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files to customize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="55b6a-238">이러한 파일은 제목 영역 및 단추 영역의 두 가지 일반 레이아웃을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-238">These files share two common layouts for the title area and the button area.</span></span> <span data-ttu-id="55b6a-239">제목의 레이아웃은 `engagement_content_title.xml` 이며, 배경에 대해 제목과 동일한 이름의 그릴 수 있는 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-239">The layout for the title is `engagement_content_title.xml` and uses the eponymous drawable file for the background.</span></span> <span data-ttu-id="55b6a-240">실행 및 종료 단추의 레이아웃은 `engagement_button_bar.xml` 이며, 배경에 대해 제목과 동일한 이름의 그릴 수 있는 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-240">The layout for the action and exit buttons is `engagement_button_bar.xml` and uses the eponymous drawable file for the background.</span></span>

<span data-ttu-id="55b6a-241">설문 조사에서 질문 레이아웃 및 선택 항목은 질문에 `engagement_question.xml` 레이아웃 파일을 사용하고 선택 항목에 `engagement_choice.xml` 파일을 여러 번 사용하여 동적으로 팽창됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-241">In a poll, the question layout and their choices are dynamically inflated using several times the `engagement_question.xml` layout file for the questions and the `engagement_choice.xml` file for the choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="55b6a-242">범주</span><span class="sxs-lookup"><span data-stu-id="55b6a-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="55b6a-243">대체 레이아웃</span><span class="sxs-lookup"><span data-stu-id="55b6a-243">Alternate layouts</span></span>
<span data-ttu-id="55b6a-244">알림과 마찬가지로 캠페인의 경우에도 범주를 사용하여 알림 및 설문 조사의 대체 레이아웃을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-244">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="55b6a-245">예를 들어 텍스트 알림의 범주를 생성하려면 다음과 같이 `EngagementTextAnnouncementActivity`을(를) 확장하고 `AndroidManifest.xml` 파일에서 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-245">For example, to create a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it the `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="55b6a-246">의도 필터의 범주는 기본 알림 작업의 차이를 구분하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-246">Note that the category in the intent filter is used to make the difference with the default announcement activity.</span></span>

<span data-ttu-id="55b6a-247">Reach SDK는 의도 시스템을 사용하여 특정 범주에 대해 올바른 작업을 확인하고, 확인에 실패하는 경우 기본 범주에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-247">The Reach SDK uses the intent system to resolve the right activity for a specific category and it falls back on the default category if the resolution failed.</span></span>

<span data-ttu-id="55b6a-248">그런 다음 `MyCustomTextAnnouncementActivity`을(를) 구현해야 하며, 레이아웃을 변경하지만 동일한 뷰 식별자를 유지하려는 경우 다음 예제와 같이 클래스를 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-248">Then you have to implement `MyCustomTextAnnouncementActivity`, if you just want to change the layout (but keep the same view identifiers), you just have to define the class like in the following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class to use R.layout.my_text_announcement
              }
            }

<span data-ttu-id="55b6a-249">텍스트 알림의 기본 범주를 바꾸려면 단지 `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` 을(를) 고유한 구현으로 바꾸면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-249">To replace the default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="55b6a-250">웹 알림 및 설문 조사는 유사한 방식으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="55b6a-251">웹 알림의 경우 `EngagementWebAnnouncementActivity`을(를) 확장하고 다음 예제와 같이 `AndroidManifest.xml`에서 작업을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in the intent is the data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="55b6a-252">설문 조사의 경우 `EngagementPollActivity`을(를) 확장하고 다음 예제와 같이 `AndroidManifest.xml`에서 작업을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-252">For polls you can extend `EngagementPollActivity` and declare your in the `AndroidManifest.xml` like in the following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="55b6a-253">처음부터 구현</span><span class="sxs-lookup"><span data-stu-id="55b6a-253">Implementation from scratch</span></span>
<span data-ttu-id="55b6a-254">Reach SDK에서 제공하는 `Engagement*Activity` 클래스 중 하나를 확장하지 않고 알림(및 설문 조사) 작업에 대한 범주를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-254">You can implement categories for your announcement (and poll) activities without extending one of the `Engagement*Activity` classes provided by the Reach SDK.</span></span> <span data-ttu-id="55b6a-255">이 작업은, 예를 들어 동일한 뷰를 표준 레이아웃으로 사용하지 않는 레이아웃을 정의하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-255">This is useful for example if you want to define a layout that does not use the same views as the standard layouts.</span></span>

<span data-ttu-id="55b6a-256">고급 알림 사용자 지정과 마찬가지로 표준 구현의 소스 코드를 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-256">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

<span data-ttu-id="55b6a-257">이때 Reach는 콘텐츠 식별자인 추가 매개 변수와 함께 특정 의도(의도 필터에 해당)를 사용하여 작업을 시작한다는 점 등 몇 가지 사항에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-257">Here are some things to keep in mind: Reach will launch the activity with a specific intent (corresponding to the intent filter) plus an extra parameter which is the content identifier.</span></span>

<span data-ttu-id="55b6a-258">웹 사이트에서 캠페인을 만들 때 지정한 필드를 포함하는 콘텐츠 개체를 검색하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-258">To retrieve the content object which contain the fields you specified when creating the campaign on the web site you can do this:</span></span>

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

<span data-ttu-id="55b6a-259">통계를 위해 다음과 같이 콘텐츠가 `onResume` 이벤트에 표시된다는 것을 보고해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-259">For statistics, you should report the content is displayed in the `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark the content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="55b6a-260">그런 다음 작업이 백그라운드로 전환되기 전에 잊지 말고 콘텐츠 개체에서 `actionContent(this)` 또는 `exitContent(this)`을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-260">Then, don't forget to call either `actionContent(this)` or `exitContent(this)` on the content object before the activity goes into background.</span></span>

<span data-ttu-id="55b6a-261">`actionContent` 또는 `exitContent`을(를) 호출하지 않은 경우 통계가 전송되지 않으며(즉, 캠페인에 대한 분석이 없음), 무엇보다도 응용 프로그램 프로세스가 다시 시작될 때까지 다음 캠페인을 알리지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on the campaign) and more importantly, the next campaigns will not be notified until the application process is restarted.</span></span>

<span data-ttu-id="55b6a-262">방향 또는 기타 구성을 변경하면 코드에서 작업을 백그라운드로 전환할지 여부를 결정하는 것이 어려워질 수 있습니다. 표준 구현에서는 사용자가 `HOME` 또는 `BACK`을(를) 눌러 작업을 떠나지만 방향이 변경되지 않은 경우 콘텐츠가 종료된 것으로 보고되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-262">Orientation or other configuration changes can make the code tricky to determine whether the activity goes into background or not, the standard implementation makes sure the content is reported as exited if the user leaves the activity (either by pressing `HOME` or `BACK`) but not if the orientation changes.</span></span>

<span data-ttu-id="55b6a-263">다음은 구현의 흥미로운 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-263">Here is the interesting part of the implementation:</span></span>

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
                 * called so we don't have to check anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="55b6a-264">여기에서 알 수 있듯이 `actionContent(this)`을(를) 호출한 후 작업을 완료하는 경우 `exitContent(this)`이(가) 영향을 받지 않고 안전하게 호출될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b6a-264">As you can see, if you called `actionContent(this)` then finished the activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
<span data-ttu-id="55b6a-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span><span class="sxs-lookup"><span data-stu-id="55b6a-265">[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html</span></span>
<span data-ttu-id="55b6a-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span><span class="sxs-lookup"><span data-stu-id="55b6a-266">[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html</span></span>
