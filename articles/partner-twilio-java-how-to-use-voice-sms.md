---
title: "음성 및 SMS에 Twilio를 사용하는 방법(Java) | Microsoft Docs"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="41347-104">Java에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="41347-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="41347-105">이 가이드에서는 Azure에서 Twilio API 서비스로 일반 프로그래밍 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41347-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="41347-106">이 문서의 시나리오에서는 전화 통화를 걸고 SMS(Short Message Service) 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41347-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="41347-107">응용 프로그램에서 음성 및 SMS 사용 방법과 Twilio에 대한 자세한 내용은 [다음 단계](#NextSteps) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="41347-108"><a id="WhatIs"></a>Twilio 정의</span><span class="sxs-lookup"><span data-stu-id="41347-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="41347-109">Twilio는 기존 웹 언어와 기술을 사용하여 음성 및 SMS 응용 프로그램을 빌드할 수 있게 해주는 전화 통신 웹 서비스 API입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="41347-110">Twilio는 타사 서비스입니다(Azure 기능 또는 Microsoft 제품 아님).</span><span class="sxs-lookup"><span data-stu-id="41347-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="41347-111">**Twilio 음성** 을 통해 응용 프로그램에서 전화를 걸고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="41347-112">**Twilio SMS** 를 사용하면 응용 프로그램에서 SMS 메시지를 작성하고 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="41347-113">**Twilio 클라이언트** 를 사용하면 응용 프로그램에서 모바일 연결을 비롯한 기존 인터넷 연결을 통해 음성 통신을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="41347-114"><a id="Pricing"></a>Twilio 가격 책정 및 특별 제공</span><span class="sxs-lookup"><span data-stu-id="41347-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="41347-115">Twilio 가격 책정 정보는 [Twilio 가격 책정][twilio_pricing]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="41347-116">Azure 고객은 [특별 제공][special_offer](문자 1000통 또는 인바운드 통화 1000분의 무료 크레딧)을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="41347-117">이 제공에 등록하거나 추가 정보를 얻으려면 [http://ahoy.twilio.com/azure][special_offer]를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="41347-118"><a id="Concepts"></a>개념</span><span class="sxs-lookup"><span data-stu-id="41347-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="41347-119">Twilio API는 응용 프로그램에 대한 음성 및 SMS 기능을 제공하는 RESTful API입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="41347-120">클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="41347-121">Twilio API의 핵심 요소는 Twilio 동사와 TwiML(Twilio Markup Language)입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="41347-122"><a id="Verbs"></a>Twilio 동사</span><span class="sxs-lookup"><span data-stu-id="41347-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="41347-123">API는 Twilio 동사를 활용합니다. 예를 들어 **&lt;Say&gt;** 동사는 Twilio에 통화 메시지를 음성으로 전달하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="41347-124">다음은 Twilio 동사의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="41347-125">**&lt;Dial&gt;**: 발신자를 다른 전화에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="41347-126">**&lt;Gather&gt;**: 전화 키패드에 입력된 숫자를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="41347-127">**&lt;Hangup&gt;**: 통화를 끝냅니다.</span><span class="sxs-lookup"><span data-stu-id="41347-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="41347-128">**&lt;Play&gt;**: 오디오 파일을 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="41347-129">**&lt;Queue&gt;**: 호출자 큐에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="41347-130">**&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="41347-131">**&lt;Record&gt;**: 발신자의 음성을 녹음하고 녹음이 포함된 파일의 URL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="41347-132">**&lt;Redirect&gt;**: 통화 또는 SMS에 대한 제어를 다른 URL의 TwiML로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="41347-133">**&lt;Reject&gt;**: 요금을 청구하지 않고 Twilio 번호의 수신 전화를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="41347-134">**&lt;Say&gt;**: 텍스트를 통화에 사용되는 음성으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="41347-135">**&lt;Sms&gt;**: SMS 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41347-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="41347-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="41347-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="41347-137">TwiML은 Twilio에 통화 또는 SMS 처리 방법을 알려 주는 Twilio 동사를 사용하는 XML 기반 명령 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="41347-138">다음 예제 TwiML은 **Hello World!** 텍스트를 음성으로</span><span class="sxs-lookup"><span data-stu-id="41347-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="41347-139">변환합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="41347-140">응용 프로그램에서 Twilio API를 호출할 때 API 매개 변수 중 하나는 TwiML 응답을 반환하는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="41347-141">개발을 위해서 Twilio 제공 URL을 사용하여 응용 프로그램에 사용되는 TwiML 응답을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="41347-142">또한 TwiML 응답을 생성하는 고유한 URL을 호스트할 수도 있고, **TwiMLResponse** 개체를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="41347-143">Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="41347-144">Twilio API에 대한 자세한 내용은 [Twilio API][twilio_api](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="41347-145"><a id="CreateAccount"></a>Twilio 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="41347-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="41347-146">Twilio 계정을 사용할 준비가 되었다면 [Twilio 체험][try_twilio](영문)에서 등록하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="41347-147">무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="41347-148">Twilio 계정을 등록하면 계정 ID 및 인증 토큰을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41347-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="41347-149">둘 다 Twilio API 통화를 하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="41347-150">계정에 대한 무단 액세스를 방지하려면 인증 토큰을 안전하게 유지하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="41347-151">계정 ID 및 인증 토큰은 [Twilio 콘솔][twilio_console]의 **ACCOUNT SID** 및 **AUTH TOKEN** 필드에서 각각 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="41347-152"><a id="create_app"></a>Java 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="41347-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="41347-153">Twilio JAR을 다운로드하여 Java 빌드 경로 및 WAR 배포 어셈블리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="41347-154">[https://github.com/twilio/twilio-java][twilio_java]에서 GitHub 원본을 다운로드한 후 고유한 JAR을 만들거나 종속성 포함 여부에 관계없이 미리 빌드된 JAR을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="41347-155">JDK의 **cacerts** keystore에 MD5 지문이 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4인 Equifax Secure Certificate Authority 인증서가 포함되어 있는지 확인합니다(일련 번호는 35:DE:F4:CF이고 SHA1 지문은 D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A임).</span><span class="sxs-lookup"><span data-stu-id="41347-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="41347-156">이 인증서는 Twilio API를 사용할 때 호출되는 [https://api.twilio.com][twilio_api_service] 서비스에 대한 CA(인증 기관) 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="41347-157">JDK의 **cacerts** keystore에 올바른 CA 인증서가 포함되어 있는지 확인하는 방법에 대한 자세한 내용은 [Java CA 인증서 저장소에 인증서 추가][add_ca_cert]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="41347-158">Java용 Twilio 클라이언트 라이브러리 사용에 대한 자세한 지침은 [Azure의 Java 응용 프로그램에서 Twilio를 사용하여 전화를 거는 방법][howto_phonecall_java]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="41347-159"><a id="configure_app"></a>Twilio 라이브러리를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="41347-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="41347-160">코드 내에서 응용 프로그램에 사용할 Twilio 패키지 또는 클래스의 원본 파일 맨 위에 **import** 문을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="41347-161">Java 원본 파일의 경우</span><span class="sxs-lookup"><span data-stu-id="41347-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="41347-162">JSP(Java Server Page) 원본 파일의 경우</span><span class="sxs-lookup"><span data-stu-id="41347-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="41347-163">사용할 Twilio 패키지 또는 클래스에 따라 **import** 문이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="41347-164"><a id="howto_make_call"></a>방법: 발신 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="41347-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="41347-165">다음은 **Call** 클래스를 사용하여 발신 전화를 거는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41347-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="41347-166">또한 이 코드는 Twilio 제공 사이트를 사용하여 TwiML(Twilio Markup Language) 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="41347-167">**from** 및 **to** 전화 번호의 값을 바꾸고, 코드를 실행하기 전에 Twilio 계정의 **from** 번호를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="41347-168">**Call.creator** 메서드에 전달된 매개 변수에 대한 자세한 내용은 [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="41347-169">언급한 대로 이 코드는 Twilio 제공 사이트를 사용하여 TwiML 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="41347-170">고유한 사이트를 대신 사용하여 TwiML 응답을 제공할 수 있습니다. 자세한 내용은 [Azure의 Java 응용 프로그램에서 TwiML 응답을 제공하는 방법](#howto_provide_twiml_responses)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="41347-171"><a id="howto_send_sms"></a>방법: SMS 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="41347-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="41347-172">다음은 **Message** 클래스를 사용하여 SMS 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41347-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="41347-173">체험 계정이 SMS 메시지를 보낼 **from** 번호 **4155992671**은 Twilio에서 자동으로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="41347-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="41347-174">코드를 실행하기 전에 Twilio 계정에 대한 **to** 번호를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="41347-175">**Message.creator** 메서드에 전달된 매개 변수에 대한 자세한 내용은 [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="41347-176"><a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공</span><span class="sxs-lookup"><span data-stu-id="41347-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="41347-177">응용 프로그램에서 Twilio API 호출을 시작하면(예: **CallCreator.create** 메서드를 통해) Twilio에서 TwiML 응답을 반환해야 하는 URL로 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="41347-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="41347-178">위 예제에서는 Twilio 제공 URL인 [http://twimlets.com/message][twimlet_message_url]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="41347-179">TwiML은 웹 서비스에서 사용되도록 설계되었지만 브라우저에서도 TwiML을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="41347-180">예를 들어 [http://twimlets.com/message][twimlet_message_url]를 클릭하면 빈 **&lt;Response&gt;** 요소가 표시됩니다. 또 다른 예로, [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world]을 클릭하면 **&lt;Say&gt;** 요소를 포함하는 **&lt;Response&gt;** 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41347-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="41347-181">Twilio 제공 URL을 사용하지 않고 HTTP 응답을 반환하는 고유한 URL 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="41347-182">HTTP 응답을 반환하는 모든 언어로 사이트를 만들 수 있습니다. 이 항목에서는 JSP 페이지에서 URL을 호스팅한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="41347-183">다음 JSP 페이지에서는 호출 시 **Hello World!**라고 말하는 TwiML 응답이</span><span class="sxs-lookup"><span data-stu-id="41347-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="41347-184">생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="41347-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="41347-185">다음 JSP 페이지에서는 일부 텍스트를 말하고 여러 일시 중지를 포함하며 Twilio API 버전 및 Azure 역할 이름에 대한 정보를 말하는 TwiML 응답이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="41347-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="41347-186">**ApiVersion** 매개 변수는 Twilio 음성 요청(SMS 요청 아님)에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="41347-187">Twilio 음성 및 SMS 요청에 사용 가능한 요청 매개 변수를 보려면 각각 <https://www.twilio.com/docs/api/twiml/twilio_request> 및 <https://www.twilio.com/docs/api/twiml/sms/twilio_request>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="41347-188">**RoleName** 환경 변수는 Azure 배포의 일부로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="41347-189">**System.getenv**에서 선택될 수 있도록 사용자 지정 환경 변수를 추가하려면 [기타 역할 구성 설정][misc_role_config_settings]의 환경 변수 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="41347-190">JSP 페이지가 TwiML 응답을 제공하도록 설정된 경우 **Call.creator** 메서드에 전달되는 URL로 JSP 페이지의 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="41347-191">예를 들어 MyTwiML이라는 웹 응용 프로그램이 Azure 호스티드 서비스에 배포되어 있고 JSP 페이지의 이름이 mytwiml.jsp인 경우 다음과 같이 URL을 **Call.creator**에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41347-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="41347-192">TwiML로 응답하는 또 다른 옵션은 **com.twilio.twiml** 패키지에 포함된 **VoiceResponse** 클래스를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41347-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="41347-193">Azure에서 Java와 함께 Twilio를 사용하는 방법에 대한 자세한 내용은 [Azure의 Java 웹 응용 프로그램에서 Twilio를 사용하여 전화를 거는 방법][howto_phonecall_java]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="41347-194"><a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="41347-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="41347-195">여기에서 보여 준 예뿐만 아니라 Twilio는 Azure 응용 프로그램에서 Twilio 기능을 활용할 수 있는 웹 기반 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41347-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="41347-196">자세한 내용은 [Twilio API 설명서][twilio_api_documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41347-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="41347-197"><a id="NextSteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="41347-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="41347-198">Twilio 서비스에 관한 기본적인 사항들을 익혔으며 자세한 내용을 보려면 다음 링크를 따라가십시오.</span><span class="sxs-lookup"><span data-stu-id="41347-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="41347-199">[Twilio 보안 지침][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="41347-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="41347-200">[Twilio 사용 방법 및 예제 코드][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="41347-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="41347-201">[Twilio 빠른 시작 자습서][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="41347-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="41347-202">[Twilio on GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="41347-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="41347-203">[Twilio 지원 문의][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="41347-203">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
