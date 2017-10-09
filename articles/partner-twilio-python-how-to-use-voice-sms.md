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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>어떻게 tooUse Twilio 음성 및 SMS 기능 Python
이 가이드에서는 Azure에서 tooperform hello Twilio API가 있는 일반적인 프로그래밍 작업을 서비스 하는 방법을 보여 줍니다. 포함 하는 hello 시나리오에는 전화를 걸어서를 Short Message Service (SMS) 메시지를 보내는 포함 됩니다. Twilio 및 음성 및 SMS를 사용 하 여 응용 프로그램에 대 한 자세한 내용은 참조 hello [다음 단계](#NextSteps) 섹션.

## <a id="WhatIs"></a>Twilio 정의
Twilio는 비즈니스 통신의 hello 미래 전원을 켜는 중, 개발자 tooembed 음성 VoIP, 활성화 및 메시징을 응용 프로그램에 합니다. Hello Twilio 통신 API 플랫폼을 통해 노출 하는 클라우드 기반, 글로벌 환경에서 필요한 모든 인프라를 가상화 합니다. 응용 프로그램은 단순 toobuild 하 고 확장 가능한 합니다. 종량제 가격의 유연성과 클라우드 안정성의 이점을 누리십시오.

**Twilio 음성** 응용 프로그램 toomake 허용 및 전화 통화를 수신 합니다.
**Twilio SMS** 응용 프로그램 toosend 있으며 특정 문자 메시지를 수신 합니다.
**Twilio 클라이언트** WebRTC 지원 및 전화, 태블릿 또는 브라우저에서 toomake VoIP 전화 있습니다.

## <a id="Pricing"></a>Twilio 가격 책정 및 특별 제공
Azure 고객은 Twilio 계정을 업그레이드할 때 [특별 제공][special_offer] 10달러의 Twilio 크레딧을 받습니다. Twilio 신용이 적용 된 tooany Twilio 사용량 ($10 신용 해당 toosending 최대 1, 000 SMS 메시지 또는 받기가 too1000 인바운드 hello 전화 번호와 메시지 또는 호출 대상 위치에 따라 음성 분) 될 수 있습니다. 이 [Twilio 크레딧][special_offer]을 충전하고 시작하세요.

Twilio는 종량제 서비스입니다. 설정 수수료는 없으며 언제든 계정을 종료할 수 있습니다. [Twilio 가격 책정][twilio_pricing]에서 자세한 내용을 볼 수 있습니다.

## <a id="Concepts"></a>개념
hello Twilio API는 응용 프로그램에 대 한 음성 및 SMS 기능을 제공 하는 RESTful API입니다. 클라이언트 라이브러리는 다양한 언어로 사용할 수 있습니다. 목록에 대해서는 [Twilio API 라이브러리][twilio_libraries](영문)를 참조하십시오.

Hello Twilio API의 주요 측면은 Twilio 동사 및 Twilio Markup Language (TwiML)입니다.

### <a id="Verbs"></a>Twilio 동사
hello API에서 Twilio 활용 동사; 예를 들어 hello  **&lt;의견을 언급 해서도&gt;**  동사 Twilio tooaudibly 배달에 대 한 호출에서 메시지 지시 합니다.

hello 다음은 Twilio 동사 목록을입니다. 자세한 내용은 다른 동사와 기능을 통해 약 hello [Twilio Markup Language 설명서][twiml]합니다.

* **&lt;전화&gt;**: hello 호출자 tooanother 전화를 연결 합니다.
* **&lt;수집&gt;**: hello 전화 키패드 입력 한 자리 숫자를 수집 합니다.
* **&lt;Hangup&gt;**: 통화를 끝냅니다.
* **&lt;Pause&gt;**: 지정된 시간(초) 동안 무음으로 대기합니다.
* **&lt;Play&gt;**: 오디오 파일을 재생합니다.
* **&lt;큐&gt;**: 호출자의 hello tooa 큐를 추가 합니다.
* **&lt;레코드&gt;**: hello 호출자의 hello 음성 기록 하 고 hello 기록이 포함 된 파일의 URL을 반환 합니다.
* **&lt;리디렉션&gt;**: 통화 또는 SMS toohello TwiML 다른 URL에 대 한 제어를 전송 합니다.
* **&lt;거부&gt;**: 들어오는 거절 하면 청구 하지 않고 tooyour Twilio 번호를 호출 합니다.
* **&lt;예를 들어&gt;**: 호출에서 만든 텍스트 toospeech를 변환 합니다.
* **&lt;Sms&gt;**: SMS 메시지를 보냅니다.

### <a id="TwiML"></a>TwiML
TwiML 방법의 Twilio를 알려주는 hello Twilio 동사에 따라 XML 기반 지침의 집합이 tooprocess 통화 나 SMS 합니다.

예를 들어, 다음 TwiML hello hello 텍스트 변환 **Hello World** toospeech 합니다.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

응용 프로그램이 호출 hello Twilio API, hello API 매개 변수 중 하나 hello TwiML 응답을 반환 하는 hello URL입니다. 개발을 위해 응용 프로그램에서 사용 하는 Twilio 제공 Url tooprovide hello TwiML 응답을 사용할 수 있습니다. 직접 Url tooproduce hello TwiML 응답을 호스트할 수 있습니다 및 두 번째 방법은 toouse hello `TwiMLResponse` 개체입니다.

Twilio 동사, 특성 및 TwiML에 대한 자세한 내용은 [TwiML][twiml](영문)을 참조하십시오. Hello Twilio API에 대 한 자세한 내용은 참조 하십시오. [Twilio API][twilio_api]합니다.

## <a id="CreateAccount"></a>Twilio 계정 만들기
준비 tooget Twilio 계정 러 우면에서 등록 [시도 Twilio][try_twilio]합니다. 무료 계정으로 시작했다가 나중에 계정을 업그레이드할 수 있습니다.

Twilio 계정을 등록하면 계정 SID 및 인증 토큰을 받게 됩니다. 둘 다 필요한 toomake Twilio API 호출 됩니다. 권한이 없음 tooprevent tooyour 계정에 액세스, 인증 토큰이 안전 하 게 유지 합니다. 사용자 계정 SID 및 인증 토큰은 hello에 볼 수 있는 [Twilio 콘솔][twilio_console]에 레이블이 지정 된 필드를 hello **계정 SID** 및 **인증 토큰**각각.

## <a id="create_app"></a>Python 응용 프로그램 만들기
Azure에서 실행 되 고 hello Twilio 서비스를 사용 하는 Python 응용 프로그램은 다른 모든 Python 응용 프로그램 hello Twilio 서비스를 사용 하는 방법과 다르지 않습니다. 이 문서는 toouse Twilio를 사용 하 여 서비스 방법을 중점 Twilio 서비스는 REST 기반 하 고 여러 가지 방법으로 Python에서 호출할 수 있습니다, [GitHub에서 Python 용 Twilio 라이브러리][twilio_python]합니다. Python 용 hello Twilio 라이브러리를 사용 하는 방법에 대 한 자세한 내용은 참조 [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs]합니다.

먼저 [새 Azure Linux VM을 설정 하는 경우] [azure_vm_setup] tooact 새 Python 웹 응용 프로그램에 대 한 호스트입니다. Hello 가상 컴퓨터가 실행 되 면, 해야 tooexpose 공용 포트에 있는 응용 프로그램 아래에 설명 된 대로.

### <a name="add-an-incoming-rule"></a>수신 규칙 추가
  1. [네트워크 보안 그룹] [azure_nsg] toohello 이동 페이지.
  2. Hello 가상 컴퓨터와 해당 하는 네트워크 보안 그룹을 선택 합니다.
  3. **포트 80**에 대한 **발신 규칙**을 추가합니다. 모든 주소 로부터 들어오는 있는지 tooallow 수 있습니다.

### <a name="set-hello-dns-name-label"></a>DNS 이름 레이블을 hello 설정
  1. [Hello 공용 IP 주소] toohello 이동 [azure_ips] 페이지.
  2. 가상 컴퓨터와 공용 IP는 correspends hello를 선택 합니다.
  3. 집합 hello **DNS 이름 레이블을** hello에 **구성** 섹션. 이 예의 경우 hello 보일지 다음과 같이 *도메인 레이블 your*. centralus.cloudapp.azure.com

Tooconnect SSH toohello 설치할 수는 가상 컴퓨터를 통해 사용자가 선택한 웹 프레임 워크 hello 수 되 면 (두 개의 Python 되에 가장 잘 알려진 hello [플라스](http://flask.pocoo.org/) 및 [Django](https://www.djangoproject.com)). Hello를 실행 하 여 둘 중 하나를 설치할 수 있습니다 `pip install` 명령입니다.

포트 80에 대해서만 구성 된 म hello 가상 컴퓨터 tooallow 트래픽 염두에서에 둬야 합니다. 따라서 있는지 tooconfigure hello 응용 프로그램 toouse이이 포트를 확인 합니다.

## <a id="configure_app"></a>응용 프로그램 tooUse Twilio 라이브러리 구성
Python에 대 한 두 가지 방법으로 응용 프로그램 toouse hello Twilio 라이브러리를 구성할 수 있습니다.

* Python에 대 한 Pip 패키지로 hello Twilio 라이브러리를 설치 합니다. 다음 명령은 hello로 설치할 수 있습니다.
   
        $ pip install twilio

    또는

* GitHub에서 Python에 대 한 hello Twilio 라이브러리를 다운로드 ([https://github.com/twilio/twilio-python][twilio_python]) 하 고 다음과 같은 설치:

        $ python setup.py install

Python 용 hello Twilio 라이브러리를 설치 하면 그런 다음 `import` Python 파일에:

        import twilio

자세한 내용은 [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme]를 참조하세요.

## <a id="howto_make_call"></a>방법: 발신 전화 걸기
다음 hello 나가는 toomake 호출 하는 방법을 보여 줍니다. 이 코드는 또한 Twilio 제공 사이트 tooreturn hello Twilio Markup Language (TwiML) 응답을 사용합니다. Hello에 대 한 값을 대체 **from_number** 및 **to_number** 전화 번호를 하 고 hello를 확인 했으면 확인 **from_number** 전화 번호 Twilio 계정에 대 한 전에 hello 코드를 실행 합니다.

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

앞서 언급 했 듯이이 코드는 Twilio 제공 사이트 tooreturn hello TwiML 응답을 사용 합니다. 사용자 고유의 사이트 tooprovide hello TwiML 응답; 대신 사용할 수 있습니다. 자세한 내용은 참조 [어떻게 tooProvide TwiML 응답에서 직접 웹 사이트](#howto_provide_twiml_responses)합니다.

## <a id="howto_send_sms"></a>방법: SMS 메시지 보내기
hello 다음 테이블에 나와 방법을 사용 하 여 SMS 메시지 toosend hello `TwilioRestClient` 클래스입니다. hello **from_number** 번호는 평가판 계정 toosend SMS 메시지에 대해 Twilio에서 제공 됩니다. hello **to_number** 번호 Twilio 계정에 대 한 hello 코드를 실행 하기 전에 확인 해야 합니다.

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

## <a id="howto_provide_twiml_responses"></a>방법: 고유한 웹 사이트에서 TwiML 응답 제공
응용 프로그램 호출 toohello Twilio API를 시작, Twilio 요청 tooa URL을 예상 tooreturn TwiML 응답 전송 합니다. hello Twilio 제공 URL을 사용 하 여 위의 hello 예제 [http://twimlets.com/message][twimlet_message_url]합니다. TwiML은 Twilio에서 사용되도록 설계되었지만 브라우저에서도 TwiML을 볼 수 있습니다. 예를 들어 클릭 [http://twimlets.com/message] [ twimlet_message_url] toosee 빈 `<Response>` 요소로 또 다른 예로, 클릭 [http://twimlets.com/message? 메시지 % 5B0 %5 D = Hello %20World] [ twimlet_message_url_hello_world] toosee는 `<Response>` 요소를 포함 하는 `<Say>` 요소입니다.)

Hello Twilio 제공 URL에 의존 하지 않고 HTTP 응답을 반환 하는 사이트를 만들 수 있습니다. XML 응답; 반환 되는 언어로 hello 사이트를 만들 수 있습니다. 이 항목에서는 Python toocreate hello TwiML 사용을 가정 합니다.

hello 다음 예제에서는 출력 이라는 TwiML 응답 **Hello World** hello 호출 합니다.

Flask 사용:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Django 사용:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

위의 hello 예제 알 수 있듯이 hello TwiML 응답은 XML 문서 하기만 합니다. Python 용 hello Twilio 라이브러리 TwiML를 생성 하는 클래스를 포함 합니다. hello 아래 예제에서는 위에 표시 된 대로 hello 해당 응답을 생성 하지만 hello를 사용 하 여 `twiml` Python에 대 한 hello Twilio 라이브러리에는 모듈:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

TwiML에 대한 자세한 내용은 [https://www.twilio.com/docs/api/twiml][twiml_reference]을 참조하세요.

Tooprovide TwiML 응답을 설정 하 여 Python 응용 프로그램을 사용 하는 후 사용 hello 응용 프로그램의 hello URL hello에 전달 된 URL을 hello `client.calls.create` 메서드. 예를 들어, 명명 된 웹 응용 프로그램의 경우 **MyTwiML** 배포 tooan Azure 호스 티 드 서비스, hello 다음 예제와 같이 해당 url webhook으로 사용할 수 있습니다.

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

## <a id="AdditionalServices"></a>방법: 추가 Twilio 서비스 사용
또한 toohello 예제 Twilio 제공 웹 기반 Api를 여기에 표시 된 Azure 응용 프로그램에서 추가 Twilio 기능 tooleverage를 사용할 수 있습니다. 전체 세부 정보에 대 한 참조 hello [Twilio API 설명서][twilio_api]합니다.

## <a id="NextSteps"></a>다음 단계
Hello Twilio 서비스의 hello 기본 사항을 파악 했으므로, 이제는 이러한 링크 toolearn 자세한 수행 합니다.

* [Twilio 보안 지침][twilio_security_guidelines]
* [Twilio 사용 방법 가이드 및 예제 코드][twilio_howtos]
* [Twilio 빠른 시작 자습서][twilio_quickstarts]
* [Twilio on GitHub][twilio_on_github]
* [Talk tooTwilio 지원][twilio_support]

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
