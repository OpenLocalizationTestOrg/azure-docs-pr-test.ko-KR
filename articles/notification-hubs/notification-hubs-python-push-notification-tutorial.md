---
title: "Python과 함께 알림 허브를 사용하는 방법"
description: "Python 백 엔드에서 Azure 알림 허브를 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="4c4a3-103">Python에서 알림 허브를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4c4a3-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="4c4a3-104">MSDN [항목 알림 허브 REST API](http://msdn.microsoft.com/library/dn223264.aspx)에 설명된 대로 알림 허브 REST 인터페이스를 사용하여 Java/PHP/Python/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="4c4a3-105">이는 Python에서 알림 보내기를 구현하기 위한 샘플 참조 구현이며 공식적으로 지원되는 알림 허브 Python SDK가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="4c4a3-106">이 샘플은 Python 3.4를 사용하여 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="4c4a3-107">이 항목에서는 다음 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-107">In this topic we show how to:</span></span>

* <span data-ttu-id="4c4a3-108">Python에서 알림 허브 기능에 대한 REST 클라이언트를 빌드하는 방법</span><span class="sxs-lookup"><span data-stu-id="4c4a3-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="4c4a3-109">Python 인터페이스를 사용하여 알림 허브 REST API에 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="4c4a3-110">디버그/교육 용도로 HTTP REST 요청/응답의 덤프를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="4c4a3-111">선택한 모바일 플랫폼에 대한 [시작 자습서](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 에 따라 Python에서 백 엔드 부분을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="4c4a3-112">샘플 범위는 알림 보내기로만 제한되며 등록 관리는 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="4c4a3-113">클라이언트 인터페이스</span><span class="sxs-lookup"><span data-stu-id="4c4a3-113">Client interface</span></span>
<span data-ttu-id="4c4a3-114">기본 클라이언트 인터페이스에서는 [.NET 알림 허브 SDK](http://msdn.microsoft.com/library/jj933431.aspx)에서 제공되는 것과 같은 메서드를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="4c4a3-115">따라서 현재 이 사이트에서 사용 가능하며 인터넷 커뮤니티에서 제공한 모든 자습서 및 샘플을 직접 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="4c4a3-116">[Python REST 래퍼 샘플]에서 사용 가능한 모든 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="4c4a3-117">예를 들어 클라이언트를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="4c4a3-118">Windows 알림 메시지를 보내려면</span><span class="sxs-lookup"><span data-stu-id="4c4a3-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="4c4a3-119">구현</span><span class="sxs-lookup"><span data-stu-id="4c4a3-119">Implementation</span></span>
<span data-ttu-id="4c4a3-120">아직 하지 않았으면 백 엔드를 구현해야 하는 [시작 자습서] 의 마지막 섹션까지 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="4c4a3-121">전체 REST 래퍼를 구현하는 방법에 대한 자세한 내용은 [MSDN](http://msdn.microsoft.com/library/dn530746.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="4c4a3-122">이 섹션에서는 알림 허브 REST 끝점에 액세스하고 알림을 보내는 데 필요한 기본 단계의 Python 구현에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="4c4a3-123">연결 문자열 구문 분석</span><span class="sxs-lookup"><span data-stu-id="4c4a3-123">Parse the connection string</span></span>
2. <span data-ttu-id="4c4a3-124">인증 토큰 생성</span><span class="sxs-lookup"><span data-stu-id="4c4a3-124">Generate the authorization token</span></span>
3. <span data-ttu-id="4c4a3-125">HTTP REST API를 사용하여 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4c4a3-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="4c4a3-126">연결 문자열 구문 분석</span><span class="sxs-lookup"><span data-stu-id="4c4a3-126">Parse the connection string</span></span>
<span data-ttu-id="4c4a3-127">연결 문자열을 구문 분석하는 생성자가 포함된 클라이언트를 구현하는 기본 클래스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="4c4a3-128">보안 토큰 만들기</span><span class="sxs-lookup"><span data-stu-id="4c4a3-128">Create security token</span></span>
<span data-ttu-id="4c4a3-129">보안 토큰 만들기에 대한 자세한 내용은 [여기](http://msdn.microsoft.com/library/dn495627.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="4c4a3-130">현재 요청의 URI 및 연결 문자열에서 추출된 자격 증명에 따라 토큰을 만들려면 **NotificationHub** 클래스에 다음 메서드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="4c4a3-131">HTTP REST API를 사용하여 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4c4a3-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="4c4a3-132">먼저 알림을 나타내는 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="4c4a3-133">이 클래스는 기본 알림 본문(또는 템플릿 알림의 경우 속성 집합), 형식(기본 플랫폼 또는 템플릿)이 포함된 헤더 집합 및 플랫폼 특정 속성(예: Apple 만료 속성 및 WNS 헤더)에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="4c4a3-134">모든 사용할 수 있는 옵션은 [알림 허브 REST API 설명서](http://msdn.microsoft.com/library/dn495827.aspx) 및 특정 알림 플랫폼의 형식을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="4c4a3-135">이제 이 클래스를 사용하여 **NotificationHub** 클래스 내부에서 알림 보내기 메서드를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="4c4a3-136">위의 메서드는 알림을 보내기 위한 올바른 본문과 헤더가 있는 알림 허브의 /messages 끝점으로 HTTP POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="4c4a3-137">디버그 속성을 통해 자세한 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="4c4a3-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="4c4a3-138">알림 허브를 초기화하는 동안 디버그 속성을 사용하면 HTTP 요청 및 응답 덤프에 대한 자세한 로깅 정보 및 자세한 알림 메시지 전송 결과가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="4c4a3-139">최근에 알림 보내기 결과에 대한 자세한 정보를 반환하는 [Notification Hubs TestSend](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) 라는 속성을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="4c4a3-140">이 속성을 사용하려면 다음을 사용하여 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="4c4a3-141">그 결과, 알림 허브 전송 요청 HTTP URL에 "test" 쿼리 문자열이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="4c4a3-142"><a name="complete-tutorial"></a>자습서 완료</span><span class="sxs-lookup"><span data-stu-id="4c4a3-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="4c4a3-143">이제 Python 백 엔드에서 알림을 보내 시작 자습서를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="4c4a3-144">알림 허브 클라이언트를 초기화합니다( [시작 자습서]에 설명된 대로 연결 문자열 및 허브 이름 대체).</span><span class="sxs-lookup"><span data-stu-id="4c4a3-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="4c4a3-145">그리고 대상 모바일 플랫폼에 따라 보내기 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="4c4a3-146">또한 이 샘플은 플랫폼에 따라 알림 보내기를 사용하도록 설정하는 상위 수준의 메서드를 추가합니다(예: send_windows_notification(Windows), send_apple_notification(Apple) 등).</span><span class="sxs-lookup"><span data-stu-id="4c4a3-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="4c4a3-147">Windows 스토어 및 Windows Phone 8.1(비 Silverlight)</span><span class="sxs-lookup"><span data-stu-id="4c4a3-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="4c4a3-148">Windows Phone 8.0 및 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="4c4a3-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="4c4a3-149">iOS</span><span class="sxs-lookup"><span data-stu-id="4c4a3-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="4c4a3-150">Android</span><span class="sxs-lookup"><span data-stu-id="4c4a3-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="4c4a3-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="4c4a3-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="4c4a3-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="4c4a3-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="4c4a3-153">Python 코드를 실행하면 대상 장치에 나타나는 알림이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="4c4a3-154">예제:</span><span class="sxs-lookup"><span data-stu-id="4c4a3-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="4c4a3-155">디버그 속성 사용</span><span class="sxs-lookup"><span data-stu-id="4c4a3-155">Enabling debug property</span></span>
<span data-ttu-id="4c4a3-156">NotificationHub를 초기화하는 동안 디버그 플래그를 사용하도록 설정하면 자세한 HTTP 요청 및 응답 덤프뿐 아니라 요청 시 전달된 HTTP 헤더 및 알림 허브에서 수신된 HTTP 응답을 확인할 수 있는 다음과 같은 NotificationOutcome이 표시됩니다. ![][1]</span><span class="sxs-lookup"><span data-stu-id="4c4a3-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="4c4a3-157">예를 들어 메시지가 푸시 알림 서비스로 전송되면</span><span class="sxs-lookup"><span data-stu-id="4c4a3-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="4c4a3-158">자세한 알림 허브 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="4c4a3-159">푸시 알림의 대상을 찾을 수 없는 경우 등록에 불일치 태그가 있어서 알림을 전달할 등록을 찾을 수 없음을 나타내는 다음 메시지가 응답에 포함되기를 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="4c4a3-160">Windows로 보내는 브로드캐스트 알림 메시지</span><span class="sxs-lookup"><span data-stu-id="4c4a3-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="4c4a3-161">Windows 클라이언트로 브로드캐스트 알림 메시지를 보낼 때 전송되는 헤더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="4c4a3-162">태그(또는 태그 식)를 지정하여 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4c4a3-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="4c4a3-163">HTTP 요청에 추가되는 태그 HTTP 헤더를 확인합니다. 아래 예제에서는 '스포츠' 페이로드가 있는 등록에만 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="4c4a3-164">여러 태그를 지정하여 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4c4a3-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="4c4a3-165">여러 태그를 보낼 때 태그 HTTP 헤더가 어떻게 변경되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="4c4a3-166">템플릿 기반 알림</span><span class="sxs-lookup"><span data-stu-id="4c4a3-166">Templated notification</span></span>
<span data-ttu-id="4c4a3-167">형식 HTTP 헤더가 변경되고 페이로드 본문이 HTTP 요청 본문의 일부로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="4c4a3-168">**클라이언트 측 - 등록된 템플릿**</span><span class="sxs-lookup"><span data-stu-id="4c4a3-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="4c4a3-169">**서버 측 - 페이로드 보내기**</span><span class="sxs-lookup"><span data-stu-id="4c4a3-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="4c4a3-170">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4c4a3-170">Next Steps</span></span>
<span data-ttu-id="4c4a3-171">이 항목에서는 알림 허브에 대한 단순한 Python REST 클라이언트를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="4c4a3-172">여기에서 다음을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-172">From here you can:</span></span>

* <span data-ttu-id="4c4a3-173">위의 모든 코드가 포함된 전체 [Python REST 래퍼 샘플]을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4c4a3-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="4c4a3-174">[속보 자습서]</span><span class="sxs-lookup"><span data-stu-id="4c4a3-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="4c4a3-175">[지역화 뉴스 자습서]</span><span class="sxs-lookup"><span data-stu-id="4c4a3-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="4c4a3-176">[Python REST 래퍼 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="4c4a3-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="4c4a3-177">[시작 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="4c4a3-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="4c4a3-178">[속보 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="4c4a3-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="4c4a3-179">[지역화 뉴스 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="4c4a3-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

