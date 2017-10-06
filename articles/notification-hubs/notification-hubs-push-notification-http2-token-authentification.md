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
# <a name="token-based-http2-authentication-for-apns"></a>APNS에 대한 토큰 기반(HTTP/2) 인증
## <a name="overview"></a>개요
이 문서는 토큰으로 toouse hello 새 APNS HTTP/2 프로토콜 기반 인증 방법을 자세히 설명 합니다.

hello hello 새 프로토콜을 사용 하 여의 주요 이점은 다음과 같습니다.
-   토큰 생성은 비교적 쉽게 배치할 가능한 (비교 toocertificates)
-   만료 날짜가 없습니다. 인증 토큰과 해당 해지를 제어할 수 있습니다.
-   페이로드는 too4 KB 구성 될 수 있습니다.
- 피드백이 동기화됩니다.
-   Apple의 최신 프로토콜에-인증서에는 여전히 사용 중단으로 표시 되는 hello 이진 프로토콜 사용

두 단계를 통해 몇 분 만에 이 새로운 메커니즘을 사용할 수 있습니다.
1.  Hello Apple 개발자 계정 포털에서 hello 필요한 정보를 가져오려면
2.  알림 허브 hello 새 정보로 구성

알림 허브는 이제 모든 집합 toouse hello 새로운 인증 시스템 apns 합니다. 

APNS에 인증서 자격 증명을 사용하는 것에서 마이그레이션한 경우
- hello 토큰 속성, 우리의 시스템에서 인증서를 덮어쓰려면
- 하지만 응용 프로그램 계속 tooreceive 알림을 원활 하 게 합니다.

## <a name="obtaining-authentication-information-from-apple"></a>Apple에서 인증 정보 가져오기
tooenable 토큰 기반 인증 hello Apple 개발자 계정에서 다음 속성이 필요 합니다.
### <a name="key-identifier"></a>키 식별자
Apple 개발자 계정에서 hello "키" 페이지에서 hello 키 식별자를 가져올 수 있습니다.

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>응용 프로그램 식별자 및 응용 프로그램 이름
hello 개발자 계정에서에서의 앱 Id 페이지 hello 통해 응용 프로그램 이름 hello ´ ù. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

hello 응용 프로그램 식별자를 개발자 계정 hello의 hello 등록 세부 정보 페이지를 통해 사용할 수 있습니다.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>인증 토큰
응용 프로그램에 대 한 토큰을 생성 한 후에 hello 인증 토큰을 다운로드할 수 있습니다. 에 대 한 어떻게 toogenerate이 토큰을 대 한 세부 정보 참조 너무[Apple 개발자 설명서](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65)합니다.

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>알림 허브 toouse 토큰 기반 인증 구성
### <a name="configure-via-hello-azure-portal"></a>Hello Azure 포털을 통해 구성
tooenable 토큰 기반 인증 hello 포털 toohello Azure 포털에서에서 로그 및 알림 허브 tooyour 이동 > Notification Services > APNS 패널입니다. 

*인증 모드*라는 새로운 속성이 있습니다. Tooupdate 토큰을 선택 하면 속성은 모두 hello 관련 토큰 허브입니다.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Apple 개발자 계정에서 검색 하는 hello 속성 입력 
- 응용 프로그램 모드(프로덕션 또는 샌드박스)를 선택합니다. 
- 클릭 tooupdate APNS 자격 증명을 저장 합니다. 

### <a name="configure-via-management-api-rest"></a>관리 API(REST)을 통해 구성

사용할 수 있습니다이 [관리 Api](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate 알림 허브 toouse 토큰 기반 인증 합니다.
구성 하는 hello 응용 프로그램 인지 (Apple 개발자 계정에 지정 된) 샌드박스 또는 프로덕션 응용 프로그램에 따라 hello 해당 끝점 중 하나를 사용 합니다.

- 샌드박스 끝점: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)
- 샌드박스 끝점: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> 토큰 기반 인증에는 API 버전 **2017-04 이상**이 필요합니다.
> 
> 

PUT 요청 tooupdate 토큰 기반 인증 된 허브의 예는 다음과 같습니다.


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
        

### <a name="configure-via-hello-net-sdk"></a>Hello.NET SDK을 통해 구성
허브 toouse 토큰 기반된 인증 사용을 구성할 수 있습니다이 [최신 클라이언트 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8)합니다. 

Hello 올바른 사용법을 보여 주는 코드 샘플은 다음과 같습니다.


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>되돌리는 중 toousing 인증서 기반 인증
Hello 토큰 속성 대신 이전 메서드와 전달 hello 인증서를 사용 하 여 시간 toousing 인증서 기반 인증에 되돌릴 수 있습니다. 작업 덮어씁니다 hello는 이전에 저장 된 자격 증명입니다.
