---
title: "음성 및 SMS에 Twilio를 사용하는 방법(PHP) | Microsoft Docs"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 코드 샘플은 PHP로 작성되었습니다."
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="d0e02-104">PHP에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="d0e02-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="d0e02-105">이 가이드에서는 Azure에서 Twilio API 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="d0e02-106">이 문서의 시나리오에서는 전화 통화를 걸고 SMS(Short Message Service) 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="d0e02-107">응용 프로그램에서 음성 및 SMS 사용 방법과 Twilio에 대한 자세한 내용은 [다음 단계](#NextSteps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="d0e02-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="d0e02-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="d0e02-109">Twilio는 개발자가 응용 프로그램에 음성, VoIP 및 메시징을 포함할 수 있도록 하면서 비즈니스 통신의 미래를 이끌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="d0e02-110">개발자는 클라우드 기반 글로벌 환경에 필요한 모든 인프라를 가상화하고, Twilio 통신 API 플랫폼을 통해 이를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="d0e02-111">덕분에 응용 프로그램을 간단히 빌드하고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="d0e02-112">종량제 가격의 유연성과 클라우드 안정성의 이점을 누리십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="d0e02-113">**Twilio 음성** 을 통해 응용 프로그램에서 전화를 걸고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="d0e02-114">**Twilio SMS** 를 사용하면 응용 프로그램에서 문자 메시지를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="d0e02-115">**Twilio 클라이언트** 를 통해서는 전화, 태블릿 또는 브라우저에서 VoIP 통화를 하고 WebRTC를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="d0e02-116"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="d0e02-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="d0e02-117">Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공](http://www.twilio.com/azure)(10달러의 Twilio 크레딧)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="d0e02-118">이 Twilio 크레딧은 모든 Twilio 사용량에 적용될 수 있습니다. 10달러의 크레딧은 전화 번호 및 메시지 또는 통화 대상의 위치에 따라 SMS 메시지를 1,000개 보내거나 최대 1000분간 인바운드 음성을 받을 수 있는 금액입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="d0e02-119">[http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)에서 이 Twilio 크레딧을 충전하고 시작하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="d0e02-120">Twilio는 종량제 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="d0e02-121">설정 수수료는 없으며 언제든 계정을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="d0e02-122">[Twilio 가격 책정][twilio_pricing]에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="d0e02-123"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="d0e02-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="d0e02-124">Twilio API는 응용 프로그램에 대한 음성 및 SMS 기능을 제공하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="d0e02-125">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="d0e02-126">Twilio API의 핵심 요소는 Twilio 동사와 TwiML(Twilio Markup Language)입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="d0e02-127"><a id="Verbs"></a>Twilio 동사</span><span class="sxs-lookup"><span data-stu-id="d0e02-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="d0e02-128">API는 Twilio 동사를 활용합니다. 예를 들어 **&lt;Say&gt;** 동사는 Twilio에 통화 메시지를 음성으로 전달하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="d0e02-129">다음은 Twilio 동사의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="d0e02-130">기타 동사 및 기능에 대해서는 [Twilio Markup Language 설명서](http://www.twilio.com/docs/api/twiml)(영문)에서 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="d0e02-131">**&lt;Dial&gt;**: 발신자를 다른 전화에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="d0e02-132">**&lt;Gather&gt;**: 전화 키패드에 입력된 숫자를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="d0e02-133">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="d0e02-134">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="d0e02-135">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="d0e02-136">**&lt;Record&gt;**: 발신자의 음성을 녹음하고 녹음이 포함된 파일의 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="d0e02-137">**&lt;Redirect&gt;**: 통화 또는 SMS에 대한 제어를 다른 URL의 TwiML로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="d0e02-138">**&lt;Reject&gt;**: 요금을 청구하지 않고 Twilio 번호의 수신 전화를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="d0e02-139">**&lt;Say&gt;**: 텍스트를 통화에 사용되는 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="d0e02-140">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="d0e02-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="d0e02-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="d0e02-142">TwiML은 Twilio에 통화 또는 SMS 처리 방법을 알려 주는 Twilio 동사를 사용하는 XML 기반 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="d0e02-143">다음 예제 TwiML은 **Hello World** 텍스트를 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="d0e02-144">응용 프로그램에서 Twilio API를 호출할 때 API 매개 변수 중 하나는 TwiML 응답을 반환하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="d0e02-145">개발을 위해서 Twilio 제공 URL을 사용하여 응용 프로그램에 사용되는 TwiML 응답을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="d0e02-146">또한 TwiML 응답을 생성하는 고유한 URL을 호스트할 수도 있고, **TwiMLResponse** 개체를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="d0e02-147">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="d0e02-148">Twilio API에 대한 자세한 내용은 [Twilio API][twilio_api](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="d0e02-149"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="d0e02-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="d0e02-150">Twilio 계정을 사용할 준비가 되었다면 [Twilio 체험][try_twilio](영문)에서 등록하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="d0e02-151">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="d0e02-152">Twilio 계정을 등록하면 계정 ID 및 인증 토큰을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="d0e02-153">둘 다 Twilio API 통화를 하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="d0e02-154">계정에 대한 무단 액세스를 방지하려면 인증 토큰을 안전하게 유지하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="d0e02-155">계정 ID 및 인증 토큰은 [Twilio 계정 페이지][twilio_account](영문)의 **ACCOUNT SID** 및 **AUTH TOKEN**에서 각기 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="d0e02-156"><a id="create_app"></a>HP 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d0e02-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="d0e02-157">Twilio 서비스를 사용하고 Azure에서 실행되고 있는 PHP 응용 프로그램은 Twilio 서비스를 사용하는 다른 PHP 응용 프로그램과 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="d0e02-158">이 문서 Twilio 서비스를 사용 하는 방법에 대해 중점적으로 Twilio 서비스는 REST 기반 하 고 여러 가지 방법으로 PHP에서 호출할 수 있습니다, [GitHub에서 PHP 용 Twilio 라이브러리][twilio_php]합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="d0e02-159">PHP 용 Twilio 라이브러리를 사용 하는 방법에 대 한 자세한 내용은 참조 [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs]합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="d0e02-160">빌드하고 Twilio/PHP 응용 프로그램을 Azure에 배포 하기 위한 자세한 지침은 [Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio를 확인 하는 방법을][howto_phonecall_php]합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="d0e02-161"><a id="configure_app"></a>Twilio 라이브러리를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="d0e02-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="d0e02-162">다음과 같은 두 가지 방법으로 PHP용 Twilio 라이브러리를 사용하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="d0e02-163">GitHub에서 PHP 용 Twilio 라이브러리를 다운로드 ([https://github.com/twilio/twilio-php][twilio_php]) 추가 하 고는 **서비스** 응용 프로그램에 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="d0e02-164">또는</span><span class="sxs-lookup"><span data-stu-id="d0e02-164">-OR-</span></span>
2. <span data-ttu-id="d0e02-165">PHP용 Twilio 라이브러리를 PEAR 패키지로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="d0e02-166">다음 명령을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="d0e02-167">PHP용 Twilio 라이브러리를 설치하고 나면 PHP 파일의 맨 위에 **require_once** 문을 추가하여 라이브러리를 참조하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="d0e02-168">자세한 내용은 참조 [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme]합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="d0e02-169"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="d0e02-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="d0e02-170">다음은 **Services_Twilio** 클래스를 사용하여 발신 전화를 거는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="d0e02-171">또한 이 코드는 Twilio 제공 사이트를 사용하여 TwiML(Twilio Markup Language) 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="d0e02-172">**From** 및 **To** 전화 번호의 값을 바꾸고, 코드를 실행하기 전에 Twilio 계정의 **From** 번호를 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="d0e02-173">언급한 대로 이 코드는 Twilio 제공 사이트를 사용하여 TwiML 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="d0e02-174">고유한 사이트를 대신 사용하여 TwiML 응답을 제공할 수 있습니다. 자세한 내용은 [고유한 웹 사이트에서 TwiML 응답을 제공하는 방법](#howto_provide_twiml_responses)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="d0e02-175">**참고**: SSL 인증서 유효성 검사 오류를 해결 하려면 참조 [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="d0e02-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="d0e02-176"><a id="howto_send_sms"></a>방법: SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="d0e02-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="d0e02-177">다음은 **Services_Twilio** 클래스를 사용하여 SMS 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="d0e02-178">평가판 계정이 SMS 메시지를 보낼 **From** 번호는 자동으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="d0e02-179">코드를 실행하기 전에 Twilio 계정에 대한 **To** 번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="d0e02-180"><a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공</span><span class="sxs-lookup"><span data-stu-id="d0e02-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="d0e02-181">응용 프로그램에서 Twilio API 호출을 시작하면 Twilio에서 TwiML 응답을 반환해야 하는 URL로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="d0e02-182">위 예제에서는 Twilio 제공 URL인 [http://twimlets.com/message][twimlet_message_url]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="d0e02-183">TwiML은 Twilio에서 사용되도록 설계되었지만 브라우저에서도 TwiML을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="d0e02-184">예를 들어 [http://twimlets.com/message][twimlet_message_url]를 클릭하면 빈 `<Response>` 요소가 표시됩니다. 또 다른 예로, [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world]를 클릭하면 `<Say>` 요소를 포함하는 `<Response>` 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="d0e02-185">Twilio 제공 URL을 사용하지 않고 HTTP 응답을 반환하는 고유한 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="d0e02-186">XML 응답을 반환하는 모든 언어로 사이트를 만들 수 있습니다. 이 항목에서는 TwiML을 만들기 위해 PHP를 사용 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="d0e02-187">다음 PHP 페이지에서는 호출 시 **Hello World** 라고 말하는 TwiML 응답이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="d0e02-188">위의 예제와 같이 TwiML 응답은 단지 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="d0e02-189">PHP용 Twilio 라이브러리에는 TwiML을 자동으로 생성하는 클래스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="d0e02-190">아래의 예제에서는 위에 표시된 것과 동일한 응답을 생성하지만 PHP용 Twilio 라이브러리의 **Services\_Twilio\_Twiml** 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="d0e02-191">TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml][twiml_reference]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0e02-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="d0e02-192">PHP 페이지가 TwiML 응답을 제공하도록 설정된 경우 `Services_Twilio->account->calls->create` 메서드에 전달되는 URL로 PHP 페이지의 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="d0e02-193">예를 들어 **MyTwiML**이라는 웹 응용 프로그램이 Azure 호스티드 서비스에 배포되어 있고 PHP 페이지의 이름이 **mytwiml.php**인 경우 다음 예와 같이 URL을 **Services_Twilio->account->calls->create**에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="d0e02-194">Twilio를 사용 하 여 PHP 사용 하 여 Azure에 대 한 자세한 내용은 참조 하십시오. [Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio를 확인 하는 방법을][howto_phonecall_php]합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="d0e02-195"><a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="d0e02-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="d0e02-196">여기에서 보여 준 예뿐만 아니라 Twilio는 Azure 응용 프로그램에서 Twilio 기능을 활용할 수 있는 웹 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d0e02-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="d0e02-197">자세한 내용은 [Twilio API 설명서][twilio_api_documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0e02-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="d0e02-198"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="d0e02-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d0e02-199">Twilio 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="d0e02-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="d0e02-200">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="d0e02-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="d0e02-201">[Twilio 사용 방법 및 예제 코드][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="d0e02-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="d0e02-202">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="d0e02-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="d0e02-203">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="d0e02-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="d0e02-204">[Twilio 지원 문의][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="d0e02-204">[Talk to Twilio Support][twilio_support]</span></span>

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
