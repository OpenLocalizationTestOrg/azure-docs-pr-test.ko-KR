---
title: "Azure Mobile Engagement Android SDK용 고급 구성"
description: "Azure Mobile Engagement Android SDK를 사용하는 Android 매니페스트를 포함하여 고급 구성 옵션에 대해 설명합니다"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0301f71c76872714aa1bf727a6c21dd7a63db036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="0834e-103">Azure Mobile Engagement Android SDK용 고급 구성</span><span class="sxs-lookup"><span data-stu-id="0834e-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0834e-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="0834e-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="0834e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0834e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="0834e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="0834e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="0834e-107">Android</span><span class="sxs-lookup"><span data-stu-id="0834e-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="0834e-108">이 절차에서는 Azure Mobile Engagement Android 앱에 대한 다양한 고급 구성 옵션을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0834e-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0834e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="0834e-110">사용 권한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0834e-110">Permission Requirements</span></span>
<span data-ttu-id="0834e-111">일부 옵션에 특정 권한이 필요하며 참조할 수 있도록 모든 권한이 여기에 나열되어 있으며 특정 기능에 인라인으로 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-111">Some options require specific permissions, all of which are listed here for reference, and in-line in the specific feature.</span></span> <span data-ttu-id="0834e-112">프로젝트의 AndroidManifest.xml에서 `<application>` 태그 바로 앞 또는 뒤에 다음 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-112">Add these permissions to the AndroidManifest.xml of your project immediately before or after the `<application>` tag.</span></span>

<span data-ttu-id="0834e-113">사용 권한 코드는 다음과 같아야 하며 여기에 아래 테이블에서 해당하는 권한을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-113">The permission code needs to look like the following, where you fill in the appropriate permission from the table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="0834e-114">사용 권한</span><span class="sxs-lookup"><span data-stu-id="0834e-114">Permission</span></span> | <span data-ttu-id="0834e-115">사용할 경우</span><span class="sxs-lookup"><span data-stu-id="0834e-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="0834e-116">인터넷</span><span class="sxs-lookup"><span data-stu-id="0834e-116">INTERNET</span></span> |<span data-ttu-id="0834e-117">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-117">Required.</span></span> <span data-ttu-id="0834e-118">기본 보고용</span><span class="sxs-lookup"><span data-stu-id="0834e-118">For basic reporting</span></span> |
| <span data-ttu-id="0834e-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="0834e-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="0834e-120">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-120">Required.</span></span> <span data-ttu-id="0834e-121">기본 보고용</span><span class="sxs-lookup"><span data-stu-id="0834e-121">For basic reporting</span></span> |
| <span data-ttu-id="0834e-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="0834e-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="0834e-123">필수입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-123">Required.</span></span> <span data-ttu-id="0834e-124">장치 재부팅 후 알림 센터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-124">To show up the notifications center after device reboot</span></span> |
| <span data-ttu-id="0834e-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="0834e-125">WAKE_LOCK</span></span> |<span data-ttu-id="0834e-126">권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-126">Recommended.</span></span> <span data-ttu-id="0834e-127">WiFi를 사용하거나 화면이 꺼져 있을 때 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="0834e-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="0834e-128">VIBRATE</span></span> |<span data-ttu-id="0834e-129">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-129">Optional.</span></span> <span data-ttu-id="0834e-130">알림이 수신될 때 진동을 울립니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="0834e-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="0834e-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="0834e-132">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-132">Optional.</span></span> <span data-ttu-id="0834e-133">Android 큰 그림 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="0834e-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="0834e-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="0834e-135">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-135">Optional.</span></span> <span data-ttu-id="0834e-136">Android 큰 그림 알림을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="0834e-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="0834e-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="0834e-138">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-138">Optional.</span></span> <span data-ttu-id="0834e-139">실시간 위치 보고를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="0834e-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="0834e-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="0834e-141">선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-141">Optional.</span></span> <span data-ttu-id="0834e-142">GPS 기반 위치 보고를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="0834e-143">Android M부터는 [일부 권한이 런타임 시 관리됩니다](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="0834e-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="0834e-144">``ACCESS_FINE_LOCATION``을 이미 사용 중인 경우 ``ACCESS_COARSE_LOCATION``을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need to also use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="0834e-145">Android 매니페스트 파일 구성 옵션</span><span class="sxs-lookup"><span data-stu-id="0834e-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="0834e-146">충돌 보고서</span><span class="sxs-lookup"><span data-stu-id="0834e-146">Crash report</span></span>
<span data-ttu-id="0834e-147">크래시 보고를 사용하지 않도록 설정하려면 `<application>` 및 `</application>` 태그 사이에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-147">To disable crash reports, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="0834e-148">버스트 임계값</span><span class="sxs-lookup"><span data-stu-id="0834e-148">Burst threshold</span></span>
<span data-ttu-id="0834e-149">기본적으로 Engagement 서비스는 로그를 실시간으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-149">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="0834e-150">응용 프로그램이 로그를 매우 자주 보고하는 경우 로그를 버퍼링한 후 정기적으로 한 번에 모두 보고하는 것이 좋습니다. 이를 "버스트 모드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-150">If your application report logs vary frequently, it is better to buffer the logs and to report them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="0834e-151">이렇게 하려면 `<application>` 및 `</application>` 태그 사이에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-151">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="0834e-152">버스트 모드를 사용하는 경우 배터리 수명은 약간 길어지지만 Engagement 모니터에 영향을 주게 됩니다. 모든 세션 및 작업 기간이 버스트 임계값으로 반올림되므로 버스트 임계값보다 짧은 세션과 작업은 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-152">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="0834e-153">버스트 임계값은 30000(30초) 이하여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="0834e-154">세션 시간 제한</span><span class="sxs-lookup"><span data-stu-id="0834e-154">Session timeout</span></span>
 <span data-ttu-id="0834e-155">**홈** 또는 **뒤로** 키를 누르거나, 휴대폰을 유휴 상태로 설정하거나, 다른 응용 프로그램으로 이동하여 활동을 끝낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-155">You can end an activity by pressing the **Home** or **Back** key, by setting the phone idle or by jumping into another application.</span></span> <span data-ttu-id="0834e-156">기본적으로 세션은 마지막 활동이 끝나고 10초 후에 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-156">By default, a session is ended ten seconds after the end of its last activity.</span></span> <span data-ttu-id="0834e-157">이를 통해 사용자가 응용 프로그램을 종료하고 빠르게 응용 프로그램으로 돌아갈 때(이미지를 선택하거나 알림을 확인하는 등의 작업을 통해)마다 세션 분할을 피할 수 있습니다. 이 매개 변수를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-157">This avoids a session split each time the user exits and returns to the application quickly, which can happen when the user picks up an image, checks a notification, etc. You may want to modify this parameter.</span></span> <span data-ttu-id="0834e-158">이렇게 하려면 `<application>` 및 `</application>` 태그 사이에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-158">To do so, add this code between the `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="0834e-159">로그 보고 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="0834e-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="0834e-160">메서드 호출 사용</span><span class="sxs-lookup"><span data-stu-id="0834e-160">Using a method call</span></span>
<span data-ttu-id="0834e-161">Engagement에서 로그 전송을 중지하려면 다음을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-161">If you want Engagement to stop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="0834e-162">이 호출은 영구적이며, 공유 기본 설정 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="0834e-163">이 함수를 호출할 때 Engagement가 활성 상태인 경우 서비스가 중지되는 데 1분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-163">If Engagement is active when you call this function, it may take one minute for the service to stop.</span></span> <span data-ttu-id="0834e-164">그러나 다음에 응용 프로그램을 시작할 때는 서비스가 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-164">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="0834e-165">또한 `true`(으)로 동일한 함수를 호출하여 로그 보고를 다시 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-165">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="0834e-166">고유한 `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="0834e-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="0834e-167">이 함수를 호출하지 않고 기존 `PreferenceActivity`에서 직접 이 설정을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="0834e-168">다음과 같이 `AndroidManifest.xml` 파일의 기본 설정 파일을(원하는 모드에서) `application meta-data`와(과) 함께 사용하도록 Engagement를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-168">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="0834e-169">`engagement:agent:settings:name` 키는 공유 기본 설정 파일의 이름을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-169">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="0834e-170">`engagement:agent:settings:mode` 키는 공유 기본 설정 파일의 모드를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-170">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file.</span></span> <span data-ttu-id="0834e-171">`PreferenceActivity`와 동일한 모드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-171">Use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="0834e-172">모드는 숫자로 전달해야 합니다. 코드에서 상수 플래그의 조합을 사용하는 경우 전체 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-172">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="0834e-173">Engagement는 이 설정을 관리하기 위한 기본 설정 파일 내에서 항상 `engagement:key` 부울 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-173">Engagement always uses the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="0834e-174">다음 `AndroidManifest.xml` 예제는 기본값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-174">The following example of `AndroidManifest.xml` shows the default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="0834e-175">이제 다음과 같은 기본 설정 레이아웃에서 `CheckBoxPreference` 을(를) 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0834e-175">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
