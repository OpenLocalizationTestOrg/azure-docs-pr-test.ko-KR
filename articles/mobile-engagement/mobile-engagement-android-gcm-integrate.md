---
title: "Azure Mobile Engagement Android SDK 통합"
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
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="3de80-103">GCM과 Mobile Engagement를 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="3de80-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3de80-104">이 가이드를 수행하기 전에 Android 문서의 Engagement를 통합하는 방법에 설명된 통합 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="3de80-105">이 문서는 도달률 모듈 및 Google Play 장치를 푸시하는 계획을 이미 통합한 경우에만 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="3de80-106">응용 프로그램에서 도달률 캠페인을 통합하려면 먼저 Android에서 Engagement 도달률을 통합하는 방법을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="3de80-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="3de80-107">소개</span><span class="sxs-lookup"><span data-stu-id="3de80-107">Introduction</span></span>
<span data-ttu-id="3de80-108">GCM을 통합하면 응용 프로그램을 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="3de80-109">SDK로 푸시된 GCM 페이로드는 데이터 개체에 항상 `azme` 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="3de80-110">따라서 응용 프로그램에서 다른 용도로 GCM을 사용하는 경우 해당 키에 따라 푸시를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3de80-111">Android 2.2 이상을 실행하고, Google Play를 설치하고, Google 백그라운드 연결이 활성화된 장치만 GCM을 사용해 푸시될 수 있지만 지원되지 않는 장치(단지 의도만 이용하는 장치)에서 이 코드를 안전하게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="3de80-112">API 키를 가진 Google Cloud Messaging 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="3de80-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="3de80-113">SDK 통합</span><span class="sxs-lookup"><span data-stu-id="3de80-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="3de80-114">장치 등록 관리</span><span class="sxs-lookup"><span data-stu-id="3de80-114">Managing device registrations</span></span>
<span data-ttu-id="3de80-115">각 장치는 Google 서버에 등록 명령을 보내야 하며, 그렇지 않은 경우 해당 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="3de80-116">장치는 GCM 알림에서 등록 취소할 수 있습니다(응용 프로그램이 제거된 경우 장치가 자동으로 등록 취소됨).</span><span class="sxs-lookup"><span data-stu-id="3de80-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="3de80-117">[Google Play SDK] 를 사용하지 않거나 등록 의도를 아직 직접 보내지 않은 경우 Engagement에서 자동으로 장치를 등록하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="3de80-118">이 기능을 사용하려면 `AndroidManifest.xml` 파일의 `<application/>` 태그 내에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="3de80-119">Engagement 푸시 서비스에 등록 ID를 전달하고 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="3de80-120">Engagement 푸시 서비스에 장치의 등록 ID를 전달하고 해당 알림을 수신하려면 `AndroidManifest.xml` 파일의 `<application/>` 태그 내에 다음을 추가합니다(장치 등록을 직접 관리하는 경우에도).</span><span class="sxs-lookup"><span data-stu-id="3de80-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="3de80-121">`AndroidManifest.xml`에서(`</application>` 태그 다음) 다음 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3de80-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="3de80-122">Mobile Engagement에 GCM API 키에 대한 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="3de80-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="3de80-123">Mobile Engagement에 GCM API 키에 대한 액세스 권한을 부여하려면 [이 가이드](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) 를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="3de80-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="3de80-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="3de80-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
