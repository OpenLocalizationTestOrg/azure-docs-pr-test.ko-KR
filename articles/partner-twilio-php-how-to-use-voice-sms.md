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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>어떻게 tooUse Twilio 음성 및 SMS 기능 PHP에 대 한
이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다. 포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다. Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.

## <a id="WhatIs"></a>Twilio 정의
Twilio는 비즈니스 통신의 hello 미래 전원을 켜는 중, 개발자 tooembed 음성 VoIP, 활성화 및 메시징을 응용 프로그램에 합니다. Hello Twilio 통신 API 플랫폼을 통해 노출 하는 클라우드 기반, 글로벌 환경에서 필요한 모든 인프라를 가상화 합니다. 응용 프로그램은 단순 toobuild 하 고 확장 가능한 합니다. 종량제 가격의 유연성과 클라우드 안정성의 이점을 누리십시오.

**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다. **Twilio SMS** 응용 프로그램 toosend 있으며 특정 문자 메시지를 수신 합니다. **Twilio 클라이언트** WebRTC 지원 및 전화, 태블릿 또는 브라우저에서 toomake VoIP 전화 있습니다.

## <a id="Pricing"></a>Twilio 가격 책정 및 특별 제공
Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공](http://www.twilio.com/azure)(10달러의 Twilio 크레딧)을 받습니다. Twilio 신용이 적용 된 tooany Twilio 사용량 ($10 신용 해당 toosending 최대 1, 000 SMS 메시지 또는 받기가 too1000 인바운드 hello 전화 번호와 메시지 또는 호출 대상 위치에 따라 음성 분) 될 수 있습니다. [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure)에서 이 Twilio 크레딧을 충전하고 시작하십시오.

Twilio는 종량제 서비스입니다. 설정 수수료는 없으며 언제든 계정을 종료할 수 있습니다. [Twilio 가격 책정][twilio_pricing]에서 자세한 내용을 볼 수 있습니다.

## <a id="Concepts"></a>개념
hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다. 클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.

Hello Twilio API의 주요 측면은 Twilio 동사 및 Twilio Markup Language (TwiML)입니다.

### <a id="Verbs"></a>Twilio 동사
hello API에서 Twilio 활용 동사; 예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.

hello 다음은 Twilio 동사 목록을입니다. 자세한 내용은 다른 동사와 기능을 통해 약 hello [Twilio Markup Language 설명서](http://www.twilio.com/docs/api/twiml)합니다.

* **&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.
* **&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.
* **&lt;Hangup&gt;**: 통화를 끝냅니다.
* **&lt;Play&gt;**: 오디오 파일을 재생합니다.
* **&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.
* **&lt;레코드&gt;**: hello 호출자의 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.
* **&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.
* **&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호 호출
* **&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.
* **&lt;Sms&gt;**: SMS 메시지를 보냅니다.

### <a id="TwiML"></a>TwiML
TwiML 방법의 Twilio를 알려주는 hello Twilio 동사에 따라 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.

예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World** toospeech 합니다.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

응용 프로그램이 호출 hello Twilio API, hello API 매개 변수 중 하나 hello TwiML 응답을 반환 하는 hello URL입니다. 개발을 위해 응용 프로그램에서 사용 하는 Twilio 제공 Url tooprovide hello TwiML 응답을 사용할 수 있습니다. 직접 Url tooproduce hello TwiML 응답을 호스트할 수 있습니다 및 두 번째 방법은 toouse hello **TwiMLResponse** 개체입니다.

Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오. Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.

## <a id="CreateAccount"></a>Twilio 계정 만들기
준비 tooget Twilio 계정 되 면에서 등록 [시도 Twilio][try_twilio]합니다. 무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.

Twilio 계정을 등록하면 계정 ID 및 인증 토큰을 받게 됩니다. 둘 다 필요한 toomake Twilio API 호출 됩니다. 권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다. 계정 ID 및 인증 토큰 hello에서 볼 수 있는 [Twilio 계정 페이지][twilio_account]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰**각각.

## <a id="create_app"></a>HP 응용 프로그램 만들기
Azure에서 실행 되 고 hello Twilio 서비스를 사용 하는 PHP 응용 프로그램은 다른 모든 PHP 응용 프로그램 hello Twilio 서비스를 사용 하는 방법과 다르지 않습니다. 이 문서는 toouse Twilio를 사용 하 여 서비스 방법을 중점 Twilio 서비스는 REST 기반 하 고 여러 가지 방법으로 PHP에서 호출할 수 있습니다, [GitHub에서 PHP 용 Twilio 라이브러리][twilio_php]합니다. PHP 용 hello Twilio 라이브러리를 사용 하는 방법에 대 한 자세한 내용은 참조 [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs]합니다.

Twilio/PHP 응용 프로그램 tooAzure 구축 하기 위한 자세한 지침은 [어떻게 tooMake Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio][howto_phonecall_php]합니다.

## <a id="configure_app"></a>응용 프로그램 tooUse Twilio 라이브러리 구성
PHP에 대 한 두 가지 방법으로 응용 프로그램 toouse hello Twilio 라이브러리를 구성할 수 있습니다.

1. GitHub에서 PHP 용 hello Twilio 라이브러리를 다운로드 ([https://github.com/twilio/twilio-php][twilio_php]) hello 추가 **서비스** 디렉터리 tooyour 응용 프로그램입니다.
   
    또는
2. PHP 용 배 패키지로 hello Twilio 라이브러리를 설치 합니다. 다음 명령은 hello로 설치할 수 있습니다.
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

PHP 용 hello Twilio 라이브러리를 설치 하면를 추가할 수 있습니다는 **require_once** 프로그램 PHP의 hello 위쪽 문을 tooreference hello 라이브러리 파일:

        require_once 'Services/Twilio.php';

자세한 내용은 참조 [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme]합니다.

## <a id="howto_make_call"></a>방법: 발신 전화 걸기
hello 다음 테이블에 나와 hello를 사용 하 여 나가는 toomake을 호출 하는 방법을 **Services_Twilio** 클래스입니다. 이 코드는 또한 Twilio 제공 사이트 tooreturn hello Twilio Markup Language (TwiML) 응답을 사용합니다. Hello에 대 한 값을 대체 **에서** 및 **를** 전화 번호를 하 고 hello를 확인 하는 확인 **에서** Twilio 계정 이전 toorunning hello 코드의 전화 번호입니다.

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

앞서 언급 했 듯이이 코드는 Twilio 제공 사이트 tooreturn hello TwiML 응답을 사용 합니다. 사용자 고유의 사이트 tooprovide hello TwiML 응답; 대신 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 tooProvide TwiML 응답에서 직접 웹 사이트](#howto_provide_twiml_responses)합니다.

* **참고**: tootroubleshoot SSL 인증서 유효성 검사 오류 참조 [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>방법: SMS 메시지 보내기
hello 다음 테이블에 나와 방법을 사용 하 여 SMS 메시지 toosend hello **Services_Twilio** 클래스입니다. hello **에서** 번호는 평가판 계정 toosend SMS 메시지에 대해 Twilio에서 제공 됩니다. hello **를** Twilio 계정 이전 toorunning hello 코드에 대 한 번호를 확인 해야 합니다.

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

## <a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공
응용 프로그램 호출 toohello Twilio API를 시작, Twilio 요청 tooa URL을 예상 tooreturn TwiML 응답 전송 합니다. hello Twilio 제공 URL을 사용 하 여 위의 hello 예제 [http://twimlets.com/message][twimlet_message_url]합니다. (볼 수 있습니다 TwiML를 Twilio에서 사용 하기 위해 디자인 된 반면 브라우저에서 hello 합니다. 예를 들어 클릭 [http://twimlets.com/message] [ twimlet_message_url] toosee 빈 `<Response>` 요소로 또 다른 예로, 클릭 [http://twimlets.com/message? 메시지 % 5B0 %5 D = Hello %20World] [ twimlet_message_url_hello_world] toosee는 `<Response>` 요소를 포함 하는 `<Say>` 요소입니다.)

Hello Twilio 제공 URL에 의존 하지 않고 HTTP 응답을 반환 하는 사이트를 만들 수 있습니다. XML 응답; 반환 되는 언어로 hello 사이트를 만들 수 있습니다. 이 항목에서는 PHP toocreate hello TwiML 사용 합니다.

PHP 페이지 결과 라는 TwiML 응답에 따라 hello **Hello World** hello 호출 합니다.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

위의 hello 예제 알 수 있듯이 hello TwiML 응답은 XML 문서 하기만 합니다. PHP 용 hello Twilio 라이브러리 TwiML를 생성 하는 클래스를 포함 합니다. 아래 예제에서는 hello 위와 같이 hello 해당 응답을 생성 하지만 hello를 사용 하 여 **서비스\_Twilio\_Twiml** PHP 용 hello Twilio 라이브러리의 클래스:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml][twiml_reference]을 참조하세요. 

Tooprovide TwiML 응답을 설정 하 여 PHP 페이지를 사용 하는 후 사용 hello PHP 페이지의 URL hello hello에 전달 된 URL을 hello `Services_Twilio->account->calls->create` 메서드. 예를 들어, 명명 된 웹 응용 프로그램의 경우 **MyTwiML** 호스 티 드 서비스를 배포 된 tooan Azure 및 hello hello PHP 페이지 이름이 **mytwiml.php**, URL을 너무 전달 될 수 있습니다. hello **서비스 Twilio 계정-> 호출->-> 만들** hello 다음 예제와 같이:

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

Twilio를 사용 하 여 PHP 사용 하 여 Azure에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooMake Azure에서 PHP 응용 프로그램에서 전화 통화를 사용 하 여 Twilio][howto_phonecall_php]합니다.

## <a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용
또한 toohello 예제 Twilio 제공 웹 기반 Api를 여기에 표시 된 Azure 응용 프로그램에서 추가 Twilio 기능 tooleverage를 사용할 수 있습니다. 전체 세부 정보에 대 한 참조 hello [Twilio API 설명서][twilio_api_documentation]합니다.

## <a id="NextSteps"></a>다음 단계
Hello Twilio 서비스의 기본 사항 hello를 알아보았습니다 했으므로 이러한 링크 toolearn 자세한 수행 합니다.

* [Twilio 보안 지침][twilio_security_guidelines]
* [Twilio 사용 방법 및 예제 코드][twilio_howtos]
* [Twilio 빠른 시작 자습서][twilio_quickstarts] 
* [Twilio on GitHub][twilio_on_github]
* [Talk tooTwilio 지원][twilio_support]

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
