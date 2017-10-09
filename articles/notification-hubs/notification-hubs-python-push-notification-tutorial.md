---
title: "aaaHow toouse python 알림 허브"
description: "자세한 내용은 방법 toouse Azure 알림 허브는 Python 백 엔드에서 합니다."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>어떻게 toouse Python에서 알림 허브
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Java/PHP/Python/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 hello MSDN 항목에 설명 된 대로 hello 알림 허브 REST 인터페이스를 사용 하 여 [알림 허브 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)합니다.

> [!NOTE]
> 이 hello 알림을 보내고 Python에서 구현 하기 위한 샘플 참조 구현 않으며 hello 알림 허브 Python SDK를 공식적으로 지원 합니다.
> 
> 이 샘플은 Python 3.4를 사용하여 작성되었습니다.
> 
> 

이 항목에서는 다음 방법을 보여 줍니다.

* Python에서 알림 허브 기능에 대한 REST 클라이언트를 빌드하는 방법
* Hello Python 인터페이스 toohello 알림 허브 REST Api를 사용 하 여 알림을 보냅니다. 
* 디버깅/교육 목적을 위해 hello HTTP REST 요청/응답의 덤프를 가져옵니다. 

Hello를 따르면 [Get 시작된 자습서](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Python에서 hello 백 엔드 부분을 구현 합니다. 원하는 모바일 플랫폼에 대 한 합니다.

> [!NOTE]
> hello 샘플의 hello 범위 제한 toosend 알림만 이며 모든 등록 관리를 수행 하지 않습니다.
> 
> 

## <a name="client-interface"></a>클라이언트 인터페이스
hello 주 클라이언트 인터페이스 hello hello에서 사용할 수 있는 동일한 방법을 제공할 수 [.NET 알림 허브 SDK](http://msdn.microsoft.com/library/jj933431.aspx)합니다. 이렇게 하면 toodirectly 모든 hello 자습서 및이 사이트에서 현재 사용할 수 있는 샘플을 변환 하 고 hello 커뮤니티 hello에 제공한 인터넷 합니다.

Hello에서 사용할 수 있는 모든 hello 코드를 찾을 수 있습니다 [Python REST 래퍼 샘플]합니다.

예를 들어 toocreate 클라이언트:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend Windows 알림 메시지:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>구현
되어 있지 않은 경우 따르십시오 우리의 [Get 시작된 자습서] tooimplement hello 백 엔드 있는 toohello 마지막 섹션을 합니다.

전체 REST 래퍼를 찾을 수 세부 정보 tooimplement hello 모든 [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)합니다. 이 섹션에서는 hello Python 구현의 hello 주요 단계는 필요한 tooaccess 알림 허브 REST 끝점에 설명 하 고 알림을 보낼합니다

1. Hello 연결 문자열을 구문 분석
2. Hello 인증 토큰을 생성 합니다.
3. HTTP REST API를 사용하여 알림 보내기

### <a name="parse-hello-connection-string"></a>Hello 연결 문자열을 구문 분석
클라이언트 hello hello 연결 문자열을 구문 분석의 생성자를 구현 하는 hello 주 클래스는 다음과 같습니다.

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>보안 토큰 만들기
hello 보안 토큰 생성 hello 세부 사항은 [여기](http://msdn.microsoft.com/library/dn495627.aspx)합니다.
hello 다음 메서드는 추가 toobe toohello **NotificationHub** hello hello 현재 요청 및 hello 연결 문자열에서 추출 된 hello 자격 증명의 URI 기반으로 클래스 toocreate hello 토큰입니다.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>HTTP REST API를 사용하여 알림 보내기
먼저 알림을 나타내는 클래스를 정의합니다.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

이 클래스는 기본 알림 본문(또는 템플릿 알림의 경우 속성 집합), 형식(기본 플랫폼 또는 템플릿)이 포함된 헤더 집합 및 플랫폼 특정 속성(예: Apple 만료 속성 및 WNS 헤더)에 대한 컨테이너입니다.

Toohello를 참조 하십시오 [알림 허브 REST Api 설명서](http://msdn.microsoft.com/library/dn495827.aspx) 모든 hello 사용할 수 있는 옵션에 대 한 특정 알림 플랫폼 형식 hello 및 합니다.

이 클래스와 같이 작성할 수 있습니다 hello 송신 hello 내 알림 방법 이제 **NotificationHub** 클래스입니다.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

메서드 위에 hello hello 올바른 본문 및 헤더 toosend hello 알림을 사용 하 여 알림 허브의 HTTP POST 요청 toohello /messages 끝점을 보냅니다.

### <a name="using-debug-property-tooenable-detailed-logging"></a>디버그 속성 tooenable를 사용 하 여 자세한 로깅을
Hello 알림 허브를 초기화 하는 동안 디버그 속성 설정에 쓰는 HTTP hello에 대 한 자세한 로깅 정보 요청 및 응답 덤프 뿐만 아니라 자세한 알림 메시지 보내기 결과입니다. 최근에 라는이 속성을 추가 했습니다 [알림 허브 TestSend 속성](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) hello 알림 보내기 결과 대 한 자세한 정보를 반환 하는 합니다. toouse 것-hello 다음을 사용 하 여 초기화 합니다.

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

결과적으로 hello 알림 허브 보내기 요청 HTTP URL "test" querystring 추가 가져옵니다. 

## <a name="complete-tutorial"></a>전체 hello 자습서
이제 Python 백 엔드에서 hello 알림을 전송 하 여 hello 시작 자습서를 완료할 수 있습니다.

알림 허브 클라이언트 초기화 (hello에 설명 된 대로 hello 연결 문자열 및 허브 이름을 대체 [Get 시작된 자습서]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

대상 모바일 플랫폼에 따라 hello 송신 코드를 추가 합니다. 이 샘플에도 windows;에 대 한 예를 들어 send_windows_notification hello 플랫폼에 따라 알림을 보낼 더 높은 수준 메서드와 tooenable 추가 send_apple_notification (apple)에 대 한 등. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows 스토어 및 Windows Phone 8.1(비 Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 및 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

Python 코드를 실행하면 대상 장치에 나타나는 알림이 생성됩니다.

## <a name="examples"></a>예제:
### <a name="enabling-debug-property"></a>디버그 속성 사용
어떤 HTTP 헤더 hello 요청에 전달 되 고 어떤 HTTP을 이해할 수 있습니다 hello 다음과 같은으로 HTTP 요청 및 응답 덤프 NotificationOutcome 자세히 볼 수 NotificationHub hello를 초기화 하는 동안 디버그 플래그를 사용 하면 hello 알림 허브에서에서 응답이 수신 되었습니다.![][1]

예를 들어 메시지가 푸시 알림 서비스로 전송되면 

* hello 메시지를 성공적으로 보내면 toohello 푸시 알림 서비스. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* 대상을 찾을 수 없습니다 푸시 알림에 다음 (나타냄 hello 등록에 일부 아마도 toodeliver hello 알림을 찾을 수 없는 등록 했다는 hello 응답에서 toosee hello 다음 보아야 가능성이 있는 경우 일치 하지 않는 태그)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>알림을 알림 tooWindows 브로드캐스트
브로드캐스트 알림을 알림 tooWindows 클라이언트를 보낼 때 아웃 전송 하는 hello 헤더를 확인 합니다. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>태그(또는 태그 식)를 지정하여 알림 보내기
Toohello HTTP 요청에 추가 되는 공지 hello 태그 HTTP 헤더 (hello 아래의 예제에서는 보낼 hello 알림만 tooregistrations '스포츠' 페이로드 포함)

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>여러 태그를 지정하여 알림 보내기
Hello 태그 HTTP 헤더에서 여러 태그를 보내면을 변경 하는 방법을 확인 합니다. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>템플릿 기반 알림
Hello 형식 HTTP 헤더 변경 내용 및 페이로드 본문 hello는 hello HTTP 요청 본문의 일부로 전송 됩니다.

**클라이언트 측 - 등록된 템플릿**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**서버 쪽-hello 페이로드를 보내기**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>다음 단계
이 항목에서 소개 된 방법을 toocreate 간단한 Python REST 클라이언트 알림 허브에 대 한 합니다. 여기에서 다음을 할 수 있습니다.

* 전체 hello 다운로드 [Python REST 래퍼 샘플], 위의 모든 hello 코드가 포함 되어 있습니다.
* 태그 기능은 hello에 알림 허브에 대해 알아보십시오 [속보 자습서]
* Hello에 알림 허브 템플릿 기능에 대 한 학습을 계속 [지역화 속보 자습서]

<!-- URLs -->
[Python REST 래퍼 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[Get 시작된 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[속보 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[지역화 속보 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

