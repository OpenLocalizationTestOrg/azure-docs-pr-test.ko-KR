---
title: "음성 및 SMS에 Twilio를 사용하는 방법(Python) | Microsoft 문서"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 코드 샘플은 Python으로 작성되었습니다."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="4b3d9-104">Python에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4b3d9-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="4b3d9-105">이 가이드에서는 Azure에서 Twilio API 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="4b3d9-106">이 문서의 시나리오에서는 전화 통화를 걸고 SMS(Short Message Service) 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="4b3d9-107">응용 프로그램에서 음성 및 SMS 사용 방법과 Twilio에 대한 자세한 내용은 [다음 단계](#NextSteps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="4b3d9-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="4b3d9-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="4b3d9-109">Twilio는 개발자가 응용 프로그램에 음성, VoIP 및 메시징을 포함할 수 있도록 하면서 비즈니스 통신의 미래를 이끌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="4b3d9-110">개발자는 클라우드 기반 글로벌 환경에 필요한 모든 인프라를 가상화하고, Twilio 통신 API 플랫폼을 통해 이를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="4b3d9-111">덕분에 응용 프로그램을 간단히 빌드하고 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="4b3d9-112">종량제 가격의 유연성과 클라우드 안정성의 이점을 누리십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="4b3d9-113">**Twilio 음성** 을 통해 응용 프로그램에서 전화를 걸고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="4b3d9-114">**Twilio SMS** 를 사용하면 응용 프로그램에서 문자 메시지를 보내고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="4b3d9-115">**Twilio 클라이언트** 를 통해서는 전화, 태블릿 또는 브라우저에서 VoIP 통화를 하고 WebRTC를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="4b3d9-116"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="4b3d9-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="4b3d9-117">Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공][special_offer] 10달러의 Twilio 크레딧을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="4b3d9-118">이 Twilio 크레딧은 모든 Twilio 사용량에 적용될 수 있습니다. 10달러의 크레딧은 전화 번호 및 메시지 또는 통화 대상의 위치에 따라 SMS 메시지를 1,000개 보내거나 최대 1000분간 인바운드 음성을 받을 수 있는 금액입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="4b3d9-119">이 [Twilio 크레딧][special_offer]을 충전하고 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="4b3d9-120">Twilio는 종량제 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="4b3d9-121">설정 수수료는 없으며 언제든 계정을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="4b3d9-122">[Twilio 가격 책정][twilio_pricing]에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="4b3d9-123"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="4b3d9-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="4b3d9-124">Twilio API는 응용 프로그램에 대한 음성 및 SMS 기능을 제공하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="4b3d9-125">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="4b3d9-126">Twilio API의 핵심 요소는 Twilio 동사와 TwiML(Twilio Markup Language)입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="4b3d9-127"><a id="Verbs"></a>Twilio 동사</span><span class="sxs-lookup"><span data-stu-id="4b3d9-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="4b3d9-128">API는 Twilio 동사를 활용합니다. 예를 들어 **&lt;Say&gt;** 동사는 Twilio에 통화 메시지를 음성으로 전달하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="4b3d9-129">다음은 Twilio 동사의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="4b3d9-130">기타 동사 및 기능에 대해서는 [Twilio Markup Language 설명서][twiml]에서 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="4b3d9-131">**&lt;Dial&gt;**: 발신자를 다른 전화에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="4b3d9-132">**&lt;Gather&gt;**: 전화 키패드에 입력된 숫자를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="4b3d9-133">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="4b3d9-134">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="4b3d9-135">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="4b3d9-136">**&lt;Queue&gt;**: 호출자 큐에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="4b3d9-137">**&lt;Record&gt;**: 발신자의 음성을 녹음하고 녹음이 포함된 파일의 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="4b3d9-138">**&lt;Redirect&gt;**: 통화 또는 SMS에 대한 제어를 다른 URL의 TwiML로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="4b3d9-139">**&lt;Reject&gt;**: 요금을 청구하지 않고 Twilio 번호의 수신 전화를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="4b3d9-140">**&lt;Say&gt;**: 텍스트를 통화에 사용되는 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="4b3d9-141">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="4b3d9-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="4b3d9-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="4b3d9-143">TwiML은 Twilio에 통화 또는 SMS 처리 방법을 알려 주는 Twilio 동사를 사용하는 XML 기반 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="4b3d9-144">다음 예제 TwiML은 **Hello World** 텍스트를 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="4b3d9-145">응용 프로그램에서 Twilio API를 호출할 때 API 매개 변수 중 하나는 TwiML 응답을 반환하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="4b3d9-146">개발을 위해서 Twilio 제공 URL을 사용하여 응용 프로그램에 사용되는 TwiML 응답을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="4b3d9-147">또한 TwiML 응답을 생성하는 고유한 URL을 호스트할 수도 있고, `TwiMLResponse` 개체를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="4b3d9-148">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="4b3d9-149">Twilio API에 대한 자세한 내용은 [Twilio API][twilio_api](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="4b3d9-150"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4b3d9-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="4b3d9-151">Twilio 계정을 사용할 준비가 되었다면 [Twilio 체험][try_twilio]에서 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="4b3d9-152">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="4b3d9-153">Twilio 계정을 등록하면 계정 SID 및 인증 토큰을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="4b3d9-154">둘 다 Twilio API 통화를 하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="4b3d9-155">계정에 대한 무단 액세스를 방지하려면 인증 토큰을 안전하게 유지하십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="4b3d9-156">계정 SID 및 인증 토큰은 [Twilio 콘솔][twilio_console]의 **ACCOUNT SID** 및 **AUTH TOKEN** 필드에서 각각 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="4b3d9-157"><a id="create_app"></a>Python 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4b3d9-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="4b3d9-158">Twilio 서비스를 사용하고 Azure에서 실행되고 있는 Python 응용 프로그램은 Twilio 서비스를 사용하는 다른 Python 응용 프로그램과 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="4b3d9-159">Twilio 서비스가 REST 기반이고 여러 가지 방법으로 Python에서 호출될 수 있기는 하지만, 이 문서에서는 [GitHub의 Python용 Twilio 라이브러리][twilio_python]와 Twilio 서비스를 사용하는 방법을 집중적으로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="4b3d9-160">Python용 Twilio 라이브러리 사용에 대한 자세한 내용은 [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="4b3d9-161">먼저, 새 Python 웹 응용 프로그램의 호스트 역할을 할 [새 Azure Linux VM을 설정][azure_vm_setup]합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="4b3d9-162">가상 컴퓨터가 실행되면 아래 설명된 대로 공개 포트에 응용 프로그램을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="4b3d9-163">수신 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="4b3d9-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="4b3d9-164">[네트워크 보안 그룹][azure_nsg] 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="4b3d9-165">가상 컴퓨터와 일치하는 네트워크 보안 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="4b3d9-166">**포트 80**에 대한 **발신 규칙**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="4b3d9-167">모든 주소에서의 수신을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="4b3d9-168">DNS 이름 레이블 설정</span><span class="sxs-lookup"><span data-stu-id="4b3d9-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="4b3d9-169">[공용 IP 주소][azure_ips] 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="4b3d9-170">가상 컴퓨터와 일치하는 공용 IP를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="4b3d9-171">**구성** 섹션에서 **DNS 이름 레이블**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="4b3d9-172">이 예제의 경우 *your-domain-label*.centralus.cloudapp.azure.com 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="4b3d9-173">SSH를 통해 가상 컴퓨터에 연결할 수 있으면 선택한 웹 프레임워크를 설치할 수 있습니다(Python에서 가장 잘 알려진 두 개의 웹 프레임워크는 [Flask](http://flask.pocoo.org/) 및 [Django](https://www.djangoproject.com)임).</span><span class="sxs-lookup"><span data-stu-id="4b3d9-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="4b3d9-174">`pip install` 명령을 실행하여 둘 중 하나를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="4b3d9-175">포트 80에서만 트래픽을 허용하도록 가상 컴퓨터를 구성했다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="4b3d9-176">따라서 이 포트를 사용하도록 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-176">So make sure to configure the application to use this port.</span></span>

## <span data-ttu-id="4b3d9-177"><a id="configure_app"></a>Twilio 라이브러리를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="4b3d9-177"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="4b3d9-178">다음과 같은 두 가지 방법으로 Python용 Twilio 라이브러리를 사용하도록 응용 프로그램을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="4b3d9-179">Python용 Twilio 라이브러리를 Pip 패키지로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="4b3d9-180">다음 명령을 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="4b3d9-181">또는</span><span class="sxs-lookup"><span data-stu-id="4b3d9-181">-OR-</span></span>

* <span data-ttu-id="4b3d9-182">GitHub([https://github.com/twilio/twilio-python][twilio_python])에서 Python용 Twilio 라이브러리를 다운로드하고 다음과 같이 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="4b3d9-183">Python용 Twilio 라이브러리를 설치한 후 Python 파일로 라이브러리를 `import`할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="4b3d9-184">자세한 내용은 [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="4b3d9-185"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="4b3d9-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="4b3d9-186">다음은 발신 전화를 거는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="4b3d9-187">또한 이 코드는 Twilio 제공 사이트를 사용하여 TwiML(Twilio Markup Language) 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="4b3d9-188">**from_number** 및 **to_number** 전화 번호의 값을 바꾸고 코드를 실행하기 전에 Twilio 계정에 대한 **from_number** 전화 번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="4b3d9-189">언급한 대로 이 코드는 Twilio 제공 사이트를 사용하여 TwiML 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="4b3d9-190">고유한 사이트를 대신 사용하여 TwiML 응답을 제공할 수 있습니다. 자세한 내용은 [고유한 웹 사이트에서 TwiML 응답을 제공하는 방법](#howto_provide_twiml_responses)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="4b3d9-191"><a id="howto_send_sms"></a>방법: SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="4b3d9-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="4b3d9-192">다음은 `TwilioRestClient` 클래스를 사용하여 SMS 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="4b3d9-193">평가판 계정이 SMS 메시지를 보낼 **from_number** 번호는 Twilio에서 자동으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="4b3d9-194">코드를 실행하기 전에 Twilio 계정에 대한 **to_number** 번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="4b3d9-195"><a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공</span><span class="sxs-lookup"><span data-stu-id="4b3d9-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="4b3d9-196">응용 프로그램에서 Twilio API 호출을 시작하면 Twilio에서 TwiML 응답을 반환해야 하는 URL로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="4b3d9-197">위 예제에서는 Twilio 제공 URL인 [http://twimlets.com/message][twimlet_message_url]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="4b3d9-198">TwiML은 Twilio에서 사용되도록 설계되었지만 브라우저에서도 TwiML을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="4b3d9-199">예를 들어 [http://twimlets.com/message][twimlet_message_url]를 클릭하면 빈 `<Response>` 요소가 표시됩니다. 또 다른 예로, [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world]를 클릭하면 `<Say>` 요소를 포함하는 `<Response>` 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="4b3d9-200">Twilio 제공 URL을 사용하지 않고 HTTP 응답을 반환하는 고유한 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="4b3d9-201">XML 응답을 반환하는 모든 언어로 사이트를 만들 수 있습니다. 이 항목에서는 TwiML을 만들기 위해 Python를 사용 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="4b3d9-202">다음 예제에서는 호출 시 **Hello World**라고 말하는 TwiML 응답이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="4b3d9-203">Flask 사용:</span><span class="sxs-lookup"><span data-stu-id="4b3d9-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="4b3d9-204">Django 사용:</span><span class="sxs-lookup"><span data-stu-id="4b3d9-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="4b3d9-205">위의 예제와 같이 TwiML 응답은 단지 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="4b3d9-206">Python용 Twilio 라이브러리에는 TwiML을 자동으로 생성하는 클래스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="4b3d9-207">아래 예제에서는 위에 표시된 것과 동일한 응답을 생성하지만 Python용 Twilio 라이브러리의 `twiml` 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="4b3d9-208">TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml][twiml_reference]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="4b3d9-209">Python 응용 프로그램이 TwiML 응답을 제공하도록 설정된 경우 `client.calls.create` 메서드에 전달되는 URL로 Python 응용 프로그램의 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="4b3d9-210">예를 들어 **MyTwiML**이라는 웹 응용 프로그램이 Azure 호스티드 서비스에 배포되어 있으면 다음 예제에 표시된 것처럼 URL을 웹후크로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="4b3d9-211"><a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="4b3d9-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="4b3d9-212">여기에서 보여 준 예뿐만 아니라 Twilio는 Azure 응용 프로그램에서 Twilio 기능을 활용할 수 있는 웹 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="4b3d9-213">자세한 내용은 [Twilio API 설명서][twilio_api]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="4b3d9-214"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b3d9-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="4b3d9-215">Twilio 서비스의 기본 사항을 배웠으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="4b3d9-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="4b3d9-216">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="4b3d9-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="4b3d9-217">[Twilio 사용 방법 가이드 및 예제 코드][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="4b3d9-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="4b3d9-218">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="4b3d9-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="4b3d9-219">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="4b3d9-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="4b3d9-220">[Twilio 지원 문의][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="4b3d9-220">[Talk to Twilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
