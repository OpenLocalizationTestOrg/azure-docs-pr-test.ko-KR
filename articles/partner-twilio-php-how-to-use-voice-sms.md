---
title: "aaaHow tooUse Twilio 음성 및 SMS (PHP) | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 PHP로 작성되었습니다."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="cce1b-104">어떻게 tooUse Twilio 음성 및 SMS 기능 PHP에 대 한</span><span class="sxs-lookup"><span data-stu-id="cce1b-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="cce1b-105">이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="cce1b-106">포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="cce1b-107">Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="cce1b-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="cce1b-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="cce1b-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="cce1b-109">Twilio는 비즈니스 통신의 hello 미래 전원을 켜는 중, 개발자 tooembed 음성 VoIP, 활성화 및 메시징을 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="cce1b-110">Hello Twilio 통신 API 플랫폼을 통해 노출 하는 클라우드 기반, 글로벌 환경에서 필요한 모든 인프라를 가상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="cce1b-111">응용 프로그램은 단순 toobuild 하 고 확장 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="cce1b-112">종량제 가격의 유연성과 클라우드 안정성의 이점을 누리십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1b-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="cce1b-113">**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="cce1b-114">**Twilio SMS** 응용 프로그램 toosend 있으며 특정 문자 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="cce1b-115">**Twilio 클라이언트** WebRTC 지원 및 전화, 태블릿 또는 브라우저에서 toomake VoIP 전화 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="cce1b-116"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="cce1b-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="cce1b-117">Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공](http://www.twilio.com/azure)(10달러의 Twilio 크레딧)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="cce1b-118">Twilio 신용이 적용 된 tooany Twilio 사용량 ($10 신용 해당 toosending 최대 1, 000 SMS 메시지 또는 받기가 too1000 인바운드 hello 전화 번호와 메시지 또는 호출 대상 위치에 따라 음성 분) 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="cce1b-119">[http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)에서 이 Twilio 크레딧을 충전하고 시작하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1b-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="cce1b-120">Twilio는 종량제 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="cce1b-121">설정 수수료는 없으며 언제든 계정을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="cce1b-122">[Twilio 가격 책정][twilio_pricing]에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="cce1b-123"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="cce1b-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="cce1b-124">hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="cce1b-125">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1b-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="cce1b-126">Hello Twilio API의 주요 측면은 Twilio 동사 및 Twilio Markup Language (TwiML)입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="cce1b-127"><a id="Verbs"></a>Twilio 동사</span><span class="sxs-lookup"><span data-stu-id="cce1b-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="cce1b-128">hello API에서 Twilio 활용 동사; 예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="cce1b-129">hello 다음은 Twilio 동사 목록을입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="cce1b-130">자세한 내용은 다른 동사와 기능을 통해 약 hello [Twilio Markup Language 설명서](http://www.twilio.com/docs/api/twiml)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="cce1b-131">**&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="cce1b-132">**&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="cce1b-133">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="cce1b-134">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="cce1b-135">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="cce1b-136">**&lt;레코드&gt;**: hello 호출자의 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="cce1b-137">**&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="cce1b-138">**&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호 호출</span><span class="sxs-lookup"><span data-stu-id="cce1b-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="cce1b-139">**&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="cce1b-140">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="cce1b-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="cce1b-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="cce1b-142">TwiML 방법의 Twilio를 알려주는 hello Twilio 동사에 따라 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="cce1b-143">예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World** toospeech 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="cce1b-144">응용 프로그램이 호출 hello Twilio API, hello API 매개 변수 중 하나 hello TwiML 응답을 반환 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="cce1b-145">개발을 위해 응용 프로그램에서 사용 하는 Twilio 제공 Url tooprovide hello TwiML 응답을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="cce1b-146">직접 Url tooproduce hello TwiML 응답을 호스트할 수 있습니다 및 두 번째 방법은 toouse hello **TwiMLResponse** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="cce1b-147">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cce1b-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="cce1b-148">Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="cce1b-149"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="cce1b-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="cce1b-150">준비 tooget Twilio 계정 되 면에서 등록 [시도 Twilio][try_twilio]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="cce1b-151">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="cce1b-152">Twilio 계정을 등록하면 계정 ID 및 인증 토큰을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="cce1b-153">둘 다 필요한 toomake Twilio API 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="cce1b-154">권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="cce1b-155">계정 ID 및 인증 토큰 hello에서 볼 수 있는 [Twilio 계정 페이지][twilio_account]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰**각각.</span><span class="sxs-lookup"><span data-stu-id="cce1b-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="cce1b-156"><a id="create_app"></a>HP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="cce1b-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="cce1b-157">Azure에서 실행 되 고 hello Twilio 서비스를 사용 하는 PHP 응용 프로그램은 다른 모든 PHP 응용 프로그램 hello Twilio 서비스를 사용 하는 방법과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="cce1b-158">이 문서는 toouse Twilio를 사용 하 여 서비스 방법을 중점 Twilio 서비스는 REST 기반 하 고 여러 가지 방법으로 PHP에서 호출할 수 있습니다, [GitHub에서 PHP 용 Twilio 라이브러리][twilio_php]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="cce1b-159">PHP 용 hello Twilio 라이브러리를 사용 하는 방법에 대 한 자세한 내용은 참조 [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="cce1b-160">Twilio/PHP 응용 프로그램 tooAzure 구축 하기 위한 자세한 지침은 [어떻게 tooMake Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio][howto_phonecall_php]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="cce1b-161"><a id="configure_app"></a>응용 프로그램 tooUse Twilio 라이브러리 구성</span><span class="sxs-lookup"><span data-stu-id="cce1b-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="cce1b-162">PHP에 대 한 두 가지 방법으로 응용 프로그램 toouse hello Twilio 라이브러리를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="cce1b-163">GitHub에서 PHP 용 hello Twilio 라이브러리를 다운로드 ([https://github.com/twilio/twilio-php][twilio_php]) hello 추가 **서비스** 디렉터리 tooyour 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="cce1b-164">또는</span><span class="sxs-lookup"><span data-stu-id="cce1b-164">-OR-</span></span>
2. <span data-ttu-id="cce1b-165">PHP 용 배 패키지로 hello Twilio 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="cce1b-166">다음 명령은 hello로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="cce1b-167">PHP 용 hello Twilio 라이브러리를 설치 하면를 추가할 수 있습니다는 **require_once** 프로그램 PHP의 hello 위쪽 문을 tooreference hello 라이브러리 파일:</span><span class="sxs-lookup"><span data-stu-id="cce1b-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="cce1b-168">자세한 내용은 참조 [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="cce1b-169"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="cce1b-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="cce1b-170">hello 다음 테이블에 나와 hello를 사용 하 여 나가는 toomake을 호출 하는 방법을 **Services_Twilio** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="cce1b-171">이 코드는 또한 Twilio 제공 사이트 tooreturn hello Twilio Markup Language (TwiML) 응답을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="cce1b-172">Hello에 대 한 값을 대체 **에서** 및 **를** 전화 번호를 하 고 hello를 확인 하는 확인 **에서** Twilio 계정 이전 toorunning hello 코드의 전화 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="cce1b-173">앞서 언급 했 듯이이 코드는 Twilio 제공 사이트 tooreturn hello TwiML 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="cce1b-174">사용자 고유의 사이트 tooprovide hello TwiML 응답; 대신 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 tooProvide TwiML 응답에서 직접 웹 사이트](#howto_provide_twiml_responses)합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="cce1b-175">**참고**: tootroubleshoot SSL 인증서 유효성 검사 오류 참조 [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="cce1b-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="cce1b-176"><a id="howto_send_sms"></a>방법: SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="cce1b-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="cce1b-177">hello 다음 테이블에 나와 방법을 사용 하 여 SMS 메시지 toosend hello **Services_Twilio** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="cce1b-178">hello **에서** 번호는 평가판 계정 toosend SMS 메시지에 대해 Twilio에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="cce1b-179">hello **를** Twilio 계정 이전 toorunning hello 코드에 대 한 번호를 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="cce1b-180"><a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공</span><span class="sxs-lookup"><span data-stu-id="cce1b-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="cce1b-181">응용 프로그램 호출 toohello Twilio API를 시작, Twilio 요청 tooa URL을 예상 tooreturn TwiML 응답 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="cce1b-182">hello Twilio 제공 URL을 사용 하 여 위의 hello 예제 [http://twimlets.com/message][twimlet_message_url]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="cce1b-183">(볼 수 있습니다 TwiML를 Twilio에서 사용 하기 위해 디자인 된 반면 브라우저에서 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="cce1b-184">예를 들어 클릭 [http://twimlets.com/message] [ twimlet_message_url] toosee 빈 `<Response>` 요소로 또 다른 예로, 클릭 [http://twimlets.com/message? 메시지 % 5B0 %5 D = Hello %20World] [ twimlet_message_url_hello_world] toosee는 `<Response>` 요소를 포함 하는 `<Say>` 요소입니다.)</span><span class="sxs-lookup"><span data-stu-id="cce1b-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="cce1b-185">Hello Twilio 제공 URL에 의존 하지 않고 HTTP 응답을 반환 하는 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="cce1b-186">XML 응답; 반환 되는 언어로 hello 사이트를 만들 수 있습니다. 이 항목에서는 PHP toocreate hello TwiML 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="cce1b-187">PHP 페이지 결과 라는 TwiML 응답에 따라 hello **Hello World** hello 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="cce1b-188">위의 hello 예제 알 수 있듯이 hello TwiML 응답은 XML 문서 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="cce1b-189">PHP 용 hello Twilio 라이브러리 TwiML를 생성 하는 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="cce1b-190">아래 예제에서는 hello 위와 같이 hello 해당 응답을 생성 하지만 hello를 사용 하 여 **서비스\_Twilio\_Twiml** PHP 용 hello Twilio 라이브러리의 클래스:</span><span class="sxs-lookup"><span data-stu-id="cce1b-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="cce1b-191">TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml][twiml_reference]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cce1b-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="cce1b-192">Tooprovide TwiML 응답을 설정 하 여 PHP 페이지를 사용 하는 후 사용 hello PHP 페이지의 URL hello hello에 전달 된 URL을 hello `Services_Twilio->account->calls->create` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cce1b-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="cce1b-193">예를 들어, 명명 된 웹 응용 프로그램의 경우 **MyTwiML** 호스 티 드 서비스를 배포 된 tooan Azure 및 hello hello PHP 페이지 이름이 **mytwiml.php**, URL을 너무 전달 될 수 있습니다. hello **서비스 Twilio 계정-> 호출->-> 만들** hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="cce1b-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="cce1b-194">Twilio를 사용 하 여 PHP 사용 하 여 Azure에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooMake Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio][howto_phonecall_php]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="cce1b-195"><a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="cce1b-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="cce1b-196">또한 toohello 예제 Twilio 제공 웹 기반 Api를 여기에 표시 된 Azure 응용 프로그램에서 추가 Twilio 기능 tooleverage를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="cce1b-197">전체 세부 정보에 대 한 참조 hello [Twilio API 설명서][twilio_api_documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="cce1b-198"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="cce1b-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="cce1b-199">Hello Twilio 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cce1b-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="cce1b-200">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="cce1b-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="cce1b-201">[Twilio 사용 방법 및 예제 코드][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="cce1b-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="cce1b-202">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="cce1b-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="cce1b-203">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="cce1b-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="cce1b-204">[Talk tooTwilio 지원][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="cce1b-204">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
