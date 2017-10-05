---
title: "Azure Notification Hubs의 APNS에 대한 토큰 기반(HTTP/2) 인증 | Microsoft Docs"
description: "이 항목에서는 APNS에 대한 새로운 토큰 인증을 활용하는 방법을 설명합니다."
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="d9088-103">APNS에 대한 토큰 기반(HTTP/2) 인증</span><span class="sxs-lookup"><span data-stu-id="d9088-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="d9088-104">개요</span><span class="sxs-lookup"><span data-stu-id="d9088-104">Overview</span></span>
<span data-ttu-id="d9088-105">이 문서에서는 토큰 기반 인증을 지원하는 새로운 APNS HTTP/2 프로토콜을 사용하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="d9088-106">새 프로토콜을 사용할 경우의 주요 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="d9088-107">인증서에 비해 토큰 생성이 비교적 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="d9088-108">만료 날짜가 없습니다. 인증 토큰과 해당 해지를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="d9088-109">이제 페이로드가 최대 4KB입니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="d9088-110">피드백이 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-110">Synchronous feedback</span></span>
-   <span data-ttu-id="d9088-111">Apple의 최신 프로토콜을 사용합니다. 인증서에서는 여전히 이진 프로토콜을 사용하며 이는 사용 중단된 것으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="d9088-112">두 단계를 통해 몇 분 만에 이 새로운 메커니즘을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="d9088-113">Apple 개발자 계정 포털에서 필요한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="d9088-114">새로운 정보로 알림 허브를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="d9088-115">이제 Notification Hubs는 모두 APNS에서 새로운 인증 시스템을 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="d9088-116">APNS에 인증서 자격 증명을 사용하는 것에서 마이그레이션한 경우</span><span class="sxs-lookup"><span data-stu-id="d9088-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="d9088-117">토큰 속성이 시스템의 인증서를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="d9088-118">그러나 응용 프로그램에서는 계속 원활하게 알림을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="d9088-119">Apple에서 인증 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="d9088-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="d9088-120">토큰 기반 인증을 사용하려면 Apple 개발자 계정에서 다음 속성을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="d9088-121">키 식별자</span><span class="sxs-lookup"><span data-stu-id="d9088-121">Key Identifier</span></span>
<span data-ttu-id="d9088-122">Apple 개발자 계정의 "키" 페이지에서 키 식별자를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="d9088-123">응용 프로그램 식별자 및 응용 프로그램 이름</span><span class="sxs-lookup"><span data-stu-id="d9088-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="d9088-124">응용 프로그램 이름은 개발자 계정의 앱 ID 페이지를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="d9088-125">응용 프로그램 식별자는 개발자 계정의 멤버 자격 세부 정보 페이지를 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="d9088-126">인증 토큰</span><span class="sxs-lookup"><span data-stu-id="d9088-126">Authentication token</span></span>
<span data-ttu-id="d9088-127">응용 프로그램에 대한 토큰을 생성한 후 인증 토큰을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="d9088-128">이 토큰을 생성하는 방법에 대한 자세한 내용은 [Apple 개발자 설명서](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9088-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="d9088-129">토큰 기반 인증을 사용하도록 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="d9088-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="d9088-130">Azure Portal을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="d9088-130">Configure via the Azure portal</span></span>
<span data-ttu-id="d9088-131">포털에서 토큰 기반 인증을 활성화하려면 Azure Portal에 로그인하여 알림 허브 > Notification Services > APNS 패널로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="d9088-132">*인증 모드*라는 새로운 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="d9088-133">토큰을 선택하면 관련된 모든 토큰 속성으로 허브를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="d9088-134">Apple 개발자 계정에서 검색한 속성을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="d9088-135">응용 프로그램 모드(프로덕션 또는 샌드박스)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="d9088-136">저장을 클릭하여 APNS 자격 증명을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="d9088-137">관리 API(REST)을 통해 구성</span><span class="sxs-lookup"><span data-stu-id="d9088-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="d9088-138">[관리 API](https://msdn.microsoft.com/library/azure/dn495827.aspx)를 사용하여 토큰 기반 인증을 사용하도록 알림 허브를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="d9088-139">구성 중인 응용 프로그램이 샌드박스 앱인지 또는 프로덕션 앱인지에 따라(Apple 개발자 계정에서 지정) 해당 끝점 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="d9088-140">샌드박스 끝점: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="d9088-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="d9088-141">샌드박스 끝점: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span><span class="sxs-lookup"><span data-stu-id="d9088-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9088-142">토큰 기반 인증에는 API 버전 **2017-04 이상**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="d9088-143">토큰 기반 인증으로 허브를 업데이트하기 위한 PUT 요청 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="d9088-144">.NET SDK를 통해 구성</span><span class="sxs-lookup"><span data-stu-id="d9088-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="d9088-145">[최신 클라이언트 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8)를 사용하여 토큰 기반 인증을 사용하도록 허브를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="d9088-146">올바른 사용법을 보여 주는 코드 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="d9088-147">인증서 기반 인증 사용으로 되돌리기</span><span class="sxs-lookup"><span data-stu-id="d9088-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="d9088-148">위 방법을 사용하고 토큰 속성 대신 인증서를 전달하여 언제든지 인증서 기반 인증 사용으로 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="d9088-149">이 작업은 이전에 저장된 자격 증명을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d9088-149">That action overwrites the previously stored credentials.</span></span>
