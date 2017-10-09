---
title: "aaaHow toouse PHP와 알림 허브"
description: "자세한 내용은 방법 toouse Azure 알림 허브는 PHP 백 엔드에서 합니다."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a>어떻게 toouse PHP에서 알림 허브
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Java/PHP/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 hello MSDN 항목에 설명 된 대로 hello 알림 허브 REST 인터페이스를 사용 하 여 [알림 허브 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)합니다.

이 항목에서는 다음 방법을 보여 줍니다.

* PHP에서 알림 허브 기능에 대한 REST 클라이언트를 빌드하는 방법
* Hello에 따라 [Get 시작된 자습서](notification-hubs-ios-apple-push-notification-apns-get-started.md) PHP에서 hello 백 엔드 부분을 구현 합니다. 원하는 모바일 플랫폼에 대 한 합니다.

## <a name="client-interface"></a>클라이언트 인터페이스
hello 주 클라이언트 인터페이스 hello hello에서 사용할 수 있는 동일한 방법을 제공할 수 [.NET 알림 허브 SDK](http://msdn.microsoft.com/library/jj933431.aspx), 이렇게 하면 모든 hello 자습서 및이 사이트에서 현재 사용할 수 있는 샘플 toodirectly 번역 및 hello 커뮤니티 hello에 제공한 인터넷 합니다.

Hello에서 사용할 수 있는 모든 hello 코드를 찾을 수 있습니다 [PHP REST 래퍼 샘플]합니다.

예를 들어 toocreate 클라이언트:

    $hub = new NotificationHub("connection string", "hubname");    

toosend iOS 기본 알림:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>구현
되어 있지 않은 경우 따르십시오 우리의 [Get 시작된 자습서] tooimplement hello 백 엔드 있는 toohello 마지막 섹션을 합니다.
또한, 원하는 경우 hello에서 hello 코드 사용할 수 [PHP REST 래퍼 샘플] toohello 직접 이동 하 고 [완료 hello 자습서](#complete-tutorial) 섹션.

전체 REST 래퍼를 찾을 수 세부 정보 tooimplement hello 모든 [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)합니다. 이 섹션의 hello PHP 구현의 hello 주요 단계는 필요한 tooaccess 알림 허브 REST 끝점을 설명 합니다.

1. Hello 연결 문자열을 구문 분석
2. Hello 인증 토큰을 생성 합니다.
3. Hello HTTP 호출 수행

### <a name="parse-hello-connection-string"></a>Hello 연결 문자열을 구문 분석
Hello 주 클래스 구현 hello 클라이언트 hello 연결 문자열을 구문 분석의 생성자는 다음과 같습니다.

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a>보안 토큰 만들기
hello 보안 토큰 생성 hello 세부 사항은 [여기](http://msdn.microsoft.com/library/dn495627.aspx)합니다.
hello 다음 메서드는 추가 toobe toohello **NotificationHub** hello hello 현재 요청 및 hello 연결 문자열에서 추출 된 hello 자격 증명의 URI 기반으로 클래스 toocreate hello 토큰입니다.

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a>알림 보내기
먼저 알림을 나타내는 클래스를 정의합니다.

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

이 클래스는 기본 알림 본문(또는 템플릿 알림의 경우 속성 집합) 및 형식(기본 플랫폼 또는 템플릿)과 플랫폼 특정 속성(예: Apple 만료 속성 및 WNS 헤더)이 포함된 헤더 집합에 대한 컨테이너입니다.

Toohello를 참조 하십시오 [알림 허브 REST Api 설명서](http://msdn.microsoft.com/library/dn495827.aspx) 모든 hello 사용할 수 있는 옵션에 대 한 특정 알림 플랫폼 형식 hello 및 합니다.

이 클래스와을 보면 작성할 수 있습니다 hello 송신 hello 내 알림 방법 **NotificationHub** 클래스입니다.

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

메서드 위에 hello hello 올바른 본문 및 헤더 toosend hello 알림을 사용 하 여 알림 허브의 HTTP POST 요청 toohello /messages 끝점을 보냅니다.

## <a name="complete-tutorial"></a>전체 hello 자습서
이제는 PHP 백 엔드에서 hello 알림을 전송 하 여 hello 시작 자습서를 완료할 수 있습니다.

알림 허브 클라이언트 초기화 (hello에 설명 된 대로 hello 연결 문자열 및 허브 이름을 대체 [Get 시작된 자습서]):

    $hub = new NotificationHub("connection string", "hubname");    

대상 모바일 플랫폼에 따라 hello 송신 코드를 추가 합니다.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows 스토어 및 Windows Phone 8.1(비 Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 및 8.1 Silverlight
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

이제 PHP 코드를 실행하면 대상 장치에 나타나는 알림이 생성되어야 합니다.

## <a name="next-steps"></a>다음 단계
이 항목에서 소개 된 방법을 toocreate 간단한 Java REST 클라이언트 알림 허브에 대 한 합니다. 여기에서 다음을 할 수 있습니다.

* 전체 hello 다운로드 [PHP REST 래퍼 샘플], 위의 모든 hello 코드가 포함 되어 있습니다.
* 태그 기능은 hello [속보 자습서]에서 알림 허브에 대 한 학습
* [사용자에 게 알림 자습서] 알림 tooindividual 사용자가 푸시하는 방법을 알아봅니다

자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.

[PHP REST 래퍼 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get 시작된 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

