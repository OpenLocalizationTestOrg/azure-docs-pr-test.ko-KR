---
title: "음성 및 SMS에 Twilio를 사용하는 방법(Ruby) | Microsoft Docs"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 코드 샘플은 Ruby로 작성되었습니다."
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="9dced-104">Ruby에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9dced-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="9dced-105">이 가이드에서는 Azure에서 Twilio API 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="9dced-106">이 문서의 시나리오에서는 전화 통화를 걸고 SMS(Short Message Service) 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="9dced-107">응용 프로그램에서 음성 및 SMS 사용 방법과 Twilio에 대한 자세한 내용은 [다음 단계](#NextSteps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="9dced-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="9dced-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="9dced-109">Twilio는 기존 웹 언어와 기술을 사용하여 음성 및 SMS 응용 프로그램을 빌드할 수 있게 해주는 전화 통신 웹 서비스 API입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="9dced-110">Twilio는 타사 서비스입니다(Azure 기능 또는 Microsoft 제품 아님).</span><span class="sxs-lookup"><span data-stu-id="9dced-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="9dced-111">**Twilio 음성** 을 통해 응용 프로그램에서 전화를 걸고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="9dced-112">**Twilio SMS** 를 사용하면 응용 프로그램에서 SMS 메시지를 작성하고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="9dced-113">**Twilio 클라이언트** 를 사용하면 응용 프로그램에서 모바일 연결을 비롯한 기존 인터넷 연결을 통해 음성 통신을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="9dced-114"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="9dced-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="9dced-115">Twilio 가격 책정 정보는 [Twilio 가격 책정][twilio_pricing]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="9dced-116">Azure 고객은 [특별 제공][special_offer](문자 1000통 또는 인바운드 통화 1000분의 무료 크레딧)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="9dced-117">이 제공에 등록하거나 추가 정보를 얻으려면 [http://ahoy.twilio.com/azure][special_offer]를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="9dced-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="9dced-118"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="9dced-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="9dced-119">Twilio API는 응용 프로그램에 대한 음성 및 SMS 기능을 제공하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="9dced-120">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="9dced-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="9dced-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="9dced-122">TwiML은 Twilio에 통화 또는 SMS 처리 방법을 알려 주는 XML 기반 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="9dced-123">다음 예제 TwiML은 **Hello World** 텍스트를 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="9dced-124">모든 TwiML 문서는 `<Response>` 를 루트 요소로 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="9dced-125">거기서 Twilio 동사를 사용하여 응용 프로그램의 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="9dced-126"><a id="Verbs"></a>TwiML 동사</span><span class="sxs-lookup"><span data-stu-id="9dced-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="9dced-127">Twilio 동사는 Twilio에 **수행할 작업**을 알려 주는 XML 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="9dced-128">예를 들어 **&lt;Say&gt;** 동사는 Twilio에 통화 메시지를 음성으로 전달하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="9dced-129">다음은 Twilio 동사의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="9dced-130">**&lt;Dial&gt;**: 발신자를 다른 전화에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="9dced-131">**&lt;Gather&gt;**: 전화 키패드에 입력된 숫자를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="9dced-132">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="9dced-133">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="9dced-134">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="9dced-135">**&lt;Record&gt;**: 발신자의 음성을 녹음하고 녹음이 포함된 파일의 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="9dced-136">**&lt;Redirect&gt;**: 통화 또는 SMS에 대한 제어를 다른 URL의 TwiML로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="9dced-137">**&lt;Reject&gt;**: 요금을 청구하지 않고 Twilio 번호의 수신 전화를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="9dced-138">**&lt;Say&gt;**: 텍스트를 통화에 사용되는 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="9dced-139">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="9dced-140">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="9dced-141">Twilio API에 대한 자세한 내용은 [Twilio API][twilio_api](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="9dced-142"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9dced-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="9dced-143">Twilio 계정을 사용할 준비가 되었다면 [Twilio 체험][try_twilio](영문)에서 등록하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="9dced-144">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="9dced-145">Twilio 계정을 등록할 때 응용 프로그램의 무료 전화 번호를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="9dced-146">계정 SID 및 인증 토큰도 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="9dced-147">둘 다 Twilio API 통화를 하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="9dced-148">계정에 대한 무단 액세스를 방지하려면 인증 토큰을 안전하게 유지하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="9dced-149">계정 SID 및 인증 토큰은 [Twilio 계정 페이지][twilio_account](영문)의 **ACCOUNT SID** 및 **AUTH TOKEN**에서 각각 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="9dced-150"><a id="VerifyPhoneNumbers"></a>전화 번호 확인</span><span class="sxs-lookup"><span data-stu-id="9dced-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="9dced-151">Twilio에서 제공한 번호 외에 응용 프로그램에서 사용하기 위해 제어하는 번호(즉, 휴대폰 또는 집 전화 번호)도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="9dced-152">전화 번호를 확인하는 방법에 대한 내용은 [번호 관리][verify_phone](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9dced-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="9dced-153"><a id="create_app"></a>Ruby 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9dced-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="9dced-154">Twilio 서비스를 사용하고 Azure에서 실행되고 있는 Ruby 응용 프로그램은 Twilio 서비스를 사용하는 다른 Ruby 응용 프로그램과 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="9dced-155">Twilio 서비스는 RESTful이며 여러 가지 방법으로 Ruby에서 호출할 수 있지만, 이 문서에서는 [Ruby용 Twilio 도우미 라이브러리][twilio_ruby](영문)를 통해 Twilio 서비스를 사용하는 방법을 집중적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="9dced-156">먼저 새 Ruby 웹 응용 프로그램의 호스트 역할을 할 [새 Azure Linux VM을 설정][azure_vm_setup]합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="9dced-157">Rails 앱을 만드는 것과 관련된 단계는 무시하고 VM 설정만 수행하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="9dced-158">외부 포트 80과 내부 포트 5000으로 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="9dced-159">아래 예제에서는 매우 간단한 Ruby용 웹 프레임워크인 [Sinatra][sinatra]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="9dced-160">그러나 Ruby on Rails를 비롯한 다른 웹 프레임워크와 함께 Ruby용 Twilio 도우미 라이브러리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="9dced-161">새 VM에 SSH를 설치하고 새 앱용 디렉터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="9dced-162">해당 디렉터리 내에 Gemfile이라는 파일을 만들고 다음 코드를 이 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="9dced-163">명령줄에서 `bundle install`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="9dced-164">그러면 위의 종속성이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-164">This will install the dependencies above.</span></span> <span data-ttu-id="9dced-165">이제 `web.rb`라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="9dced-166">이 파일은 웹앱 코드가 있는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="9dced-167">다음 코드를 이 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="9dced-168">이때 명령 `ruby web.rb -p 5000`을 실행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="9dced-169">그러면 포트 5000에서 작은 웹 서버가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="9dced-170">브라우저에서 Azure VM에 대해 설정한 URL을 방문하여 이 앱으로 이동할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="9dced-171">브라우저에서 웹앱에 연결할 수 있으면 Twilio 앱 빌드를 시작할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="9dced-172"><a id="configure_app"></a>Twilio를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="9dced-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="9dced-173">다음 줄을 포함하도록 `Gemfile` 을 업데이트하여 Twilio 라이브러리를 사용하도록 웹 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="9dced-174">명령줄에서 `bundle install`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="9dced-175">이제 `web.rb` 를 열고 맨 위에 다음 줄을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="9dced-176">이제 웹앱에서 Ruby용 Twilio 도우미 라이브러리를 사용할 준비가 모두 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="9dced-177"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="9dced-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="9dced-178">다음은 발신 전화를 거는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="9dced-179">핵심 개념에는 Ruby용 Twilio 도우미 라이브러리를 사용하여 REST API 호출을 만드는 작업과 TwiML 렌더링 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="9dced-180">**From** 및 **To** 전화 번호의 값을 바꾸고, 코드를 실행하기 전에 Twilio 계정의 **From** 번호를 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="9dced-181">다음 함수를 `web.md`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="9dced-182">브라우저에서 `http://yourdomain.cloudapp.net/make_call`을 열면 Twilio API에 대한 호출이 트리거되어 전화가 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="9dced-183">`client.account.calls.create`에서 처음 두 개의 매개 변수는 별도의 설명이 없어도 바로 이해할 수 있습니다. 전화를 거는 번호는 `from`이고 전화를 받는 번호는 `to`입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="9dced-184">세 번째 매개 변수(`url`)는 전화가 연결된 후 수행할 작업에 대한 지침을 받기 위해 Twilio가 요청하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="9dced-185">이 경우 간단한 TwiML 문서를 반환하고 `<Say>` 동사를 사용하여 텍스트를 음성으로 변환하고 전화를 받는 사람에게 "Hello Monkey"라고 말하는 URL(`http://yourdomain.cloudapp.net`)을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="9dced-186"><a id="howto_recieve_sms"></a>방법: SMS 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="9dced-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="9dced-187">앞의 예제에서는 **발신** 전화 통화를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="9dced-188">이번에는 등록하는 동안 Twilio가 제공한 전화 번호를 사용하여 **수신** SMS 메시지를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="9dced-189">먼저 [Twilio 대시보드][twilio_account](영문)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="9dced-190">위쪽 탐색 표시줄에서 "Numbers(번호)"를 클릭한 후 제공받은 Twilio 번호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="9dced-191">구성할 수 있는 URL 두 개가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="9dced-192">하나는 음성 요청 URL이고 다른 하나는 SMS 요청 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="9dced-193">이러한 URL은 전화 통화가 걸리거나 SMS가 사용자의 번호로 전송될 때마다 Twilio가 호출하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="9dced-194">이러한 URL을 "웹 후크"라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="9dced-195">수신 SMS 메시지를 처리할 것이므로, URL을 `http://yourdomain.cloudapp.net/sms_url`로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="9dced-196">계속해서 페이지 아래쪽에 있는 Save Changes(변경 내용 저장)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="9dced-197">이제 다시 `web.rb` 에서 이를 처리하기 위한 응용 프로그램을 프로그래밍합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="9dced-198">변경한 후 웹앱을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="9dced-199">이제 휴대폰을 사용하여 SMS를 Twilio 번호로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="9dced-200">즉시 "Hey, thanks for the ping!</span><span class="sxs-lookup"><span data-stu-id="9dced-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="9dced-201">Twilio and Azure rock!"이라는 SMS 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="9dced-202"><a id="additional_services"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="9dced-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="9dced-203">여기에서 보여 준 예뿐만 아니라 Twilio는 Azure 응용 프로그램에서 Twilio 기능을 활용할 수 있는 웹 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9dced-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="9dced-204">자세한 내용은 [Twilio API 설명서][twilio_api_documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9dced-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="9dced-205"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="9dced-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="9dced-206">Twilio 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="9dced-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="9dced-207">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="9dced-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="9dced-208">[Twilio 사용 방법 및 예제 코드][twilio_howtos](영문)</span><span class="sxs-lookup"><span data-stu-id="9dced-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="9dced-209">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="9dced-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="9dced-210">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="9dced-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="9dced-211">[Twilio 지원 문의][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="9dced-211">[Talk to Twilio Support][twilio_support]</span></span>

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
