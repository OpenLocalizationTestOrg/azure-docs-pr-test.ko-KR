---
title: "aaaHow tooUse Twilio 음성 및 SMS (Java) | Microsoft Docs"
description: "Azure의 hello Twilio API 서비스와 메시지 toomake 전화 통화 및 SMS 송신에 알아봅니다. 코드 샘플은 Java로 작성되었습니다."
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
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>어떻게 tooUse 음성 및 SMS 기능 java에서 Twilio
이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다. 포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다. Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.

## <a id="WhatIs"></a>Twilio 정의
Twilio는 기존 웹 언어와 기술 toobuild 음성 및 SMS 응용 프로그램을 사용 하는 전화 통신 웹 서비스 API입니다. Twilio는 타사 서비스입니다(Azure 기능 또는 Microsoft 제품 아님).

**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다. **Twilio SMS** 응용 프로그램 toomake 있으며 SMS 메시지를 수신 합니다. **Twilio 클라이언트** 모바일 연결을 포함 하 여 기존 인터넷 연결을 사용 하 여 tooenable 음성 통신 응용 프로그램을 허용 합니다.

## <a id="Pricing"></a>Twilio 가격 책정 및 특별 제공
Twilio 가격 책정 정보는 [Twilio 가격 책정][twilio_pricing]에서 확인할 수 있습니다. Azure 고객은 [특별 제공][special_offer](문자 1000통 또는 인바운드 통화 1000분의 무료 크레딧)을 받습니다. 이 대해 toosign 제공 또는 자세한 정보를 얻을, 방문 하십시오 [http://ahoy.twilio.com/azure][special_offer]합니다.

## <a id="Concepts"></a>개념
hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다. 클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.

Hello Twilio API의 주요 측면은 Twilio 동사 및 Twilio Markup Language (TwiML)입니다.

### <a id="Verbs"></a>Twilio 동사
hello API에서 Twilio 활용 동사; 예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.

hello 다음은 Twilio 동사 목록을입니다.

* **&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.
* **&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.
* **&lt;Hangup&gt;**: 통화를 끝냅니다.
* **&lt;Play&gt;**: 오디오 파일을 재생합니다.
* **&lt;큐&gt;**: 호출자의 hello tooa 큐를 추가 합니다.
* **&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.
* **&lt;레코드&gt;**: hello 호출자의 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.
* **&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.
* **&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호를 호출 합니다.
* **&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.
* **&lt;Sms&gt;**: SMS 메시지를 보냅니다.

### <a id="TwiML"></a>TwiML
TwiML 방법의 Twilio를 알려주는 hello Twilio 동사에 따라 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.

예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World!** toospeech 합니다.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

응용 프로그램이 호출 hello Twilio API, hello API 매개 변수 중 하나 hello TwiML 응답을 반환 하는 hello URL입니다. 개발을 위해 응용 프로그램에서 사용 하는 Twilio 제공 Url tooprovide hello TwiML 응답을 사용할 수 있습니다. 직접 Url tooproduce hello TwiML 응답을 호스트할 수 있습니다 및 두 번째 방법은 toouse hello **TwiMLResponse** 개체입니다.

Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오. Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.

## <a id="CreateAccount"></a>Twilio 계정 만들기
준비 tooget Twilio 계정 되 면에서 등록 [시도 Twilio][try_twilio]합니다. 무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.

Twilio 계정을 등록하면 계정 ID 및 인증 토큰을 받게 됩니다. 둘 다 필요한 toomake Twilio API 호출 됩니다. 권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다. 계정 ID 및 인증 토큰 hello에서 볼 수 있는 [Twilio 콘솔][twilio_console]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰**각각.

## <a id="create_app"></a>Java 응용 프로그램 만들기
1. Twilio JAR hello 받으며 tooyour Java 빌드 경로 WAR 배포 어셈블리를 추가 합니다. [https://github.com/twilio/twilio-java][twilio_java], hello GitHub 소스를 다운로드 하 고 사용자 고유의 JAR 작성 하거나 (종속성이 없는 또는) 미리 작성 된 JAR 다운로드 수 있습니다.
2. JDK의 확인 **cacerts** MD5 지문 67:CB:9 D와 hello Equifax 보안 인증 기관 인증서를 포함 하는 키 저장소: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 hello 일련 번호는 (35:DE:F4:CF 및 hello SHA1 D2:32:09:AD:23:D3:14:23:21:74:E4:0 D 지 문은: 7F:9 D: 62:13:97:86:63:3A). 이 hello에 대 한 인증 기관 (CA) 인증서 hello [https://api.twilio.com] [ twilio_api_service] Twilio Api를 사용 하는 경우 호출 되는 서비스입니다. JDK의 확인에 대 한 내용은 **cacerts** hello 올바른 CA 인증서를 포함 하는 키 저장소를 참조 하십시오. [인증서 toohello Java CA 인증서 저장소에 있는 추가][add_ca_cert]합니다.

Java 용 hello Twilio 클라이언트 라이브러리를 사용 하기 위한 자세한 지침은 [어떻게 tooMake Azure에서 Java 응용 프로그램에서 전화 통화를 사용 하 여 Twilio][howto_phonecall_java]합니다.

## <a id="configure_app"></a>응용 프로그램 tooUse Twilio 라이브러리 구성
내 코드를 추가할 수 있습니다 **가져올** hello 위쪽 hello Twilio 패키지 또는 클래스에 대 한 소스 파일의 문 toouse 응용 프로그램에서 원하는 합니다.

Java 원본 파일의 경우

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

JSP(Java Server Page) 원본 파일의 경우

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
원하는 toouse, 어떤 Twilio 패키지 또는 클래스에 따라 프로그램 **가져올** 문을 다를 수 있습니다.

## <a id="howto_make_call"></a>방법: 발신 전화 걸기
hello 다음 테이블에 나와 hello를 사용 하 여 나가는 toomake을 호출 하는 방법을 **호출** 클래스입니다. 이 코드는 또한 Twilio 제공 사이트 tooreturn hello Twilio Markup Language (TwiML) 응답을 사용합니다. Hello에 대 한 값을 대체 **에서** 및 **를** 전화 번호를 하 고 hello를 확인 하는 확인 **에서** Twilio 계정 이전 toorunning hello 코드의 전화 번호입니다.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Hello 매개 변수 toohello를 전달 하는 방법에 대 한 자세한 내용은 **Call.creator** 메서드를 참조 [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls]합니다.

앞서 언급 했 듯이이 코드는 Twilio 제공 사이트 tooreturn hello TwiML 응답을 사용 합니다. 사용자 고유의 사이트 tooprovide hello TwiML 응답; 대신 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 tooProvide Azure에서 Java 응용 프로그램에서 TwiML 응답](#howto_provide_twiml_responses)합니다.

## <a id="howto_send_sms"></a>방법: SMS 메시지 보내기
hello 다음 테이블에 나와 방법을 사용 하 여 SMS 메시지 toosend hello **메시지** 클래스입니다. hello **에서** 번호, **4155992671**, 평가판 계정 toosend SMS 메시지에 대해 Twilio에서 제공 됩니다. hello **를** Twilio 계정 이전 toorunning hello 코드에 대 한 번호를 확인 해야 합니다.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

Hello 매개 변수 toohello를 전달 하는 방법에 대 한 자세한 내용은 **Message.creator** 메서드를 참조 [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms]합니다.

## <a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공
응용 프로그램 예를 들어 hello 통해 호출 toohello Twilio API를 시작 하는 경우 **CallCreator.create** 메서드, Twilio 송신할 예상된 tooreturn 있는 요청 tooa URL TwiML 응답 합니다. hello Twilio 제공 URL을 사용 하 여 위의 hello 예제 [http://twimlets.com/message][twimlet_message_url]합니다. (TwiML를 웹 서비스에서 사용 하기 위해 디자인 된 반면 볼 수 있습니다 hello TwiML 브라우저에서. 예를 들어 클릭 [http://twimlets.com/message] [ twimlet_message_url] toosee 빈  **&lt;응답&gt;**  요소로 또 다른 예로, 클릭[http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee는  **&lt;응답&gt;**  요소를 포함 하는  **&lt;말하기 &gt;**  요소입니다.)

Hello Twilio 제공 URL에 의존 하지 않고 HTTP 응답을 반환 하는 URL 사이트를 만들 수 있습니다. HTTP 응답; 반환 되는 언어로 hello 사이트를 만들 수 있습니다. 이 항목에서는 hello URL JSP 페이지에서 호스트 됩니다.

JSP 페이지 결과 라는 TwiML 응답에 따라 hello **Hello World!** hello 호출인 합니다.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

다음 텍스트를 표시 하는 TwiML 응답에서 페이지 결과 JSP hello 여러 일시 중지 개이고 hello Twilio API 버전 및 hello Azure 역할 이름에 대 한 정보를 표시 합니다.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

hello **ApiVersion** 매개 변수는 Twilio 음성 요청 (SMS 요청 되지 함)에서 사용할 수 있습니다. Twilio 음성 및 SMS 요청에 대 한 toosee hello 사용 가능한 요청 매개 변수를 참조 <https://www.twilio.com/docs/api/twiml/twilio_request> 및 <https://www.twilio.com/docs/api/twiml/sms/twilio_request >각각. hello **RoleName** 환경 변수를 사용 하는 Azure 배포의 일환으로 합니다. (원하면 tooadd 사용자 정의 환경 변수에서 선택할 수 수 있도록 **System.getenv**에 hello 환경 변수 섹션을 참조 [기타 역할 구성 설정] [misc_role_config_settings].)

Tooprovide TwiML 응답 설정 JSP 페이지를 사용 하는 후 사용 hello JSP 페이지의 hello URL hello에 전달 된 URL을 hello **Call.creator** 메서드. 예를 들어 웹 응용 프로그램의 경우 배포 MyTwiML tooan 라는 Azure 호스팅 서비스 및 hello hello JSP 페이지 이름이 mytwiml.jsp, hello URL을 너무 전달 될 수 있습니다.**Call.creator** hello 다음과 같이 합니다.

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Hello를 통해 TwiML로 응답에 대 한 또 다른 옵션은 **VoiceResponse** hello에서 사용할 수 있는 클래스 **com.twilio.twiml** 패키지 합니다.

Twilio를 사용 하 여 Java 사용 하 여 Azure에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooMake Azure에서 Java 응용 프로그램에서 전화 통화를 사용 하 여 Twilio][howto_phonecall_java]합니다.

## <a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용
또한 toohello 예제 Twilio 제공 웹 기반 Api를 여기에 표시 된 Azure 응용 프로그램에서 추가 Twilio 기능 tooleverage를 사용할 수 있습니다. 전체 세부 정보에 대 한 참조 hello [Twilio API 설명서][twilio_api_documentation]합니다.

## <a id="NextSteps"></a>다음 단계
Hello Twilio 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [Twilio 보안 지침][twilio_security_guidelines]
* [Twilio 사용 방법 및 예제 코드][twilio_howtos]
* [Twilio 빠른 시작 자습서][twilio_quickstarts]
* [Twilio on GitHub][twilio_on_github]
* [Talk tooTwilio 지원][twilio_support]

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
