---
title: "aaaHow tooUse Twilio 음성 및 SMS (Ruby) | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 Ruby로 작성되었습니다."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="541c2-104">어떻게 tooUse Twilio 음성 및 SMS 기능 Ruby</span><span class="sxs-lookup"><span data-stu-id="541c2-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="541c2-105">이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="541c2-106">포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="541c2-107">Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="541c2-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="541c2-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="541c2-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="541c2-109">Twilio는 기존 웹 언어와 기술 toobuild 음성 및 SMS 응용 프로그램을 사용 하는 전화 통신 웹 서비스 API입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="541c2-110">Twilio는 타사 서비스입니다(Azure 기능 또는 Microsoft 제품 아님).</span><span class="sxs-lookup"><span data-stu-id="541c2-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="541c2-111">**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="541c2-112">**Twilio SMS** 응용 프로그램 toomake 있으며 SMS 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="541c2-113">**Twilio 클라이언트** 모바일 연결을 포함 하 여 기존 인터넷 연결을 사용 하 여 tooenable 음성 통신 응용 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="541c2-114"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="541c2-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="541c2-115">Twilio 가격 책정 정보는 [Twilio 가격 책정][twilio_pricing]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="541c2-116">Azure 고객은 [특별 제공][special_offer](문자 1000통 또는 인바운드 통화 1000분의 무료 크레딧)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="541c2-117">이 대해 toosign 제공 또는 자세한 정보를 얻을, 방문 하십시오 [http://ahoy.twilio.com/azure][special_offer]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="541c2-118"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="541c2-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="541c2-119">hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="541c2-120">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="541c2-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="541c2-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="541c2-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="541c2-122">TwiML 방법의 Twilio를 알려주는 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="541c2-123">예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World** toospeech 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="541c2-124">모든 TwiML 문서는 `<Response>` 를 루트 요소로 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="541c2-125">여기에서 응용 프로그램의 Twilio 동사 toodefine hello 동작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="541c2-126"><a id="Verbs"></a>TwiML 동사</span><span class="sxs-lookup"><span data-stu-id="541c2-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="541c2-127">Twilio 동사 지시 하는 Twilio 너무 XML 태그는**않습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="541c2-128">예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="541c2-129">hello 다음은 Twilio 동사 목록을입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="541c2-130">**&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="541c2-131">**&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="541c2-132">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="541c2-133">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="541c2-134">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="541c2-135">**&lt;레코드&gt;**: hello 호출자의 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="541c2-136">**&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="541c2-137">**&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호 호출</span><span class="sxs-lookup"><span data-stu-id="541c2-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="541c2-138">**&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="541c2-139">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="541c2-140">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="541c2-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="541c2-141">Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="541c2-142"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="541c2-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="541c2-143">준비 tooget Twilio 계정 되 면에서 등록 [시도 Twilio][try_twilio]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="541c2-144">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="541c2-145">Twilio 계정을 등록할 때 응용 프로그램의 무료 전화 번호를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="541c2-146">계정 SID 및 인증 토큰도 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="541c2-147">둘 다 필요한 toomake Twilio API 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="541c2-148">권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="541c2-149">사용자 계정 SID 및 인증 토큰은 hello에서 볼 수 있는 [Twilio 계정 페이지][twilio_account]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰** 각각.</span><span class="sxs-lookup"><span data-stu-id="541c2-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="541c2-150"><a id="VerifyPhoneNumbers"></a>전화 번호 확인</span><span class="sxs-lookup"><span data-stu-id="541c2-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="541c2-151">또한 toohello 번호 Twilio에 의해 제공 됩니다, 응용 프로그램에서 사용 하기 위해 (예: 휴대폰 이나 집 전화 번호)를 제어 하는 번호를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="541c2-152">방법에 대 한 내용은 tooverify 전화 번호를 참조 [관리 숫자][verify_phone]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="541c2-153"><a id="create_app"></a>Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="541c2-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="541c2-154">Azure에서 실행 되 고 hello Twilio 서비스를 사용 하는 Ruby 응용 프로그램은 다른 Ruby 응용 프로그램 hello Twilio 서비스를 사용 하는 방법과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="541c2-155">이 문서는 toouse Twilio를 사용 하 여 서비스 방법을 중점 Twilio 서비스는 RESTful을 여러 가지 방법으로 Ruby에서 호출할 수 있지만 [Ruby 용 Twilio 도우미 라이브러리][twilio_ruby]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="541c2-156">첫째, [새 Azure Linux VM 설정] [ azure_vm_setup] tooact 새 Ruby 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="541c2-157">레일 앱만 설치 hello VM의 hello 만들기와 관련 된 hello 단계를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="541c2-158">외부 포트 80과 내부 포트 5000으로 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="541c2-159">아래의 hello 예제를 사용 합니다 [Sinatra][sinatra], Ruby에 대 한 매우 간단한 웹 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="541c2-160">하지만 모든 다른 웹 프레임 워크와를 레일에 Ruby를 비롯 한 Ruby 용 hello Twilio 도우미 라이브러리를 대부분 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="541c2-161">새 VM에 SSH를 설치하고 새 앱용 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="541c2-162">해당 디렉터리 내에 코드를 다음 Gemfile 및 복사 hello 라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="541c2-163">Hello 명령줄 실행에서 `bundle install`합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="541c2-164">그러면 위의 hello 종속성 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-164">This will install hello dependencies above.</span></span> <span data-ttu-id="541c2-165">이제 `web.rb`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="541c2-166">이 웹 앱에 대 한 hello 코드 거주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="541c2-167">Hello에 코드를 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="541c2-168">이 시점에서 실행할 수 hello hello 명령 있어야 `ruby web.rb -p 5000`합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="541c2-169">그러면 포트 5000에서 작은 웹 서버가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="541c2-170">에서 해야 할 수 toobrowse toothis 앱 브라우저 hello URL을 방문 하 여 Azure VM에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="541c2-171">Hello 브라우저에서 웹 앱에 연결할 수 준비 toostart Twilio 앱 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="541c2-172"><a id="configure_app"></a>응용 프로그램 tooUse Twilio 구성</span><span class="sxs-lookup"><span data-stu-id="541c2-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="541c2-173">웹 앱 toouse hello Twilio 라이브러리를 업데이트 하 여 구성할 수 있습니다 프로그램 `Gemfile` tooinclude이이 줄:</span><span class="sxs-lookup"><span data-stu-id="541c2-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="541c2-174">Hello 명령줄에서 실행 `bundle install`합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="541c2-175">이제 열 `web.rb` hello 위쪽에이 줄을 포함 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="541c2-176">모든 설정 toouse hello Twilio 도우미 라이브러리 Ruby 용 웹 응용 프로그램에 이제 것입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="541c2-177"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="541c2-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="541c2-178">다음 hello 나가는 toomake 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="541c2-179">주요 개념 hello Twilio 도우미 라이브러리를 사용 하 여 Ruby toomake REST API 호출에 대 한 및 TwiML 렌더링 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="541c2-180">Hello에 대 한 값을 대체 **에서** 및 **를** 전화 번호를 하 고 hello를 확인 하는 확인 **에서** Twilio 계정 이전 toorunning hello 코드의 전화 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="541c2-181">이 함수를 너무 추가`web.md`:</span><span class="sxs-lookup"><span data-stu-id="541c2-181">Add this function too`web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="541c2-182">경우 하면 오픈 접속 `http://yourdomain.cloudapp.net/make_call` 브라우저에서 hello 호출 toohello Twilio API toomake hello 전화 통화 트리거할입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="541c2-183">처음 두 매개 변수를 hello `client.account.calls.create` 은 비교적 쉽게 이해할 수: hello 숫자 hello 호출이 `from` hello 숫자 hello 호출 이며 `to`합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="541c2-184">세 번째 매개 변수를 hello (`url`) Twilio hello 호출 연결 된 후에 어떤 toodo tooget 지침을 요청 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="541c2-185">이 예에서는 URL 설정 (`http://yourdomain.cloudapp.net`) 하는 간단한 TwiML 문서를 반환 하 고 hello를 사용 하 여 `<Say>` 동사 toodo 일부 텍스트 음성 변환, 예: "Hello 원숭이" toohello person 받는 hello를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="541c2-186"><a id="howto_recieve_sms"></a>방법: SMS 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="541c2-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="541c2-187">Hello 이전 예에서는 시작 프로그램 **나가는** 전화 통화입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="541c2-188">이 시간, Twilio 제공 하는 동안 등록 tooprocess 했습니다 hello 전화 번호를 사용해 보겠습니다는 **들어오는** SMS 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="541c2-189">첫째, 로그인 tooyour [Twilio 대시보드][twilio_account]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="541c2-190">"번호" hello 최상위 탐색에서 클릭 하 고 클릭 hello에 Twilio 번호 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="541c2-191">구성할 수 있는 URL 두 개가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="541c2-192">하나는 음성 요청 URL이고 다른 하나는 SMS 요청 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="541c2-193">이 Twilio 전화 통화 될 때마다은 호출 하는 hello Url 또는 SMS tooyour 번호 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="541c2-194">hello Url "웹 후크" 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="541c2-195">들어오는 SMS 메시지 tooprocess 보겠습니다 hello URL을 너무 업데이트 같은`http://yourdomain.cloudapp.net/sms_url`합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="541c2-196">Hello hello 페이지 맨 아래에 작업을 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="541c2-197">이제 다시 `web.rb` 이 응용 프로그램 toohandle를 프로그램 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="541c2-198">Hello 변경한 후 웹 앱 toore 시작 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="541c2-199">이제 휴대폰 꺼내서를 보낼 SMS tooyour Twilio 번호.</span><span class="sxs-lookup"><span data-stu-id="541c2-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="541c2-200">"Hey, hello ping 주셔서 감사 합니다 라는 SMS 응답을 신속 하 게 얻어야!</span><span class="sxs-lookup"><span data-stu-id="541c2-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="541c2-201">Twilio and Azure rock!"이라는 SMS 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="541c2-202"><a id="additional_services"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="541c2-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="541c2-203">또한 toohello 예제 Twilio 제공 웹 기반 Api를 여기에 표시 된 Azure 응용 프로그램에서 추가 Twilio 기능 tooleverage를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="541c2-204">전체 세부 정보에 대 한 참조 hello [Twilio API 설명서][twilio_api_documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="541c2-205"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="541c2-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="541c2-206">Hello Twilio 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="541c2-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="541c2-207">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="541c2-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="541c2-208">[Twilio 사용 방법 및 예제 코드][twilio_howtos](영문)</span><span class="sxs-lookup"><span data-stu-id="541c2-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="541c2-209">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="541c2-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="541c2-210">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="541c2-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="541c2-211">[Talk tooTwilio 지원][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="541c2-211">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
