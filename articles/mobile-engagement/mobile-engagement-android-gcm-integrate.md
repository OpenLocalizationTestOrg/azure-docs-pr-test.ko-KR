---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="11cf7-103">어떻게 tooIntegrate Mobile Engagement와 GCM</span><span class="sxs-lookup"><span data-stu-id="11cf7-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="11cf7-104">이 가이드를 수행 하기 전에 Android에서 Engagement tooIntegrate 문서화 하는 방법을 hello에 설명 된 hello 통합 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="11cf7-105">이 문서는 이미 통합 된 hello 장치 모듈 및 계획 toopush Google Play에 도달 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="11cf7-106">toointegrate Reach 캠페인을 읽으십시오 먼저 방법을 응용 프로그램에서 Android에서 Engagement Reach tooIntegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="11cf7-107">소개</span><span class="sxs-lookup"><span data-stu-id="11cf7-107">Introduction</span></span>
<span data-ttu-id="11cf7-108">GCM 통합 프로그램 응용 프로그램 toobe를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="11cf7-109">항상 toohello SDK 푸시 GCM 페이로드 포함 hello `azme` hello 데이터 개체의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="11cf7-110">따라서 응용 프로그램에서 다른 용도로 GCM을 사용하는 경우 해당 키에 따라 푸시를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11cf7-111">Android 2.2 이상을 실행하고, Google Play를 설치하고, Google 백그라운드 연결이 활성화된 장치만 GCM을 사용해 푸시될 수 있지만 지원되지 않는 장치(단지 의도만 이용하는 장치)에서 이 코드를 안전하게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="11cf7-112">API 키를 가진 Google Cloud Messaging 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="11cf7-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="11cf7-113">SDK 통합</span><span class="sxs-lookup"><span data-stu-id="11cf7-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="11cf7-114">장치 등록 관리</span><span class="sxs-lookup"><span data-stu-id="11cf7-114">Managing device registrations</span></span>
<span data-ttu-id="11cf7-115">각 장치 보내야 등록 명령 toohello Google 서버, 그렇지 않으면은 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="11cf7-116">장치는 GCM 알림 (hello 장치가 하지 않으면 자동으로 등록 된 hello 응용 프로그램을 제거 하는 경우)에서 등록 취소도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="11cf7-117">사용 하지 않는 경우 [Google 재생 SDK] 또는 이미 보내지 않으면 hello 등록 의도 자신, Engagement 드립니다 hello 장치를 자동으로 등록을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="11cf7-118">tooenable이 hello tooyour 다음 추가 `AndroidManifest.xml` hello 내 파일 `<application/>` 태그:</span><span class="sxs-lookup"><span data-stu-id="11cf7-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="11cf7-119">등록 id toohello Engagement 푸시 서비스를 통신 하 고 알림을 받기</span><span class="sxs-lookup"><span data-stu-id="11cf7-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="11cf7-120">Hello 장치 toohello Engagement 푸시의 순서 toocommunicate hello 등록 id에서 서비스 및 해당 알림이 제공, hello tooyour 다음 추가 `AndroidManifest.xml` hello 내 파일 `<application/>` 태그 (도 관리 하는 경우 장치 등록 직접):</span><span class="sxs-lookup"><span data-stu-id="11cf7-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="11cf7-121">다음에서 권한을 hello 해야 프로그램 `AndroidManifest.xml` (hello 후 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="11cf7-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="11cf7-122">Grant Mobile Engagement 액세스 tooyour GCM API 키</span><span class="sxs-lookup"><span data-stu-id="11cf7-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="11cf7-123">에 따라 [이 가이드](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement 액세스 tooyour GCM API 키입니다.</span><span class="sxs-lookup"><span data-stu-id="11cf7-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google 재생 SDK]:https://developers.google.com/cloud-messaging/android/start
