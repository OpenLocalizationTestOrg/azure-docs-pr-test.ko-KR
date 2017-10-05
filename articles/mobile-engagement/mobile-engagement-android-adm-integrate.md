---
title: "Azure Mobile Engagement Android SDK 통합"
description: "Azure Mobile Engagement용 Android SDK의 최신 업데이트 및 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="a6db9-103">ADM와 Engagement를 통합하는 방법</span><span class="sxs-lookup"><span data-stu-id="a6db9-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a6db9-104">이 가이드를 수행하기 전에 Android 문서의 Engagement를 통합하는 방법에 설명된 통합 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="a6db9-105">이 문서는 도달률 모듈 및 Amazon 장치를 푸시하는 계획을 이미 통합한 경우에만 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="a6db9-106">응용 프로그램에서 도달률 캠페인을 통합하려면 먼저 Android에서 Engagement 도달률을 통합하는 방법을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a6db9-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a6db9-107">소개</span><span class="sxs-lookup"><span data-stu-id="a6db9-107">Introduction</span></span>
<span data-ttu-id="a6db9-108">ADM을 통합하면 Amazon Android 장치를 대상으로 할 때 응용 프로그램을 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="a6db9-109">SDK로 푸시된 ADM 페이로드는 데이터 개체에 항상 `azme` 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="a6db9-110">따라서 응용 프로그램에서 다른 용도로 ADM을 사용하는 경우 해당 키에 따라 푸시를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6db9-111">Android 4.0.3 이상을 실행하는 Amazon Kindle 장치만 Amazon 장치 메시징을 통해 지원되지만 다른 장치에서 안전하게 이 코드를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="a6db9-112">ADM에 등록</span><span class="sxs-lookup"><span data-stu-id="a6db9-112">Sign up to ADM</span></span>
<span data-ttu-id="a6db9-113">아직 등록하지 않은 경우 Amazon 계정에서 ADM를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="a6db9-114">절차는 [<https://developer.amazon.com/sdk/adm/credentials.html>]에 자세히 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="a6db9-115">절차를 완료하면 다음을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="a6db9-116">Engagement에서 장치를 푸시하는 데 사용할 수 있는 OAuth 자격 증명(클라이언트 ID 및 클라이언트 암호)</span><span class="sxs-lookup"><span data-stu-id="a6db9-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="a6db9-117">응용 프로그램에 통합해야 하는 API 키</span><span class="sxs-lookup"><span data-stu-id="a6db9-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="a6db9-118">SDK 통합</span><span class="sxs-lookup"><span data-stu-id="a6db9-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="a6db9-119">장치 등록 관리</span><span class="sxs-lookup"><span data-stu-id="a6db9-119">Managing device registrations</span></span>
<span data-ttu-id="a6db9-120">각 장치에서 ADM 서버로 등록 명령을 보내야 하며, 그렇지 않은 경우 서버에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="a6db9-121">이미 [ADM 클라이언트 라이브러리]를 사용하며 이미 [ADM을 통합]한 경우 android-sdk-adm-receive로 직접 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="a6db9-122">ADM을 아직 통합하지 않은 경우 Engagement를 통해 응용 프로그램에서 더 간단히 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="a6db9-123">`AndroidManifest.xml` 파일을 다음과 같이 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="a6db9-124">Amazon 네임스페이스를 추가하면 파일 시작 부분은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="a6db9-125">`<application/>` 태그 내에 다음 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="a6db9-126">Amazon 태그를 추가한 후 프로젝트 빌드 대상이 Android 2.1 이하인 경우 빌드 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="a6db9-127">**Android 2.1 이상**의 빌드 대상을 사용해야 합니다(여전히 `minSdkVersion`을(를) 4로 설정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="a6db9-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="a6db9-128">[이 절차]를 따라 ADM API 키를 자산으로 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="a6db9-129">그런 후 다음 섹션의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="a6db9-130">Engagement 푸시 서비스에 등록 ID를 전달하고 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="a6db9-131">Engagement 푸시 서비스에 장치의 등록 ID를 전달하고 해당 알림을 수신하려면 `AndroidManifest.xml` 파일의 `<application/>` 태그 내에 다음을 추가합니다(Engagement 없이 ADM을 사용하는 경우에도).</span><span class="sxs-lookup"><span data-stu-id="a6db9-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="a6db9-132">`AndroidManifest.xml`에서(`</application>` 태그 앞에) 다음 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="a6db9-133">Engagement OAuth 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="a6db9-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="a6db9-134">Engagement 포털에서 OAuth 자격 증명(클라이언트 ID 및 클라이언트 암호)을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db9-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="a6db9-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="a6db9-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="a6db9-136">[ADM 클라이언트 라이브러리]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="a6db9-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="a6db9-137">[ADM을 통합]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="a6db9-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="a6db9-138">[이 절차]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="a6db9-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
