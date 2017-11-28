---
title: "템플릿"
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="a854e-103">템플릿</span><span class="sxs-lookup"><span data-stu-id="a854e-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="a854e-104">개요</span><span class="sxs-lookup"><span data-stu-id="a854e-104">Overview</span></span>
<span data-ttu-id="a854e-105">템플릿을 사용하여 클라이언트 응용 프로그램이 받고자 하는 알림의 정확한 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="a854e-106">템플릿을 사용하면 앱이 다음을 포함한 여러 가지 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="a854e-107">플랫폼 제약이 없는 백 엔드</span><span class="sxs-lookup"><span data-stu-id="a854e-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="a854e-108">개인화된 알림</span><span class="sxs-lookup"><span data-stu-id="a854e-108">Personalized notifications</span></span>
* <span data-ttu-id="a854e-109">클라이언트 버전 독립성</span><span class="sxs-lookup"><span data-stu-id="a854e-109">Client-version independence</span></span>
* <span data-ttu-id="a854e-110">간편한 지역화</span><span class="sxs-lookup"><span data-stu-id="a854e-110">Easy localization</span></span>

<span data-ttu-id="a854e-111">이 섹션에서는 템플릿을 사용해 플랫폼 전체의 모든 장치를 대상으로 지정하여 플랫폼 제약 없는 알림을 보내고 각 장치에 대한 브로드캐스트 알림을 개인화하는 방법에 대한 심층 예제 두 가지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="a854e-112">플랫폼 간 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="a854e-112">Using templates cross-platform</span></span>
<span data-ttu-id="a854e-113">푸시 알림을 보내는 표준 방법은 보낼 각 알림에 대해 특정 페이로드를 플랫폼 알림 서비스(WNS, APNS)에 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="a854e-114">예를 들어 APNS에 경고를 보내려면 페이로드는 다음과 같은 형식의 Json 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="a854e-115">Windows 스토어 응용 프로그램에서 유사한 토스트 메시지를 보내기 위한 XML 페이로드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="a854e-116">MPNS(Windows Phone) 및 GCM(Android) 플랫폼에 대해 유사한 페이로드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="a854e-117">이 요구 사항 때문에 앱 백 엔드가 각 플랫폼에 대해 서로 다른 페이로드를 생성하며 결국 백 엔드는 앱의 프레젠테이션 계층의 일부를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="a854e-118">이 경우 지역화 및 그래픽 레이아웃(특히 여러 유형의 타일에 대한 알림을 포함하는 Windows 스토어 앱의 경우)을 포함한 몇 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="a854e-119">알림 허브 템플릿 기능을 사용하여 클라이언트 앱은 태그 집합 외에 템플릿도 포함하는 템플릿 등록이라는 특수 등록을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="a854e-120">알림 허브 템플릿 기능을 사용하여 클라이언트 앱은 설치(기본 설정) 또는 등록 중 작업할 템플릿과 장치를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="a854e-121">앞의 페이로드 예제를 가정할 때 유일한 플랫폼 독립적인 정보는 실제 경고 메시지(Hello!)입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="a854e-122">템플릿은 특정 클라이언트 앱을 등록하기 위해 플랫폼 독립적인 메시지의 형식을 지정하는 방법에 관한 알림 허브에 대한 지침의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="a854e-123">앞의 예제에서 플랫폼 독립적 메시지는 단일 속성 **message = Hello!**입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="a854e-124">다음 그림은 위의 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="a854e-125">iOS 클라이언트 앱 등록에 대한 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="a854e-126">Windows 스토어 클라이언트 앱에 대한 해당 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="a854e-127">식 $(message)가 실제 메시지로 대체된 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="a854e-128">이 식은 알림 허브에 대해 이 특정 등록에 메시지를 보낼 때마다 다음에 오는 메시지 및 공통 값의 스위치를 구축하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="a854e-129">설치 모델에 대해 작업하는 경우 설치 "템플릿" 키가 여러 템플릿의 JSON을 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="a854e-130">등록 모델에 대해 작업하는 경우 클라이언트 응용 프로그램은 여러 템플릿, 예를 들어 경고 메시지용 템플릿과 타일 업데이트용 템플릿을 사용하기 위해 여러 등록을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="a854e-131">또한 클라이언트 응용 프로그램은 기본 등록(템플릿이 없는 등록)과 템플릿 등록을 혼합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="a854e-132">알림 허브는 각 템플릿이 같은 클라이언트 앱에 속하는지 여부를 고려하지 않고 각 템플릿마다 하나의 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="a854e-133">이 동작을 사용하면 플랫폼 독립적인 알림을 더 많은 알림으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="a854e-134">예를 들어 알림 허브에 대한 동일한 플랫폼 독립적 메시지를 백 엔드에서 해당 메시지를 인식하도록 요구하지 않고 토스트 경고와 타일 업데이트로 완벽하게 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="a854e-135">참고로 알림을 짧은 기간에 보내는 경우 일부 플랫폼(예: iOS)은 여러 알림을 동일한 장치로 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="a854e-136">개인 설정에 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="a854e-136">Using templates for personalization</span></span>
<span data-ttu-id="a854e-137">템플릿 사용의 또 다른 장점은 알림 허브를 사용하여 알림의 등록별 개인 설정을 수행할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="a854e-138">예를 들어 특정 지역의 기상 조건이 포함된 타일을 표시하는 날씨 앱을 생각해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="a854e-139">사용자는 섭씨 또는 화씨 온도 및 1일 또는 5일 예보 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="a854e-140">템플릿을 사용하여 각 클라이언트 앱 설치에서 필요한 형식(1일 섭씨, 1일 화씨, 5일 섭씨, 5일 화씨)에 대해 등록하고 템플릿을 채우는 데 필요한 모든 정보가 포함된 단일 메시지(예를 들어 섭씨 및 화씨 도가 포함된 5일 예보)를 백 엔드가 보내도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="a854e-141">섭씨 온도가 포함된 1일 예보용 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="a854e-142">알림 허브로 전송되는 메시지에는 다음과 같은 속성이 모두 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="a854e-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="a854e-143">day1_image</span></span></td><td><span data-ttu-id="a854e-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="a854e-144">day2_image</span></span></td><td><span data-ttu-id="a854e-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="a854e-145">day3_image</span></span></td><td><span data-ttu-id="a854e-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="a854e-146">day4_image</span></span></td><td><span data-ttu-id="a854e-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="a854e-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="a854e-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="a854e-148">day1_tempC</span></span></td><td><span data-ttu-id="a854e-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="a854e-149">day2_tempC</span></span></td><td><span data-ttu-id="a854e-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="a854e-150">day3_tempC</span></span></td><td><span data-ttu-id="a854e-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="a854e-151">day4_tempC</span></span></td><td><span data-ttu-id="a854e-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="a854e-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="a854e-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="a854e-153">day1_tempF</span></span></td><td><span data-ttu-id="a854e-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="a854e-154">day2_tempF</span></span></td><td><span data-ttu-id="a854e-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="a854e-155">day3_tempF</span></span></td><td><span data-ttu-id="a854e-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="a854e-156">day4_tempF</span></span></td><td><span data-ttu-id="a854e-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="a854e-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="a854e-158">이 패턴을 사용하면 백 엔드는 앱 사용자에 대한 특정 개인 설정 옵션을 저장할 필요 없이 단일 메시지만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="a854e-159">다음 그림은 이 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="a854e-160">템플릿을 등록하는 방법</span><span class="sxs-lookup"><span data-stu-id="a854e-160">How to register templates</span></span>
<span data-ttu-id="a854e-161">설치 모델(기본 설정) 또는 등록 모델을 사용하여 템플릿에 등록하는 방법은 [등록 관리](notification-hubs-push-notification-registration-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a854e-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="a854e-162">템플릿 식 언어</span><span class="sxs-lookup"><span data-stu-id="a854e-162">Template expression language</span></span>
<span data-ttu-id="a854e-163">템플릿은 XML 또는 JSON 문서 형식으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="a854e-164">또한 식을 특정 장소에만 배치할 수 있습니다. 예를 들어 XML은 노드 속성 또는 값에, JSON은 문자열 속성 값에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="a854e-165">다음 표는 템플릿에 허용되는 언어를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="a854e-166">식</span><span class="sxs-lookup"><span data-stu-id="a854e-166">Expression</span></span> | <span data-ttu-id="a854e-167">설명</span><span class="sxs-lookup"><span data-stu-id="a854e-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a854e-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="a854e-168">$(prop)</span></span> |<span data-ttu-id="a854e-169">지정한 이름을 가진 이벤트 속성에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="a854e-170">속성 이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="a854e-171">이 식은 속성이 없으면 속성의 텍스트 값 또는 빈 문자열로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="a854e-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="a854e-172">$(prop, n)</span></span> |<span data-ttu-id="a854e-173">위와 같이 텍스트는 n 자에서 명시적으로 잘립니다. 예를 들어 $(title, 20)은 title 속성의 내용을 20 자에서 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="a854e-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="a854e-174">.(prop, n)</span></span> |<span data-ttu-id="a854e-175">위와 같지만 잘릴 때 뒤에 점 세 개가 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="a854e-176">잘린 문자열과 접미사의 총 크기는 n 문자를 초과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="a854e-177">입력 속성이 “This is the title line”인 .(title, 20)은 **This is the title...**</span><span class="sxs-lookup"><span data-stu-id="a854e-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="a854e-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="a854e-178">%(prop)</span></span> |<span data-ttu-id="a854e-179">출력이 URI 인코딩된다는 것을 제외하고 $(name)과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="a854e-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="a854e-180">#(prop)</span></span> |<span data-ttu-id="a854e-181">JSON 템플릿(예: iOS 및 Android 템플릿)에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="a854e-182">이 함수는 JSON 템플릿(예: Apple 템플릿)과 함께 사용되는 경우를 제외하고 앞에 지정된 $(prop)와 똑같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="a854e-183">이 경우 이 함수를 “{‘,’}”로 둘러싸지(예: ‘myJsonProperty’ : ‘#(name)’) 않고 Javascript 형식의 숫자로 평가하면, 예를 들어 regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?와 같이 지정하면 출력 JSON은 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="a854e-184">예를 들어 ‘badge : ‘#(name)’은 ‘badge’ : 40 이 됩니다(‘40‘이 아니라).</span><span class="sxs-lookup"><span data-stu-id="a854e-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="a854e-185">'text' 또는 "text"</span><span class="sxs-lookup"><span data-stu-id="a854e-185">‘text’ or “text”</span></span> |<span data-ttu-id="a854e-186">리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-186">A literal.</span></span> <span data-ttu-id="a854e-187">리터럴에는 작은따옴표 또는 큰따옴표로 묶인 임의의 텍스트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="a854e-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="a854e-188">expr1 + expr2</span></span> |<span data-ttu-id="a854e-189">두 개의 식을 단일 문자열로 합치는 연결 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="a854e-190">위의 모든 형태가 식이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="a854e-191">연결을 사용할 경우 전체 식을 {}로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="a854e-192">예: {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="a854e-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="a854e-193">예를 들어, 다음은 올바른 XML 템플릿이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="a854e-194">위에서 설명한 대로 연결을 사용하는 경우 식을 중괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a854e-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="a854e-195">예:</span><span class="sxs-lookup"><span data-stu-id="a854e-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

