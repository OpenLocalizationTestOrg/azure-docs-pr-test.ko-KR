---
title: "Mobile Engagement Android SDK 통합 aaaAzure"
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
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="4b1b6-103">어떻게 tooIntegrate ADM Engagement와</span><span class="sxs-lookup"><span data-stu-id="4b1b6-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4b1b6-104">이 가이드를 수행 하기 전에 Android에서 Engagement tooIntegrate 문서화 하는 방법을 hello에 설명 된 hello 통합 절차를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="4b1b6-105">이 문서는 이미 hello Reach 모듈 및 계획 toopush Amazon 장치를 통합 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="4b1b6-106">toointegrate Reach 캠페인을 읽으십시오 먼저 방법을 응용 프로그램에서 Android에서 Engagement Reach tooIntegrate 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="4b1b6-107">소개</span><span class="sxs-lookup"><span data-stu-id="4b1b6-107">Introduction</span></span>
<span data-ttu-id="4b1b6-108">통합 ADM 푸시 Amazon Android 장치를 대상으로 하는 경우 사용자 응용 프로그램 toobe를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="4b1b6-109">항상 toohello SDK 푸시 ADM 페이로드 포함 hello `azme` hello 데이터 개체의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="4b1b6-110">따라서 응용 프로그램에서 다른 용도로 ADM을 사용하는 경우 해당 키에 따라 푸시를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b1b6-111">Android 4.0.3 이상을 실행하는 Amazon Kindle 장치만 Amazon 장치 메시징을 통해 지원되지만 다른 장치에서 안전하게 이 코드를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="4b1b6-112">TooADM 등록</span><span class="sxs-lookup"><span data-stu-id="4b1b6-112">Sign up tooADM</span></span>
<span data-ttu-id="4b1b6-113">아직 등록하지 않은 경우 Amazon 계정에서 ADM를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="4b1b6-114">hello 프로시저에서 자세히 설명 되어: [ <https://developer.amazon.com/sdk/adm/credentials.html>]합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="4b1b6-115">Hello 절차를 완료 되 면 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4b1b6-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="4b1b6-116">OAuth 자격 증명 (클라이언트 ID 및 클라이언트 암호) Engagement toobe 수 toopush에 대 한 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="4b1b6-117">응용 프로그램에 통합해야 하는 API 키</span><span class="sxs-lookup"><span data-stu-id="4b1b6-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="4b1b6-118">SDK 통합</span><span class="sxs-lookup"><span data-stu-id="4b1b6-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="4b1b6-119">장치 등록 관리</span><span class="sxs-lookup"><span data-stu-id="4b1b6-119">Managing device registrations</span></span>
<span data-ttu-id="4b1b6-120">각 장치 보내야 등록 명령 toohello ADM 서버, 그렇지 않으면은 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="4b1b6-121">이미 hello를 사용 하는 경우 [ADM 클라이언트 라이브러리], 이미 있고 [ADM 통합] tooandroid-sdk-adm 수신 직접 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="4b1b6-122">ADM를 통합 하지 아직 Engagement에 더 간단한 방법은 tooenable 경우 응용 프로그램에서:</span><span class="sxs-lookup"><span data-stu-id="4b1b6-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="4b1b6-123">`AndroidManifest.xml` 파일을 다음과 같이 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="4b1b6-124">Amazon 네임 스페이스 hello, hello 파일은 다음과 같이 시작 해야를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="4b1b6-125">내부 hello `<application/>` 태그,이 섹션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="4b1b6-126">Hello amazon 태그를 추가한 후 프로젝트 빌드 대상 Android 2.1 미만인 경우 빌드 오류를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="4b1b6-127">Toouse 있는 **Android 2.1 이상** 빌드 대상 (스 러을 사용할 수 있습니다는 `minSdkVersion` too4 설정).</span><span class="sxs-lookup"><span data-stu-id="4b1b6-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="4b1b6-128">수행 하 여 hello ADM API 키를 자산으로 통합 [이 절차]합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="4b1b6-129">다음 섹션에서는 hello의 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="4b1b6-130">등록 id toohello Engagement 푸시 서비스를 통신 하 고 알림을 받기</span><span class="sxs-lookup"><span data-stu-id="4b1b6-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="4b1b6-131">Hello 장치 toohello Engagement 푸시의 순서 toocommunicate hello 등록 id에서 서비스 및 해당 알림이 제공, hello tooyour 다음 추가 `AndroidManifest.xml` hello 내 파일 `<application/>` 태그 (경우에 참여 하지 않고 ADM 사용):</span><span class="sxs-lookup"><span data-stu-id="4b1b6-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="4b1b6-132">다음에서 권한을 hello 해야 프로그램 `AndroidManifest.xml` (hello 전에 `</application>` 태그).</span><span class="sxs-lookup"><span data-stu-id="4b1b6-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="4b1b6-133">Engagement OAuth 자격 증명 부여</span><span class="sxs-lookup"><span data-stu-id="4b1b6-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="4b1b6-134">Engagement 포털에서 OAuth 자격 증명(클라이언트 ID 및 클라이언트 암호)을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="4b1b6-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM 클라이언트 라이브러리]:https://developer.amazon.com/sdk/adm/setup.html
[ADM 통합]:https://developer.amazon.com/sdk/adm/integrating-app.html
[이 절차]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
