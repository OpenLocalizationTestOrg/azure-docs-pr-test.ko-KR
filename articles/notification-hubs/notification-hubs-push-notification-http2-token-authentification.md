---
title: "Azure 알림 허브에서 APNS aaaToken 기반 (HTTP/2) 인증 | Microsoft Docs"
description: "이 항목에서는 방법을 tooleverage hello APNS에 대 한 새 토큰 인증 설명"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="06734-103">APNS에 대한 토큰 기반(HTTP/2) 인증</span><span class="sxs-lookup"><span data-stu-id="06734-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="06734-104">개요</span><span class="sxs-lookup"><span data-stu-id="06734-104">Overview</span></span>
<span data-ttu-id="06734-105">이 문서는 토큰으로 toouse hello 새 APNS HTTP/2 프로토콜 기반 인증 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="06734-106">hello hello 새 프로토콜을 사용 하 여의 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="06734-107">토큰 생성은 비교적 쉽게 배치할 가능한 (비교 toocertificates)</span><span class="sxs-lookup"><span data-stu-id="06734-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="06734-108">만료 날짜가 없습니다. 인증 토큰과 해당 해지를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="06734-109">페이로드는 too4 KB 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="06734-110">피드백이 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="06734-110">Synchronous feedback</span></span>
-   <span data-ttu-id="06734-111">Apple의 최신 프로토콜에-인증서에는 여전히 사용 중단으로 표시 되는 hello 이진 프로토콜 사용</span><span class="sxs-lookup"><span data-stu-id="06734-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="06734-112">두 단계를 통해 몇 분 만에 이 새로운 메커니즘을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="06734-113">Hello Apple 개발자 계정 포털에서 hello 필요한 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="06734-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="06734-114">알림 허브 hello 새 정보로 구성</span><span class="sxs-lookup"><span data-stu-id="06734-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="06734-115">알림 허브는 이제 모든 집합 toouse hello 새로운 인증 시스템 apns 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="06734-116">APNS에 인증서 자격 증명을 사용하는 것에서 마이그레이션한 경우</span><span class="sxs-lookup"><span data-stu-id="06734-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="06734-117">hello 토큰 속성, 우리의 시스템에서 인증서를 덮어쓰려면</span><span class="sxs-lookup"><span data-stu-id="06734-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="06734-118">하지만 응용 프로그램 계속 tooreceive 알림을 원활 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="06734-119">Apple에서 인증 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="06734-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="06734-120">tooenable 토큰 기반 인증 hello Apple 개발자 계정에서 다음 속성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="06734-121">키 식별자</span><span class="sxs-lookup"><span data-stu-id="06734-121">Key Identifier</span></span>
<span data-ttu-id="06734-122">Apple 개발자 계정에서 hello "키" 페이지에서 hello 키 식별자를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="06734-123">응용 프로그램 식별자 및 응용 프로그램 이름</span><span class="sxs-lookup"><span data-stu-id="06734-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="06734-124">hello 개발자 계정에서에서의 앱 Id 페이지 hello 통해 응용 프로그램 이름 hello ´ ù.</span><span class="sxs-lookup"><span data-stu-id="06734-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="06734-125">hello 응용 프로그램 식별자를 개발자 계정 hello의 hello 등록 세부 정보 페이지를 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="06734-126">인증 토큰</span><span class="sxs-lookup"><span data-stu-id="06734-126">Authentication token</span></span>
<span data-ttu-id="06734-127">응용 프로그램에 대 한 토큰을 생성 한 후에 hello 인증 토큰을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="06734-128">에 대 한 어떻게 toogenerate이 토큰을 대 한 세부 정보 참조 너무[Apple 개발자 설명서](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65)합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="06734-129">알림 허브 toouse 토큰 기반 인증 구성</span><span class="sxs-lookup"><span data-stu-id="06734-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="06734-130">Hello Azure 포털을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="06734-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="06734-131">tooenable 토큰 기반 인증 hello 포털 toohello Azure 포털에서에서 로그 및 알림 허브 tooyour 이동 > Notification Services > APNS 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="06734-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="06734-132">*인증 모드*라는 새로운 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="06734-133">Tooupdate 토큰을 선택 하면 속성은 모두 hello 관련 토큰 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="06734-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="06734-134">Apple 개발자 계정에서 검색 하는 hello 속성 입력</span><span class="sxs-lookup"><span data-stu-id="06734-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="06734-135">응용 프로그램 모드(프로덕션 또는 샌드박스)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="06734-136">클릭 tooupdate APNS 자격 증명을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="06734-137">관리 API(REST)을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="06734-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="06734-138">사용할 수 있습니다이 [관리 Api](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate 알림 허브 toouse 토큰 기반 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="06734-139">구성 하는 hello 응용 프로그램 인지 (Apple 개발자 계정에 지정 된) 샌드박스 또는 프로덕션 응용 프로그램에 따라 hello 해당 끝점 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="06734-140">샌드박스 끝점: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="06734-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="06734-141">샌드박스 끝점: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="06734-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06734-142">토큰 기반 인증에는 API 버전 **2017-04 이상**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="06734-143">PUT 요청 tooupdate 토큰 기반 인증 된 허브의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="06734-144">Hello.NET SDK을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="06734-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="06734-145">허브 toouse 토큰 기반된 인증 사용을 구성할 수 있습니다이 [최신 클라이언트 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8)합니다.</span><span class="sxs-lookup"><span data-stu-id="06734-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="06734-146">Hello 올바른 사용법을 보여 주는 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="06734-147">되돌리는 중 toousing 인증서 기반 인증</span><span class="sxs-lookup"><span data-stu-id="06734-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="06734-148">Hello 토큰 속성 대신 이전 메서드와 전달 hello 인증서를 사용 하 여 시간 toousing 인증서 기반 인증에 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06734-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="06734-149">작업 덮어씁니다 hello는 이전에 저장 된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="06734-149">That action overwrites hello previously stored credentials.</span></span>
