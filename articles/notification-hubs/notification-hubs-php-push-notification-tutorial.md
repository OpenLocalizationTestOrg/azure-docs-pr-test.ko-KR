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
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="08ec3-103">어떻게 toouse PHP에서 알림 허브</span><span class="sxs-lookup"><span data-stu-id="08ec3-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="08ec3-104">Java/PHP/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 hello MSDN 항목에 설명 된 대로 hello 알림 허브 REST 인터페이스를 사용 하 여 [알림 허브 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="08ec3-105">이 항목에서는 다음 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-105">In this topic we show how to:</span></span>

* <span data-ttu-id="08ec3-106">PHP에서 알림 허브 기능에 대한 REST 클라이언트를 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="08ec3-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="08ec3-107">Hello에 따라 [Get 시작된 자습서](notification-hubs-ios-apple-push-notification-apns-get-started.md) PHP에서 hello 백 엔드 부분을 구현 합니다. 원하는 모바일 플랫폼에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="08ec3-108">클라이언트 인터페이스</span><span class="sxs-lookup"><span data-stu-id="08ec3-108">Client interface</span></span>
<span data-ttu-id="08ec3-109">hello 주 클라이언트 인터페이스 hello hello에서 사용할 수 있는 동일한 방법을 제공할 수 [.NET 알림 허브 SDK](http://msdn.microsoft.com/library/jj933431.aspx), 이렇게 하면 모든 hello 자습서 및이 사이트에서 현재 사용할 수 있는 샘플 toodirectly 번역 및 hello 커뮤니티 hello에 제공한 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="08ec3-110">Hello에서 사용할 수 있는 모든 hello 코드를 찾을 수 있습니다 [PHP REST 래퍼 샘플]합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="08ec3-111">예를 들어 toocreate 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="08ec3-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="08ec3-112">toosend iOS 기본 알림:</span><span class="sxs-lookup"><span data-stu-id="08ec3-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="08ec3-113">구현</span><span class="sxs-lookup"><span data-stu-id="08ec3-113">Implementation</span></span>
<span data-ttu-id="08ec3-114">되어 있지 않은 경우 따르십시오 우리의 [Get 시작된 자습서] tooimplement hello 백 엔드 있는 toohello 마지막 섹션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="08ec3-115">또한, 원하는 경우 hello에서 hello 코드 사용할 수 [PHP REST 래퍼 샘플] toohello 직접 이동 하 고 [완료 hello 자습서](#complete-tutorial) 섹션.</span><span class="sxs-lookup"><span data-stu-id="08ec3-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="08ec3-116">전체 REST 래퍼를 찾을 수 세부 정보 tooimplement hello 모든 [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="08ec3-117">이 섹션의 hello PHP 구현의 hello 주요 단계는 필요한 tooaccess 알림 허브 REST 끝점을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="08ec3-118">Hello 연결 문자열을 구문 분석</span><span class="sxs-lookup"><span data-stu-id="08ec3-118">Parse hello connection string</span></span>
2. <span data-ttu-id="08ec3-119">Hello 인증 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="08ec3-120">Hello HTTP 호출 수행</span><span class="sxs-lookup"><span data-stu-id="08ec3-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="08ec3-121">Hello 연결 문자열을 구문 분석</span><span class="sxs-lookup"><span data-stu-id="08ec3-121">Parse hello connection string</span></span>
<span data-ttu-id="08ec3-122">Hello 주 클래스 구현 hello 클라이언트 hello 연결 문자열을 구문 분석의 생성자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="08ec3-123">보안 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="08ec3-123">Create security token</span></span>
<span data-ttu-id="08ec3-124">hello 보안 토큰 생성 hello 세부 사항은 [여기](http://msdn.microsoft.com/library/dn495627.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="08ec3-125">hello 다음 메서드는 추가 toobe toohello **NotificationHub** hello hello 현재 요청 및 hello 연결 문자열에서 추출 된 hello 자격 증명의 URI 기반으로 클래스 toocreate hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="08ec3-126">알림 보내기</span><span class="sxs-lookup"><span data-stu-id="08ec3-126">Send a notification</span></span>
<span data-ttu-id="08ec3-127">먼저 알림을 나타내는 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="08ec3-128">이 클래스는 기본 알림 본문(또는 템플릿 알림의 경우 속성 집합) 및 형식(기본 플랫폼 또는 템플릿)과 플랫폼 특정 속성(예: Apple 만료 속성 및 WNS 헤더)이 포함된 헤더 집합에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="08ec3-129">Toohello를 참조 하십시오 [알림 허브 REST Api 설명서](http://msdn.microsoft.com/library/dn495827.aspx) 모든 hello 사용할 수 있는 옵션에 대 한 특정 알림 플랫폼 형식 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="08ec3-130">이 클래스와을 보면 작성할 수 있습니다 hello 송신 hello 내 알림 방법 **NotificationHub** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="08ec3-131">메서드 위에 hello hello 올바른 본문 및 헤더 toosend hello 알림을 사용 하 여 알림 허브의 HTTP POST 요청 toohello /messages 끝점을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="08ec3-132"><a name="complete-tutorial"></a>전체 hello 자습서</span><span class="sxs-lookup"><span data-stu-id="08ec3-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="08ec3-133">이제는 PHP 백 엔드에서 hello 알림을 전송 하 여 hello 시작 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="08ec3-134">알림 허브 클라이언트 초기화 (hello에 설명 된 대로 hello 연결 문자열 및 허브 이름을 대체 [Get 시작된 자습서]):</span><span class="sxs-lookup"><span data-stu-id="08ec3-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="08ec3-135">대상 모바일 플랫폼에 따라 hello 송신 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="08ec3-136">Windows 스토어 및 Windows Phone 8.1(비 Silverlight)</span><span class="sxs-lookup"><span data-stu-id="08ec3-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="08ec3-137">iOS</span><span class="sxs-lookup"><span data-stu-id="08ec3-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="08ec3-138">Android</span><span class="sxs-lookup"><span data-stu-id="08ec3-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="08ec3-139">Windows Phone 8.0 및 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="08ec3-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="08ec3-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="08ec3-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="08ec3-141">이제 PHP 코드를 실행하면 대상 장치에 나타나는 알림이 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08ec3-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08ec3-142">Next Steps</span></span>
<span data-ttu-id="08ec3-143">이 항목에서 소개 된 방법을 toocreate 간단한 Java REST 클라이언트 알림 허브에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="08ec3-144">여기에서 다음을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-144">From here you can:</span></span>

* <span data-ttu-id="08ec3-145">전체 hello 다운로드 [PHP REST 래퍼 샘플], 위의 모든 hello 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="08ec3-146">태그 기능은 hello [속보 자습서]에서 알림 허브에 대 한 학습</span><span class="sxs-lookup"><span data-stu-id="08ec3-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="08ec3-147">[사용자에 게 알림 자습서] 알림 tooindividual 사용자가 푸시하는 방법을 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="08ec3-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="08ec3-148">자세한 내용은 참고 항목 hello [PHP 개발자 센터](/develop/php/)합니다.</span><span class="sxs-lookup"><span data-stu-id="08ec3-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[PHP REST 래퍼 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[Get 시작된 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

