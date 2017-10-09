---
title: aaaTemplates
description: "이 항목에서는 Azure 알림 허브용 템플릿에 대해 설명합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="e4278-103">템플릿</span><span class="sxs-lookup"><span data-stu-id="e4278-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="e4278-104">개요</span><span class="sxs-lookup"><span data-stu-id="e4278-104">Overview</span></span>
<span data-ttu-id="e4278-105">템플릿을 사용 하는 클라이언트 응용 프로그램 toospecify hello 정확한 형식 tooreceive 브로드캐스트하며 hello 알림입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="e4278-106">템플릿을 사용 하는 응용 프로그램 hello 다음을 비롯 한 여러 가지 서로 다른 이점을 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="e4278-107">플랫폼 제약이 없는 백 엔드</span><span class="sxs-lookup"><span data-stu-id="e4278-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="e4278-108">개인화된 알림</span><span class="sxs-lookup"><span data-stu-id="e4278-108">Personalized notifications</span></span>
* <span data-ttu-id="e4278-109">클라이언트 버전 독립성</span><span class="sxs-lookup"><span data-stu-id="e4278-109">Client-version independence</span></span>
* <span data-ttu-id="e4278-110">간편한 지역화</span><span class="sxs-lookup"><span data-stu-id="e4278-110">Easy localization</span></span>

<span data-ttu-id="e4278-111">이 섹션에서는 어떻게 toouse 템플릿 toosend 플랫폼 제약 없는 알림 플랫폼과 toopersonalize 간에 모든 장치를 대상으로 브로드캐스팅 알림 tooeach 장치는 두 가지 심층 분석 예.</span><span class="sxs-lookup"><span data-stu-id="e4278-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="e4278-112">플랫폼 간 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="e4278-112">Using templates cross-platform</span></span>
<span data-ttu-id="e4278-113">hello 표준 방식으로 toosend 푸시 알림을 특정 페이로드 tooplatform notification services (WNS, APNS) toobe 전송 되는 각 알림에 대해 toosend입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="e4278-114">예를 들어, 경고는 tooAPNS toosend hello 페이로드는 hello 다음 폼의 Json 개체를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e4278-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="e4278-115">Windows 스토어 응용 프로그램에서 비슷한 알림 메시지를 toosend hello XML 페이로드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="e4278-116">MPNS(Windows Phone) 및 GCM(Android) 플랫폼에 대해 유사한 페이로드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="e4278-117">이 요구 사항을 hello 앱 백 엔드 tooproduce 다른 페이로드 각 플랫폼에 대 한 하 고 효과적으로 사용 하면 hello 백 엔드 hello 앱의 hello 프레젠테이션 계층의 일부를 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="e4278-118">이 경우 지역화 및 그래픽 레이아웃(특히 여러 유형의 타일에 대한 알림을 포함하는 Windows 스토어 앱의 경우)을 포함한 몇 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="e4278-119">hello 알림 허브 템플릿 기능에 대 한 클라이언트 응용 프로그램 toocreate 특수 등록, 호출 또한 toohello 태그 집합으로, 서식 파일을 포함 하는 템플릿 등록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="e4278-120">hello 알림 허브 템플릿 기능 설치 (기본 설정) 또는 등록을 사용 하 여 작업할 수 있는지 여부를 템플릿으로 클라이언트 응용 프로그램 tooassociate 장치를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="e4278-121">페이로드 예제 앞 hello 들어 hello만 플랫폼 독립적인 정보는 hello 실제 경고 메시지 (Hello!)입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="e4278-122">템플릿은 일련의 어떻게 tooformat 플랫폼 독립적인 메시지 해당 특정 클라이언트 응용 프로그램의 hello 등록에 알림 허브 hello에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="e4278-123">앞 예제는 hello, hello 플랫폼 독립적인 메시지는 단일 속성: **메시지 = Hello!**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="e4278-124">다음 그림 hello를 프로세스 위에 hello를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="e4278-125">hello iOS 클라이언트 앱 등록에 대 한 hello 서식 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="e4278-126">hello Windows 스토어 클라이언트 응용 프로그램에 대 한 hello 해당 서식 파일은입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="e4278-127">실제 메시지 hello는 hello 식 $(메시지)에 대 한 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="e4278-128">이 식은 특정 등록을 하 고 hello 공통 값에 스위치 다음에 나오는 메시지 toobuild 메시지 toothis 보낼 때마다 hello 알림 허브에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="e4278-129">설치 모델을 사용 하는 hello 설치 "템플릿" 키 여러 서식 파일의 JSON을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="e4278-130">등록 모델을 사용 하는 hello 클라이언트 응용 프로그램에서에서 만들 수 여러 등록 순서 toouse 템플릿이 여러 개 있습니다. 예를 들어 경고 메시지에 대 한 템플릿과 템플릿이 타일에 대 한 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="e4278-131">또한 클라이언트 응용 프로그램은 기본 등록(템플릿이 없는 등록)과 템플릿 등록을 혼합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="e4278-132">알림 허브 hello toohello 속하는지 여부를 고려 하지 않고 각 서식 파일에 대 한 알림을 보냅니다 같은 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="e4278-133">이 문제를 더 많은 사용된 tootranslate 플랫폼 독립적인 알림이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="e4278-134">예를 들어 hello 동일한 플랫폼 독립적인 메시지 toohello hello 백 엔드 toobe 것을 요구 하지 않고 알림 경고 및 타일 업데이트 알림 허브를 원활 하 게 번역할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="e4278-135">참고 일부 플랫폼 (예를 들어 iOS)가 여러 알림을 toohello를 축소할 수는 짧은 시간 내에 보낼 경우 동일한 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="e4278-136">개인 설정에 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="e4278-136">Using templates for personalization</span></span>
<span data-ttu-id="e4278-137">또 다른 이점은 toousing 템플릿 hello 기능 toouse 알림의 알림 허브 tooperform 등록 당 개인 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="e4278-138">예를 들어 날씨 응용 프로그램을 특정 위치에 hello 날씨 조건 사용 하 여 타일을 표시 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="e4278-139">사용자는 섭씨 또는 화씨 온도 및 1일 또는 5일 예보 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="e4278-140">템플릿을 사용 하 여, 필요한 hello 형식에 대 한 각 클라이언트 응용 프로그램 설치를 등록할 수 (1 일 섭씨, 1 일 화씨, 5 한 일 섭씨, 화씨), 있고 hello 정보가 모두 들어 있는 단일 메시지 필요한 toofill 하는 것을 전송 하는 hello 백 엔드 서식 파일 (예를 들어는 5 일 섭씨 및 화씨도 예측 하는 경우).</span><span class="sxs-lookup"><span data-stu-id="e4278-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="e4278-141">hello 템플릿 hello 하루 섭씨를 예측 하는 온도 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="e4278-142">hello 메시지 전송 toohello 알림 허브는 모든 hello를 다음 속성이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="e4278-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="e4278-143">day1_image</span></span></td><td><span data-ttu-id="e4278-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="e4278-144">day2_image</span></span></td><td><span data-ttu-id="e4278-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="e4278-145">day3_image</span></span></td><td><span data-ttu-id="e4278-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="e4278-146">day4_image</span></span></td><td><span data-ttu-id="e4278-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="e4278-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="e4278-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="e4278-148">day1_tempC</span></span></td><td><span data-ttu-id="e4278-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="e4278-149">day2_tempC</span></span></td><td><span data-ttu-id="e4278-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="e4278-150">day3_tempC</span></span></td><td><span data-ttu-id="e4278-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="e4278-151">day4_tempC</span></span></td><td><span data-ttu-id="e4278-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="e4278-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="e4278-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="e4278-153">day1_tempF</span></span></td><td><span data-ttu-id="e4278-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="e4278-154">day2_tempF</span></span></td><td><span data-ttu-id="e4278-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="e4278-155">day3_tempF</span></span></td><td><span data-ttu-id="e4278-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="e4278-156">day4_tempF</span></span></td><td><span data-ttu-id="e4278-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="e4278-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="e4278-158">이 패턴을 사용 하 여 hello 백 엔드 hello 응용 프로그램 사용자에 대 한 특정 개인 설정 옵션 toostore 필요 없이 단일 메시지만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="e4278-159">hello 다음 그림에서는이 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="e4278-160">어떻게 tooregister 템플릿</span><span class="sxs-lookup"><span data-stu-id="e4278-160">How tooregister templates</span></span>
<span data-ttu-id="e4278-161">hello 설치 모델 (기본 설정)를 사용 하 여 템플릿을 또는 hello 등록 모델 tooregister 참조 [등록 관리](notification-hubs-push-notification-registration-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="e4278-162">템플릿 식 언어</span><span class="sxs-lookup"><span data-stu-id="e4278-162">Template expression language</span></span>
<span data-ttu-id="e4278-163">서식 파일은 제한 된 tooXML 또는 JSON 문서 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="e4278-164">또한 식을 특정 장소에만 배치할 수 있습니다. 예를 들어 XML은 노드 속성 또는 값에, JSON은 문자열 속성 값에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="e4278-165">hello 아래 표에 나와 hello 언어 템플릿에서 허용.</span><span class="sxs-lookup"><span data-stu-id="e4278-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="e4278-166">식</span><span class="sxs-lookup"><span data-stu-id="e4278-166">Expression</span></span> | <span data-ttu-id="e4278-167">설명</span><span class="sxs-lookup"><span data-stu-id="e4278-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4278-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="e4278-168">$(prop)</span></span> |<span data-ttu-id="e4278-169">Hello 지정 된 이름의 tooan 이벤트 속성 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="e4278-170">속성 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="e4278-171">이 식은 hello 속성이 없으면 hello 속성의 텍스트 값 또는 빈 문자열을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="e4278-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="e4278-172">$(prop, n)</span></span> |<span data-ttu-id="e4278-173">위의 예와 같지만 hello 텍스트가 명시적으로 대로 n 문자에 맞게 잘립니다, 예를 들어 $(제목, 20) hello title 속성의 hello 내용을에서 클립 20 자까지 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="e4278-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="e4278-174">.(prop, n)</span></span> |<span data-ttu-id="e4278-175">위, 같지만 hello 텍스트를 잘라냅니다 대로 세 개의 점 접미사로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="e4278-176">hello hello의 전체 크기 문자열 잘리고 hello 접미사 n 자를 초과 하지 않는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="e4278-177">. (제목, 20)에서 "hello 제목 줄은" 결과의 입력된 속성이 있는 **hello 제목 이것이...**</span><span class="sxs-lookup"><span data-stu-id="e4278-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="e4278-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="e4278-178">%(prop)</span></span> |<span data-ttu-id="e4278-179">해당 hello 출력을 제외한 비슷한 too$(name)는 URI로 인코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="e4278-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="e4278-180">#(prop)</span></span> |<span data-ttu-id="e4278-181">JSON 템플릿(예: iOS 및 Android 템플릿)에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="e4278-182">이 함수 작동 정확 하 게 hello 동일으로 $(prop) JSON 템플릿 (예를 들어, 사과 템플릿)에 사용 되는 경우를 제외 하 고 이전에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="e4278-183">이 경우,이 함수는 둘러싸인 되지 "{','을 (를)" (예를 들어 'myJsonProperty': '#(이름)'), 예를 들어 regexp Javascript 형태로 tooa 수를 계산 하 고: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 &#93;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, hello JSON은 숫자를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="e4278-184">예를 들어 ‘badge : ‘#(name)’은 ‘badge’ : 40 이 됩니다(‘40‘이 아니라).</span><span class="sxs-lookup"><span data-stu-id="e4278-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="e4278-185">'text' 또는 "text"</span><span class="sxs-lookup"><span data-stu-id="e4278-185">‘text’ or “text”</span></span> |<span data-ttu-id="e4278-186">리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-186">A literal.</span></span> <span data-ttu-id="e4278-187">리터럴에는 작은따옴표 또는 큰따옴표로 묶인 임의의 텍스트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="e4278-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="e4278-188">expr1 + expr2</span></span> |<span data-ttu-id="e4278-189">hello 연결 연산자 두 식을 단일 문자열로 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="e4278-190">hello 식 앞에 forms hello 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="e4278-191">연결을 사용할 경우 hello 전체 식은 {}로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="e4278-192">예: {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="e4278-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="e4278-193">예를 들어 hello 다음 유효한 XML 서식 파일은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="e4278-194">위에서 설명한 대로 연결을 사용하는 경우 식을 중괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4278-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="e4278-195">예:</span><span class="sxs-lookup"><span data-stu-id="e4278-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

