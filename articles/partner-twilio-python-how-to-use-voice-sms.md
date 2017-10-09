---
title: "aaaHow tooUse 음성 및 SMS (Python)는 Twilio | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 Python으로 작성되었습니다."
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
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="8b02b-104">어떻게 tooUse Twilio 음성 및 SMS 기능 Python</span><span class="sxs-lookup"><span data-stu-id="8b02b-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="8b02b-105">이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="8b02b-106">포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="8b02b-107">Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.</span><span class="sxs-lookup"><span data-stu-id="8b02b-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="8b02b-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="8b02b-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="8b02b-109">Twilio는 비즈니스 통신의 hello 미래 전원을 켜는 중, 개발자 tooembed 음성 VoIP, 활성화 및 메시징을 응용 프로그램에 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="8b02b-110">Hello Twilio 통신 API 플랫폼을 통해 노출 하는 클라우드 기반, 글로벌 환경에서 필요한 모든 인프라를 가상화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="8b02b-111">응용 프로그램은 단순 toobuild 하 고 확장 가능한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="8b02b-112">종량제 가격의 유연성과 클라우드 안정성의 이점을 누리십시오.</span><span class="sxs-lookup"><span data-stu-id="8b02b-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="8b02b-113">**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="8b02b-114">**Twilio SMS** 응용 프로그램 toosend 있으며 특정 문자 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="8b02b-115">**Twilio 클라이언트** WebRTC 지원 및 전화, 태블릿 또는 브라우저에서 toomake VoIP 전화 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="8b02b-116"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="8b02b-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="8b02b-117">Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공][special_offer] 10달러의 Twilio 크레딧을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="8b02b-118">Twilio 신용이 적용 된 tooany Twilio 사용량 ($10 신용 해당 toosending 최대 1, 000 SMS 메시지 또는 받기가 too1000 인바운드 hello 전화 번호와 메시지 또는 호출 대상 위치에 따라 음성 분) 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="8b02b-119">이 [Twilio 크레딧][special_offer]을 충전하고 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="8b02b-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="8b02b-120">Twilio는 종량제 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="8b02b-121">설정 수수료는 없으며 언제든 계정을 종료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="8b02b-122">[Twilio 가격 책정][twilio_pricing]에서 자세한 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="8b02b-123"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="8b02b-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="8b02b-124">hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="8b02b-125">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b02b-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="8b02b-126">Hello Twilio API의 주요 측면은 Twilio 동사 및 Twilio Markup Language (TwiML)입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="8b02b-127"><a id="Verbs"></a>Twilio 동사</span><span class="sxs-lookup"><span data-stu-id="8b02b-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="8b02b-128">hello API에서 Twilio 활용 동사; 예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="8b02b-129">hello 다음은 Twilio 동사 목록을입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="8b02b-130">자세한 내용은 다른 동사와 기능을 통해 약 hello [Twilio Markup Language 설명서][twiml]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="8b02b-131">**&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="8b02b-132">**&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="8b02b-133">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="8b02b-134">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="8b02b-135">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="8b02b-136">**&lt;큐&gt;**: 호출자의 hello tooa 큐를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="8b02b-137">**&lt;레코드&gt;**: hello 호출자의 hello 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="8b02b-138">**&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="8b02b-139">**&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="8b02b-140">**&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="8b02b-141">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="8b02b-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="8b02b-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="8b02b-143">TwiML 방법의 Twilio를 알려주는 hello Twilio 동사에 따라 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="8b02b-144">예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World** toospeech 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="8b02b-145">응용 프로그램이 호출 hello Twilio API, hello API 매개 변수 중 하나 hello TwiML 응답을 반환 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="8b02b-146">개발을 위해 응용 프로그램에서 사용 하는 Twilio 제공 Url tooprovide hello TwiML 응답을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="8b02b-147">직접 Url tooproduce hello TwiML 응답을 호스트할 수 있습니다 및 두 번째 방법은 toouse hello `TwiMLResponse` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="8b02b-148">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8b02b-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="8b02b-149">Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="8b02b-150"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="8b02b-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="8b02b-151">준비 tooget Twilio 계정 러 우면에서 등록 [시도 Twilio][try_twilio]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="8b02b-152">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="8b02b-153">Twilio 계정을 등록하면 계정 SID 및 인증 토큰을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="8b02b-154">둘 다 필요한 toomake Twilio API 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="8b02b-155">권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="8b02b-156">사용자 계정 SID 및 인증 토큰은 hello에 볼 수 있는 [Twilio 콘솔][twilio_console]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰**각각.</span><span class="sxs-lookup"><span data-stu-id="8b02b-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="8b02b-157"><a id="create_app"></a>Python 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8b02b-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="8b02b-158">Azure에서 실행 되 고 hello Twilio 서비스를 사용 하는 Python 응용 프로그램은 다른 모든 Python 응용 프로그램 hello Twilio 서비스를 사용 하는 방법과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="8b02b-159">이 문서는 toouse Twilio를 사용 하 여 서비스 방법을 중점 Twilio 서비스는 REST 기반 하 고 여러 가지 방법으로 Python에서 호출할 수 있습니다, [GitHub에서 Python 용 Twilio 라이브러리][twilio_python]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="8b02b-160">Python 용 hello Twilio 라이브러리를 사용 하는 방법에 대 한 자세한 내용은 참조 [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="8b02b-161">먼저 [새 Azure Linux VM을 설정 하는 경우] [azure_vm_setup] tooact 새 Python 웹 응용 프로그램에 대 한 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="8b02b-162">Hello 가상 컴퓨터가 실행 되 면, 해야 tooexpose 공용 포트에 있는 응용 프로그램 아래에 설명 된 대로.</span><span class="sxs-lookup"><span data-stu-id="8b02b-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="8b02b-163">수신 규칙 추가</span><span class="sxs-lookup"><span data-stu-id="8b02b-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="8b02b-164">[네트워크 보안 그룹] [azure_nsg] toohello 이동 페이지.</span><span class="sxs-lookup"><span data-stu-id="8b02b-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="8b02b-165">Hello 가상 컴퓨터와 해당 하는 네트워크 보안 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="8b02b-166">**포트 80**에 대한 **발신 규칙**을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="8b02b-167">모든 주소 로부터 들어오는 있는지 tooallow 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="8b02b-168">DNS 이름 레이블을 hello 설정</span><span class="sxs-lookup"><span data-stu-id="8b02b-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="8b02b-169">[Hello 공용 IP 주소] toohello 이동 [azure_ips] 페이지.</span><span class="sxs-lookup"><span data-stu-id="8b02b-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="8b02b-170">가상 컴퓨터와 공용 IP는 correspends hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="8b02b-171">집합 hello **DNS 이름 레이블을** hello에 **구성** 섹션.</span><span class="sxs-lookup"><span data-stu-id="8b02b-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="8b02b-172">이 예의 경우 hello 보일지 다음과 같이 *도메인 레이블 your*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="8b02b-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="8b02b-173">Tooconnect SSH toohello 설치할 수는 가상 컴퓨터를 통해 사용자가 선택한 웹 프레임 워크 hello 수 되 면 (두 개의 Python 되에 가장 잘 알려진 hello [플라스](http://flask.pocoo.org/) 및 [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="8b02b-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="8b02b-174">Hello를 실행 하 여 둘 중 하나를 설치할 수 있습니다 `pip install` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="8b02b-175">포트 80에 대해서만 구성 된 म hello 가상 컴퓨터 tooallow 트래픽 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="8b02b-176">따라서 있는지 tooconfigure hello 응용 프로그램 toouse이이 포트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="8b02b-177"><a id="configure_app"></a>응용 프로그램 tooUse Twilio 라이브러리 구성</span><span class="sxs-lookup"><span data-stu-id="8b02b-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="8b02b-178">Python에 대 한 두 가지 방법으로 응용 프로그램 toouse hello Twilio 라이브러리를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="8b02b-179">Python에 대 한 Pip 패키지로 hello Twilio 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="8b02b-180">다음 명령은 hello로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="8b02b-181">또는</span><span class="sxs-lookup"><span data-stu-id="8b02b-181">-OR-</span></span>

* <span data-ttu-id="8b02b-182">GitHub에서 Python에 대 한 hello Twilio 라이브러리를 다운로드 ([https://github.com/twilio/twilio-python][twilio_python]) 하 고 다음과 같은 설치:</span><span class="sxs-lookup"><span data-stu-id="8b02b-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="8b02b-183">Python 용 hello Twilio 라이브러리를 설치 하면 그런 다음 `import` Python 파일에:</span><span class="sxs-lookup"><span data-stu-id="8b02b-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="8b02b-184">자세한 내용은 [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b02b-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="8b02b-185"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="8b02b-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="8b02b-186">다음 hello 나가는 toomake 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="8b02b-187">이 코드는 또한 Twilio 제공 사이트 tooreturn hello Twilio Markup Language (TwiML) 응답을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="8b02b-188">Hello에 대 한 값을 대체 **from_number** 및 **to_number** 전화 번호를 하 고 hello를 확인 했으면 확인 **from_number** 전화 번호 Twilio 계정에 대 한 전에 hello 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="8b02b-189">앞서 언급 했 듯이이 코드는 Twilio 제공 사이트 tooreturn hello TwiML 응답을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="8b02b-190">사용자 고유의 사이트 tooprovide hello TwiML 응답; 대신 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 tooProvide TwiML 응답에서 직접 웹 사이트](#howto_provide_twiml_responses)합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="8b02b-191"><a id="howto_send_sms"></a>방법: SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="8b02b-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="8b02b-192">hello 다음 테이블에 나와 방법을 사용 하 여 SMS 메시지 toosend hello `TwilioRestClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="8b02b-193">hello **from_number** 번호는 평가판 계정 toosend SMS 메시지에 대해 Twilio에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="8b02b-194">hello **to_number** 번호 Twilio 계정에 대 한 hello 코드를 실행 하기 전에 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="8b02b-195"><a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공</span><span class="sxs-lookup"><span data-stu-id="8b02b-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="8b02b-196">응용 프로그램 호출 toohello Twilio API를 시작, Twilio 요청 tooa URL을 예상 tooreturn TwiML 응답 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="8b02b-197">hello Twilio 제공 URL을 사용 하 여 위의 hello 예제 [http://twimlets.com/message][twimlet_message_url]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="8b02b-198">TwiML은 Twilio에서 사용되도록 설계되었지만 브라우저에서도 TwiML을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="8b02b-199">예를 들어 클릭 [http://twimlets.com/message] [ twimlet_message_url] toosee 빈 `<Response>` 요소로 또 다른 예로, 클릭 [http://twimlets.com/message? 메시지 % 5B0 %5 D = Hello %20World] [ twimlet_message_url_hello_world] toosee는 `<Response>` 요소를 포함 하는 `<Say>` 요소입니다.)</span><span class="sxs-lookup"><span data-stu-id="8b02b-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="8b02b-200">Hello Twilio 제공 URL에 의존 하지 않고 HTTP 응답을 반환 하는 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="8b02b-201">XML 응답; 반환 되는 언어로 hello 사이트를 만들 수 있습니다. 이 항목에서는 Python toocreate hello TwiML 사용을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="8b02b-202">hello 다음 예제에서는 출력 이라는 TwiML 응답 **Hello World** hello 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="8b02b-203">Flask 사용:</span><span class="sxs-lookup"><span data-stu-id="8b02b-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="8b02b-204">Django 사용:</span><span class="sxs-lookup"><span data-stu-id="8b02b-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="8b02b-205">위의 hello 예제 알 수 있듯이 hello TwiML 응답은 XML 문서 하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="8b02b-206">Python 용 hello Twilio 라이브러리 TwiML를 생성 하는 클래스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="8b02b-207">hello 아래 예제에서는 위에 표시 된 대로 hello 해당 응답을 생성 하지만 hello를 사용 하 여 `twiml` Python에 대 한 hello Twilio 라이브러리에는 모듈:</span><span class="sxs-lookup"><span data-stu-id="8b02b-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="8b02b-208">TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml][twiml_reference]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b02b-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="8b02b-209">Tooprovide TwiML 응답을 설정 하 여 Python 응용 프로그램을 사용 하는 후 사용 hello 응용 프로그램의 hello URL hello에 전달 된 URL을 hello `client.calls.create` 메서드.</span><span class="sxs-lookup"><span data-stu-id="8b02b-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="8b02b-210">예를 들어, 명명 된 웹 응용 프로그램의 경우 **MyTwiML** 배포 tooan Azure 호스 티 드 서비스, hello 다음 예제와 같이 해당 url webhook으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="8b02b-211"><a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="8b02b-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="8b02b-212">또한 toohello 예제 Twilio 제공 웹 기반 Api를 여기에 표시 된 Azure 응용 프로그램에서 추가 Twilio 기능 tooleverage를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="8b02b-213">전체 세부 정보에 대 한 참조 hello [Twilio API 설명서][twilio_api]합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="8b02b-214"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b02b-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="8b02b-215">Hello Twilio 서비스의 hello 기본 사항을 파악 했으므로, 이제는 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b02b-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="8b02b-216">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="8b02b-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="8b02b-217">[Twilio 사용 방법 가이드 및 예제 코드][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="8b02b-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="8b02b-218">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="8b02b-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="8b02b-219">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="8b02b-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="8b02b-220">[Talk tooTwilio 지원][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="8b02b-220">[Talk tooTwilio Support][twilio_support]</span></span>

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
