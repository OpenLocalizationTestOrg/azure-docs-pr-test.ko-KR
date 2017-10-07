---
title: "aaaHow tooUse 음성 및 SMS (.NET)에 대 한 Twilio | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 .NET으로 작성되었습니다."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="41dce-104">어떻게 toouse Twilio 음성 및 SMS 기능에서 Azure에 대 한</span><span class="sxs-lookup"><span data-stu-id="41dce-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="41dce-105">이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="41dce-106">포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="41dce-107">Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="41dce-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="41dce-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="41dce-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="41dce-109">Twilio는 비즈니스 통신의 hello 미래 전원을 켜는 중, 개발자 tooembed 음성 VoIP, 활성화 및 메시징을 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="41dce-110">Hello Twilio 통신 API 플랫폼을 통해 노출 하는 클라우드 기반, 글로벌 환경에서 필요한 모든 인프라를 가상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="41dce-111">응용 프로그램은 단순 toobuild 하 고 확장 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="41dce-112">종량제 가격 책정의 유연성과 클라우드 안정성의 이점을 누리세요.</span><span class="sxs-lookup"><span data-stu-id="41dce-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="41dce-113">**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="41dce-114">**Twilio SMS** 응용 프로그램 toosend 있으며 특정 SMS 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="41dce-115">**Twilio 클라이언트** WebRTC 지원 및 전화, 태블릿 또는 브라우저에서 toomake VoIP 전화 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="41dce-116"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="41dce-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="41dce-117">Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공](http://www.twilio.com/azure)(10달러의 Twilio 크레딧)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="41dce-118">Twilio 신용이 적용 된 tooany Twilio 사용량 ($10 신용 해당 toosending 최대 1, 000 SMS 메시지 또는 받기가 too1000 인바운드 hello 전화 번호와 메시지 또는 호출 대상 위치에 따라 음성 분) 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="41dce-119">[ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)에서 이 Twilio 크레딧을 충전하고 시작하십시오.</span><span class="sxs-lookup"><span data-stu-id="41dce-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="41dce-120">Twilio는 종량제 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="41dce-121">설치 수수료는 없으며 언제든 계정을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="41dce-122">[Twilio 가격 책정](http://www.twilio.com/voice/pricing)(영문)에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="41dce-123"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="41dce-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="41dce-124">hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="41dce-125">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41dce-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="41dce-126">Hello Twilio API의 주요 측면은 Twilio 동사 및 Twilio Markup Language (TwiML)입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="41dce-127"><a id="Verbs"></a>Twilio 동사</span><span class="sxs-lookup"><span data-stu-id="41dce-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="41dce-128">hello API에서 Twilio 활용 동사; 예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="41dce-129">hello 다음은 Twilio 동사 목록을입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="41dce-130">자세한 내용은 다른 동사와 기능을 통해 약 hello [Twilio Markup Language 설명서](http://www.twilio.com/docs/api/twiml)합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="41dce-131">**&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="41dce-132">**&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="41dce-133">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="41dce-134">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="41dce-135">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="41dce-136">**&lt;레코드&gt;**: hello 호출자의 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="41dce-137">**&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="41dce-138">**&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호 호출</span><span class="sxs-lookup"><span data-stu-id="41dce-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="41dce-139">**&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="41dce-140">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="41dce-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="41dce-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="41dce-142">TwiML 방법의 Twilio를 알려주는 hello Twilio 동사에 따라 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="41dce-143">예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World** toospeech 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="41dce-144">응용 프로그램이 호출 hello Twilio API, hello API 매개 변수 중 하나 hello TwiML 응답을 반환 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="41dce-145">개발을 위해 응용 프로그램에서 사용 하는 Twilio 제공 Url tooprovide hello TwiML 응답을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="41dce-146">직접 Url tooproduce hello TwiML 응답을 호스트할 수 있습니다 및 두 번째 방법은 toouse hello **TwiMLResponse** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="41dce-147">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41dce-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="41dce-148">Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="41dce-149"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="41dce-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="41dce-150">준비 tooget Twilio 계정 되 면에서 등록 [시도 Twilio][try_twilio]합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="41dce-151">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="41dce-152">Twilio 계정을 등록하면 계정 ID 및 인증 토큰을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="41dce-153">둘 다 필요한 toomake Twilio API 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="41dce-154">권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="41dce-155">계정 ID 및 인증 토큰 hello에서 볼 수 있는 [Twilio 계정 페이지][twilio_account]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰**각각.</span><span class="sxs-lookup"><span data-stu-id="41dce-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="41dce-156"><a id="create_app"></a>Azure 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="41dce-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="41dce-157">Twilio 사용 응용 프로그램을 호스트하는 Azure 응용 프로그램도 다른 Azure 응용 프로그램과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="41dce-158">Hello Twilio.NET 라이브러리를 추가 하 고 hello 역할 toouse hello Twilio.NET 라이브러리를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="41dce-159">초기 Azure 프로젝트 만들기에 대한 자세한 내용은 [Visual Studio에서 Azure 프로젝트 만들기][vs_project]를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41dce-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="41dce-160"><a id="configure_app"></a>응용 프로그램 toouse Twilio 라이브러리 구성</span><span class="sxs-lookup"><span data-stu-id="41dce-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="41dce-161">Twilio는 Twilio tooprovide 단순 하 고 간편한 방법도 toointeract hello Twilio REST API와 Twilio 클라이언트의 다양 한 측면을 래핑하는.NET 도우미 라이브러리 집합이 toogenerate TwiML 응답을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="41dce-162">Twilio는 다음과 같이 .NET 개발자를 위한 5가지 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="41dce-163">라이브러리</span><span class="sxs-lookup"><span data-stu-id="41dce-163">Library</span></span>|<span data-ttu-id="41dce-164">설명</span><span class="sxs-lookup"><span data-stu-id="41dce-164">Description</span></span>
---|---
<span data-ttu-id="41dce-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="41dce-165">Twilio.API</span></span>|<span data-ttu-id="41dce-166">친숙 한.NET 라이브러리의 hello Twilio REST API를 래핑하는 hello 코어 Twilio 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="41dce-167">이 라이브러리는 .NET, Silverlight 및 Windows Phone 7에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="41dce-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="41dce-168">Twilio.TwiML</span></span>|<span data-ttu-id="41dce-169">.NET 친화적인 방식 toogenerate TwiML 태그를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="41dce-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="41dce-170">Twilio.MVC</span></span>|<span data-ttu-id="41dce-171">ASP.NET MVC를 사용하는 개발자를 위해 이 라이브러리는 TwilioController, TwiML ActionResult 및 요청 유효성 검사 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="41dce-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="41dce-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="41dce-173">Microsoft의 무료 WebMatrix 개발 도구를 사용하는 개발자를 위해 이 라이브러리는 다양한 Twilio 작업에 사용할 수 있는 Razor 구문을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="41dce-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="41dce-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="41dce-175">Hello 토큰 생성기 hello Twilio 클라이언트 JavaScript SDK와 함께 사용할 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="41dce-176">모든 라이브러리를 사용하려면 .NET 3.5, Silverlight 4 또는 Windows Phone 7 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="41dce-177">이 가이드에서 제공 하는 hello 샘플 hello Twilio.API 라이브러리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="41dce-178">hello 라이브러리 수 [hello NuGet 패키지 관리자 확장을 사용 하 여 설치](http://www.twilio.com/docs/csharp/install) too2015를 Visual Studio 2010에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="41dce-179">hello 소스 코드에서 호스팅되는 [GitHub][twilio_github_repo], hello 라이브러리 사용에 대 한 전체 설명서를 포함 하는 Wiki를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="41dce-180">기본적으로, Microsoft Visual Studio 2010은 버전 1.2의 NuGet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="41dce-181">Hello Twilio 라이브러리를 설치 하려면 버전 1.6의 NuGet이 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="41dce-182">NuGet 설치 또는 업데이트에 대해서는 [http://nuget.org/][nuget](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41dce-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="41dce-183">tooinstall hello 최신 버전의 NuGet에서는 hello Visual Studio 확장 관리자를 사용 하 여 hello 로드 된 버전을 먼저 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="41dce-184">toodo, 관리자 권한으로 Visual Studio를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="41dce-185">그렇지 않으면 hello 제거 단추가 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="41dce-186"><a id="use_nuget"></a>tooadd hello Twilio 라이브러리 tooyour Visual Studio 프로젝트:</span><span class="sxs-lookup"><span data-stu-id="41dce-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="41dce-187">Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="41dce-188">**참조**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-188">Right-click **References**.</span></span>
3. <span data-ttu-id="41dce-189">**NuGet 패키지 관리...**</span><span class="sxs-lookup"><span data-stu-id="41dce-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="41dce-190">**온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-190">Click **Online**.</span></span>
5. <span data-ttu-id="41dce-191">Hello 검색 온라인 상자에 입력 *twilio*합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="41dce-192">클릭 **설치** hello Twilio 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="41dce-193"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="41dce-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="41dce-194">hello 다음 테이블에 나와 hello를 사용 하 여 나가는 toomake을 호출 하는 방법을 **CallResource** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="41dce-195">이 코드는 또한 Twilio 제공 사이트 tooreturn hello Twilio Markup Language (TwiML) 응답을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="41dce-196">Hello에 대 한 값을 대체 **를** 및 **에서** 전화 번호를 하 고 hello를 확인 하는 확인 **에서** hello 코드를 실행 하기 전에 전화 Twilio 계정에 대 한 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="41dce-197">Hello 매개 변수 toohello를 전달 하는 방법에 대 한 자세한 내용은 **CallResource.Create** 메서드를 참조 [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="41dce-198">앞서 언급 했 듯이이 코드는 Twilio 제공 사이트 tooreturn hello TwiML 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="41dce-199">대신 사용자 고유의 사이트 tooprovide hello TwiML 응답을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="41dce-200">자세한 내용은 [방법: 고유한 웹 사이트에서 TwiML 응답 제공](#howto_provide_twiml_responses)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41dce-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="41dce-201"><a id="howto_send_sms"></a>방법: SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="41dce-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="41dce-202">hello 다음 스크린샷은 방법을 사용 하 여 SMS 메시지 toosend hello **MessageResource** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="41dce-203">hello **에서** 번호는 평가판 계정 toosend SMS 메시지에 대해 Twilio에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="41dce-204">hello **를** hello 코드를 실행 하기 전에 Twilio 계정에 대 한 번호를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="41dce-205"><a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공</span><span class="sxs-lookup"><span data-stu-id="41dce-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="41dce-206">때 응용 프로그램 시작 호출 toohello Twilio API-예를 들어 hello를 통해 **CallResource.Create** 방법-Twilio 예상된 tooreturn 있는 요청 tooan URL TwiML 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="41dce-207">hello 예제 [하는 방법: 나가는 호출](#howto_make_call) 사용 하 여 hello Twilio 제공 URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="41dce-208">TwiML를 웹 서비스에서 사용 하기 위해 디자인 된 반면 hello TwiML 브라우저에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="41dce-209">예를 들어 클릭 [http://twimlets.com/message] [ twimlet_message_url] toosee 빈 &lt;응답&gt; 요소로 또 다른 예로, 클릭 [http://twimlets.com/message ? 메시지 % 5B0 %5 D = Hello %20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee는 &lt;응답&gt; 요소를 포함 하는 &lt;의견을 언급 해서도&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="41dce-210">Hello Twilio 제공 URL에 의존 하지 않고 HTTP 응답을 반환 하는 URL 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="41dce-211">HTTP 응답에 반환 되는 언어로 hello 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="41dce-212">이 항목에서는 ASP.NET 일반 처리기에서 hello URL를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="41dce-213">ASP.NET 처리기를 다음 hello 라는 TwiML 응답 crafts **Hello World** hello 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="41dce-214">위의 hello 예제 알 수 있듯이 hello TwiML 응답은 XML 문서 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="41dce-215">hello Twilio.TwiML 라이브러리 TwiML를 생성 하는 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="41dce-216">hello 아래 예제에서는 위에 표시 된 대로 hello 해당 응답을 생성 하지만 hello를 사용 하 여 **VoiceResponse** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="41dce-217">TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml)(영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41dce-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="41dce-218">해당 URL toohello를 전달할 수 방식으로 tooprovide TwiML 응답을 설정한 후 **CallResource.Create** 메서드.</span><span class="sxs-lookup"><span data-stu-id="41dce-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="41dce-219">예를 들어 배포 MyTwiML tooan Azure 클라우드 서비스 웹 응용 프로그램의 ASP.NET 처리기 hello 이름이 mytwiml.ashx, 있고 hello URL 전달 될 수 있습니다 너무**CallResource.Create** hello 코드 다음에 표시 된 대로 샘플:</span><span class="sxs-lookup"><span data-stu-id="41dce-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="41dce-220">Twilio를 사용 하 여 ASP.NET 사용 하 여 Azure에 대 한 자세한 내용은 참조 하십시오. [toomake 휴대폰 호출 방법을 Twilio를 사용 하 여 Azure에서 웹 역할에서][howto_phonecall_dotnet]합니다.</span><span class="sxs-lookup"><span data-stu-id="41dce-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
